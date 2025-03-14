# Ultimate Beneficial Owners Data Rulebook

## Table of Contents

1. [Introduction](#1-introduction)
   
    1.1. [Scope](#11-scope)  
    1.2. [Background](#12-background)  
    1.3. [Goal of the UBO attestation](#13-goal-of-the-UBO-attestation)  
    1.4. [Key words](#14-key-words)  
    1.5. [Terminology](#15-terminology)  
2. [UBO Issuance process](#2-UBO-issuance-process)  
3. [UBO Verification process](#3-UBO-verification-process)  
4. [UBO attributes](#4-UBO-attributes)  
5. [Trust infrastructure details](#5-trust-infrastructure-details)
   
    5.1. [Trust requirements on the UBO attestation from the perspective of company registration offices as authentic sources for the UBO](#51-trust-requirements-on-the-UBO-attestation-from-the-perspective-of-company-registration-offices-as-authentic-sources-for-the-UBO)  
    5.2. [Trust a signature or seal over a UBO](#52-trust-a-signature-or-seal-over-a-UBO)  
    5.3. [UBO Provider Trusted List](#53-UBO-provider-trusted-list)  
    5.4. [SD-JWT-compliant](#54-sd-jwt-compliant)  
6. [References](#6-references)  

## 1. Introduction

*Disclaimer: This document is a draft and needs to be commented on and completed to be published as EWC WP3 T3.2.3 deliverable. The definitions (part 1.5) have been generated by AI and are only a base for Business Registries to discuss with their legal departments which terminology is the most suitable in our context.*

### 1.1 Scope

This document is the Ultimate Beneficial Owners (referred to as **UBO**) Data Rulebook. It contains requirements specific to the UBO attestation and its issuance process. This UBO Rulebook covers the following topics: background of UBO, a reference to UBO attributes, a reference to the generic UBO issuance and verification process, and Trust Infrastructure details.

[Topic 10/23](https://github.com/eu-digital-identity-wallet/eudi-doc-architecture-and-reference-framework/blob/main/docs/annexes/annex-2/annex-2-high-level-requirements.md#a2310-topic-10---issuing-a-pid-or-attestation-to-the-eudi-wallet) in the ARF 1.4 specifies that attestation must be issued in the [SD-JWT VC] format, among others. This rulebook supports the [SD-JWT VC] requirements.

### 1.2 Background
Since the Directive (EU) 2024/1640 (Article 12), the access to ultimate beneficial owners is strictly regulated, but in this Directive, the UBO data elements are not listed. Thanks to the work of Business Registers participating in EWC, we were able to adapt this attributes list to the data availability in the registries and the reality of national usages and requirements.
The UBO attestation are expected be used by companies in the EWC pilots, and some modifications to this rulebook might be made.

### 1.3 Goal of the UBO attestation
Directive (EU) 2024/1640 Article 14 covers the provision of a template for the request of the UBO information and the refusal of request but doesn’t provide a template to share the data when authorized. So, the UBO attestation intend to provide a standardized data set and rulebook associated to allow EWC pilots to use in their business scenarios.
As the UBO data are sensitive personal data for which the access is strictly limited and regulated, the regulation needs to be completed and transferred to the legal wallet ecosystem.
The goal of the UBO attestation is to avoid isolated initiatives that wouldn’t respect UBO data privacy.
This is also a way for relying parties to ensure that they only verify one standard attestation, which allows machine automation and simplifies human comprehension.

### 1.4 Key words

This document uses the capitalized key words 'SHALL', 'SHOULD', and 'MAY' as specified in [RFC 2119], i.e., to indicate requirements, recommendations, and options specified in this document.

In addition, 'must' (non-capitalized) is used to indicate an external constraint, i.e., a requirement that is not mandated by this document, but, for instance, by an external document. The word 'can' indicates a capability, whereas other words, such as 'will', and 'is' or 'are' are intended as statements of fact.

### 1.5 Terminology

This document uses terminology specified in Regulation (EU) 2024/1183.

In addition to the attributes definition necessary to understand the data schema, it’s important to understand:

- **Natural person**: an individual human being who has legal rights and obligations. Unlike a legal person (which refers to an organization or entity), a natural person is a human with the capacity to engage in legal relationships, enter into contracts, own property, and be subject to legal actions.
  Natural persons are distinct from artificial entities (like corporations or governments).
  In legal terms, a natural person is someone who exists as a human being, as opposed to a corporate or fictional entity. 
- **Legal person**: an entity that has legal rights and obligations, similar to a natural person (an individual). It is an organization or group recognized by law as having the capacity to enter into contracts, sue, and be sued, and own property. Legal persons are distinct from the individuals who may own, manage, or be part of them.
  Examples of legal persons include Corporations, Government agencies, public entities (that are granted legal recognition to act on behalf of the state), Nonprofit organizations
  A legal person exists as a separate legal entity, meaning it can perform legal actions in its own name, distinct from the actions of its members. 
- **Legal entity**: an organization or structure that is recognized by law as having legal rights and responsibilities distinct from those of its members or owners. A legal entity can enter into contracts, own property, incur debts, and be held liable for legal actions in its own name.
  Legal entities include various forms of organizations such as Corporations, Limited liability companies (LLCs), Nonprofit organizations, Partnerships
  The key characteristic of a legal entity is that it has its own legal existence, allowing it to perform actions independently of the individuals who are involved with it.  
- **Legal representative**: Natural or legal person authorized to act on behalf of another person or organization in legal matters. This person has the legal authority to represent the interests of the entity, such as a company, in dealings with other parties, including signing contracts, making decisions, and appearing in legal proceedings.
  For businesses, a legal representative can be a director, officer, or another person designated by the company’s governing body (like the board of directors) to represent the company in legal matters. In the case of individuals, a legal representative might include a guardian, power of attorney holder, or someone with similar legal authority to act on behalf of the person.  
- **Signatory rights**: the authority or power granted to an individual or entity to legally bind an organization or company by signing contracts, agreements, or other formal documents. This authority can be granted to a specific person, such as an executive, director, or authorized representative, and can be either individual (where one person alone can sign) or joint (where multiple individuals are required to sign together). Signatory rights are important because they ensure that any commitments made by the organization are legally valid and enforceable.
  The terms and scope of signatory rights are usually outlined in the organization's internal governance documents, such as its bylaws, and can vary based on the level of responsibility and the nature of the agreements being signed. 
- **Beneficial owners**:  “the individuals who ultimately own or control legal entities and arrangements, including individuals designated in relation to targeted financial sanctions”. Ref Directive (EU) 2024/1640 

## 2. UBO Issuance process
In the EWC context, a generic attestation issuance process has been described by wallet providers in the pilots. Those controls and generic steps are described in [RFC-001](https://github.com/EWC-consortium/eudi-wallet-rfcs/blob/main/ewc-rfc001-issue-verifiable-credential.md).

However, the UBO attestation differs from other attestations in that it must be issued on demand for each presentation request. It is not possible to store and present this attestation several times, as every need requires a request. 
To comply with the Regulation (Art.10), only Business Registries are allowed to be the authentic source of the EUCC attestation, and they can decide to use a Pub-EAAs provider to issue it on their behalf. 

The Directive (EU) 2024/1640 defines the specific access rules to beneficial ownership registers for person with legitimate interest. 
Therefore, the attestation can only be requested by the legal representative itself. By his power, a legal representative has a valid legitimate interest in requesting the list of the beneficial owners of the company over which he or she exercises this right.

As a legal representative can be a natural or a legal person, the attestation can be requested only to natural person able to present a LoA high PID attestation or a Signatory Rights attestation to the UBO issuer to ensure the security of the personal data of the beneficial owner. 

The attestation can be issued to a valid organizational wallet (with a compliant LPID).

Nota bene : The possibility of allowing beneficial owners to request the UBO certificate themselves has been studied, but to date no secure solution has been found. The main reason for this is that beneficiaries' names are self-declared without mandatory identity verification, and may be written in a different way from the person's PID, leading to a high risk of errors when authenticating beneficiaries for access.
## 3. UBO Verification process

In the EWC context, a generic attestation verification process has been described by wallet providers in the pilots. Those controls and generic steps are described in [RFC-002](https://github.com/EWC-consortium/eudi-wallet-rfcs/blob/main/ewc-rfc002-present-verifiable-credentials.md).
The legal representative is the only one having the authorization to present this attestation. He is responsible for GDPR compliance and engage his responsibility by accepting to present the information to a Relying Party with legitimate interest. 

EWC participating Business Registries don’t impose any data or attributes specific verification at this stage of the pilot; it is up to the Relying Party needs and requirements in the business or administrative process to decide.

## 4. UBO attributes

UBO attributes have been decided together by business registries in the EWC pilot in accordance with the BORIS (Beneficial ownership registers interconnection system) data model.

This table contains the name of the attribute, its description, and whether the attribute is required or not.

| Property Name                       | Description                                                                                                                                                 | Required |
|-------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------|----------|
| legal_person      | Attributes about the legal person.                                                                                                                           | Yes      |
| legal_person_name | Official current legal person name as registered in the business register.                                                                                   | Yes      |
| legal_person_id   | Unique ID for organisations in EUID structure.                                                                                                               | Yes      |
| legal_form_type    | Legal form of the company.                                                                                                                                   | Yes      |
|registered_address | The address of the company.                                                                                                                                  | Yes      |
| ultimate_beneficial_owner | Details of the Ultimate Beneficial Owner(s) of the company.                                                                                                 | Yes      |
| natural_person_details | Details of the natural person representing the UBO.                                                                                                        | Yes      |
| family_name | Family name of the natural person representing the UBO.                                                                                                     | Yes      |
| first_name  | First name of the natural person representing the UBO.                                                                                                      | Yes      |
| identifier   | Unique identifier for the natural person representing the UBO.                                                                                             | Yes      |
| birth_date  | Date of birth of the natural person representing the UBO.                                                                                                  | Yes      |
|postal_address | Postal address of the natural person representing the UBO.                                                                                                 | Yes      |
| tax_domicile | Country of taxation of the natural person representing the UBO in the ISO 3166-1 alpha-3 standard.                                                           | No       |
| is_alive     | Indicates if the natural person representing the UBO is alive.                                                                                             | No       |
| nationality  | Citizenship of the natural person representing the UBO.                                                                                                   | No       |
| ownership_details | Details of the ownership of the UBO on the company.                                                                                                         | Yes      |
| nature_of_control | Nature of the control held by the UBO in the company.                                                                                                      | Yes      |
| ownership_type   | The type of ownership held by the UBO (e.g., direct, indirect).                                                                                             | Yes      |
| ownership_percentage | The percentage of ownership held by the UBO in the company. Must be between 0 and 100.                                                                       | Yes      |
| registrable_date | Date when the UBO’s interest was registered.                                                                                                                 | Yes      |
| inactive_date    | Date when the UBO’s interest became inactive (if applicable).                                                                                                | No       |
| last_change_date | Date when the UBO’s interest was last changed.                                                                                                               | No       |

The UBO schema is available in the EWC schemas and rulebooks repository: [UBO data schema](https://github.com/EWC-consortium/eudi-wallet-rulebooks-and-schemas/blob/main/data-schemas/ds006-ultimate-beneficial-owners-attestation.json).

**Note**: The UBO attestation metadata are aligned with the LPID. The necessary information about those can be found in the [LPID Rulebook](https://github.com/EWC-consortium/eudi-wallet-rulebooks-and-schemas/blob/main/rulebooks/rb001-legal-person-identification-data.md).

### 4.3 Minimum number of optional attributes

There is no minimum number of optional attributes for the UBO. Each Business Registry will have the responsibility to fill in the attributes when registered in their national registry.

## 5. Trust infrastructure details

In this chapter, trust requirements and general considerations regarding the UBO attestation itself are described.

### 5.1 Trust requirements on the UBO attestation from the perspective of company registration offices as authentic sources for the UBO attestation

In the ARF 1.4, the following information for Pub-EAAs and QEAAs Providers is given.

Pub-EAAs and QEAAs Providers are trusted entities responsible to:

- Verify the identity of the EUDI Wallet User in compliance with LoA high requirements.
- Issue attestations to the EUDI Wallet in a harmonized common format.
- Make available information for Relying Parties to verify the validity of the attestation.

The UBO attestation SHALL contain the qualified electronic signature or qualified electronic seal of the issuing body and adhere to the legal requirements defined in Annex VII of the Regulation (EU) 2024/1183.

The UBO attestation SHALL follow the SD-JWT format.

It SHALL not be possible to log into company registers solely with the UBO attestation, since procedures legally require an individual person to act.

UBO attestation Issuers SHALL follow the UBO attestation requirements and trust mechanisms defined by Authentic Sources on a national level.
Authentic Sources that are company registration offices need to accept each other's PUB-EAA attestations according to the regulation. Therefore, common legal trust mechanisms need to be established ifor the trust ecosystem to be trustworthy: 

- There SHALL be one common schema for the UBO which is accepted by all company registries offices.
- Only mandatory metadata and attributes SHALL be present in the UBO attestations.
- The UBO attestation SHALL be in a machine-readable format defined in the ARF during its whole lifecycle.
- The UBO attestation SHALL be in a format that can scale to additional/new legal forms.
- The UBO attestation SHALL apply for all legal persons.
- The issuer of the UBO attestation SHALL be responsible for its revocation. 

### 5.2 Trust a signature or seal over a UBO attestation

To trust a signature or seal over an UBO attestation, the Relying Party needs a mechanism to validate that the public key it uses to verify that signature or seal is trusted. OpenID4VP provides such mechanisms. However, additional details need to be analyzed to fully specify these mechanisms for UBO attestations within the EUDI Wallet ecosystem and the trust anchor for it. It is assumed that this will be part of a detailed specification from a standardization authority.

### 5.3 UBO attestation Provider Trusted List

For authenticating UBO attestations, trust anchors will be used that are present in an UBO attestation issuer Provider Trusted List.

### 5.4 SD-JWT-compliant

UBO attestation is fully compliant with [OpenID4VP] and [SD-JWT VC].

## 6. References

- RFC-001: [Issue Verifiable Credential](https://github.com/EWC-consortium/eudi-wallet-rfcs/blob/main/ewc-rfc001-issue-verifiable-credential.md)
- RFC-002: [Present Verifiable Credentials](https://github.com/EWC-consortium/eudi-wallet-rfcs/blob/main/ewc-rfc002-present-verifiable-credentials.md)
- SD-JWT VC: [SD-JWT VC Specification](https://datatracker.ietf.org/doc/draft-ietf-oauth-sd-jwt-vc/)
- OpenID4VP: [OpenID4VP Specification](https://openid.net/specs/openid-4-verifiable-presentations-1_0.html)
