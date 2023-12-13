# Problem

Sites often differ dramatically depending on the device where they are loaded.
This has long been the case with "mobile" and "desktop" versions of sites, but
novel user-agent form-factors such as cars, televisions, and virtual reality
introduce new opportunities for site customization.

Historically, sites have derived the form-factor of a user-agent through some
combination of the user-agent string, the `Sec-CH-UA-Mobile` hint, and screen
size. The signal from these sources is unclear, and incorrect derivations lead
to poor user experience, such as a desktop site designed for mouse and keyboard
interaction appearing on a television.

In some cases, it is important to know the form-factor of a user-agent before
the first request is served. For example, some form-factors require large
client-side libraries which should not be transmitted when not required.

Providing a detailed description of the user-agent's form factor could provide
signficant metadata for undesirable fingerprinting, especially for early-adopter
users of new form-factors. We must avoid providing such metadata except where
desired by the user.

# Proposal

[Client Hints](https://github.com/WICG/ua-client-hints) support providing sites
with clear signals about client characteristics in a privacy-preserving fashion.
We propose a new hint,
[`Sec-CH-UA-Form-Factor`](https://wicg.github.io/ua-client-hints/#sec-ch-ua-form-factor),
to include information about the device's form factor.

This hint is considered "high-entropy" and thus only available to sites that
request it. In most situations, the hint value can be retrieved using
[`Accept-CH`](https://www.rfc-editor.org/rfc/rfc8942#name-the-accept-ch-response-head)
or by consulting the
[`userAgentData.getHighEntropyData()`](https://wicg.github.io/ua-client-hints/#getHighEntropyValues)
API. Where necessary, sites can receive the value on the first request
using the
[`Critical-CH`](https://datatracker.ietf.org/doc/html/draft-davidben-http-client-hint-reliability#name-the-critical-ch-response-he)
response header.

## Format

The header is an `sf-list`, which includes all applicable form-factor values.
The spec includes non-normative descriptions of the allowed values and outlines
circumstances where new values might be added.

# Security Considerations

The form-factor hint provides information that is already available to sites
via the `user-agent` header and thus exposes no new information about the
client.

# References

* https://github.com/WICG/ua-client-hints - client hints spec
* https://github.com/WICG/ua-client-hints/issues/344 - discussion of the form of
  the hint
* https://chromestatus.com/feature/5162545698045952 - chromestatus item
