##Cymon  

>Largest tracker of security reports with over 15,000 unique IPs saved daily

* Malware  
* Phishing  
* botnets  
* Others    

>Almost 200 sources ingested daily

* eSentire AMP  
* DNSBL
* Blacklists
* Antivirus vendors




## API Documentation

####Required Packages/Libraries:
  
 [Requests](https://pypi.python.org/pypi/requests)  
### To install:  
 Pip install cymon



### Authentication

This existing API is synchronous - a search request is issued via a simple GET and POST HTTP call, and the result is computed and returned. Any request made to the Cymon API needs to include an HTTP Basic Authentication header using an authenticaton token. All modern browsers (as well as command line tools like curl and wget) support basic authentication. This is secure, since all communication with the cymon api service happens over SSL/HTTPS.




### HTTP Status Codes

<table>
<tr>

<th>Status code</th>

<th>Description</th>

</tr>

<tr>
<td><tt>200</tt></td>
<td><tt>Ok Success</tt></td>
</tr>


<tr>
<td><tt>401</tt></td>


<td> Unauthorized: Access is denied due to invalid token.</td>
</tr>

<tr>
<td><tt>404</tt></td>

<td>NOT FOUND. The request was invalid or cannot be otherwise served.</td>
</tr>
<tr>
<td><tt>500</tt></td>
<td><tt>Internal service error</tt></td>
</tr>
</table>



#### Example Error Response

```json
{
raise HTTPError(http_error_msg, response=self)
requests.exceptions.HTTPError:  
401 Client Error: UNAUTHORIZED
}
```

#### Other errors
#####AttributeError: 'Cymon object has no attribute'

* A query isn't specified.
* A query is invalid.

###Rate Limits
* Up to 1000 requests/day  
* To request for a limit increase, please contact [eSentire](https://esentire.com//)

### Using the API

<table>

<td><tt>Base endpoint</tt></td>
<td><tt>https://cymon.io/api/nexus/v1</tt></td>
</tr>
</table>


### ip_lookup

Provides IP object details

```/api/nexus/v1/ip/{addr}/```  

Method: ```GET```

<table>
<tr>
<th>Parameter</th>
<th>Type</th>
<th>Required</th>
<th>Description</th>
</tr>
<tr>
<td><tt>addr</tt></td>
<td>String</td>
<td>Yes</td>
<td>IP address</td>
</tr>
</table>


#### Sample response body
```
{
  "addr": "8.8.8.8",
  "created": "2015-03-23T12:03:42",
  "updated": "2015-05-21T19:21:29",
  "sources": [
    "malwr.com",
    "virustotal.com",
    "urlquery.net",
    "google safebrowsing"
  ],
  "events": "https://cymon.io/api/nexus/v1/ip/8.8.8.8/events",
  "domains": "https://cymon.io/api/nexus/v1/ip/8.8.8.8/domains",
  "urls": "https://cymon.io/api/nexus/v1/ip/8.8.8.8/urls",
  "timeline": "https://cymon.io/api/nexus/v1/ip/8.8.8.8/timeline"
}
```



### ip_events

Provides security event resources

```/api/nexus/v1/ip/{addr}/events/```  

Method: ```GET```


<table>
<tr>
<th>Parameter</th>
<th>Type</th>
<th>Required</th>
<th>Description</th>
</tr>
<tr>
<td><tt>addr</tt></td>
<td>String</td>
<td>Yes</td>
<td>IP address</td>
</tr>
</table>


#### Sample response body

```
{
    "title": "Malicious activity reported by urlquery.net",
    "description": "Posted: 2015-06-28 12:55:50\nIDS Alerts: 0\nURLQuery Alerts:
    1\nBlacklists:0\nMalicious page URL: http://iad12s04-in-f22.1h100.net/irwravxrc/tra_q.php",
    "details_url": "http://urlquery.net/report.php?id=1435488950438",
    "created": "2015-06-28T10:56:26",
    "updated": "2015-06-28T10:56:26",
    "tag": "malicious activity"
},


```
### ip_domains

Provides domains associated with an IP

```/api/nexus/v1/ip/{addr}/domains/```  

Method: ```GET```


<table>
<tr>
<th>Parameter</th>
<th>Type</th>
<th>Required</th>
<th>Description</th>
</tr>
<tr>
<td><tt>addr</tt></td>
<td>String</td>
<td>Yes</td>
<td>IP address</td>
</tr>
</table>


#### Sample response body

```
{
    {
  "count": 86,
  "next": "https://cymon.io/api/nexus/v1/ip/8.8.8.8/domains/?offset=10",
  "previous": null,
  "results": [
    {
      "name": "ms08067.com",
      "created": "2015-06-12T02:55:16",
      "updated": "2015-06-20T18:19:21",
      "sources": [
        "urlquery.net",
        "google safebrowsing"
      ],
      "ips": [
        "https://cymon.io/api/nexus/v1/ip/61.44.22.36",
        "https://cymon.io/api/nexus/v1/ip/69.80.104.253",
        "https://cymon.io/api/nexus/v1/ip/38.64.152.247",
        "https://cymon.io/api/nexus/v1/ip/206.46.186.241",
        ...
},
```

### ip_url

Provides URLs associated with an IP

```/api/nexus/v1/ip/{addr}/urls/```  

Method: ```GET```


<table>
<tr>
<th>Parameter</th>
<th>Type</th>
<th>Required</th>
<th>Description</th>
</tr>
<tr>
<td><tt>addr</tt></td>
<td>String</td>
<td>Yes</td>
<td>IP address</td>
</tr>
</table>


#### Sample response body

```
{
  "count": 84,
  "next": "https://cymon.io/api/nexus/v1/ip/8.8.8.8/urls/?offset=10",
  "previous": null,
  "results": [
    {
      "location": "http://iad12s04-in-f22.1h100.net/irwravxrc/tra_q.php",
      "created": "2015-06-28T10:56:26",
      "updated": "2015-06-28T10:56:26",
      "sources": [
        "urlquery.net"
      ],
      "ips": [
        "https://cymon.io/api/nexus/v1/ip/8.8.8.8"
      ],
      "domains": "https://cymon.io/api/nexus/v1/domain/iad12s04-in-f22.1h100.net"
    },
     ...
```

### ip_timeline

Provides a timeline of details

```/api/nexus/v1/ip/{addr}/timeline/```  

Method: ```GET```


<table>
<tr>
<th>Parameter</th>
<th>Type</th>
<th>Required</th>
<th>Description</th>
</tr>
<tr>
<td><tt>addr</tt></td>
<td>String</td>
<td>Yes</td>
<td>IP address</td>
</tr>
</table>


#### Sample response body

```
{
      "time_label": "Jun. 28, 2015",
      "events": [
        {
          "description": "Posted: 2015-06-28 12:55:50\nIDS Alerts: 0\nURLQuery Alerts: 1\nBlacklists: 0\nMalicious page URL: http://iad12s04-in-f22.1h100.net/irwravxrc/tra_q.php",
          "created": "2015-06-28T10:56:26",
          "title": "Malicious activity reported by urlquery.net",
          "details_url": "http://urlquery.net/report.php?id=1435488950438",
          "tag": "malicious activity"
        },
        {
          "description": "Posted: 2015-06-28 12:53:10\nIDS Alerts: 0\nURLQuery Alerts: 1\nBlacklists: 0\nMalicious page URL: http://iad12s04-in-f22.1h100.net",
          "created": "2015-06-28T10:53:24",
          "title": "Malicious activity reported by urlquery.net",
          "details_url": "http://urlquery.net/report.php?id=1435488790307",
          "tag": "malicious activity"
        }
      ]
    },
     ...
```

### domain_lookup

Provides domain object detail

```/api/nexus/v1/domain/{name}```  

Method: ```GET```


<table>
<tr>
<th>Parameter</th>
<th>Type</th>
<th>Data Type</th>
<th>Required</th>
<th>Description</th>

</tr>
<tr>
<td><tt>name</tt></td>
<td>Path</td>
<td>String</td>
<td>Yes</td>
<td>Domain name</td>

</tr>
</table>

#### Sample response body

```
{
  "name": "google.com",
  "created": "2015-01-26T12:31:37",
  "updated": "2015-07-03T18:14:23",
  "sources": [
    "malwr.com",
    "ptr",
    "urlquery.net",
    "cleanmx-malware",
    "cleanmx-phishing"
  ],
  "ips": [
    "https://cymon.io/api/nexus/v1/ip/168.235.156.164",
    "https://cymon.io/api/nexus/v1/ip/208.146.44.191",
    "https://cymon.io/api/nexus/v1/ip/173.194.67.91",
     ...
```

### domain_events

Provides security events resource

```/api/nexus/v1/domain/{name}/events/```  

Method: ```GET```


<table>
<tr>
<th>Parameter</th>
<th>Type</th>
<th>Data Type</th>
<th>Required</th>
<th>Description</th>

</tr>
<tr>
<td><tt>name</tt></td>
<td>Path</td>
<td>String</td>
<td>Yes</td>
<td>Domain name</td>

</tr>
</table>


#### Sample response body

```

```


### url_lookup

Provides security events resource

```/api/nexus/v1/domain/{name}/events/```  

Method: ```GET```


<table>
<tr>
<th>Parameter</th>
<th>Type</th>
<th>Data Type</th>
<th>Required</th>
<th>Description</th>

</tr>
<tr>
<td><tt>URL</tt></td>
<td>Path</td>
<td>String</td>
<td>Yes</td>
<td>url path</td>

</tr>
</table>


#### Sample response body

```

```
### ip_blacklist

Retrieve list of IPs that are associated with certain tag

```/api/nexus/v1/blacklist/ip/{tag}/ ```  

Method: ```GET```

<table>
<tr>
<th>Parameter</th>
<th>Type</th>
<th>Data Type</th>
<th>Required</th>
<th>Description</th>

</tr>
<tr>
<td><tt>tag</tt></td>
<td>Path</td>
<td>String</td>
<td>Yes</td>
<td>Tag name</td>

</tr>
</table>

####Supported tags:  
* malware  
* botnet  
* spam  
* phishing  
* malicious activity  
* blacklist  
* dnsb  

#### Sample response body

```
{u'count': 228, u'previous': None, u'results': 
[{u'url': u'https://cymon.io/api/nexus/v1/ip/185.58.116.134',
u'addr': u'185.58.116.134'},
{u'url': u'https://cymon.io/api/nexus/v1/ip/188.213.133.67',
u'addr': u'188.213.133.67'},
...

Process finished with exit code 0


```


##For more information:

Cymon API library (Python): [Here](https://github.com/eSentire/cymon-python)  

Contact: roy.firestein@esentire.com






