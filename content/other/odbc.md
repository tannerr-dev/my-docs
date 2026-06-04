
ODBC = Open Databse Connectivity
DSN = Data Source Name

---
## NetSuite ODBC setup

### Install driver
- download NetSuite ODBC linux driver
- extract
- copy to /opt/netsuite

```
sudo apt-get install unixodbc unixodbc-dev
```

- copy over the contents of odbc.ini and odbcinst.ini from Netsuite driver installation directory into the files in /etc
- enable OAuth 2.0, this is preferred over token
### Ports
Port 1708 needs to be open for outgoing connections


### todo?
- create Client credentials Flow mapping
- get the auth string?
- set OAuth2 token in the ini file
```
OAuth2Token=<token>
```



---

Netsuite config link
https://5296311.app.netsuite.com/app/external/odbc/suiteAnalyticsConnectDownload.nl

OAuth2 links
https://5296311.app.netsuite.com/app/help/helpcenter.nl?fid=article_0907013016.html
https://5296311.app.netsuite.com/app/help/helpcenter.nl?fid=section_157771482304.html

---
https://5296311.app.netsuite.com/app/help/helpcenter.nl?fid=article_0907012731.html


https://5296311.app.netsuite.com/app/help/helpcenter.nl?fid=section_157771733782.html

https://5296311.app.netsuite.com/app/help/helpcenter.nl?fid=section_162686838198.html