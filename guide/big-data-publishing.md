# A Guide to Publishing Big (Open) Data

*Tom Heath, Ulrich Atz, et al.
*The Open Data Institute


## Abstract

While much has been written on the subject of Big Data, the majority assumes application and exploitation of proprietary data sets in enterprise settings. Little consideration has been given to how openly-licensed Big Data may be widely distributed over the public Internet, and the challenges this may pose. This guide presents several case studies of Big Data published under open licenses [check the licenses are solid] that highlight different approaches that may be taken, before exploring distribution mechanisms and emerging best practices for publishing 'Big Open Data'. Guidance is provided covering topics such as file formats, data partitioning, compression, and inclusion of metadata. The guide concludes with examination of various data hosting/publishing platforms and associated costs.

## Executive Summary
In recent years Big Data gained significant coverage, but usually assumes proprietary data sets in enterprise settings. This guide is one of the first that explores the intersection of Big and Open Data and its practicalities. 

We explain different approaches that tackle the challenge of how to distribute large data set over the public Internet. The **four case studies** are:

1. The [1,000 Genome project](http://www.1000genomes.org/data#DataAccess) with an extreme size of 260 terabytes, using a proprietary variant on FTP.
2. The Tiny Images data set, which can be accessed via a conventional hyperlink to download these files over HTTP.
3. The BioTorrents project provides a platform allowing scientists to share data via the BitTorrent peer-to-peer file sharing protocol.
4. Researchers at the [Measurement Lab (M-Lab)](http://www.measurementlab.net/), who publish over 747Tb of data under a CCZero licence.

Some **principles** of publishing Open Data can be directly applied to Big Data:

1. Understanding your Audience: For example, by applying for an [Open Data Certificate](http://certificates.theodi.org/) for a particular data set.
2. Understanding your Data: What is the nature of the data in terms of, for example, the "three Vs"?
3. Understanding your Resources: For example, what do you need to consider for the first release vs updates?

In many cases it is desirable, and much more practical, to publish Big Data in **small fragments**. We explain different *compression formats*, *sharding/partitioning* complete database dumps and different *distribution formats*.

Cost for **hosting programmes and platforms** have, and continued to, decrease. An example of the popular *Amazon S3* service is in the table below. However, if you are a public institution you may qualify for *free hosting programmes*.


| size | no. of full downloads | cost per month (as of June 2013) |
|---|---|---|
|  |  |All prices based on the region EU (Ireland). |
|10 GB | 10 times | ~ $11 |
|10 GB | 1000 times | ~ $1319 |
|1 TB | 10 times | ~ $1456 |

Lastly, it is important that you publish a minimum of metadata that explains your open data. This includes a *licence*, its *provenance* and some *contact information* for users.




## Introduction: from Big Data to Big Open Data

The notion of *Big Data* has gained significant coverage in the technology press and broader media, with commentators seeing opportunities for new business insights to be derived from routine, large-scale data analysis. Most definitions of the term reference the "three Vs" (Volume, Variety, and Velocity, [Douglas, 2001][Douglas2001]) and loosely define Big Data as that which is not easily managed using traditional computing/data management approaches and infrastructures. Needless to say, 'traditional' remains ambiguous, and the volume of data that may be easily processed on any infrastructure continues to increase, making it almost impossible to quantify Big Data.

A more meaningful understanding of the concept may be gained by considering the context in which data is used. Broadly speaking, the majority of the discourse on Big Data assumes it will be applied in an enterprise setting. For example, a large retailer may process massive volumes of proprietary transaction data to produce insights into shopping habits, such as which items are typically bought during the same shopping trip. Alternatively, a retailer may attempt to relate purchasing habits to external factors, such as weather trends or sporting events, where the analysis would involve consumption of third party data.

In either case, data processing is assumed to take place 'behind the firewall', where it can be transferred relatively easily across corporate networks or aggregated in a data warehouse. Less consideration is given to scenarios where large, varied, or rapidly changing data is made publicly available under an open license for reuse by a wide range of consumers. The first challenge in such cases, before any processing/analysis can take place, is to distribute the data. The limited network connectivity available for accessing large data sets may mean that a more conservative definition/quantification of Big Data is required when considering publication of 'Big Open Data'. To put it another way, the challenges of 'bigness' apply to smaller data sets in an open publication scenario than they do in a bounded, enterprise setting. For example, it may be trivial to transport gigabytes of data across an internal network, but publishing the same data volume on the public Web for anyone to access would likely require special measures to be taken in order to be feasible. It is these special measures which are the focus of this guide.

In addition, fewer assumptions about the audience can be made when large data volumes are openly published. In an enterprise setting, for example, the sole audience for a dataset may be in-house data analysts whose technical skills and available resources are well understood. In contrast, data published more openly may reach a wide range of audiences with varied skills and technical/computing resources, and who may use it for a wider range of purposes than was originally envisaged. Consequently, additional measures should be taken where possible to cater for these diverse audiences.

This guide is designed to highlight the challenges presented when openly publishing data via the Web (or through other Internet-based protocols) and, where possible, to describe the measures that can be taken to mitigate these challenges. Crucially, these challenges do not relate simply to volume or velocity of the data published, but to technical, practical and legal factors that may hinder the utility/usability of the data if not addressed.


## Case Studies of Big Open Data Publication

The four case studies below illustrate different approaches to publishing big open data via the public Internet.


### 1,000 Genomes

The [1,000 Genome project](http://www.1000genomes.org/data#DataAccess) is an extreme case in terms of size. With 260 terabytes, and growing, it is one of the largest distributed data projects ever undertaken in biology. The project provides a resource on human genetic variation by sequencing the genomes of a large number of people. Details of the project are published in an [article in Nature Methods](The 1000 Genomes Project: data management and community access): "In March 2012 the still-growing project resources include more than 260 terabytes of data in more than 250,000 publicly accessible files." The Wellcome Trust alone supports the project with an amount above £5 million [ref].

Distributing the data poses several technical challenges:

1. **Discovering parts of the data**: Some people do not want to or cannot download all of the data. We describe the main method for publication in the next section. The 1,000 Genomes project also provides key components of the data via Amazon Web Services as an alternative distribution channel. The authors notice that most users are more interested specific regions of the genome rather than the entire data set. Consequently, the files are distributed in directories named for the sequence. The complexity of the data, however, may make it extremely difficult to find the relevant parts. The publishers provide among other tools a **directory file**, a **FTP search tool** and a **data browser** to assist users in searching the data. \[TH: think this para needs more work]

2. **Downloading the whole data**: Some \[UA: all?] TCP based protocols such as FTP do not scale well [TH: not happy with this passage without references; unsupported assertion]. The 1,000 Genomes project relies on a service from [Aspera](http://asperasoft.com/): Their UDP-based method achieves data transfer rates which in typical usage are 20-30 times faster than FTP. Aspera's [fasp&trade;](http://asperasoft.com/technology/transport/fasp/) is a commercial product, but is, according to one technical team member, used with great success \[TH: what are the requirements for users? a proprietary client?]. At least two mirror download sites provide access simultaneously and efficiently increase the overall download capacity. \[TH: this whole section sounds too promotional; need to make it more objective]

In conclusion, the 1,000 Genome project tackles the technical challenges by publishing the data in different ways. Users can download the whole data set using a proprietary variant on FTP, discussed above. Parts of the data are available and discoverable via an FTP structure, an FTP search, a data slicer, the 1000 Genomes browser \[redundancy here with point 1 above], a public MySQL Instance and a mirror in the Amazon Simple Storage Service (S3). Additional support is manifold. Announcements \[TH: of what?] are made available via RSS, Twitter and also via an email list \[link]. The website [1,000 Genomes](http://www.1000genomes.org/) hosts all links and information about the data and the project. 


### [Tiny Images Dataset]
The Tiny Images data set [http://horatio.cs.nyu.edu/mit/tiny/data/index.html] consists of almost 80 million (79,302,017) images stored in the form of large binary files. They appear \[TH: in what sense do they appear?] in an [academic paper](http://ieeexplore.ieee.org/xpl/login.jsp?tp=&arnumber=4531741&url=http%3A%2F%2Fieeexplore.ieee.org%2Fxpls%2Fabs_all.jsp%3Farnumber%3D4531741) on scene recognition from 2008.

In total there are 5 files that can be downloaded via a download link on the site:

  - Image binary (227 Gb)
  - Metadata binary (57 Gb)
  - Gist binary (114 Gb)
  - Index data (7 Mb)
  - Matlab Tiny Images toolbox (150 Kb) 

Despite data files totalling hundreds of gigabytes in size, consumers of the data must simply follow a conventional hyperlink to download these files over HTTP. While this approach provides a simple distribution mechanism from the perspective of the publisher, it has a number of shortcomings:

  1. Smaller subsets of the data cannot be downloaded individually, meaning it is not possible to explore a sample of the data to see whether it suits a user's needs.
  2. A user whose Internet connection is interrupted during the download may initiate a fresh download of the entire data file, depending on the client being used, rather than resuming a partially completed download. This can increase both the overall time to retrieve the data and the data transfer costs of both parties. Resumability is discussed in more detail below.
  3. Support and documentation is very limited. \[@UA: is this a shortcoming of this publication approach or of the project in general?]

\[UA: More on these shortcomings]

In conclusion, provision of large data files over HTTP provides a low barrier of entry for publication, but may not be well suited to all audiences and/or usage contexts.


### BioTorrents

The BioTorrents project, described in a [research article](http://www.plosone.org/article/info%3Adoi%2F10.1371%2Fjournal.pone.0010071) \[UA: Good read for more on bittorrent], provides a platform allowing scientists to share data via the [BitTorrent](http://en.wikipedia.org/wiki/BitTorrent) peer-to-peer file sharing protocol. All data published via the platform is open-access and discoverable, while the platform itself provides features such as keyword search, category browsing, RSS feeds, torrent comments and a discussion forum. The BioTorrents source code is published on [GitHub](https://github.com/mlangill/biotorrents/). At the time of writing the site counts 1,851 registered users and 120 data sets. 

As described in [ref](http://www.plosone.org/article/info%3Adoi%2F10.1371%2Fjournal.pone.0010071), sharing data on BioTorrents is a three step process:

  1. The user creates a torrent file on their personal computer. This assumes they already have a BitTorrent client installed.
  2. The newly created torrent file is uploaded to the website. It includes metadata such as a user description, category, and license type. This assumes the user previously created an account.
  3. The user shares the data by continuously running a BitTorrent client on their computer/server.

\[@UA: is this a direct quote?]

BioTorrents provides a rich case study of using BitTorrent for data distribution. Advantages and disadvantages of BitTorrent as a distribution protocol are discussed below.


### Measurement Lab

The [Measurement Lab (M-Lab)](http://www.measurementlab.net/) publishes over 747Tb of data under CCZero and they get about 430Gb of uncompressed data a day.




## 2. Publishing Big Open Data

### 2.1 General considerations

#### 2.1.1 Understanding your Audience

Technical considerations, such as the nature of the data and the resources available to data consumers, will shape many decisions when publishing big open data. Answering the following questions may help in understanding the needs of the target audience for the data:

  1. How much **technical knowledge** can be assumed? For example, can users be expected to download/install a BitTorrent or FTP client?
  2. What are the **computing resources** available to users? If your data exceeds the limits of a personal computer, the data may need to be 'sharded' into managable pieces.
  3. What is the potential **reach** for the data? Is it of interest to 10 users or 10,000?
  4. What are likely **use cases** for the data?

Keeping the user in mind also ought to guide all other aspects of publishing, such as:
  - How the data is documented
  - What further context is provided about the data
  - What level of support is offered

Further guidance on these broader aspects of open data publishing can be obtained by applying for an [Open Data Certificate](http://certificates.theodi.org/) for a particular data set.


#### 2.1.2 Understanding your Data

As the case studies above illustrate, there is great variety in the methods used for publication of Big Open Data. Before exploring the most appropriate methods for a particular data set it is critical to consider the nature of the data itself, and how this may influence the choice of publication mechanism.

If the data to be published changes rarely, or the intention is to simply publish static, historic snapshots of the data, then the data dump techniques described in the section below on *Publishing Data Dumps* will be most suitable. Conversely, if the data to be published has great *variety*, changes regularly (*velocity*), or is required by consumers in near real-time, the *Publishing Many Small Data Fragments* and *Publishing Streaming Data* section below will likely be of greatest value.

#### 2.1.3. Understanding your Resources
A list of questions you might consider:

* How many hours are required to publish it the first time?
* How many hours are required to maintain it?
* How many hours are required to add new data streams?
* How many hours are required to add new data sets?



### Publishing Big Open Data in Small Fragments

\[@TH move into/integrate into next section]

In many cases, publishing large data dumps alone is undesirable, as this may limit the usability of the data for downstream consumers. For example, consumers may wish to:

* inspect portions of the data before gathering more
* download only a portion of the data; the portion required may not be easily predicted and may vary between consumers, making it hard to cater for this requirement using data dumps (see also the section on *Partitioning* below)
* regularly reharvest sub-sets of the data that change frequently (i.e. high velocity data)

To give an example, horizontal e-commerce sites such as Amazon.com or Tesco.com may have a wide variety of data, such as product information across multiple vertical segments, product reviews, pricing information, and stock levels. Each of these may change at a different rate, while individual downstream consumers may want access to different sub-sets of the data.

This diversity in the dynamics of the data, and in consumer requirements, makes periodic data dumps unsuitable for any applications that rely on prompt access to the most recent data. Therefore, in addition to data dumps, it is appropriate to consider publishing Big Open Data in smaller fragments via a conventional Web site or Web API.


#### Web APIs and Web sites

Web APIs (Application Programming Interfaces) "provide simple query access to structured data over the HTTP protocol" [Linked Data: Evolving the Web into a Global Data Space][LDBook]. Deploying a Web API can enable consumers to access smaller fragments of an otherwise very large data set, and vary how the data is retrieved according to the nature of the data itself.

While many Web APIs are deployed in parallel to but separately from a conventional Web site, there is a school of thought that argues that "your Web site is your API" [ref?]. The essence of this argument is that the data should be deployed alongside conventional Web content, i.e. as part of the same site.

A number of methods exist to enable this data publication pattern. For example, RDFa [ref] allows data to be embedded within HTML documents, while data in other formats may be published in separate files alongside HTML documents that present the data for human users.


#### File Formats
\[@TH]

\[OKFN recommend csv and json]
(http://data.okfn.org/standards)

\[*CSV vs JSON vs XML vs RDFx vs proprietary db dumps vs whatever...*]

\[*block robots using robots.txt? what are the hosting/resource requirements of this?*]



### Publishing Data Dumps


#### Compression

In many big data publishing scenarios it is highly desirable to compress the data before publication to reduce the size of files downloaded by consumers. Compression becomes particularly important as the volume of data increases, but does bring a number of disadvantages. For example, consumers must decompress files in order to inspect the data, and compressed files are less likely to be indexed by search engines, thereby limiting the discoverability of data and the potential for onward linking to related data. The remainder of the section briefly reviews various open compression formats that may be used for big data publishing.

Two formats that are widely supported are *Zip* and *Gzip*. \[*do both use the same compression algorithm?*]. The trade-offs between these two formats are discussed in more detail in [this article](http://www.differencebetween.net/technology/difference-between-zip-and-gzip/), but in this context the salient differences between these formats can be summarised as follows:

##### Support for Archives

The Zip format is able to gather together multiple input files into one output archive, compressing each input file individually. By contrast, Gzip is a pure compression format that relies on an external programme such as *Tar* to first collect multiple input files into one archive before compression.

##### Compression Performance

By compressing each file in an archive individually, Zip is unable to exploit redundancy between files in the archive, and therefore typically achieves inferior compression performance compared to Gzip. This performance difference can be significant, but is naturally dependent on there being more than one file in an archive [check this -- do they use the same compression algorithm?] and on the degree of redundancy between files in the archive.

\[*@TH show some indicative stats about the performance of different methods on the same data in one file or split across several*]

##### Individual Files

Conversely, Zip has an advantage when individual files need to be retrieved from an archive, as each can be extracted without requiring the entire contents to be decompressed. In the case of Gzip applied to Tar archives, the Tar programme has a compression-aware mode that can extract specific files from an archive, but in the worst case the entire archive may need to be decompressed before the target file is located \[*double check that this is the case*]. It should be noted that the compression-aware mode in Tar supports multiple compression formats in addition to Gzip, including *Bzip2* and *LZO*.

##### Platform Support

Historically, use of the Zip format has been more prevalent on Windows platforms, while Gzip has a stronger association with Unix-like platforms (e.g. Mac OSX and Linux). In reality, all of these platforms support both compression formats, but users of each may be more familiar with the respective *de facto* standard for their platform and have tools more readily available. As a broad generalisation, consumers of big data are more likely to use Unix-like platforms, and therefore Gzip may be a sensible default, but the downstream usage context should always be considered.

[@TH]
[*Is Zip supported at all by Hadoop?*]

\[*splittability]
\[*BZ2, LZO?, 7Z(arch)?*]

In summary, the most appropriate compression scheme to adopt will depend on the intended audience, the tooling likely to be used, the nature of the data itself (i.e. it's inherent redundancy), and how it is packaged/partitioned for publication.


#### Partitioning/Sharding

For publication as static dumps, data sets beyond a certain size will likely need to be split up into smaller pieces to aid discovery, distribution, and reuse. This process could be referred to as *partitioning* or *sharding*, with different segments of one logical dataset contained within different files. Various (and multiple) partitioning schemes could be used for the same data set, depending on how the data may be used.

##### Logical Partitioning

Perhaps the most obvious partitioning scheme is to split the data into logical groups, according to how consumers may wish to use it. For example, descriptive product data may be partitioned by product category, while transaction or event data may be partitioned by time period (e.g. daily, weekly, monthly, yearly depending on the data volume).

##### Size-Optimised Partitioning

How the data will be retrieved and processed has an impact on how large each partition should be. On the one hand, a large number of small files published on the Web is desirable, as this enables each partition to be identified by its own URI at a granular level, referenced in other data sources and documents, and easily inspected with common desktop tools (e.g. spreadsheet applications or text editors).

On the other hand, a smaller number of larger files may have advantages for consumers of the data. For example, retrieving many small files over HTTP may incur a cumulative *round-trip time* that significantly and negatively impacts the time taken to download the entire data set.

\[*any considerations here in ease of downloading? depends on tools being used*]

How the data may be processed downstream also has a bearing on the optimum file size of partitions. For example, *[Apache Hadoop](http://hadoop.apache.org/) MapReduce* is a widely used framework for large-scale, distributed data processing. Architectural features of the MapReduce framework and underlying HDFS filesystem dictate that storing and processing large numbers of small files is significantly less efficient and less reliable than processing fewer, larger files. These issues are described in more detail in the following articles:

* [The Small Files Problem][WhiteHadoopSmallFiles]
* [Apache Hadoop: Best Practices and Anti-Patterns][YahooHadoopAntiPatterns]

In conclusion, a sensible compromise may be to partition the data into multiple smaller files but publish these alongside larger files that combine many smaller partitions (i.e. using less fine-grained partitioning). Alternatively, larger files may be published alongside sample data so potential consumers can easily inspect the contents.



#### Distribution Protocols

[@TH]

| Protocol	| Technical Skills Required 	| Resumability 	| Throttling 	|
|-----------------|-----------------------------------|-----------------|-----------------|
| HTTP		| Low				|		|		|
| FTP		| Medium				|		|		|
| Rsync		| High				|		|		|
| BitTorrent 	| Medium				|		|


* HTTP: talk here about things like wget that are nicer than a browser
* FTP: Advantages over HTTP?
* Rsync
* Bittorrent
    \[* From James: *We discussed distributing data over bittorrent, and how you can ensure provenance, reliability etc. Well, if you had the .torrent file contained in a data package type git repository and included an md5sum of the contents, you presumably could use that to verify that the torrented version was correct with the official release. Perhaps data packages (or other metadata formats) could be extended to include a md5sum of the data in the referenced file.*]

##### Advantages of using BitTorrent

* Compared to hosting files through FTP or HTTP, the BitTorrent protocol excels when data sets are distributed among many users. Especially with large files the bandwidth requirements spread across all computers which seed and actively download the data. This may also yield much faster download rates. 
* BioTorrents can act as a central listing of results, datasets, and software that can be browsed and searched.
* Data published with the BitTorrent protocol can be decentralised and is still available even if one server becomes disabled.


##### Disadvantages of using BitTorrent

* BioTorrents faces the problem that it requires users to download additional software to access torrents (files and data). 
* Moreover, BitTorrent is often associated with illegal file-sharing, which may become a barrier in some institutions. 
* BitTorrent is a rather unknown method of publishing data, hence, a lot of technical questions remain open; such as where to publish the torrent and how to communicate this method of publishing.



### Importability

@TH
\[*Generic discussion/overview of different formats and how they impact on importability*]

\[*Discuss different consumption scenarios, e.g. public processing on EC2/EMR vs pulling down into a proprietary solution vs a behind the firewall solution on something like OpenStack]

\[*Object vs Block storage in e.g. Amazon EC2/EMR/S3; ease of mounting block storage from nodes in a cluster vs pulling down from object storage; compare this to disk requirements on each node; what is the optimum approach in different settings]



### Metadata Publishing
[@TH]

#### licensing

\[*relatively understood problem for small fragments and streaming data, dumps likely to be more ad-hoc. what is best practice? bundle a license statement/document in the root of every dump archive?*]

#### provenance

\[*same as above re licensing, but make sure it's also in machine-readable form?*]


#### update frequency

\[*follow similar approaches to documenting this as for licensing and provenance*]

\[*ref ODCs*]


## Hosting Programmes and Platforms

### Free Hosting Programmes

Probably the most well-known option for free hosting of open data sets is the [Amazon Public Data Sets](http://aws.amazon.com/publicdatasets) programme. This has obvious cost benefits for data owners/publishers, but also brings advantages to consumers as the data sets are readily accessible within the Amazon EC2 cloud computing infrastructure, either as block storage snapshots that can be instantiated and attached to virtual machines in the Amazon cloud environment or as files within the S3 file storage service. This reduces the need for consumers to download the data to local computing infrastructure before it can be used/analysed. Data sets hosted under this programme are typically in the 1GB to 1TB range, and publishers must have the rights to make the data publicly available.

\[*should we also cover the Google Public Datasets programme? not as open or comprehensive from what I can tell* / what other services are available?]


\[@UA]
http://data.okfn.org/about

### Paid Hosting Services

\[@UA]
\[*If you want to pay for hosting and publishing of large data sets, the options include the following:*]

* Amazon S3...
* Rackspace Cloud...
* [others...?]





#### Costs

\[*@ulrich: do you want to work out some sample costs for different sizes of data for S3 and Rackspace Cloud, e.g. 100GB, 1TB, 10TB, 100TB?*]

\[@UA move tables into appendix / intro text which explains pricing models]

Pricing follows a pay-as-you-grow model. 

##### Amazon S3

###### Examples

| size | x full downloads | cost per month |
|---|---|---|
|10 GB | 10 times | ~ $11 |
|10 GB | 1000 times | ~ $1319 |
|1 TB | 10 times | ~ $1456 |

All prices based on the region EU (Ireland).

###### Storage Pricing
| Data Storage| Standard | Reduced Redundancy | Glacier* |
|---|---|---|---|
|First 1 TB / month	| 	$0.095 per GB|	$0.076 per GB| $0.011 per GB|
|Next 49 TB / month|	$0.080 per GB|	$0.064 per GB| $0.011 per GB|
|Next 450 TB / month|	$0.070 per GB|	$0.056 per GB| $0.011 per GB|
|Next 500 TB / month	|	$0.065 per GB|	$0.052 per GB| $0.011 per GB|


\*Amazon Glacier is optimised for data that is infrequently accessed and for which retrieval times of several hours are suitable.

###### Bandwidth Pricing

|Data transfer **out** | Pricing |
|---|---|
|First 1 GB / month	 | $0.000 per GB |
|Up to 10 TB / month |	$0.120 per GB |
|Next 40 TB / month	 | $0.090 per GB |
|Next 100 TB / month |	$0.070 per GB |
|Next 350 TB / month |	$0.050 per GB |

All **incoming** data transfer: $0.000 per GB

##### Rackspace Cloud Files

###### Examples

| size | x full downloads | cost per month |
|---|---|---|
|10 GB | 10 times | ~ $13 |
|10 GB | 1000 times | ~ $1201 |
|1 TB | 10 times | ~ $1300 |


###### Storage Pricing

|Data storage| Pricing |
|---|---|
|First 1 TB / month	 | $0.100 per GB |
|Next 49 TB / month	 | $0.090 per GB |
|Next 150 TB / month |	$0.085 per GB |
|Next 300 TB / month |	$0.080 per GB |

###### Bandwidth Pricing

|Data transfer **out**| Pricing |
|---|---|
|First 10 TB / month	 | $0.120 per GB |
|Next 40 TB / month	 | $0.100 per GB |
|Next 150 TB / month |	$0.070 per GB |
|Next 300 TB / month |	$0.050 per GB |

All **incoming** data transfer: $0.000 per GB





## Acknowledgements

\[*acknowledge people here who have helped*]


## References

[Douglas2001]:	Douglas, Laney. "3D Data Management: Controlling Data Volume, Velocity and Variety". Gartner. Retrieved 6 February 2001. http://blogs.gartner.com/doug-laney/files/2012/01/ad949-3D-Data-Management-Controlling-Data-Volume-Velocity-and-Variety.pdf 
[WhiteHadoopSmallFiles]: http://blog.cloudera.com/blog/2009/02/the-small-files-problem/	"The Small Files Problem"
[YahooHadoopAntiPatterns]:	http://developer.yahoo.com/blogs/hadoop/apache-hadoop-best-practices-anti-patterns-465.html	"Apache Hadoop: Best Practices and Anti-Patterns"
[LDBook]:http://linkeddatabook.com/editions/1.0/#htoc4 "Linked Data: Evolving the Web into a Global Data Space"



## Appendix
