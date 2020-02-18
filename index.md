# win-acme
This is a ACMEv2 client for Windows that aims to be very simple to start with, 
but powerful enough to grow into almost every scenario.

- A very simple text interface to create and install certificates on a local IIS server
- A more advanced text interface for many other use cases, including [Apache](/manual/advanced-use/examples/apache) and [Exchange](/manual/advanced-use/examples/exchange)
- Automatically creates a scheduled task to renew certificates when needed
- Get certificates with 
	wildcards (`*.example.com`), 
	international names (`证书.example.com`), 
	[OCSP Must Staple](/reference/plugins/csr/rsa) extension, optional 
	[re-use](/reference/plugins/csr/rsa) of private keys,
	[EC](/reference/plugins/csr/ec) crypto or use your own 
	[CSR](/reference/plugins/target/csr)
- Advanced toolkit for DNS, HTTP and TLS validation:
	[SFTP](/reference/plugins/validation/http/sftp)/[FTPS](/reference/plugins/validation/http/ftps), 
	[acme-dns](/reference/plugins/validation/dns/acme-dns), 
	[Azure](/reference/plugins/validation/dns/azure), 
	[Route53](/reference/plugins/validation/dns/route53), 
	[Cloudflare](/reference/plugins/validation/dns/cloudflare) 
	and more...
- Completely unattended operation from the command line
- Other forms of automation through manipulation of `.json` files
- Write your own Powershell `.ps1` scripts to handle custom installation and validation
- Build your own plugins with C# and make the program do exactly what you want

![screenshot](/assets/screenshot.png)

# Sponsors
- <img src="https://user-images.githubusercontent.com/11052380/74772623-a7128b00-5290-11ea-958d-10420c770b30.png" alt="Insurance Technology Services" width="150px" /> [eGov Strategies](https://www.egovstrategies.com/)
- <img src="https://user-images.githubusercontent.com/11052380/72933908-fb465000-3d62-11ea-9b97-57b8a29fd783.png" alt="Insurance Technology Services" width="50px" /> [Insurance Technology Services](https://insurancetechnologyservices.com/)
- [e-shop LTD](https://www.e-shop.co.il/)
- The Proof Group @proofgroup
- [imagenia.fr](http://www.imagenia.fr/)

# Getting started
Download the `.zip` file from the download menu, unpack it to a location on your hard disk
and run `wacs.exe`. If you require assistance please check the [manual](/manual/getting-started)
first before looking for [support](/support/).
