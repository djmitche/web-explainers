# How to experiment with the form-factor hint

In general, the form-factor hint behaves like any other [client
hint](https://developer.mozilla.org/en-US/docs/Web/HTTP/Client_hints).

## Enabling

Until this hint is enabled by default, it must be enabled as a feature, with
the command-line argument `--enable-features=ClientHintsFormFactor`.

## Via Headers

Include `Sec-CH-UA-Form-Factor` in the `Accept-CH` HTTP response header, e.g.,

```
Accept-CH: Sec-CH-UA-Form-Factor
```

Browsers which support the hint will include the `Sec-CH-UA-Form-Factor` header
in subsequent requests. The value of the header will be a comma-separated list
of form factors as described in the [draft
standard](https://github.com/WICG/ua-client-hints).

## Via getHighEntropyValues

Call
[NavigatorUAData.getHighEntropyValues](https://developer.mozilla.org/en-US/docs/Web/API/NavigatorUAData/getHighEntropyValues)
with `"formFactor"` included in the `hints` argument.

Browsers which support the hint will include a property `formFactor` in the
returned object, containing an array of form factors.
