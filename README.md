.SYNOPSIS
    Initializes PowerCLI by importing the module, optionally updating it, and connecting to a specified vCenter server.

.DESCRIPTION
    The Initialize-PowerCLI function automates the setup of your PowerCLI environment. It verifies that the VMware.PowerCLI module is installed and imports it if necessary, optionally updates the module, and then connects to a vCenter server. If multiple vCenter servers are provided, the function prompts the user to select one. The function also checks for existing connections to avoid redundant logins.

.PARAMETER vCenterNames
    An array of one or more vCenter server names. If more than one server is provided, you'll be prompted to select the desired vCenter.

.PARAMETER Credential
    An optional PSCredential object used for authentication when connecting to the vCenter server.

.PARAMETER UpdateModule
    An optional switch parameter. When specified, the function will attempt to update the VMware.PowerCLI module before establishing a connection.

.EXAMPLE
    Initialize-PowerCLI -vCenterNames @("vcenter1.example.com", "vcenter2.example.com") -Credential (Get-Credential) -UpdateModule

    This example imports (and optionally updates) the VMware.PowerCLI module, then prompts the user to select between the two provided vCenter servers and connects to the selected one.

.NOTES
    - Requires the VMware.PowerCLI module to be installed.
    - Utilizes Out-GridView for selection if multiple vCenter servers are provided.



xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx




Below is an explanation and example of how to package your code as a module and then use it in a separate PowerShell script:

---

### 1. **Package Your Code as a Module**

1. **Create a Module Folder:**

   - Create a folder for your module (e.g., `MyPowerCLIModule`).
   - Save your code in a file named `MyPowerCLIModule.psm1` within that folder.

   **Folder structure example:**

   ```
   C:\Modules\MyPowerCLIModule\
       └── MyPowerCLIModule.psm1
   ```

2. **(Optional) Create a Module Manifest:**

   - For more control (versioning, dependencies, etc.), create a manifest file named `MyPowerCLIModule.psd1` by running:
     ```powershell
     New-ModuleManifest -Path "C:\Modules\MyPowerCLIModule\MyPowerCLIModule.psd1" -RootModule "MyPowerCLIModule.psm1"
     ```
   - This manifest can then be used to import the module with all its metadata.

---

### 2. **Using the Module in a PowerShell Script**

1. **Import the Module:**

   In your PowerShell script (`.ps1`), import your module with the `Import-Module` command. For example:
   ```powershell
   # Import the module from its location
   Import-Module "C:\Modules\MyPowerCLIModule\MyPowerCLIModule.psm1" -Force
   ```
   The `-Force` switch is optional but useful if you are actively developing the module and want to reload any changes.

2. **Call the Function:**

   Now that the module is imported, you can call the `Initialize-PowerCLI` function just like any other cmdlet. For example:
   ```powershell
   # Define your vCenter names; replace with actual values for your environment
   $vCenters = @("vcenter1.myorg.com", "vcenter2.myorg.com")

   # Obtain credentials if required
   $cred = Get-Credential

   # Call the function; include -UpdateModule if you want to update the VMware.PowerCLI module as part of initialization
   Initialize-PowerCLI -vCenterNames $vCenters -Credential $cred -UpdateModule
   ```

3. **Continue With Additional Automation:**

   Once connected to vSphere, you can add additional PowerCLI commands in the same script:
   ```powershell
   # For example, list all virtual machines
   Get-VM | Format-Table Name, PowerState, VMHost -AutoSize
   ```

---

### 3. **Summary of the Workflow**

- **Module Creation:**
  - Place your function inside a `.psm1` file.
  - (Optionally) Create a module manifest (`.psd1`) for additional module metadata.

- **Module Import:**
  - In your `.ps1` script, use `Import-Module` to load your module.
  - The module will then export the `Initialize-PowerCLI` function.

- **Module Usage:**
  - Use the function in your script to update, import PowerCLI, and connect to the specified vCenter.
  - Replace placeholder values (like vCenter names) with actual values from your organization.

This modular approach lets you reuse your PowerCLI initialization logic across multiple scripts, keeping your code clean and maintainable.
