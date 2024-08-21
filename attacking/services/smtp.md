---
icon: envelope
description: >-
  SMTP is a protocol used for sending emails across networks. It facilitates the
  transmission of email messages between servers and is a fundamental component
  of email communication.
---

# SMTP

<mark style="background-color:red;">This chapter is in-progress.</mark>

#### Check Mail Relay

```bash
# https://github.com/mludvig/smtp-cli
./smtp-cli --verbose --server 203.0.113.50 --from sender@example.com --to recipient@example.com --subject "test" --body-plain "Greetings from Acuity."
```

#### Connect via openssl to IMAPS

```bash
openssl s_client -connect 203.0.113.50:imaps
```
