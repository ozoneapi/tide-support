# Usage guides

This document is for TPPs who want to migrate their existing clients(registered with legacy certificates) to use the new eidas certificates


## Scenarios

1) TPP have existing clients setup using legacy OB certificates.
2) TPP have consents and tokens created using legacy OB certificates

## Migration Steps

1) Register new certs for existing clients

1.1) Invoke the token endpoint to obtain a client credentials grant token. TPP's should use their existing valid legacy certificates to call the token endpoint 

1.2) Make a Dynamic Client Registration 'PUT' call with the new certificate DN to associate their existing clients with new eIDAS certs
The 'tls_client_auth_subject_dn' claim in the DCR put call should be set to the new certificate subject

e.g. in the DCR put call, set the tls_client_auth_subject_dn claim as below
tls_client_auth_subject_dn="CN=0015800001041RHAAY,2.5.4.97=#132250534447422D4F422D556E6B6E6F776E303031353830303030313034315248414159,O=Ozone Financial Technology Limited,C=GB",

Once the above call is successful , existing clients will get associated with the new certificates.
Any resource server call with the old certificates will fail.
Additionally any tokens associated with old certificates will not work.

2) Generate new access token bound to new certificate
Invoke the token endpoint with refresh token grant to obtain new access token. TPP's should pass their existing refresh token and new certificates in order to get a new access token.
The new access token can then be used to access accounts/balances endpoints without the need to reauthenticate the PSU