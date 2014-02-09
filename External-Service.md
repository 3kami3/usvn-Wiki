External Integration
=====================

This document provide methods and documentations for external documentation with USVN

----------

Service
---------

All methods are implemented on serviceController, located on:

```
http://usvn.domain.com/service/METHOD_NAME
``` 

Request
---------

All integration are composed by a POST request and an XML in the body (RAW data)

Authentication
--------- 

All request need to send username and password of user who making access. The section with contain this information, is the tag **auth**, like the follow sample

Documentation
--------- 

### Listing projects of the user

To retrieve projects where user can access, the integration method used is the _projects_

```
http://usvn.domain.com/service/projects
```

The XML follow is used for make request

```
<?xml version="1.0" encoding="UTF-8"?>
<usvn>
   <auth>
      <username>myusername</username>
      <password>mypassword</password>
   </auth>
</usvn>
```

And the follow XML are returned

```
<?xml version="1.0" encoding="UTF-8"?>
<usvn>
  <projects>
    <project>
      <id>2</id>
      <name>project1</name>
      <start_date>2013-12-09 13:06:37</start_date>
      <description>Repository of my first project</description>
    </project>
    <project>
      <id>7</id>
      <name>project2</name>
      <start_date>2013-04-29 17:31:06</start_date>
      <description>Repository of another project</description>
    </project>
  </projects>
</usvn>
```

An example of this integration:

```
<?php

// Create XML request
$xml = "<?xml version=\"1.0\" encoding=\"UTF-8\"?>
<usvn>
   <auth>
      <username>myusername</username>
      <password>mypassword</password>
   </auth>
</usvn>";

// Do a request
$ch = curl_init();
curl_setopt($ch, CURLOPT_URL, "http://usvn.domain.com/service/projects" );
curl_setopt($ch, CURLOPT_RETURNTRANSFER, 1 );
curl_setopt($ch, CURLOPT_POST, 1 );
curl_setopt($ch, CURLOPT_POSTFIELDS, $xml); 
curl_setopt($ch, CURLOPT_HTTPHEADER, array("Content-Type: application/xml")); 
$result = curl_exec($ch);

// Show result
var_dump($result);
```
