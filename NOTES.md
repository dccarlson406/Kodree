Claude.md contains three sections Commands, Architecture, and Conventions
In conventions I specifically included Use CommonJS as this is the language of this project. Other projects may use python or powershell. By default, it should use python, but could change to some other language on a project by project basis

I removed the CI to keep things clean as it was not needed.

/memory showed Claude.md was loaded and had appropriate settings
/permissions showed correct settings for Ask, allow, and deny

Permission rules were set to the recommended settings as listing in the project examples. The deny rule exists because reading the .env could be detrimental to the project if run on a different machine with a different environment.

  "permissions": {
    "allow": ["Bash(npm test:*)"],
    "ask": ["Bash(git push:*)"],
    "deny": ["Read(./.env)", "Bash(git push --force:*)"]