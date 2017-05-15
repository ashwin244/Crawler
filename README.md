# Web Crawler
Task : https://gist.github.com/mjgp2/d698087cf27ceae775c3b57051546a8e#file-readme-md

Installation :

 - Download the https://github.com/ashwin244/Crawler/blob/master/WebCrawler.zip and unzip it to the local directory.
 - Go to \WebCrawler\gs-spring-boot\complete folder
 - run ./gradlew bootRun
 
Implementation :

1. Spring boot java application which crawls web-pages from root url at depth 0 until it reaches the maxDepth.

2. Restful request to initiate crawler : http://localhost:8080/setInfo?url=<URL\>&maxDepth=\<depth\>. By default maxDepth is set to 2.

3. Restful request to get information about crawled pages : http://localhost:8080/getInfo?url=<URL>.
  a. If URL exist in database returns : {"url":"http://events.eclipse.org","statusCode":200,"timeStamp":1494885529000}
  b. If URL doesn't exist in database : {"url":"URL doesn't exist","statusCode":0,"timeStamp":0}

4. Use Jetty Asynchronous call to send crawl request and fetch the data on the page, once received look for a:href tags on the page and crawl the individual links. If the domain/host are same as the parent url then increment depth else depth remains the same as parent.

5. Using JSoup to parse the HTML for href tags.

6. Using RocksDB as key-value store to persist the information for crawled pages.
  a. <key, value> = <url, {url, statusCode, timeStamp}
  b. Currently, rocksDB is created in local environment as "C:/rocksDB" where it would store all the key-value pairs in documents.

7. Logging : Invalid URLs (hrefs)

Limitations and Tried efforts:

1. Current, implementation is a single-threaded implementation, I wanted to submit a working solution and due to time constraint I was not able to implemented multi-threaded application. But, I am in process of doing it, I will add the updated zip in the same repository, if possible, please have a look at it.

2. Add a message if user enters incorrect rest request.

3. Tried using Redis/Jedis as key-value store, had issues with configuring it, so considered something on the similar lines hence used RocksDB.

4. URL encoding pending.
