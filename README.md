# ssnit-branches
A repo for the Realm database of SSNIT Branches used by SSNIT's mobile app.

Every time the SSNIT app is launched, it downloads a copy of `current=database.json`, which points the app to the most current Realm database of SSNIT branches to use. If the app isn't already using that database, it will download it for use. All the databases (both current and old versions) are stored in the `databases` folder.

To make changes to this repo (or to test it), you should use the `dev-testing` branch and only make the changes in master branch when everything works (to prevent affecting live builds).

## Steps for Updating
The process for updating all live builds of the app with a new SSNIT branch database is very simple:

1. Download the most current database form the `databases` folder
2. Make your changes to the database (probably using Realm Studio), but do not rename fields or add new ones— ⚠️ **This will break production on all live builds!** ⚠️ If you want to make any of those types of updates, you'll need to make a proper update of the app (and remember to increase the `schemaVersion` in the `Realm.open` command used in the branch module (that'll be in `MainBranchPage.js`)).
3. Upload the new database to the `databases` folder under a unique name. There's no need to remove the older databases in the folder.
4. Update the `current-database.json` file with the correct URL to this new database, as well as a name for this database. This name doesn't necessarily have to be the same as the database file; it's just the file name the app will use when saving the datbase. Make sure this name is unique and hasn't been used before.
5. Increment the `currentDatabaseVersion` in the `current-database` json.
