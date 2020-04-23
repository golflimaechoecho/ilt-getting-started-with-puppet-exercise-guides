# Lab 9.1: Test module syntax and style

In this lab you will learn how to:

* Use the PDK Validate tool to check the syntax in the module you created in the previous lab.
* Use the PDK Validate tool to ensure your module's code meets style recommendations.
* Run compilation tests and update the code to resolve issues found.

## Steps

### Validate your module's syntax and style

1. Open the Visual Studio Code editor.
1. Choose **File > Open File**.
1. Select the `time` module directory that you created previously.
1. Change directories into `manifests`.
1. Edit the `init.pp` file you created previously.
1. Select the ellipsis in the upper right corner of the editor pane.
1. Choose **PDK Validate** from the drop down menu.

The output should be similar to this:

```plaintext
PS C:\Users\Administrator\time\manifests> pdk validate
pdk (INFO): Using Ruby 2.5.7
pdk (INFO): Using Puppet 6.13.0
pdk (INFO): Running all available validators...
+ [X] Running metadata validators ...
|-- [X] Checking metadata syntax (metadata.json tasks/*.json).
|__ [X] Checking module metadata style (metadata.json).
+ [*] Running puppet validators ...
|-- [*] Checking Puppet manifest syntax (**/*.pp).
|__ [*] Checking Puppet manifest style (**/*.pp).
+ [*] Running ruby validators ...
|__ [*] Checking Ruby code style (**/**.rb).
+ [*] Running tasks validators ...
|-- [*] Checking task names (tasks/**/*).
|__ [*] Checking task metadata style (tasks/*.json).
+ [*] Running yaml validators ...
|__ [*] Checking YAML syntax (**/*.yaml **/*.yml).
```

**_If the output of your PDK Validate does not appear close to the above, review the error and attempt to fix it using the steps in the next task._**

### Simulate a syntax error

If there were no errors in your syntax, proceed with this step to simulate one. If you had an error, skip to the **Fix the syntax errors** section below.

1. Edit the `init.pp` file to introduce a syntax error:
    1. Remove `$` from the `$servers` variable.
    1. Click **File > Save**.
1. Re-run the PDK Validate tool:
    1. Select the ellipsis in the upper right hand corner of the editor pane.
    1. Select **PDK Validate** from the drop down menu.

The output should be similar to this:

```plaintext
PS C:\Users\Administrator\time> pdk validate
pdk (INFO): Running all available validators...
pdk (INFO): Using Ruby 2.4.4
pdk (INFO): Using Puppet 5.5.2
[✔] Checking metadata syntax (metadata.json tasks/*.json).
[✖] Checking module metadata style (metadata.json).
[✖] Checking Puppet manifest syntax (**/**.pp).
[✔] Checking Ruby code style (**/**.rb).
Error: puppet-syntax: manifests/init.pp:9:7: Could not parse for environment production: Illegal attempt to assign to 'a Name'. Not an assignable reference
```

In the error message above, the message indicates the error in syntax is in `manifests/init.pp` on line **9** and column **7**.

### Fix the syntax errors

Using the output and the syntax highlighting, find all errors in your code and resolve them.

1. Identify each line and column called out in PDK Validate error messages.
1. Fix the errors by referring to the solutions guide or working with your instructor.
1. Rerun PDK Validate until all errors are gone.

## Discussion questions

1. If you had not caught the syntax errors with this tool, when and how do you think those errors might cause problems later?

|  [Previous Lab](../lab-08.1-Create-a-wrapper-module)  |  [Next Lab](../lab-10.1-Create-roles-and-profiles)  |
