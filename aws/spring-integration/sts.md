Errro message after changing to OIDC for EKS Service account:
```
To use web identity tokens, the 'sts' service module must be on the class path.
```


See https://docs.awspring.io/spring-cloud-aws/docs/3.0.0/reference/html/index.html#prerequisites. Add ```
<dependency>
    <groupId>software.amazon.awssdk</groupId>
    <artifactId>sts</artifactId>
</dependency>
```
