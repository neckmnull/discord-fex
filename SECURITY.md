# Security Policy

## Safe use

Discord Fex processes network traffic at the driver level and requires elevated privileges. Before running it:

1. download files only from a trusted source;
2. fully extract the bundle into a separate directory;
3. review BAT, CMD, and PowerShell scripts before executing them;
4. verify binary checksums and digital signatures when available;
5. create a restore point before installing a service or driver;
6. do not disable antivirus protection entirely to run an unknown file.

WinDivert and network packet modification tools may trigger security software because of how they operate. A detection should not automatically be treated as either proof of malware or a guaranteed false positive.

The file `Запустить майнер.exe` is not involved in zapret operation. According to the original bundle documentation, it is a joke program from [Priler/AlbanianVirus](https://github.com/Priler/AlbanianVirus). Do not run it if you only need the core bundle functionality.

## Reporting a vulnerability

If a vulnerability affects this repository—for example, a configuration issue, a documentation issue, or a binary that does not match its stated source—submit a private report through **Security → Report a vulnerability** on GitHub. Do not publish a working exploit, personal network information, or sensitive diagnostic reports in a public issue.

If the issue is in a third-party component, report it to that component's maintainers:

- zapret: <https://github.com/bol-van/zapret/security>
- zapret-win-bundle: <https://github.com/bol-van/zapret-win-bundle/security>
- WinDivert: <https://github.com/basil00/WinDivert/security>

Include the following information in a report:

- the affected file and its SHA-256 hash;
- the Windows version;
- minimal reproduction steps;
- expected and actual behavior;
- the security impact;
- a safe way to contact you, if necessary.

Remove IP addresses, usernames, profile paths, and other personal information from logs before submitting them.
