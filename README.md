# PKCS#7 signedData

PKCS#7 signedData library for php.

# Data format

### SignedData

    SignedData ::= SEQUENCE {
        version Version,
        digestAlgorithms DigestAlgorithmIdentifiers,
        contentInfo ContentInfo,
        certificates [0] IMPLICIT ExtendedCertificatesAndCertificates OPTIONAL,
        crls [1] IMPLICIT CertificateRevocationLists OPTIONAL,
        signerInfos SignerInfos
    }

### version

    Integer

### digestAlgorithms

    Set of DigestAlgorithmIdentifier

    DigestAlgorithmIdentifier ::= AlgorithmIdentifier

    AlgorithmIdentifier  ::=  SEQUENCE  {
        algorithm               OBJECT IDENTIFIER,
        parameters              ANY DEFINED BY algorithm OPTIONAL
    }

### contentInfo

    ContentInfo ::= SEQUENCE {
        contentType ContentType,
        content [0] EXPLICIT ANY DEFINED BY contentType OPTIONAL
    }

    ContentType ::= OBJECT IDENTIFIER

### certificates

    Set of ExtendedCertificateOrCertificate

    ExtendedCertificateOrCertificate ::= CHOICE {
        certificate Certificate, -- X.509
        extendedCertificate [0] IMPLICIT ExtendedCertificate
    }

    ExtendedCertificate ::= SEQUENCE {
        extendedCertificateInfo ExtendedCertificateInfo,
        signatureAlgorithm SignatureAlgorithmIdentifier,
        signature Signature 
    }

    ExtendedCertificateInfo ::= SEQUENCE {
        version CMSVersion,
        certificate Certificate,
        attributes UnauthAttributes 
    }

    UnauthAttributes ::= SET SIZE (1..MAX) OF Attribute

    Attribute ::= SEQUENCE {
        attrType OBJECT IDENTIFIER,
        attrValues SET OF AttributeValue
    }

    AttributeValue ::= ANY

    SignatureAlgorithmIdentifier ::= AlgorithmIdentifier

    Signature ::= BIT STRING

### crls

    Set of CertificateRevocationList

    CertificateRevocationList ::= CertificateList

    CertificateList ::= SEQUENCE {
        crlToSign           CRLToSign,
        algorithmIdentifier AlgorithmIdentifier,
        signatureValue      BIT STRING
    }

    CRLToSign ::= SEQUENCE {
        version           Version OPTIONAL, -- if present, version must be v2
        signature         AlgorithmIdentifier,
        issuer            Name,
        thisUpdate        Time,
        nextUpdate        Time OPTIONAL,
        revokedCertificates   SEQUENCE OF SEQUENCE {
              userCertificate      CertificateSerialNumber,
              revocationDate       Time,
              crlEntryExtensions   Extensions OPTIONAL } OPTIONAL,
        crlExtensions   [0]  Extensions OPTIONAL
    }

### signerInfos

    Set of SignerInfo

    SignerInfo ::= SEQUENCE {
        version Version,
        issuerAndSerialNumber IssuerAndSerialNumber,
        digestAlgorithm DigestAlgorithmIdentifier,
        authenticatedAttributes [0] IMPLICIT Attributes OPTIONAL,
        digestEncryptionAlgorithm DigestEncryptionAlgorithmIdentifier,
        encryptedDigest EncryptedDigest,
        unauthenticatedAttributes [1] IMPLICIT Attributes OPTIONAL
    }

   EncryptedDigest ::= OCTET STRING

# Install

    to be continued

# Usage

    to be continued

# Development

    to be continued

# Reference

[RFC2315](https://www.ietf.org/rfc/rfc2315.txt)

[RFC3852](https://www.ietf.org/rfc/rfc3852.txt)

[RFC5652](https://tools.ietf.org/html/rfc5652#section-5.3)

[RFC5280](https://tools.ietf.org/html/rfc5280#section-4.1.1.2)

[PKIGlobe](http://www.pkiglobe.org/pkcs7.html)

[BounceCastle CMS](https://www.bouncycastle.org/docs/pkixdocs1.4/org/bouncycastle/cms/CMSSignedData.html)

[Go pkcs7](https://godoc.org/github.com/fullsailor/pkcs7)

[PKCS7 OID](http://www.alvestrand.no/objectid/1.2.840.113549.1.7.html)

[Apple](https://opensource.apple.com/source/Security/Security-55471/libsecurity_asn1/asn1/sm_x509af.asn)

# Licence

MIT
