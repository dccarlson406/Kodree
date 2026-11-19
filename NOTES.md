Claude.md contains three sections Commands, Architecture, and Conventions
In conventions I specifically included Use CommonJS as this is the language of this project. Other projects may use python or powershell. By default, it should use python, but could change to some other language on a project by project basis

Permission rules were set to the recommended settings as listing in the project examples. The deny rule exists because reading the .env could be detrimental to the project if run on a different machine with a different environment.
    Allow npm test:
    Ask git push:
    Deny Read(./.env)", "Bash(git push --force: