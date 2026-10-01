# OAST Lab

OAST Lab is a Windows x64 desktop application for receiving HTTP, HTTPS, and DNS callbacks. It creates callback identifiers and displays received events in a shared table. The interface and user guide are in English.

## Download and install

Download `OastLab-Setup-1.0.0-Win64.exe` from GitHub Releases. It includes the application, TLS companion, F1 user guide, certificate helper, and license. The default installation is for the current user; the wizard also offers an all-users installation. Read and accept the license before installing.

For a portable run, keep these files in the indicated layout:

```text
OastLab.exe
OastLab.TlsHost.exe
Help/OastLab.chm
Tools/Create-TestCertificate.ps1
LICENSE.txt
```

Start `OastLab.exe`; the listener is initially stopped.

OAST Lab requires Windows 10 or later (x64). HTTPS uses .NET Framework 4.8 through `OastLab.TlsHost.exe`.

## Use

1. Select a local address in **Listen on IPv4** and a TCP port from 1024 to 65535. The default `0.0.0.0` listens on all IPv4 interfaces; `127.0.0.1` listens only on this computer.
2. Select **Start**. The application creates a callback URL whose identifier remains valid until the session is cleared.
3. Select **Send local test**. A successful test returns HTTP 204 and adds an event showing the UTC time, protocol, method, peer, and correlation ID.
4. Use **New callback** to create another identifier. The copy icon at the end of the URL field copies the displayed URL to the clipboard.
5. Use **Clear session** to remove events and invalidate identifiers, or **Stop** to close the listener and clear the session.

For HTTPS, select a `.pfx` or `.p12` file containing the certificate and private key, enter its password, then start the receiver. The password is kept only in memory. The optional `Create-TestCertificate.ps1` helper creates a local test certificate.

The **DNS** section has a separate UDP listener, configurable IPv4 address, port, and delegated zone. **New token** creates a callback domain; **Send local DNS test** checks the listener from this computer. External DNS callbacks require your own DNS delegation and network routing.

The event table retains the most recent 200 events in memory. Up to 100 identifiers can be active at once; use **Clear session** before creating more. Press **F1** or use the sidebar help link to open the user guide.

## Verify downloads

`sha256.txt` lists SHA-256 checksums for the release files. After downloading, compare a file with its listed hash in PowerShell:

```powershell
(Get-FileHash -Algorithm SHA256 -LiteralPath 'OastLab-Setup-1.0.0-Win64.exe').Hash
```

## License

OAST Lab is free for non-commercial use under the OAST Lab license included with the distribution. Commercial use requires a separate written agreement with the author.
