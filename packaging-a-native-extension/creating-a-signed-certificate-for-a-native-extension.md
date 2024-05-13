# Creating a signed certificate for a native extension

You can choose to digitally sign your native extension. Signing an extension is
optional.

Digitally signing your native extension with a certificate issued by a
recognized certification authority (CA) provides significant assurance to AIR
application developers that:

- the native extension they are packaging with their application has not been
  accidentally or maliciously altered.

- you are the signer (publisher) of the native extension.

> Note: When an AIR application is packaged, the AIR application's certificate,
> not the native extension's certificate if it is provided, is what the
> application's users see.

Obtain a certificate from a certification authority. Creating a digitally signed
certificate for your native extension is the same as creating a certificate for
an AIR application. See
[Signing AIR applications](https://web.archive.org/web/20160929212314/http://help.adobe.com/en_US/air/build/WSfffb011ac560372f-19aa73f128cc9f05e8-8000.html)
in
[Building Adobe® AIR® Applications](https://web.archive.org/web/20160929212314/http://help.adobe.com/en_US/air/build/index.html).
