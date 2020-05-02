---
sidebar: manual
---

# Advanced use
The default settings works well for the most common use case, but there are many 
reasons to go for full options mode. For example:
- You don't use IIS
- You need to use [DNS validation](/reference/plugins/validation/dns) because
	- You are requesting a wildcard certificate
	- Port 80 is blocked on your network
- You are not running the program from your web server
- You are load balancing
- You need to run a script after each renewal, e.g. for [Exchange](/manual/advanced-use/examples/exchange)

## Interactive
This describes the basic steps of an full options rewenal from the interactive menu. It touches 
on concepts described [here](/reference/plugins/), because this mode of operation 
exposes more of the internal logic of the program to use to your advantage. Don't worry if
this seems overwhelming: most options have sensible defaults that you can select by just 
pressing `<Enter>` in response to a question.

- Choose `M` in the main menu to create a new certificate in full options mode
- Choose a [target plugin](/reference/plugins/target/) that will be used 
  to determine for which domain(s) the certificate should be issued.
- Choose a [validation plugin](/reference/plugins/validation/) to pick the
  method that will be used to prove ownership of your domain(s) to the ACME server.
- Pick between RSA and EC private keys, which are both [plugins](/reference/plugins/csr/) 
  used to generate a certificate signing request (CSR).
- One or more [store plugins](/reference/plugins/store/) must be selected to save
  the certificate. For Apache, nginx and others web servers the `PemFiles` plugin is commonly 
  chosen.
- One or more [installation plugins](/reference/plugins/installation/) can be selected 
  to run after the certificate has been requested. The standard IIS option is of course available, 
  but also the powerful [script installer](/reference/plugins/installation/script).
- A registration with the ACME server is created, if it doesn't already exist. You will be 
  asked to agree to the terms of service and to provide an email address that the server 
  administrators can use to contact you.
- The program negotiates with ACME server to try and prove your ownership of the domain(s) that you want to 
  create the certificate for, using the method of your choice. Getting validation right is often the most tricky 
  part of getting an ACME certificate. If there are problems please check out some 
  [common issues](/manual/validation-problems).
- After validating the domains, a certificate signing request is prepared according to 
  your specifications.
- The CSR is submitted to the ACME server and the signed response is saved according to your wishes.
- The program runs the requested installation steps.
- The program remembers all choices that you made while creating the certificate and applies them 
for each subsequent [renewal](/manual/automatic-renewal).

## Unattended
By providing the right [command line arguments](/reference/cli) at start up you can do 
everything that is possible in interactive mode (and more) without having to jump through the menu's.
This is great way to make win-acme part of a larger automation workflow.

### Examples
The `--target` switch, used to select a [target plugin](/reference/plugins/target/), 
triggers the unattended creation of new certificate.

- `--target manual` - selects the [manual plugin](/reference/plugins/target/manual).
- `--target iis` - selects the [iis plugin](/reference/plugins/target/iis).

Each plugin has their own inputs which it needs to generate the certificate, for example:

```wacs.exe --target manual --host www.domain.com --webroot C:\sites\wwwroot```
```wacs.exe --target iis --siteid 1 --excludebindings exclude.me```

There are some other parameters needed for first-time unattended use (e.g. on a clean server) 
to create the Let's Encrypt registration automatically (```--emailaddress myaddress@example.com --accepttos```). 
So a full command line to create a certificate for IIS site 1 on a clean server (except for 
the 'exclude.me' binding) would look like this:

```wacs.exe --target iis --siteid 1 --excludebindings exclude.me --emailaddress myaddress@example.com --accepttos```

#### More examples
Some application-specific examples are available [here](/manual/advanced-use/examples).
