# Table of Contents

- [DNS](#dns)
  - [dns.getServers()](#dnsgetservers)
  - [dns.lookup(hostname[, options], callback)](#dnslookuphostname-options-callback)
    - [Supported getaddrinfo flags](#supported-getaddrinfo-flags)
  - [dns.lookupService(address, port, callback)](#dnslookupserviceaddress-port-callback)
  - [dns.resolve(hostname[, rrtype], callback)](#dnsresolvehostname-rrtype-callback)
  - [dns.resolve4(hostname, callback)](#dnsresolve4hostname-callback)
  - [dns.resolve6(hostname, callback)](#dnsresolve6hostname-callback)
  - [dns.resolveCname(hostname, callback)](#dnsresolvecnamehostname-callback)
  - [dns.resolveMx(hostname, callback)](#dnsresolvemxhostname-callback)
  - [dns.resolveNs(hostname, callback)](#dnsresolvenshostname-callback)
  - [dns.resolveSoa(hostname, callback)](#dnsresolvesoahostname-callback)
  - [dns.resolveSrv(hostname, callback)](#dnsresolvesrvhostname-callback)
  - [dns.resolvePtr(hostname, callback)](#dnsresolveptrhostname-callback)
  - [dns.resolveTxt(hostname, callback)](#dnsresolvetxthostname-callback)
  - [dns.reverse(ip, callback)](#dnsreverseip-callback)
  - [dns.setServers(servers)](#dnssetserversservers)
  - [Error codes](#error-codes)
  - [Implementation considerations](#implementation-considerations)
    - [dns.lookup()](#dnslookup)
    - [dns.resolve(), dns.resolve*() and dns.reverse()](#dnsresolve-dnsresolve-and-dnsreverse)



# DNS
```javascript
var dns = require("dns")
```
# dns.getServers()
- 以字串的方式回傳當前DNS的IP。

==

# dns.lookup(hostname[, options], callback)
- 將網域名稱解析為A(IPv4)或AAAA(IPv6)   
- options包含3個參數(family, hints, all)
  - family-只能為整數4或6,沒提供的話IPv4,IPv6都是有效的。
  - hints-如果提供,必須是一個或多個支持的`getaddrinfo`標示。
  - all-Boolean,如果true,將以陣列的方式回傳所有解析的IP,false的話只會回傳一個IP,預設為false。


==

### Supported getaddrinfo flags

==

# dns.lookupService(address, port, callback)
- 將傳入的IP和PORT號轉成網域名稱跟服務。
```javascript
var dns = require('dns')
dns.lookupService("8.8.8.8", 22, function(err, hostname, service) {
	console.log('主機：%s，服務：%s',hostname,service);
})
#結果：主機：google-public-dns-a.google.com，服務：ssh
```

==

# dns.resolve(hostname[, rrtype], callback)
- 網域名稱轉IP  
- rrtype:  
 - A:IPv4,預設.   
 - AAAA:IPv6.  
 - MX:郵件交換紀錄.  
 - TXT:text紀錄.  
 - SRV:SRV紀錄.  
 - PTR:用來IP找網域名稱.  
 - NS:域名服務器紀錄.  
 - CNAME:別名紀錄.  
 - SOA: 查詢權威紀錄.  
    - nsname    
    - hostmaster  
    - serial  
    - refresh  
    - retry   
    - expire  
    - minttl   
```javascript
var dns = require('dns')
dns.resolve('www.google.com.tw', rrtype = 'A', function(err, addresses) {
	console.log('IP：%s',JSON.stringify(addresses));
})
#結果：IP：["203.211.0.44","203.211.0.50","203.211.0.30","203.211.0.40","203.211.0.49","203.211.0.59","203.211.0.24","203.211.0.34","203.211.0.39","203.211.0.20","203.211.0.35","203.211.0.45","203.211.0.54","203.211.0.29","203.211.0.25","203.211.0.55"]

```

==

# dns.resolve4(hostname, callback)
# dns.resolve6(hostname, callback)
# dns.resolveCname(hostname, callback)
# dns.resolveMx(hostname, callback)
# dns.resolveNs(hostname, callback)
# dns.resolveSoa(hostname, callback)
# dns.resolveSrv(hostname, callback)
# dns.resolvePtr(hostname, callback)
# dns.resolveTxt(hostname, callback)
# dns.reverse(ip, callback)
# dns.setServers(servers)
# Error codes
# Implementation considerations
### dns.lookup()
### dns.resolve(), dns.resolve*() and dns.reverse()
