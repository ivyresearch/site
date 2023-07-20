---
title: "DMARC vs DKIM"
date: 2023-06-23T15:58:00-06:00
draft: false
---

DMARC (Domain-based Message Authentication, Reporting & Conformance), DKIM (DomainKeys Identified Mail), and SPF (Sender Policy Framework) are three protocols that enhance the security of email communications and reduce the chance of spoofing and phishing attacks. Here's how DMARC relates to DKIM:

DKIM: DomainKeys Identified Mail allows an organization to take responsibility for transmitting a message in a way that can be verified by mailbox providers. This is achieved by adding a digital signature to the headers of an email message. This signature can be validated back to the domain that signed it, demonstrating to the recipient that the email hasn’t been altered in transit.

DMARC: Domain-based Message Authentication, Reporting & Conformance builds on the two aforementioned technologies, SPF and DKIM. It allows the owner of a domain to publish a policy in their DNS records to specify which mechanism (DKIM, SPF or both) the receiver should use to authenticate incoming email messages. If neither of those authentication methods passes, then the domain owner can tell the receiver what to do with the email (either allow it, quarantine it, or reject it).

In essence, DMARC uses the validation results of both SPF and DKIM, along with the alignment of the sending domain, to make a decision on an email's legitimacy. It therefore brings additional security and reliability to the email system by reducing the chance of a domain being fraudulently used in phishing or spoofing attacks.

## Goodbye world is a `templ` template example

Every time `Click Me!` is clicked, a request is sent to the API server, which renders `templ GoodbyeWorld()` from `partial/templates.templ`.

{{< html.inline >}}
<button
  hx-get="{{ .Site.Params.apiBaseUrl }}/goodbyeworld.html"
  hx-trigger="click"
  hx-target="#goodbye"
  hx-swap="beforeend">
  Click Me!
</button>
<div id="goodbye"></div>
{{< /html.inline >}}

