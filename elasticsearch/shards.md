Fluentd was not able to push logs into Elasticsearch:
1. Enable log 400's: https://github.com/uken/fluent-plugin-elasticsearch#log_es_400_reason
2. Check for error messages like:
`Validation Failed: 1: this action would add [10] total shards, but this cluster currently has [994]/[1000] maximum shards open;`
These are some way's to fix it:
* (Scale out elasticsearch &&) change max shards settings
* Cleanup data (Drop indeces or shrink them)
