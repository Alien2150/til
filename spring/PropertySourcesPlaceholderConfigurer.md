I was chasing a bug where @ConfigurationProperties and @Value did not work in test (String like "${....}" were displayed instead of having the value.
It turned out that we had our our own "PropertySourcesPlaceholderConfigurer" Bean defined which could not be loaded as it caused some circualr dependecy with Flywa (We tried loading props from the db which could not be loaded as migration was not executed yet). So the way I fixed it:

1. Create the default PropertySourcesPlaceholderConfigurer so that config settings can get loaded:

```
@Configuration
    static class PropertyTestConfig {
        @Bean
        static PropertySourcesPlaceholderConfigurer propertySourcesPlaceholderConfigurer() {
            return new PropertySourcesPlaceholderConfigurer()
        }
    }
```

2. Enable "EnableConfigurationProperties" (if using non SpringBootTest) for datasource for example:

```
@EnableConfigurationProperties([DataSourceProperties.class])
```

3. Assign the ContextConfiguration (if using non spring-boot-test)

```
@ContextConfiguration(classes = [PropertyTestConfig.class, ...])
```
