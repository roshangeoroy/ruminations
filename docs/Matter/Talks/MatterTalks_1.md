# Scaling Secure products into volume production

This is the summary of the tech talk conducted by [Silicon Labs](https://www.silabs.com/support/training/scaling-secure-matter-products-into-production) on February 15th, 2024 as part of the 2024 Tech Talks : Matter Series. The talk was oriented towards the difficulties and possible design methodologies that could be followed to facilitate the manufacture of large volume Matter products.

## Context overview
Matter devices will contain unique certificates - Device Attestation Certificates (DACs) which are used to verify the device before commissioning them to the Matter fabric (network). There are mainly 3 certification authorities, and the hierarchy is as listed below:

Connectivity Standards Alliance’s Test and Certification Oversight Committee (TCOC) -> Product Attestation Authority (PAA) -> Product Attestation Intermediate (PAI) -> DACs

After the development of a Matter product, the vendor needs to apply for certification from the Connectivity Standards Alliance (CSA) by applying for membership and going through various procedures which include testing the devices in authorized test labs and so on. CSA then assigns the status of PAA to authorities which become root certificate authorities for the DA process. Each PAA contains a private key-public key pair. The private key is used to sign PAI, an entity directly in charge of issuing DACs. PAI private key is used to sign the DACs.

## When Matters get Complicated
The talk detailed complications that can arise during the manufacturing of Matter products and deployment, and it provided appropriate solutions based on the type of product as well.

Manufacturing used to be simple when all products were unique, but this is not the case for Matter products where each product has its own keys and certificates. And these data needs to be kept secure for it to make sense.

The standard method of provisioning and device is to use a loader application programmed into the device which can accept the loader information and program the device. This introduces the following two challenges:

### Challenge 1: Storage Gets More Complex
Storing the keys simply in the flash of the device is not secure and is not easily updatable as well. Introducing proper storage is therefore necessary but increases complexity.
- Key will be wrapped with PUF.
- Stored in psa_crypto ITS (Internal Trusted Storage) format for consistency with industry standard and ease of use.
- Stored in non-volatile memory database for efficiently updating it (Silicon Labs provides a library for NVM data management).

The loader is indeed complex, but all of the libraries to execute these already exist; therefore, the effort required is less. Usually, when there's a high-level scripting language and a low-level language, the highly complex features are implemented in the high-level script. But here quite the opposite is done and for two reasons:
- The code to handle all the complex tasks already exists.
- Manufacturing environments keep changing. The loader will always run on the device.

This leads to a scalable way for the tester to provision the data to the device.

### Challenge 2: How to Get the Data?
The DACs will contain the private key. The device itself making the private key is most secure but DACs certificates can't be made ahead of time. If PAI creates the key, we can make it ahead of time but the transport will make it vulnerable.

### The Simplest Setup
![simplest_setup]
The simplest setup involves the PAI periodically generating a lot of DACs with private keys and sending them to the Tester for provisioning using the loader (provided by Silicon Labs). This is good when cost is prioritized over security. It's bad for security as the private keys are transported and stored in multiple places.

### On-Line Manufacturing
![on_line]
The change in this method is the device will generate the private key on its own. The tester will set the loader on the device which generates the private key. The public key is sent to the Tester and up to the PAI which generates the DAC which is sent back to the device via the Tester. This has some issues of its own - extra test time due to this communication, dependence on internet connection, DDoS attack. Contract manufacturers will not be technically (insert appropriate word here) to manage all this.
It is appropriate for OEMs who can tolerate production interruption and value the security increase.

### Most Secure Solution
![most_secure]
Here PAI is moved from Cloud to Contract Manufacturer. For Matter, this is difficult due to the way the requirements are structured. This is good for products that need high security and can tolerate high cost and OEMs who have their own manufacturing sites.

All these solutions do not matter if we're not proactive about manufacturing. Best practice would be to use the same script and loader that will be used in production so there are no surprises when going into production. Production will be debugged during development itself. Tools can easily support this. Post-build steps can run provisioning scripts. If structured properly firmware can be updated without changing provisioned data for faster firmware development.

Silicon Labs will provide provisioning support with scripts and loaders for dev and prod. Will provide consistency between protocols and ecosystems. The SDK provided by them will contain all these support tools straight out on a demo application.

## Conclusion
While developers are jumping onto Matter development it is important to have a high-level plan from development to manufacturing to deployment. The talk gave insight into the challenges that need to be addressed and solved during this cycle. Each product has its own needs therefore no solution works best, but the common pattern can be used to deliver all of the desired benifits.

[simplest_setup]: MatterTalks_1/simplest_setup.png
[on_line]: MatterTalks_1/on_line.png
[most_secure]: MatterTalks_1/most_secure.png

## References
* [Tech Talk by Silion Labs](https://www.silabs.com/support/training/scaling-secure-matter-products-into-production) 

* [Information regarding Device Attestation from Nordic](https://developer.nordicsemi.com/nRF_Connect_SDK/doc/latest/nrf/protocols/matter/end_product/attestation.html#device-attestation-certificates)