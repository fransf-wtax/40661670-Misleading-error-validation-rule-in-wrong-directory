# Case #40661670 - Misleading error message "An object '<name>' of type <type> was named in package.xml, but was not found in zipped directory"

This is a minimal project to show misleading error message shown when pushing code to a scratch org for a project where a metadata file is in the "wrong" location.


# To reproduce

Create a new scratch org:

    sfdx force:org:create -f config/project-scratch-def.json -d 1 -s

Push the source:

    sfdx force:source:push

An error is shown:

    *** Deploying with REST ***
    Job ID | 0Af8E00002GHG2ySAH
    SOURCE PROGRESS | ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░ | 0/1 Components
    TYPE   PROJECT PATH  PROBLEM
    ─────  ────────────  ──────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────
    Error  N/A           An object 'Account.Account_Number_Must_Be_6_Digits' of type ValidationRule was named in package.xml, but was not found in zipped directory
    ERROR running force:source:push:  Push failed.


When the file is moved to the correct location, the push operation succeeds.

    mv force-app/main/default/objects/Account/fields/validationRules/Account_Number_Must_Be_6_Digits.validationRule-meta.xml force-app/main/default/objects/Account/validationRules
    sfdx force:source:push

