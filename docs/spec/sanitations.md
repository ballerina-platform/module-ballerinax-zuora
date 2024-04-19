# Sanitation: Ballerina Zuoro connector

_Author_: @ayeshLK \
_Created_: 2024/04/18 \
_Updated_: 2024/04/19 \
_Edition_: Swan Lake

## Sanitation for OpenAPI specification

This document records the sanitation done on top of the official OpenAPI specification from Zuora REST API. The OpenAPI specification is obtained from the [Zuora REST API official documentation](https://developer.zuora.com/api-references/api/overview/). These changes are done to improve the overall usability and as workarounds for some known language limitations.

1. Remove the invalid default value set for the `writeOffOptions` field of the `PostRefundwithAutoUnapplyType` schema.
2. Remove `passthrough[1,2,3,4,5]` and `param_gwOptions_[*option*]` fields from the `POSTRSASignatureType` schema.
    * As the Ballerina OpenAPI tool generates open records for the schemas, users can still use these fields but have to manually define them and set values.
3. Remove the `type` field from the following schemas as they already inherit the `type` field from the `PaymentMethodCommonFields` schema.
    * `POSTPaymentMethodRequest`
    * `CreatePaymentMethodCreditCard`
    * `CreatePaymentMethodCCReferenceTransaction`
    * `CreatePaymentMethodACH`
    * `CreatePaymentMethodSEPA`
    * `CreatePaymentMethodSEPA`
    * `CreatePaymentMethodAutogiro`
    * `CreatePaymentMethodBacs`
    * `CreatePaymentMethodBecs`
    * `CreatePaymentMethodBecsnz`
    * `CreatePaymentMethodPAD`
    * `CreatePMPayPalNativeEC`
    * `CreatePMPayPalCP`
    * `CreatePMPayPalEC`
    * `CreatePaymentMethodPayPalAdaptive`
    * `CreatePaymentMethodApplePayAdyen`
    * `CreatePaymentMethodGooglePayChase`
    * `CreatePaymentMethodBetalingsservice`
4. Introduce security schemas for OAuth2.0 and remove usage of the `GLOBAL_HEADER_Authorization_OAuth_optional` parameter from the API specification.

## OpenAPI CLI command

The following command was used to generate the Ballerina client from the OpenAPI specification. The command should be executed from the repository root directory.

```bash
JAVA_OPTS="$JAVA_OPTS -DmaxYamlCodePoints=99999999" bal openapi -i docs/spec/openapi.yml --mode client --license docs/license.txt -o ballerina
```

Note: The license year is hardcoded to 2024, change if necessary.
