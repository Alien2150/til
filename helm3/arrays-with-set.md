# Issue
I was running into an issue with arrays:

* I could not see it on the template (using helm template) 
* I was unable to set it via command line flag an array using helm --set 

Here's how I fixed both:

## Fixing "output not been seen on helm template":

Fix the order
```
helm template --set foo={bar} -f values.yaml
```

Does not work when there's a value for "foo" set on values.yaml. So fix the order:
```
helm template --set foo={bar} -f values.yaml
```

## Fixing "Unable to use --set flag" 
Does not work
```
helm template --set foo={bar} -f values.yaml
```

works: 
```
helm template --set 'foo={bar}' -f values.yaml
```
