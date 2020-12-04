JsonProperty vs JsonValue

JsonValue builds an aggregated output of the object while JsonProperty does the same for the attribute / method

Example:
```
@Data
@RequiredArgsConstructor
class A {
   @JsonValue
   private String foo;
   
   private Boolean bar;
}

var a = new A("123", false);
```

will become ```"123"``` not ```{"foo":"123", "bar": false}```


While 


```
@Data
@RequiredArgsConstructor
class A {
   @JsonProperty
   private String foo;
   
   @JsonProperty
   private Boolean bar;
}

var a = new A("123", false);
```

will become ```{"foo":"123", "bar": false}```
