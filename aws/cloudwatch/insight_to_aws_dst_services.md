Find the top 10 traffic receiving AWS Services:

1. Enable field "pkt-dst-aws-service" and eventually "pkt-src-aws-service"
2. Use cloudwatch insight with this query (Where VPC CIDR can vary):

```
filter !isIpv4InSubnet(dstAddr, "10.0.0.0/16") and isIpv4InSubnet(srcAddr, "10.0.0.0/16")
| stats sum(bytes) / (1024*1024*1024) as bytesTransferred by pktDstAwsService
| sort bytesTransferred desc
| limit 20
```
