# Virtual-Machine
Powershell script to create a new VM in Microsoft Hyper-V

Run it from an elevated PowerShell session on the Hyper-V host. The only required parameter is -VMName; everything else has sensible defaults (Gen 2, 2 vCPUs, 4 GB RAM, 80 GB dynamically expanding VHDX, the host's default storage paths, and the first external switch it finds).

A few things worth knowing. Use -WhatIf first to dry-run it without creating anything. For Windows 11 guests, add -EnableTPM along with an ISO, since the installer requires a TPM. For most Linux distributions, pass -SecureBootTemplate MicrosoftUEFICertificateAuthority, otherwise the VM will refuse to boot the ISO under Secure Boot. If anything fails partway through, the script removes the half-built VM and its VHDX so you can fix the issue and re-run cleanly.

If execution policy blocks it, Set-ExecutionPolicy -Scope Process RemoteSigned will allow it for the current session only.
