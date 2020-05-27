# Lab 10.1: Create roles and profiles

In this lab you will learn how to:

* Clone a Puppet Enterprise control repository.
* Refactor the time module into a profile.
* Add the time profile to the base profile.
* Create a bastion role and add the base profile to it.

**_Whenever you see_** **classXXXX,** **_it refers to your class ID, such as_** **class1809.**

**_Whenever you see_** **studentN,** **_it refers to your assigned student number, such as_** **student4.**

## Steps

### Clone the control repository

In this task, you will clone the control repository to your Windows or Linux workstation.

Run these commands to clone the control repository:

   ```cd ~```

   ```git clone git@gitlab.classroom.puppet.com:puppet/control-repo.git```

   ```cd control-repo```

   ```git checkout studentN```

### Create a base profile

With your control repository cloned locally, you are ready to start updating Puppet code. In this task, you will take the **time** class you created in the previous lab and declare it in a profile.

Time is a perfect module to add to the `base` profile: that is, a profile that should be configured on every workstation. In this simple profile, you are going to include your time class. In this way, you will ensure that all systems apply the `base` profile, and included in the `base` profile is the time class.

1. In the `control-repo/site/profile/manifests` directory, create a new file called `base.pp`. It will open in the Visual Studio Code window on the right.
1. Update `base.pp` to contain these contents:

    ```ruby
    class profile::base {
      include time
    }
    ```

### Convert the profile module using the Puppet Developer Kit

1. Change directories to `control-repo/site/profile`

    ```cd ~/control-repo/site/profile```

2. Run the PDK convert command

    ```pdk convert --add-tests```

3. Accept `Y` when asked `Do you want to continue and make these changes to your module?

### Validate and test the syntax

1. Test the syntax. From your shell window run:

    ```pdk validate```

Now when you apply the `base` profile to all workstations, they will have NTP configured by default.

### Add the time module to the control repo branch

1. Edit the file named `Puppetfile` in the `~/control-repo`.
1. In `Puppetfile`, add a module (`mod`) entry for the Git remote you pushed your module to previously. Remember to set the `branch` key to your correct student number.

    ```ruby
    mod 'time',
      :git    => 'git@gitlab.classroom.puppet.com:puppet/time.git',
      :branch => 'studentN'
    ```

### Create bastion host role

Now that you have a `base` profile, increase your level of abstraction by placing that `base` profile in a **role**. Roles are used to classify node types in Puppet Enterprise Console.

For this example, you will ensure all bastion hosts have the `base` profile applied. It applies the class `ntp` or `winntp` to Linux or Windows respectively.

1. Navigate to the `~/control-repo/site/role/manifests` directory.
1. Create a new file called `bastion.pp` in the `manifests` directory.
1. To configure the `bastion` role, enter the following code into the empty `bastion.pp` file:

    ```ruby
    class role::bastion {
      include profile::base
    }
    ```

### Convert the role module using the Puppet Developer Kit

1. Change directories to `control-repo/site/role`

    ```cd ~/control-repo/site/role```

2. Run the PDK convert command

    ```pdk convert --add-tests```

3. Accept `Y` when asked `Do you want to continue and make these changes to your module?`

4. Test the syntax by running:

    ```pdk validate```

5. If any syntax errors are detected, fix them and re-run the PDK Validate tool.

## Apply the `bastion` role to your workstation

Now that you have tested your profile and role, it is time to apply the role to your workstation.

In this lab, you will test it with `puppet apply`. In a future lab, you will see how to classify your node in the Puppet Enterprise master.

Create an `examples` directory where you can place files to test your profile:

1. Navigate to `~/control-repo/site/role` and make the `examples` directory.
1. Inside the `examples` directory, add a file called `bastion.pp`. Your file system structure should look like this:

    ```plaintext
    site
    |_role
      |_examples
        |_bastion.pp
    ```

1. Add these contents into `bastion.pp`:

    ```ruby
    include role::bastion
    ```

1. Save `bastion.pp`.
1. Now you can smoke test this class, change directory to your `control-repo\site\role` directory. First run a smoke test (noop) and then `puppet apply` the role:

### Smoke test your code

1. Navigate to the right directory:

    ```cd ~/control-repo/site/role```

2. Run a smoke test:

    ```sudo puppet apply examples/bastion.pp --modulepath=/etc/puppetlabs/code/environments/production/modules:/home/centos/control-repo/site:/home/centos  --noop```

3. Apply the role for real:

    ```sudo puppet apply examples/bastion.pp --modulepath=/etc/puppetlabs/code/environments/production/modules:/home/centos/control-repo/site:/home/centos```

4. Verify Puppet actually changed your time server to `time.google.com` by running this command. Your output should be similar.

    ```grep server /etc/ntp.conf```
    ```server time.google.com```

**_In the commands above, you might wonder what `modulepath` is. We need to supply this option so Puppet knows where to look for Puppet code._**

### Commit your branch to Git

Run these commands:

```cd control-repo```

```git add .```

```git commit -m 'Adding Bastion Role and Base Profile'```

```git push origin studentN```

In the next lab, you will expand on the base profile.

## Discussion questions

1. How do roles and profiles differ?
1. At your job, what are some roles that could be useful?

|  [Previous Lab](../lab-09.1-Test-module-syntax-and-style)  |  [Next Lab](../lab-12.1-Expand-initial-roles-and-profiles)  |
