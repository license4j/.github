
# LICENSE4J Licensing Library


[LICENSE4J](htps://www.license4j.com/) is a comprehensive **licensing library** and **license server** designed to streamline the software licensing process for developers. It facilitates the straightforward integration of licensing features into Java applications, allowing developers to implement necessary licensing functionality with minimal lines of code.

One of the standout features of LICENSE4J is its user-friendly, web-based License Manager running on top of the license server. This powerful tool is accessible from both desktop and mobile devices, making it convenient for users to manage licenses anytime and anywhere. The License Manager provides a seamless experience, enabling users to easily generate, validate, and manage licenses, thereby enhancing the overall efficiency of the licensing process.

With its robust capabilities, LICENSE4J not only simplifies the licensing workflow but also helps developers protect their intellectual property and ensure compliance with licensing agreements. This empowers businesses to focus more on development and less on the complexities of licensing, ultimately leading to a more efficient software delivery process.

The Licensing Library offers a variety of licensing models to cater to the diverse needs of customers. It supports different types of licenses, including both node-locked and floating licenses, providing flexibility in software deployment. Once you select the appropriate license type, you can customize it by adding specific features that meet your requirements.

For example, you can choose trial licenses, which allow for a limited-time evaluation of the software, or subscription-based licenses that grant access for a defined period. Additionally, you can opt for named-user licenses, which are assigned to specific individuals, or feature-based licenses that provide access to certain functionalities within the software.

Moreover, the Licensing Library allows the use of USB license dongles instead of relying on device IDs generated from hardware. These dongles serve as physical keys to enable software access. This comprehensive approach ensures that businesses can tailor their licensing strategies according to operational needs, budget considerations, and usage patterns.

## Getting Started
The Licensing Library can be found on [LICENSE4J @ Maven Central](https://central.sonatype.com/artifact/com.license4j/licensing-library), which allows developers to seamlessly integrate it into their projects. This library can be easily included by using either Maven or Gradle as your build automation tools. To add the Licensing Library to your project, simply include the appropriate dependency in your project's configuration file, following the guidelines provided in the documentation. This enables you to leverage the library's features without any hassle, ensuring a smooth development process.

    <dependency>
        <groupId>com.license4j</groupId>
        <artifactId>licensing-library</artifactId>
        <version>5.0.0</version>
    </dependency>

## Validate a License
To validate a license, you simply need to configure the necessary properties within your application and then invoke the validate method. This process checks the integrity and authenticity of the license. If the validation is successful, the system will automatically save the relevant license information. This can be stored either in a specified license file on disk, which can be easily accessed, or in the system registry if you are operating on a Windows platform.

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

    
