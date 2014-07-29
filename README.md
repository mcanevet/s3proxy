S3Proxy
=======
S3Proxy allows applications using the S3 API to interface with a variety of
object stores, e.g., EMC Atmos, Microsoft Azure, OpenStack Swift.  It runs a
local HTTP server which translates S3 operations into provider-specific
operations.  S3Proxy also allows developers to test against S3 without the cost
or latency associated with using AWS by using the local file system.

Features
--------
* create, remove, list containers
* put, get, remove, list blobs (up to 2 GB in size)
* store and retrieve user metadata

Supported object stores:

* atmos
* aws-s3
* azureblob
* cloudfiles-uk and cloudfiles-us
* filesystem (on-disk storage)
* hpcloud-objectstorage
* s3
* swift and swift-keystone
* transient (in-memory storage)

Installation
------------
S3Proxy requires Java 7 to run.  Presently there is no binary release but
[Bintray](https://bintray.com/) will host releases in the future.

One can build the project by running `mvn package` which produces a binary at
`target/s3proxy`.

Examples
--------
Linux and Mac OS users can run S3Proxy either via the executable jar or by
explicitly invoking java:

```
s3proxy --properties s3proxy.conf
java -jar s3proxy --properties s3proxy.conf
```

Windows users must explicitly invoke java.

Configuration
-------------
Users can configure S3Proxy via a properties file.  An example:

```
jclouds.provider=transient
jclouds.identity=identity
jclouds.credential=credential
#jclouds.endpoint=http://127.0.0.1:8081  # optional for some providers
jclouds.filesystem.basedir=/tmp/blobstore
s3proxy.endpoint=http://127.0.0.1:8080
```

Users can also set a variety of Java and
[jclouds properties](https://github.com/jclouds/jclouds/blob/master/core/src/main/java/org/jclouds/Constants.java).

Limitations
-----------
S3Proxy does not support:

* single-part uploads larger than 2 GB ([upstream issue](https://github.com/jclouds/jclouds/pull/426))
* multi-part uploads
* authorization of clients
* bucket ACLs
* server-side copy
* URL signing
* metadata with filesystem provider ([upstream issue](https://github.com/jclouds/jclouds/pull/443))
* listening on HTTPS

References
----------
[jclouds](http://jclouds.apache.org/) provides object store support for
S3Proxy.  [s3fs-fuse](https://github.com/s3fs-fuse/s3fs-fuse) provides
file system access to S3 and S3Proxy allows use of other providers.

License
-------
Copyright (C) 2014 Andrew Gaul

Licensed under the Apache License, Version 2.0