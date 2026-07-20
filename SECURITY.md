# Security Policy of using Amazon Corretto with Pterodactyl Panel

## Supported versions/eligible for update

All Amazon Corretto Java version is long-term maintained from [Amazon Web Service](https://aws.amazon.com). For more information, visit https://aws.amazon.com/vi/corretto/faqs/ to know more.

> [!NOTE]
> Deprecated/Unsupported Java version is removed from the eggs list. For more information about life expentacy of specific Java version, visit https://endoflife.date/amazon-corretto.

| Version            | Supported                               |
| ------------------ | --------------------------------------- |
| Java 8 LTS         | LTS until 31 Dec 2030                   |
| Java 11 LTS        | LTS until 31 Jan 2032                   |
| Java 15            | Ended at 20 Apr 2021                    |
| Java 16            | Ended at 19 Oct 2021                    |
| Java 17 LTS        | LTS until 31 Oct 2029                   |
| Java 18, 19 and 20 | Ended at Apr - Oct 2023                 |
| Java 21 LTS        | LTS until 31 Oct 2030                   |
| Java 22, 23, 24    | Ended at Oct 2024-2025                  |
| Java 25 LTS        | LTS until 31 Oct 2032                   |
| Java 26            | Currently not receiving LTS updates yet |

## Reporting a Vulnerability

### If there is an issue from the egg

Create an issue/PR and describe what happend or pinpoint out the fix, I'll work with it in less than 24 hours after receive the notification and will release the fix as soon as possible.

### If there is an issue from specific Java version

Contact Amazon Web Service Security support by send a mail to [aws-security@amazon.com](mailto:aws-security@amazon.com) or visit https://www.amazon.com/gp/help/customer/contact-us to reach out to AWS support center.
