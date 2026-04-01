# EXPath HTTP Client oXygen Plugin

This project bundles the implementation of the [EXPath HTTP
Client](https://github.com/expath/expath-http-client-java) as a plugin
for the oXygen XML editor and makes the `http:send-request(...)`
extension function available throughout the editor.

## Installation

Install from this URL:

```
https://scdh.github.io/http-client-oxygen-plugin/descriptor.xml
```

Add this URL to the user dialogue in **Help** -> **Install new
add-ons...** and click through the dialogue. Currently the plugin is
not cryptographically signed, thus you have to choose "Continue
anyway" in order to install it.

## Usage

```xsl
<xsl:stylesheet
	xmlns:xsl="http://www.w3.org/1999/XSL/Transform"
	xmlns:http="http://expath.org/ns/http-client"
	...>

  <xsl:template name="get-from-url">
	<xsl:sequence select="http:send-request(...)"/>
  </xsl:template>

</xsl:stylesheet>
```

This plugin makes the `http:send-request(...)` XPath function known
throughout oXygen by the editor's mechanism for registering [XPath
extension
functions](https://www.oxygenxml.com/doc/versions/28.1/ug-editor/topics/saxon_extension_functions-x1.html)
(which is simply based on the service provider Java standard). So, all
you need to do is declare the correct namespace and use the function
from it like in the example above. **No need** to register the
extension function in a Saxon config file!

## Version Compatibility

The different minor and major releases of the EXPath HTTP Client have
a [dependency on certain versions of the Saxon XSLT
processor](https://github.com/expath/expath-http-client-java/tree/main?tab=readme-ov-file#using-the-saxon-ri). So
does Oxygen. Installing from the above URL manages versions for
you. Here's a version map, that is behind it.


| oXygen | HTTP Client | Saxon | Transformation Scenarios | XSLTOperation |
|:--|:--|:--|:--|:--|
| 23 | 1.3.0 | 9.9.1-7 | ⬜ | ⬜ |
| 24 | 1.4.2 | 10.6 | ⬜ | ❌[¹](issues/1) |
| 25 | 1.4.2 | 11.2 | ⬜ | ⬜ |
| 26+ | 1.5.2 | 12.3+ | ✅ | ✅ |

Why are there white squares? These combinations are
untested. Contributions of experience is welcome!

## License

As the EXPath HTTP Client is licensed under the Mozilla Public License
(MPL) and because this project re-assembles one of their java
archives, this project is licensed under the [MPL](LICENSE), too.
