## Some hints on using the current state of the project
To use groovy-liquibase you'll need [Gradle](http://www.gradle.org/). 

1)  Download the source and go into the directory

2)  command line $:  gradle build

3)  Edit file database.properties

            #database.properties 

            url: "yourDatabaseUrl"
            username: "yourDatabaseUser"
            password: "yourPassword"
            change.log.file: changelog.groovy

4)  changelog.groovy calls al changelogs in /changelogs. Create file(s) changelog(s) in directory /changelogs (See LiquibaseGroovyMigrations.pdf for content of this file)

5)  Execute liquibase functions: command line $:  

       gradle -q -b liquibase.gradle "function"


## Functions

###Standard Commands

* update                          ---Updates database to current version
* updateSQL                       ---Writes SQL to update database to current version to STDOUT
* update -Dcount=<num>            ---Applies next NUM changes to the database
* updateSQL -Dcount=<num>         ---Writes SQL to apply next NUM changes to the database
* rollback <tag>                  ---Rolls back the database to the the state is was when the tag was applied
* rollbackSQL <tag>               ---Writes SQL to roll back the database to that state it was in when the tag was applied to STDOUT
* rollback -Ddate=<date/time>     ---Rolls back the database to the the state is was at the given date/time. Date Format: yyyy-MM-dd HH:mm:ss
* rollbackSQL -Ddate=<date/time>  ---Writes SQL to roll back the database to that state it was in at the given date/time to STDOUT
* rollback -Dcount=<value>        ---Rolls back the last <value> change sets applied to the database
* rollbackSQL -Dcount<value>      ---Writes SQL to roll back the last <value> change sets to STDOUT applied to the database
* futureRollbackSQL               ---Writes SQL to roll back the database to the current state after the changes in the changeslog have been applied
* updateTestingRollback           ---Updates database, then rolls back changes before updating again. Useful for testing rollback support
* generateChangeLog               ---Writes Change Log XML to copy the current state of the database to standard out

###Diff Commands

* diff [diff parameters]          ---Writes description of differences to standard out [diff paramaters -DreferenceUrl=, -DreferenceUsername=, -DreferencePassword=]

###Documentation Commands

* dbDoc -Ddir=<outputDirectory>         ---Generates Javadoc-like documentation based on current database and change log

###Maintenance Commands

* tag -Dtag=<tag string>          ---'Tags' the current database state for future rollback
* status 		    ---Outputs count of unrun changesets
* validate                  ---Checks changelog for errors
* clearCheckSums            ---Removes all saved checksums from database log. Useful for 'MD5Sum Check Failed' errors
* changelogSync             ---Mark all changes as executed in the database
* changelogSyncSQL          ---Writes SQL to mark all changes as executed in the database to STDOUT
* markNextChangeSetRan      ---Mark the next change changes as executed in the database
* markNextChangeSetRanSQL   ---Writes SQL to mark the next change as executed in the database to STDOUT
* listLocks                 ---Lists who currently has locks on the database changelog
* releaseLocks              ---Releases all locks on the database changelog
* dropAll                   ---Drop all database objects owned by user

###Contexts

You can use contexts just as in liquibase core. Use -Dcontexts after any command. See [liquibase] (http://www.liquibase.org/manual/contexts) for full description .
