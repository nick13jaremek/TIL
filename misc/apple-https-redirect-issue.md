# Problem

When having a **HTTP**  URL with query parameters and a string appended after a hash symbol (#) as follows:

```
   http://www.my-url.com/login/?token=1234#user=johndoe
```

If at a given time, this URL triggers a redirect to some **HTTPS** URL, then the string after the hash symbol is dropped in **Apple's Safari web browsers**, yielding the following URL:

```
   https://www.my-url.com/home/?token=1234
```

The problem lies in the redirect from a non-secure protocol (HTPP) to a secure protocol (HTTPS). It seems Apple enforces the after-hash-string drop due to security considerations. Other Web browsers such as *Google's Chrome* or *Mozilla's Firefox* do not apply such an action.

# Solution

The most straightforward solution is to work with the **HTTPS** protocol on both URLs. In such a case *Apple's Safari* will not drop the characters after the hash symbol present on the URL.

That is, redirect from HTTPS-based URL to  another HTTPS-based URL, do **NOT mix up** protocols in the redirect process.

Additionally, if your infrastructure makes use of some CDNs such as *Amazon's Cloudfront*, make sure the CDN is configured to redirect the URLs to the proper protocols.

