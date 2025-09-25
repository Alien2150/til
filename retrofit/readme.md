# Impact
All parameters using @Path annotation. The default value for encoded is set to false. Retrofit encoding by default does not encode "+" which might be problematic. 

#fix
Set encoded to true:
```
val foo = "test+foo@bar.com"
getComplaint(...., urlEncoded(address))

@GET("/v3/{domainID}/complaints/{address}")
Call<ComplaintResponse> getComplaint(
        @Header("Authorization") String basicAuth,
        @Path("domainID") String domainID,
        @Path(value = "address", encoded = true) String address
);

```
