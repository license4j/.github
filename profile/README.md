
# LICENSE4J Licensing Library


[LICENSE4J](https://www.license4j.com "LICENSE4J Homepage") is a comprehensive **licensing library** and **license server** designed to streamline the software licensing process for developers. It facilitates the straightforward integration of licensing features into Java applications, allowing developers to implement necessary licensing functionality with minimal lines of code.

One of the standout features of LICENSE4J is its user-friendly, web-based License Manager running on top of the license server. This powerful tool is accessible from both desktop and mobile devices, making it convenient for users to manage licenses anytime and anywhere. The License Manager provides a seamless experience, enabling users to easily generate, validate, and manage licenses, thereby enhancing the overall efficiency of the licensing process.

With its robust capabilities, LICENSE4J not only simplifies the licensing workflow but also helps developers protect their intellectual property and ensure compliance with licensing agreements. This empowers businesses to focus more on development and less on the complexities of licensing, ultimately leading to a more efficient software delivery process.

The Licensing Library offers a variety of licensing models to cater to the diverse needs of customers. It supports different types of licenses, including both node-locked and floating licenses, providing flexibility in software deployment. Once you select the appropriate license type, you can customize it by adding specific features that meet your requirements.

For example, you can choose trial licenses, which allow for a limited-time evaluation of the software, or subscription-based licenses that grant access for a defined period. Additionally, you can opt for named-user licenses, which are assigned to specific individuals, or feature-based licenses that provide access to certain functionalities within the software.

Moreover, the Licensing Library allows the use of USB license dongles instead of relying on device IDs generated from hardware. These dongles serve as physical keys to enable software access. This comprehensive approach ensures that businesses can tailor their licensing strategies according to operational needs, budget considerations, and usage patterns.

## Getting Started
[![Maven Central Version](https://img.shields.io/maven-central/v/com.license4j/licensing-library)](https://central.sonatype.com/artifact/com.license4j/licensing-library)
[![javadoc](https://javadoc.io/badge2/com.license4j/licensing-library/javadoc.svg)](https://javadoc.io/doc/com.license4j/licensing-library)

The Licensing Library can be found on [LICENSE4J @ Maven Central](https://central.sonatype.com/artifact/com.license4j/licensing-library), which allows developers to seamlessly integrate it into their projects. This library can be easily included by using either Maven or Gradle as your build automation tools. To add the Licensing Library to your project, simply include the appropriate dependency in your project's configuration file, following the guidelines provided in the documentation. This enables you to leverage the library's features without any hassle, ensuring a smooth development process.

    <dependency>
        <groupId>com.license4j</groupId>
        <artifactId>licensing-library</artifactId>
        <version>5.0.3</version>
    </dependency>

## Validate (activate) a License
To validate a license, you simply need to configure the necessary properties within your application and then invoke the validate method. This process checks the integrity and authenticity of the license. If the validation is successful, the system will automatically save the relevant license information. This can be stored either in a specified license file on disk, which can be easily accessed, or in the system registry if you are operating on a Windows platform. See [quick start](https://www.license4j.com/documents/java-licensing-library/quick-start/) also.

    // Use builder to build the License object
    // The only required parameter is product
    // hash code given on web-application
    // Products page
    License.getInstance().getBuilder()
            .product("product-hash-code")
            .build();
    
    // Validate the license key
    License.getInstance()
            .validate("12345-12345-12345-12345");
    
    // Check the status to see whether it is valid or not
    License.getInstance().getStatus();

    
## Invalidate (deactivate) a License
License invalidation is a crucial process in software licensing that involves deactivating a license key that has already been validated. This action is necessary in situations such as transferring software ownership, upgrading a license, or revoking access due to compliance issues.

The method used to invalidate a license is `License.getInstance().invalidate()`. When this method is invoked, it accomplishes two important tasks: first, it invalidates the license, rendering it unusable for future access to the software. This ensures that the software can no longer be operated using that specific license key. Second, the method removes any associated saved license file from the local storage or deletes the license data from the system registry. This cleanup is essential to prevent any potential misuse or unauthorized access to the software.

By implementing license invalidation, software developers can better manage their licensing systems, ensuring only authorized users have access to their products while maintaining compliance with licensing agreements.

The Licensing Library is designed to efficiently manage activated license data by providing the functionality to save and load this information from file stored on your computer's disk or directly from the Windows registry.  This streamlined process is entirely managed by the library itself, allowing you as a developer to avoid the complexities of implementing your own routines for saving and loading license files.  This means you can focus on other aspects of your application without worrying about the underlying mechanisms for license management.

## License Loading/Saving on Disk or Windows Registry

The `Builder` class offers two distinct methods for specifying the location of the license file.  **`file`** method allows users to define the exact path to the license file on their file system. **`registry`** method provides an option to set the location via the Windows registry, enabling integration with system-level configurations. These methods ensure flexibility in managing license files according to user preferences or system requirements.

The license file saving feature is enabled by default. If you also utilize the **`registry`** method to define a Windows registry location, it will be applied on Windows systems when the software is executed.  This allows you to use both **`file`** and **registry** methods: you can save the license file on non-Windows systems while storing the license data in the registry on Windows systems.

Both **`file`** and **`registry`** methods for license management are optional. If neither method is used, the default location will be utilized.

**License File:** The default license file will be located in the current user's home folder, with the last eight characters of the product hash code appended to it. For example, if the product hash code is `94E1B381016BEE2CBC5F644B6F078C28` and the username is `john`, the default license file location on Windows would be `C:\Users\john\.6F078C28\license.l4j`. Similarly, on Linux and Mac systems, the location would be `/home/john/.6F078C28/license.l4j`.

**License Registry:** If using the registry method, the defined location will be under `HKEY_CURRENT_USER\SOFTWARE\`. Both the key and value must be defined and separated with a double backslash (\\). For instance, if you use `MySoftware\\license`, the resulting location would be `HKEY_CURRENT_USER\SOFTWARE\MySoftware\license`.

When the `validate()` method is invoked without providing a license key argument, it will initiate a search for any previously activated and stored license data. This data can be located on either the disk or in the registry, depending on the preferences specified in the builder method used during initialization. The validation process will check the integrity of the stored license information and confirm its validity. Notably, this validation does not require an active internet connection, making it a convenient choice for environments that are offline or have restricted internet access.

In contrast, when the `validate("the-license-key")` method is called with a specific license key argument, the process takes a different route. This version of the method will establish a connection to the designated license server to validate the provided license key. It will attempt to both validate and activate the license remotely. If the activation is successful, the system will securely save the newly activated license data for future reference, again storing it either on disk or in the registry, as determined by the settings specified in the builder method. This ensures that the license can be easily accessed for subsequent validation without needing to connect to the internet again, assuming the licensing policy allows it.

**An Example:**
<pre>License.getInstance().getBuilder() .product("product-hash-code")
		.file(System.getProperty("user.home") + "/MyProduct/license.l4j")
		.registry(MyProduct\\license) 
		.build();</pre>


## Hardware, Virtualization Detection
The License4J Licensing library offers advanced capabilities for detecting the hardware features of client systems. It gathers detailed information from various components, including the Central Processing Unit (CPU), Hard Disk Drive (HDD), disk partitions, the manufacturer of the hardware, and the mainboard specifications. 

In addition to this hardware information, the library is capable of detecting whether the system is operating in a virtualization or containerized environment, which is essential for ensuring that licensing and usage compliance are maintained across different deployment scenarios. 

Furthermore, License4J can identify many popular cloud service providers, allowing it to recognize environments such as Amazon EC2, Microsoft Azure, Google Cloud Platform, Oracle Cloud, Alibaba Cloud, DigitalOcean, and UpCloud. This functionality helps developers and organizations manage their licensing effectively in various deployment situations, whether on local hardware or in the cloud.

See example repository: [https://github.com/license4j/license4j-hardware-virtualization-container-cloud-usb-detection](https://github.com/license4j/license4j-hardware-virtualization-container-cloud-usb-detection)

## On-Premises License Server
For organizations prioritizing complete control over their licensing infrastructure, the [On-Premises License Server](https://www.license4j.com/products/on-premises-license-server/) provides a robust solution that mirrors the full feature set of its SaaS counterpart. This version allows you to download and install the license server directly within your own environment, whether it's on your private network, a dedicated server, or a private cloud instance. This ensures that all license data, operations, and server management remain entirely under your direct supervision, making it ideal for those with stringent security or compliance requirements.

The on-premises deployment delivers the exact same comprehensive features as the SaaS version. You'll have access to identical capabilities for generating, managing, validating, activating, and deactivating licenses, along with advanced functionalities like sending notification emails, integrating with webhooks, and processing payment information.

The key distinction lies in the deployment model, offering perpetual licensing for the software itself, meaning you own the license outright. To ensure continued access to future enhancements, security updates, and new features, an optional yearly maintenance plan is available. This plan offers a cost-effective way to keep your licensing system current and optimized over time, making the on-premises server an ideal choice for businesses seeking long-term ownership and maximum operational autonomy.

## Floating License Server
The [Floating License Server](https://www.license4j.com/products/floating-license-server/) is ideal for deployment within a customer's local network, especially when internet connectivity is limited or unavailable. Its main purpose is to expertly control and manage the concurrent usage of floating (network concurrent) licenses among users within that internal network. This ensures that a defined number of users can access and utilize the licensed software simultaneously, all without needing external network access for license validation.

This server solution features a highly streamlined, single-page management interface. This intuitive design simplifies the critical tasks of installing new licenses and monitoring concurrent use. Administrators can quickly gain an overview of active licenses and usage patterns, making it easy to ensure compliance and allocate resources efficiently, all from one accessible dashboard. This makes the Floating License Server an excellent choice for organizations needing robust, self-contained license management for their offline operations.
