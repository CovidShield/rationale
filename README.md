# ![COVID Shield logo](/assets/covid-shield-logo.svg)

COVID Shield is a free exposure notification solution built with privacy as its top priority. It was built by a group of volunteers in order to help Canadians and the rest of the world safely return to work.

COVID Shield is a private, secure, and easy-to-use tool to help governments launch their own exposure notification systems. It is based on the exposure notification technology provided by [Apple and Google](https://www.apple.com/covid19/contacttracing), the most privacy-preserving approach currently available.

* [Overview](#overview)
* [Principles](#principles)
* [Privacy](#privacy)
* [Key decisions](#key-decisions)
* [Questions](#questions)
* [Additional resources](#additional-resources)

## Overview

Our approach consists of three components: a mobile app, a server, and a web-based results portal. These three components work together to help notify users if they have been near someone in the past 14 days who has the app installed and has tested positive for COVID-19.

![Three iOS devices showing the default screen, an exposure notification, and the detail screen in COVID Shield mobile app](https://github.com/CovidShield/rationale/raw/master/assets/ios-screens.png)

#### [Mobile app](https://github.com/CovidShield/mobile)
The mobile app runs in the background and requires no user interaction after onboarding. It uses Bluetooth to collect and share random IDs with nearby phones with COVID Shield installed. If a user tests positive for COVID-19, they can choose to anonymously share their data so others can be notified of possible exposure. Sharing of random IDs is voluntary and only possible with a positive test result confirmed by a health care professional. COVID Shield periodically downloads the shared random IDs from the server and compares them on each user’s device to determine if a possible exposure has occurred.

#### [Server](https://github.com/CovidShield/backend)
The server securely collects and stores random IDs uploaded from the mobile app after a confirmed positive test result. It also generates unique temporary codes which grant permission for people with a positive COVID-19 test result to upload their random IDs. The server is flexible enough to be deployed at various levels of government.

#### [Web portal](https://github.com/CovidShield/portal) (optional)
The web-based results portal provides health care professionals unique temporary codes which can be shared with users who have tested positive for COVID-19. This code gives a user access to upload their random IDs via the mobile app if they choose. No personal information is collected and there is no association between the codes and specific tests.

Use of the portal is optional, as the server can also be used to generate temporary COVID Shield codes.

### Diagrams

#### Normal usage

![A diagram outlining the normal usage workflow for COVID Shield](/assets/summary-diagram.png)

#### Positive test result

![A diagram outlining the positive test result workflow for COVID Shield](/assets/keyupload-diagram.png)

## Principles

Alongside the  [principles laid out by the Federal, Provincial and Territorial Privacy Commissioners](https://priv.gc.ca/en/opc-news/speeches/2020/s-d_20200507/), we use these principles to guide our work:

* Focus on individual consent, trust, and clarity
* Provide as much value as possible with a focused feature set
* Be easy to use and accessible
* Avoid false positives by optimizing for test result certainty over self-reporting
* Be as unobtrusive as possible in people’s lives by requiring minimal interaction
* Request only the permissions necessary for exposure notification to work
* Give users only as much information as they need to make good decisions
* Delete all data 21 days after capture and decommission the app as soon as it is no longer useful
* Deliver openly and transparently so all interested users can explore the code

## Privacy

**COVID Shield has been designed with user privacy as the top priority.** We must strike a balance between opening the economy and preserving personal privacy, and COVID Shield takes a privacy-first approach. The COVID Shield app, its server, and the web-based results portal are all designed to make it as difficult as possible to personally identify users or link them to their test results. To learn more about how we’ve approached privacy, read [our privacy policy](/privacy-policy.md).

## Key decisions

#### Use Apple and Google's Exposure Notification technology
The need for digital contact tracing is both urgent and important. While there are many possible approaches, we chose Apple and Google’s [Privacy-Preserving Contact Tracing](https://www.apple.com/covid19/contacttracing) for COVID Shield because it allows us to provide exposure notifications without sharing any personally identifiable information.

#### Trust in test delivery
By becoming part of the test results delivery process, and not the test distribution or administration processes, COVID Shield can be used to connect more directly with patients with positive test results without massive integration efforts between test manufacturers, health agencies, and other organizations. The goal is maximum certainty with minimal required integration with existing health systems and software.

#### Federal database and federal, provincial, or territorial apps/portals
A centralized, shared database allows diagnosis keys to be distributed to all provinces and territories across Canada. Meanwhile, per-province/territory deployment and management of the mobile apps and web-based results portals allows each region to operate in accordance with its own guidelines while still taking advantage of the national, shared database.

The ability to share diagnosis keys is especially important for Canadians living and working close to provincial and territorial borders as in the Ottawa/Gatineau region, or for those who travel between provinces.

A similar model of deployment at various levels of government could be effective in any country. By making the project open source, we are welcoming widespread adoption and adaptation.

#### Minimal exposure information
We believe it is important for the app to only provide enough information to make good decisions. Apple and Google provide  [more information about exposures](https://developer.apple.com/documentation/exposurenotification/enexposureinfo) such as number of exposures, duration of exposure, date of exposure, signal strength, and more. COVID Shield only shows users that they have possibly been exposed within the past 14 days and does not provide the rest of this information.

More information introduces more privacy risk. We have concerns that additional information, such as date and duration of exposure, increases the likelihood that users who were possibly exposed to COVID-19 could determine the specific person they were near and therefore how they were possibly exposed. Also, if users believe their exposure was insufficient to warrant isolation or quarantine, they may engage in riskier behaviour. Our goal is to provide app users what they need to make good decisions about the risk to themselves or others, in conjunction with health care professionals.

#### Minimally intrusive
We chose to make COVID Shield minimally intrusive in users’ lives by running effectively in the background and by only notifying users if they have been possibly exposed to COVID-19. In an typical scenario, users run this app in the background and don't have to think about it again. If they have possibly been exposed, the app provides clear links to governmental health guidance to help them make the most informed decisions.

#### Random IDs are stored securely on devices
Phones with the app installed use Bluetooth to collect and share random IDs with nearby phones. These IDs are stored securely on each phone. A user with a positive test result must receive a COVID Shield code from a health care professional to be granted access to share their random IDs, and the user must then grant permission to share their random IDs. Sharing is voluntary.

#### COVID Shield does not use location data such as GPS or WiFi signals
We do not request any device permissions outside of those necessary for Apple and Google’s Exposure Notification technology. This ensures that we are not accidentally collecting any data that we do not need for the explicit purpose of exposure notification.

#### Only people with confirmed positive test results can share their data
It will only be possible for a user to share random IDs if a positive COVID-19 test result has been confirmed by a health care professional. The health care professional will grant access via a numeric code. It will not be possible for bad actors to falsely report a positive test result.

#### Use of COVID Shield is voluntary
The user must choose to download and turn on the app, and they can choose to turn off or uninstall the app at any time. The random IDs sent by the app change every 10-20 minutes to prevent tracking. COVID Shield does not tie COVID-19 test results directly to app users, so their random IDs cannot be used to determine their identity. After receiving a positive test result, a user can choose to share random IDs. Sharing is voluntary and not required to continue receiving exposure notifications.

#### COVID Shield is easy to use and accessible
This includes [writing in plain language](https://design.gccollab.ca/content/content-guidelines), ensuring the web-based results portal meets [WCAG guidelines](https://www.w3.org/TR/WCAG21/), and focusing on clear information hierarchy and straightforward design.

#### COVID Shield is not a health app
We direct users to already-published resources from government health authorities. COVID Shield does not provide medical advice. It is complementary to any existing public health efforts, including traditional contact tracing performed by trained health care professionals.

## Questions

#### How can I use COVID Shield?
COVID Shield is provided as a reference for your local public health authority to build their own app. If you are interested in using COVID Shield, please contact your local government representative and ask what they are doing about exposure notification for COVID-19.

#### Who built COVID Shield?
We are a group of Shopify volunteers who want to help to slow the spread of COVID-19 by offering our skills and experience developing scalable, easy to use applications. We are releasing COVID Shield free of charge with a flexible open-source license.

For questions, we can be reached at press@covidshield.app.

#### How can I contribute?
See [our guidelines](/CONTRIBUTING.md) for more information on contributing to the project.

## Additional resources

- [Apple documentation on privacy-preserving contact tracing and exposure notifications](https://www.apple.com/covid19/contacttracing)
- [Apple and Google Exposure Notification FAQ](https://blog.google/documents/73/Exposure_Notification_-_FAQ_v1.1.pdf)
- [Office of the Privacy Commissioner of Canada joint statement on Privacy principles for contact tracing and similar apps](https://priv.gc.ca/en/opc-news/speeches/2020/s-d_20200507/)
- [How privacy-first contact tracing works](https://ncase.me/contact-tracing/)
- [Why is Exposure Notification important?](https://ncase.me/covid-19/)
