
# LICENSE4J Licensing Library


[LICENSE4J](https://www.license4j.com "LICENSE4J Homepage") is a comprehensive **licensing library** and **license server** designed to streamline the software licensing process for developers. It facilitates the straightforward integration of licensing features into Java applications, allowing developers to implement necessary licensing functionality with minimal lines of code.

One of the standout features of LICENSE4J is its user-friendly, web-based License Manager running on top of the license server. This powerful tool is accessible from both desktop and mobile devices, making it convenient for users to manage licenses anytime and anywhere. The License Manager provides a seamless experience, enabling users to easily generate, validate, and manage licenses, thereby enhancing the overall efficiency of the licensing process.

With its robust capabilities, LICENSE4J not only simplifies the licensing workflow but also helps developers protect their intellectual property and ensure compliance with licensing agreements. This empowers businesses to focus more on development and less on the complexities of licensing, ultimately leading to a more efficient software delivery process.

The Licensing Library offers a variety of licensing models to cater to the diverse needs of customers. It supports different types of licenses, including both node-locked and floating licenses, providing flexibility in software deployment. Once you select the appropriate license type, you can customize it by adding specific features that meet your requirements.

For example, you can choose trial licenses, which allow for a limited-time evaluation of the software, or subscription-based licenses that grant access for a defined period. Additionally, you can opt for named-user licenses, which are assigned to specific individuals, or feature-based licenses that provide access to certain functionalities within the software.

Moreover, the Licensing Library allows the use of USB license dongles instead of relying on device IDs generated from hardware. These dongles serve as physical keys to enable software access. This comprehensive approach ensures that businesses can tailor their licensing strategies according to operational needs, budget considerations, and usage patterns.

## Getting Started
[![Maven Central Version](https://img.shields.io/maven-central/v/com.license4j/licensing-library)](https://central.sonatype.com/artifact/com.license4j/licensing-library)

The Licensing Library can be found on [LICENSE4J @ Maven Central](https://central.sonatype.com/artifact/com.license4j/licensing-library), which allows developers to seamlessly integrate it into their projects. This library can be easily included by using either Maven or Gradle as your build automation tools. To add the Licensing Library to your project, simply include the appropriate dependency in your project's configuration file, following the guidelines provided in the documentation. This enables you to leverage the library's features without any hassle, ensuring a smooth development process.

    <dependency>
        <groupId>com.license4j</groupId>
        <artifactId>licensing-library</artifactId>
        <version>5.0.1</version>
    </dependency>

## Validate (activate) a License
To validate a license, you simply need to configure the necessary properties within your application and then invoke the validate method. This process checks the integrity and authenticity of the license. If the validation is successful, the system will automatically save the relevant license information. This can be stored either in a specified license file on disk, which can be easily accessed, or in the system registry if you are operating on a Windows platform. See [quick start](https://www.license4j.com/documents/quickstart/) also.

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

## Hardware, Virtualization Detection
The License4J Licensing library offers advanced capabilities for detecting the hardware features of client systems. It gathers detailed information from various components, including the Central Processing Unit (CPU), Hard Disk Drive (HDD), disk partitions, the manufacturer of the hardware, and the mainboard specifications. 

In addition to this hardware information, the library is capable of detecting whether the system is operating in a virtualization or containerized environment, which is essential for ensuring that licensing and usage compliance are maintained across different deployment scenarios. 

Furthermore, License4J can identify many popular cloud service providers, allowing it to recognize environments such as Amazon EC2, Microsoft Azure, Google Cloud Platform, Oracle Cloud, Alibaba Cloud, DigitalOcean, and UpCloud. This functionality helps developers and organizations manage their licensing effectively in various deployment situations, whether on local hardware or in the cloud.

See example repository: [https://github.com/license4j/license4j-hardware-virtualization-container-cloud-usb-detection](https://github.com/license4j/license4j-hardware-virtualization-container-cloud-usb-detection)
