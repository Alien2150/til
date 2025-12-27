# Issue #
Seeing stack-traces as multiple log-entries when using Fluentbit for EKS (https://github.com/aws/eks-charts)

# Solved 
1. Upgrade Image to 2.21.2 (using helm)
2. Change on config-map: Remove Parser, Docker_Mode. Add "multiline.parser  docker, cri" (See https://docs.fluentbit.io/manual/pipeline/inputs/tail#multiline-core-v1.8)
3. Add extra Filter:
```
[FILTER]
   Name                  multiline
   match                 *
   multiline.key_content log
   multiline.parser      java, python, go, docker, cri
```

