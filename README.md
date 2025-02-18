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
