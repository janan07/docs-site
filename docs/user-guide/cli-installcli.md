# Installing Zowe CLI

As a systems programmer or application developer, you install Zowe CLI on your PC.

## Methods to install Zowe CLI

You can use either of the following methods to install Zowe CLI.

- [Install Zowe CLI from local package](#installing-zowe-cli-from-local-package)
- [Install Zowe CLI from online registry](#installing-zowe-cli-from-online-registry)

If you encounter problems when you attempt to install Zowe CLI, see [Troubleshooting installing Zowe CLI](troubleshootinstall.html#troubleshooting-installing-zowe-cli).

### Installing Zowe CLI from local package

If you do not have internet access at your site, use the following method to install Zowe CLI from a local package.

**Follow these steps:**

1. Ensure that the following prerequisite software is installed on your PC:

    -  [**Node.js V8.0 or later**](https://nodejs.org/en/download/)

        **Tip:** You might need to restart the command prompt after installing Node.js. Issue the command `node --version` to verify that Node.js is installed.

    - **Node Package Manager V5.0 or later**

        npm is included with the Node.js installation. Issue the command `npm --version` to verify that npm is installed.

2. [Obtain the Zowe installation media](gettingstarted.md). The Zowe installation media contains the `zowe-cli-bundle.zip` file. Use FTP to distribute the zip file to client workstations.

3. Open a command line window. For example, Windows Command Prompt. Browse to the directory where you downloaded the Zowe CLI installation bundle (.zip file). Issue the following command to unzip the files:

    ```
    unzip zowe-cli-bundle.zip
    ```

    The command expands files into your working directory for Zowe CLI and Zowe CLI plug-ins.

4. Issue the following command to install Zowe CLI on your PC:

    ```
    npm install -g zowe-cli-<VERSION_NUMBER>.tgz 
    ```
    - **<VERSION_NUMBER>**

        The version of Zowe CLI that you want to install from the package. The following is an example of a full package name for Zowe CLI: `zowe-core-2.0.0-next.201810161407.tgz`

    **Note:** On Linux, you might need to prepend `sudo` to your `npm` commands so that you can issue the install and uninstall commands. For more information, see [Troubleshooting installing Zowe CLI](troubleshootinstall.html#troubleshooting-installing-zowe-cli).

    Zowe CLI is installed on your PC. See [Installing Plug-ins](cli-installplugins.md) for information about the commands for installing plug-ins from the package.

5. Create a `zosmf` profile so that you can issue commands that communicate with z/OSMF.

    **Note:** For information about how to create a profile, see [Creating a Zowe CLI profile](#creating-a-zowe-cli-profile).

    **Tip:** Zowe CLI profiles contain information that is required for the product to interact with remote systems. For example, host name, port, and user ID. Profiles let you target unique systems, regions, or instances for a command. Most Zowe CLI [command groups](cli-usingcli.html#zowe-cli-command-groups) require a Zowe CLI `zosmf` profile.

After you install and configure Zowe CLI, you can issue the `zowe --help` command to view a list of available commands. For more information, see [Display Help](cli-usingcli.html#displaying-zowe-cli-help).


### Installing Zowe CLI from online registry

If your PC is connected to the Internet, you can use the following method to install Zowe CLI from an npm registry.

**Follow these steps:**

1.  Ensure that the following prerequisite software is installed on your PC:

    - [**Node.js V8.0 or later**](https://nodejs.org/en/download/)

        **Tip:** You might need to restart the command prompt after installing Node.js. Issue the command `node --version` to verify that Node.js is installed.

    - **Node Package Manager V5.0 or later**

        npm is included with the Node.js installation. Issue the command `npm --version` to verify that npm is installed.

2.  Issue the following command to set the registry to the Zowe CLI scoped package on Bintray. In addition to setting the scoped registry, your non-scoped registry must be set to an npm registry that includes all of the dependencies for Zowe CLI, such as the global npm registry:

    ```
    npm config set @brightside:registry https://api.bintray.com/npm/ca/brightside
    ```

3.  Issue the following command to install Zowe CLI from the registry:

    ```
    npm install -g @brightside/core@next
    ```

4. (Optional) To install all available plug-ins to Zowe CLI, issue the following command:

    ```
    bright plugins install @brightside/cics@next
    ```
    **Note:** For more information about how to install multiple plug-ins, update to a specific version of a plug-in, and install from specific registries, see [Installing plug-ins](cli-installplugins.md).

5.  Create a `zosmf` profile so that you can issue commands that communicate with z/OSMF. For information about how to create a profile, see [Creating a Zowe CLI profile](#creating-a-zowe-cli-profile).

    **Tip:** Zowe CLI profiles contain information that is required for the product to interact with remote systems. For example, host name, port, and user ID. Profiles let you target unique systems, regions, or instances for a command. Most Zowe CLI [command groups](cli-usingcli.html#zowe-cli-command-groups) require a Zowe CLI `zosmf` profile.

After you install and configure Zowe CLI, you can issue the `zowe --help` command to view a list of available commands. For more information, see [How to display Zowe CLI help](cli-usingcli.html#displaying-zowe-cli-help).



## Creating a Zowe CLI profile

Profiles are a Zowe CLI functionality that let you store configuration information for use on multiple commands. You can create a profile that contains your username, password, and connection details for a particular mainframe system, then reuse that profile to avoid typing it again on every command. You can switch between profiles to quickly target different mainframe subsystems.

**Important\!** A `zosmf` profile is required to issue most Zowe CLI commands. The first profile that you create becomes your default profile. When you issue any command that requires
a `zosmf` profile, the command executes using your default profile
unless you specify a specific profile name on that command.

**Follow these steps:**

1.  To create a `zosmf` profile, issue the following command.  
  Refer to the available options in the help text to define your profile:   
    ```
    zowe profiles create zosmf-profile --help
    ```

**Note:** After you create a profile, verify that it can communicate with z/OSMF. For more information, see [Testing Zowe CLI connection to z/OSMF](#testing-zowe-cli-connection-to-zosmf).


## Testing Zowe CLI connection to z/OSMF
After you configure a Zowe CLI `zosmf` profile to connect to z/OSMF on your mainframe systems, you can issue a command at any time to receive diagnostic information from the server and confirm that your profile can communicate with z/OSMF.

**Tip:** In this documentation we provide command syntax to help you create a basic profile. We recommend that you append `--help` to the end of commands in the product to see the complete set of commands and options available to you. For example, issue `zowe profiles --help` to learn more about how to list profiles, switch your default profile, or create different profile types.

After you create a profile, run a test to verify that Zowe CLI can communicate properly with z/OSMF. You can test your default profile and any other Zowe CLI profile that you created.

**Default profile**

  - Verify that you can use your default profile to communicate with z/OSMF by issuing the following command:

    ```
    zowe zosmf check status
    ```

**Specific profile**

  - Verify that you can use a specific profile to communicate with
    z/OSMF by issuing the following command: 

    ```
    zowe zosmf check status --zosmf-profile <profile_name>
    ```

The commands return a success or failure message and display information about your z/OSMF server. For example, the z/OSMF version number and a list of installed plug-ins. Report any failure to your systems administrator and use the information for diagnostic purposes.
