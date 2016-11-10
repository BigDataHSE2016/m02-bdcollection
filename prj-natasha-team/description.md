# duck and cover <sup>1</sup>
(более крутое и/или смешное название приветствуется)

## The Idea
Object recognition from satellite images is a very important application for various purposes. Objects can be recognized based on certain features and then applying some algorithm to extract those objects. Basically object recognition is a classification problem.
We'd like to make a service that recognises some living objects in satellite images using machine learning. 
The service can be he helpful in solving the following tasks:
- Animal (birds, fish, etc.) migration exploring
- Refugees and illegal immigrants movements tracking



### Schema
```
@startuml

package "Images" {
    component [Satellite images] as si
    component [Drone images] as di
    component [Plane images] as pi
    component [Custom photos from the internet] as cust
}

cloud neuronet {
}

cloud "Traditionally gathered data" as td {
}

database "Storage" {
    [study samples]
    [real data]
}

si -down-> neuronet
di -down-> neuronet
pi -down-> neuronet
cust -down-> neuronet
neuronet -down-> [real data]
[study samples] -up-> neuronet
td -up-> [study samples] 
@enduml
```
![shema](https://github.com/BigDataHSE2016/m02-bdcollection/blob/master/prj-natasha-team/blob/hw01-schema-gen.png)

Inside the "neuronet" cloud:

```
@startuml

component [Satellite Image] as si
component [Image Processing Module] as ipm
component [Classifier] as cl
component [Weight file] as wf
component [Extractes birds tribe] as eb

package "Images" {
    component [Output class] as oc
    component [Color assignment] as ca
}

si -down-> ipm
ipm -right-> cl
wf -up-> cl
cl -right-> oc
oc -down-> eb

@enduml
```
![img](https://github.com/BigDataHSE2016/m02-bdcollection/blob/master/prj-natasha-team/blob/hw01-qqq.png)

### Animal migration exploring
The traditional methods require  <sup>2</sup> placing a transmitter or an old-fashioned id ring or nfc-tag on (or in) an animal - it takes a lot of effort, time and money. The result is unstable as a tagged animal may not survive the migration and all will be in vain.

Our method requires not to interact with the animals directly, so we don't need the field biologists, the transmitters and nfc tags.

We also get the data automatically - we don't need to catch the bird again and manually enter the date to a database.

## The Data
Several sourses of images:
- Satellite images
- Drone images
- Plane images
- Custom photos from the internet

All images have to be layer-stacked, georectified and when covering the same spatial subset have been co-registered to each other.

### Satellite images
A satellite image consists of collection of pixels arranged in matrix form i.e. rows and column. Each pixel can be represented by a vector of the size of number of bands. In case of multispectral data, there are 3 or 4 bands corresponding to each pixel. Satellite captures the data of area covered by them in form of reflectance values which are then converted into pixel values based on certain well established computation. These images are captured by various remote sensing satellites. Satellite images are having significant information with respect to natural objects. These images are used for various applications for civilian sector.

Satellite images can be bought from some imagery provider like DigitalGlobe or Orbital Insight. 

Over the next 18 months, companies dealing in satellite imagery plan to place several dozen new satellites in orbit. By the middle of next year, many of those same companies expect to achieve daily “refresh rates”—new imagery of the same parts of the planet—at least once every 24 hours. Humans will soon be able to see huge swaths of the planet change daily.

### Other types of images 

Other types of images can also be used to get more information about sertain objects. 
Pros:
- custom perspective
- can observe a certain area with a longer period of time

Cons: 
- have to clear and classify them 
- the classifier has to be trained separately 


--------

**Footnotes:**

1. See [urbandictionary](http://www.urbandictionary.com/define.php?term=duck+and+cover)
2. See [1](https://www.wbsj.org/nature/kisyou/bfs/pdf/tracking.pdf), [2](http://www.audubon.org/news/tracking-birds-migration-paths-online), [3](http://www.werc.usgs.gov/researchtopicpage.aspx?id=12), [4](https://www.allaboutbirds.org/the-basics-how-why-and-where-of-bird-migration/), [5](http://www.futurity.org/ducks-migration-conservation-733402/)
3. Fish:
    - http://www.futurity.org/ducks-migration-conservation-733402/
    - https://www.sciencedaily.com/releases/2012/05/120522175408.htm
    - http://www.iphc.int/publications/scirep/SciReport0082.pdf
4. Satellite image processing
    - http://www.iaeng.org/publication/WCE2012/WCE2012_pp406-414.pdf
    - http://www.sciencedirect.com/science/article/pii/S0924271698000069
    - http://research.ijcaonline.org/volume95/number10/pxc3896502.pdf
    - http://www.cis.rit.edu/people/faculty/kerekes/pdfs/Meng_Final.pdf
    - Performance Evaluation of Machine Learning Algorithms for Urban Pattern Recognition from Multi-spectral Satellite Image by Marc Wieland and Massimiliano Pittore
    - http://research.ijcaonline.org/volume95/number10/pxc3896502.pdf
5. https://techcrunch.com/2016/04/30/why-image-recognition-is-about-to-transform-business/
6. https://goberoi.com/comparing-the-top-five-computer-vision-apis-98e3e3d7c647#.vlyn60amd
7. http://fortune.com/2016/03/30/facebook-ai-satellite-imagery/
