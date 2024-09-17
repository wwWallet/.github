# Meet wwWallet.org 🌐

**wwWallet.org** (hereinafter referred to as "wwWallet") brings an innovative approach to identity wallets that challenges the dominance of native mobile apps. Aiming for user-friendliness and digital inclusion, it leverages modern web technologies and redefines how identity wallets can be made available to citizens by positioning web browsers as an alternative or complementary platform for identity wallets.

Key technologies underpinning wwWallet’s design include **Progressive Web Applications (PWA)**, the **Web Cryptography API (WebCryptoAPI)** and **FIDO** standards, specifically **Web Authentication (WebAuthn)** and the **Client to Authenticator Protocol (CTAP2)**. The PWA design ensures a native application-like experience and seamless operation across various types of devices, all using a single JavaScript/TypeScript, HTML and CSS codebase. WebAuthn and CTAP2 enable passkey-based authentication for wallet holders and empower them to choose their WSCD from built-in options (TPM, SE, TEE) or external security keys. Combined with ongoing efforts to incorporate advanced cryptographic systems, such as Hierarchical Deterministic Keys (HDK) for efficient key management, these are the technologies that differentiate wwWallet.

This shift from a mobile-based to a web-based strategy, enables a unified view of the wallet across desktop computers, mobile devices, and tablets. It frees users from the limitation of single-device dependency, while ensuring that the holder retains sole control of their wallet and private keys via the chosen WebAuthn authenticator, which could be either local or roaming.

## Holder Authentication 🔒

For signing in to the wallet, wwWallet uses the WebAuthn for strong, phishing-resistant authentication. This enables a high LoA for this authentication stage thanks to WebAuthn’s authenticator attestation feature. During WebAuthn credential registration, the wwWallet deployment can enforce a policy on what kinds of authenticators are acceptable. The newly created credential may then include a cryptographic proof that the WebAuthn credential private key is held by an authenticator of an approved model. This enables the wallet provider to ensure that users’ authenticators satisfy the requirements of LoA high.

## Web & Edge Wallet 🌍

For single-instance edge wallets, such as those provided by native mobile apps, the non-custodial property is considered a given. This refers not only to the holder's sole control over their private keys within the embedded WSCD but also to the fact that the wallet provider is not involved in issuer-holder-verifier transactions. However, this is not always apparent with web-based wallets, as it is often assumed that core wallet operations are handled at the backend, managed by the wallet provider. In contrast, wwWallet takes a different approach: all wallet-related functions are implemented on the client side, providing users with full control and transparency. As a result, wwWallet combines the versatility and convenience of web wallets with the enhanced privacy and security features traditionally found in edge wallets.

### Client-Side Cryptographic Functions 🔑

Cryptographic functions required for device binding and end-to-end encryption of users’ wallet contents, including all proof signing keys, are performed also on the client side. This is achieved using keys derived via the WebAuthn PRF extension. The encryption keys are not sent to the server, so users’ proof signing keys are secure against a breach of the server side. Once the user is authenticated using WebAuthn, the user can download their encrypted wallet contents and decrypt them on the client side. 

The currently used WebAuthn PRF extension only enables derivation of software keys, so wwWallet does not currently achieve LoA high for (Q)EAA proof signing keys. To achieve LoA high, wwWallet's roadmap includes plans to implement newer proposed WebAuthn and CTAP2 extensions (https://github.com/w3c/webauthn/pull/2078). These extensions would enable wwWallet to generate hardware-bound asymmetric key pairs, whose public keys can be tied as proof keys during credential issuance while the private keys never leave the secure element of the WebAuthn authenticator. During credential presentation, wwWallet would invoke WebAuthn with the extension to have the WebAuthn authenticator sign the presentation with the hardware-bound private key. This would ensure the user has sole control of their (QEAA) proof keys, even if encryption keys are compromised.

### Client-Side Protocol Implementation 📜

The issuance (**OID4VCI**) and presentation (**OID4VP**) protocols in wwWallet are also implemented on the client side, further enhancing user privacy and supporting a fully non-custodial approach. This is an important step toward realizing the full potential of edge wallets, while also demonstrating that web browsers are strong platform candidates for the identity wallets’ ecosystem.

### Offline Capability ✈️

Despite its web-based nature, wwWallet is capable of operating in offline or airplane mode, a key and distinctive feature of PWAs. Even when the device is offline, the holder can authenticate to the wallet using a passkey stored in either a local or roaming WebAuthn authenticator. Furthermore, wwWallet leverages background service workers and the W3C’s Indexed Database API for client-side encrypted storage, securely housing the wallet’s contents. This enables offline access to verifiable credentials and to the history of all presentations. Upon detecting network recovery, the wallet prompts the user to reauthenticate, after which a background sync updates and makes the latest content accessible. The offline feature is not only crucial for user-friendliness and practical purposes but also represents an important step toward enabling offline presentations via NFC.

### Installable ⬇️

One of the key features of wwWallet as a Progressive Web App (PWA) is its ability to be promoted for installation directly from the browser's settings menu. Once installed, wwWallet functions like a native application, allowing users to launch it from an icon on their home screen, manage notifications or uninstall whether on a mobile device or desktop. This behavior is controlled by the wwWallet Manifest file, which adheres to the [W3C's Web Application Manifest](https://www.w3.org/TR/appmanifest/) specification. This approach simplifies the distribution path, enabling a wwWallet-based solution to bypass traditional platform app store procedures.

In addition to direct installation through the browser’s settings menu, PWAs can also be distributed via platform app stores using tools like [PWABuilder](https://www.pwabuilder.com/). This offers wwWallet providers a versatile approach, combining the ease of browser-based installation with the broader reach of app store distribution.

## Privacy 🛡️

Holder privacy is the ultimate goal of identity wallets and the core principle behind the issuer-holder-verifier paradigm. Without this focus on privacy, most—if not all—scenarios could have been implemented using existing protocols and products. Privacy in the context of the identity wallets encompasses a broad range of design considerations, and it remains a work in progress, particularly when viewed through the lens of post-quantum cryptography. Discussions about privacy typically revolve around the cryptographic protocols and primitives that need to be considered, which of them are available on certified WSCDs, and how they can be leveraged to achieve various forms of unlinkability in conjunction with selective disclosure requirements.

In its current phase, wwWallet enhances privacy by generating unique, unrelated key pairs for each credential. This ensures that cryptographic keys do not compromise unlinkability, preventing tracking by relying parties, provided the holder does not use the same credential instance for every presentation. It also supports selective disclosure mechanisms, allowing users to share only the necessary information while keeping other details private.

While the current implementation is effective, it is admittedly not optimal. Our goal is to remain at the forefront of privacy-enhancing technologies by incorporating cutting-edge advancements as they become available. Batch issuance using **HDK/ARKG** is the immediate next realistic goal, however other **ZKP** implementations are also on the wwWallet team’s radar.


## Protocols, Profiles, Formats 🪪  

wwWallet has been participating in various initiatives and projects, often with diverging goals and incompatible verifiable credential profiles. The variations include different credential formats, key management methods for holders and issuers, differing trust frameworks—or none at all—and, of course, a wide variety of issuance and presentation protocol profiles, as well as wallet attestation methods. However, all implementations were built on the common foundation of the OID4VC family of protocols.

## Interoperability & Compliance 🤝

The convergence of various design approaches for identity wallets is still underway, leaving significant room for standardization—an essential component for ensuring interoperability. In Europe, considerable efforts have been directed towards this goal, as evidenced by the EUDI Wallet Architectural Reference Framework and the work of other European standardization bodies. wwWallet closely monitors these developments to ensure compatibility with other implementations. Our aim is to comply with the forthcoming EU CSA Certification Scheme, meeting both functional and security requirements while also operating efficiently in cross-border and even cross-continental scenarios.

## wwWallet in Action 🎬

Explore how **wwWallet** performs in interoperability scenarios across various LSPs and demos. These videos showcase the wallet’s capabilities in handling diverse use cases and its adaptability across various issuers, verifiers and credential formats.

 - [EBSI Ecosystem Day (Formal Accreditation and Recognition Cluster)](https://www.youtube.com/watch?v=yIdVfc-srY8): Diploma issuance and verification with University of Athens and University of Lausanne
 - [DC4EU (Social Security Case)](https://www.youtube.com/watch?v=gnDeTEmWdok): PID, EHIC and PDA1 issuance and verification
 - [SPRIND Funke (Stage 1)](https://www.youtube.com/watch?v=VTjZ0lZBWH4): German PID issuance and verification

## Getting Started 🚀
*TBD*

## Roadmap 🛤️

**Tasks**
- Publish wwWallet to Google Play Store
- Publish wwWallet to iOS App Store
- Publish wwWallet to Microsoft Store
- Safari / iOS 18 FCM fallback using APN
- ‘Remember me’ function (https://github.com/gunet/funke-wallet-frontend/issues/23)
- Searchable presentations history log
- OWASP HTTP security headers for enhanced web security
- Multi-Language Support
- Support [Bitstring Status List v1.0](https://www.w3.org/TR/vc-bitstring-status-list/)


**SuperTasks**
- Offline proximity presentation of mDoc over NFC and / or BLE (ISO/IEC 18013-5 or ISO/IEC 23220-4)
- OID4VCI batch issuance support using [HDK](https://datatracker.ietf.org/doc/draft-dijkhuis-cfrg-hdkeys/) approach for key management, to prevent correlation by verifiers. Enhanced UX to handle multi-instance credentials
- Cloud WSCD using passkeys and the WebAuthn PRF extension to encrypt the users cryptographic material in the cloud so that it can only be decrypted based on the users activation of the WSCD

**Projects**
- PID issuance and presentation using [EUDI Wallet Interoperability Framework](https://github.com/WalletInteroperabilityLab/eudi-wif)
- PID issuance and presentation using [Architecture Proposal for the German eIDAS Implementation](https://bmi.usercontent.opencode.de/eudi-wallet/eidas-2.0-architekturkonzept/)

**Ideas**
- Test Automation: Enhance wwWallet CI/CD pipeline with QA workflows
- Offline proximity presentations using [OpenID for Verifiable Presentations over BLE](https://openid.net/specs/openid-4-verifiable-presentations-over-ble-1_0.html)
- Instead of batch issuance, explore ZKP alternatives based BBS+ or BBS# signature schemes
- Demonstrating OpenBadges EAAs
- Demonstrating ELM EAAs
- Support [SD-JWT VC DM Credential Format](https://github.com/danielfett/sd-jwt-vc-dm?tab=readme-ov-file#sd-jwt-vc-dm-credential-format)

  
## Pronunciation 🎤

At wwWallet, we embrace the playful ambiguity in how our name is pronounced. Whether you say:
- ɣuˈɣu wallet
- ɣwaˈɣwa wallet
- ˈdabliju ˈdabliju wallet

you can pronounce it however suits you – we'll respond either way! It adds to the fun and uniqueness of what we're building, and we’re perfectly happy keeping it that way!

## The wwWallet Team 👥

wwWallet is a collaborative effort led by **GUnet**, **Sunet**, and **Yubico**. As an open-source project, it welcomes contributions from forward-thinking individuals and organizations interested in enhancing existing functionalities, developing new features, or exploring bold, innovative ideas driven by their unique use cases.
