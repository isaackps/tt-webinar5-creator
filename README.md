# Trade trust Webinar 5 - Document creator

## Pre-requisite

- Wallet
- Document Store or Token Registry
- Configured DNS

---

## What is the config file?

It is a json file that contains informations about the user and the documents that will be created.

## What is needed to be inside the config file?

- network (mainnet, ropsten or rinkeby)
- wallet
- forms

It will look something like this:

```
{
  "network": "ropsten",
  "waller": "...",
  "forms": [{...}]
}
```

---

## Setting up of transferable document in the forms section

To set up a transferable document, the forms will look something like this:

```
{
  "name": "Bill of Lading",
  "type": "TRANSFERABLE_RECORD",
  "defaults": {...},
  "schema": {...},
  "attachments": {...}
}
```

##### Name

It will be the name of the document.

##### Type

It will be the type of the document, either `"TRANSFERABLE_RECORD"` or `"VERIFIABLE_DOCUMENT"`.

##### defaults

It contains information about the template/renderer and the issuer and some other information depending on your forms requirement.

In this case it will look something like this:

```
"defaults": {
  "$template": {
    "type": "EMBEDDED_RENDERER",
    "name": "BILL_OF_LADING",
    "url": "https://demo-cnm.openattestation.com"
  },
  "issuers": [
    {
      "identityProof": {
        "type": "DNS-TXT",
        "location": "isaactest.xyz"
      },
      "name": "Demo Issuer",
      "tokenRegistry": "0x6D489a6A2cbcB76FcEeA26102d1273cd4d3B6b10"
    }
  ],
  "name": "Demo bill of lading"
}
```

##### schema

It contains the structure of the form in JSON schema format.

A simple form structure will look something like this:

```
"schema": {
  "type": "object",
  "required": ["blNumber"],
  "properties": {
    "blNumber": {
      "type": "string",
      "title": "BL number"
    },
    "item": {
      "type": "string",
      "title": "Goods"
    }
  }
}
```

##### attachments

It contains the information about the required attachments for this document.

It will look something like:

```
"attachments": {
  "allow": true,
  "accept": ".pdf, .tt, .json, .jpg"
}
```

The `"allow"` accepts a boolean value(true or false) and it will display the attachment section based on this value.

The `"accept"` set the accepted file types. If you want to accept all file types, remove the entire `"accept"` from `"attachments"`.

---

## Setting up of verifiable document in the forms section

To set up a verifiable document, the forms will look something like this:

```
{
  "name": "Cover Letter",
  "type": "VERIFIABLE_DOCUMENT",
  "defaults": {...},
  "schema": {...},
  "attachments": {...}
}
```

##### Name

It will be the name of the document.

##### Type

It will be the type of the document, either `"TRANSFERABLE_RECORD"` or `"VERIFIABLE_DOCUMENT"`.

##### defaults

It contains information about the template/renderer and the issuer and some other information depending on your forms requirement.

In this case it will look something like this:

```
"defaults": {
  "$template": {
    "type": "EMBEDDED_RENDERER",
    "name": "COVERING_LETTER",
    "url": "https://generic-templates.openattestation.com"
  },
  "issuers": [
    {
      "name": "Demo Issuer",
      "documentStore": "0x2D96973f9553652E49F3901bEcAADb20b8CC5622",
      "identityProof": {
        "type": "DNS-TXT",
        "location": "isaactest.xyz"
      }
    }
  ],
  "name": "Covering Letter",
  "logo": "https://www.aretese.com/images/govtech-animated-logo.gif",
  "title": "Document Bundle",
  "description": "Some very important document bundle together."
}
```

The `"logo"` will be a url of the image.

##### schema

It contains the structure of the form in JSON schema format.

A simple form structure will look something like this:

```
"schema": {
  "type": "object",
  "properties": {
    "title": {
      "type": "string",
      "title": "Document Title"
    },
    "description": {
      "type": "string",
      "title": "Document Description"
    }
  }
}
```

##### attachments

It contains the information about the required attachments for this document.

It will look something like:

```
"attachments": {
  "allow": true,
  "accept": ".pdf, .tt, .json, .jpg"
}
```

The `"allow"` accepts a boolean value(true or false) and it will display the attachment section based on this value.

The `"accept"` set the accepted file types. If you want to accept all file types, remove the entire `"accept"` from `"attachments"`.

---

## Issuing the Document

1. Go to creator.tradetrust.io
2. Drag and drop or upload the newly created config file
3. Enter your wallet password
4. Select the form in which you want to issue
5. Fill up the form
6. Click "Issue Document" and wait for the document to be issued
7. Once the document has been successfully issued, you can click the download button to download the issued document

---

## Verifying the Document

1. Go to dev.tradetrust.io(ropsten) or tradetrust.io(mainnet) to verify the document
2. Drag and drop or upload the newly issued document on to the dropzone
3. It will verify the document and redirect to the viewer page
4. Once at the viewer page, you can view the contents of the document

---

## Useful Links

- creator.tradetrust.io - Document Creator website

- dev.tradetrust.io - Ropsten testnet document verifier

- tradetrust.io - Mainnet network document verifier

- rinkeby.tradetrust.io - rinkeby testnet document verifier

- https://rjsf-team.github.io/react-jsonschema-form/ - Json schema form playground
