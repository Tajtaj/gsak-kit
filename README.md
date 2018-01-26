
# GSAK-KIT 

This project provides a plugin for graph analysis and visualization through which you can easily embed, visualize, and analyze your data on any website or web page.<br>

# Building the Project:

#### Prerequisits: 
  * Apache Maven 3.x <br>
  * Java 8 <br>
  * Git (Optional)<br>

#### Steps 
  * Download or clone Gsak-Kit from github into any convenient Directory (Path should not contain special Characters like spaces etc.). <br>
  * Go to Project root directory (Directory containing src, pom.xml) <br>
  * To add dependencies run the following commands in project root directory using command line.</br>
     `mvn install:install-file -Dfile=src/lib/gephi-toolkit.jar -DgroupId=gephi-toolkit -DartifactId=gephi-toolkit -Dversion=1.0 -Dpackaging=jar`</br></br>
      `mvn install:install-file -Dfile=src/lib/gephi-cw.jar -DgroupId=gephi-cw -DartifactId=gephi-cw -Dversion=0.0.1 -Dpackaging=jar`</br></br>
     `mvn install:install-file -Dfile=src/lib/uk-ac-ox-oii-sigmaexporter.jar -DgroupId=uk-ac-ox-oii-sigmaexporter -DartifactId=uk-ac-ox-oii-sigmaexporter -Dversion=1.0 -Dpackaging=jar`</br></br>
  * To build the Project, execut the following commands:<br>
      <code>mvn compile</code><br>
      <code>mvn clean package</code><br>
  * If compilation completed without any error, a <code>target</code> directory will be created inside project root directory. <br>
  * The <code>target</code> directory should contain a jar file with possible name <code>gsak-kit-with-dependencies.jar</code>.<br>
  * To deploy gsak-kit server, execute the following command inside <code>target</code> directory.<br>
      <code>java -jar gephikit-0.0.1-SNAPSHOT-jar-with-dependencies.jar ../configuration.json</code><br>
  * Open <a href="localhost:8282/">localhost:8282/</a> in any browser; A welcome message will be display.<br>
  
  
# Routes:
  Routes define different graph operations that can be applied to the visulized graph. Standard operations mainly include  graph Layouts, Filtration or combination of both.
#### Welcome Route
 * *__Route__*: <code>/</code> It will display welcome message <br><br>

#### Basic Graph
  * *__Route__*: <code>/gephi</code> <br>
  * *__Parameter(optional and Data Source Specific):__*
  * *__Elasticsearch Params Options:__* <code>basicSettings={"selectedDataSource":"elasticsearch","searchValue":"KEYWORDS","host":"localhost","port":"9300","clusterName":"elasticsearch","index":"indexName","type":"indexTypeName","documentsLimit":"1000"}</code> <br>

* *__Text File Params Options:__* <code>basicSettings={"selectedDataSource":"file","filePath":"path_to_the_tweets_file"}</code> <br>
  * *__e.g. File as Data source:__*: <code>localhost:8282/gephi?basicSettings={"selectedDataSource":"file", "filePath":"/etc/tweets.txt"} </code> <br>
  
#### Layouts
  * *__Route__*: <code>/layout</code> <br>
  * *__Layout name:__* <code>"name"=YifanHuLayout</code> <br>
  * *__e.g. YifanHuLayout__*: <code>localhost:8282/layout?layoutSettings={"name":"YifanHuLayout","distance":100, "iterations":100}</code> <br>
  * *__e.g. FruchtermanReingold__*: <code>localhost:8282/layout?layoutSettings={"name":"FruchtermanReingold","size":10, "iterations":100, "gravity":0.1}</code> <br>
  * __Possible Layouts__: <code>YifanHuLayout, FruchtermanReingold</code>

#### Filters
  * *__Route__*: <code>/filter</code> <br>
  * *__Possible Filter Options:__* <code>pageRankThreashhold, nodeCentrailityThreashhold, neighborRangeThreashhold</code> <br>
  * *__e.g. YifanHuLayout__*: <code>localhost:8282/filter?filterSettings={"pageRankThreashhold":10,"nodeCentrailityThreashhold":10, "neighborRangeThreashhold":10}</code> <br> <br>
   
#### KIT-Route
  * *__Route__*: <code>/gsakkit</code> <br>
  * *__Possible Filter Options:__* <code>pageRankThreashhold, nodeCentrailityThreashhold, neighborRangeThreashhold</code> <br>
  * *__Description__*: This route bascially combines all three major functionalities of GSAK-KIT; i.e. Source selection, Layouts, and graph Filteration.<br>
  * *__e.g. Example__*: <code>localhost:8282/gsakkit?basicSettings={"selectedDataSource":"file", "filePath":"/etc/tweets.txt"}&filterSettings={"pageRankThreashhold":10,"nodeCentrailityThreashhold":10, "neighborRangeThreashhold":10}&layoutSettings={"name":"FruchtermanReingold","size":10, "iterations":100, "gravity":0.1}</code> <br> <br>
   
  
GSAK-KIT is divided into two sections.
#### The server side 
  * **input** <br>Text data or the built-in graph<br>
  * **output**<br>Processed graph<br>
  * **Description** <br>
 The server side will do all the data processing, graph generation, analysis, filteration, etc.
 When the server is provided with text data, it generates a graph based on specific keywords or relationships that exist   within the data.
 When the server is provided with the built-in graph, it will analyze and filter the graph to create another processed graph.  The server specifies formats for the input data. From this, the server generates the graph and provides a way to write your  own implementation code for the graph generator. <br>
  * **Third Party Libraries**<br> 
For graph processing we'll use the [GephiToolkit](https://gephi.org/toolkit/) <br>
For java web server we'll use the [Undertow](https://github.com/undertow-io/undertow) <br>
For logging we'll use [log4j2](https://github.com/logentries/le_java/wiki/Log4j2)

#### The front end side 
  * **input** <br> Processed graph data <br> 
  * **output** <br> Sigma graph <br>
  * **Description** <br> The front end will provide a way for visualizing the graph generated by the server. The front end will also provide a way to use the graph services in a webpage. <br>
  * **Third Party Libraries** <br> For front end visualization we'll use the [SigmaJs](http://sigmajs.org/) <br><br>
  The front-end visualization is completely independent of the backend graph generation/processing, it will enable users to design their own front-end layouts and to use graph services where they need.
  
## License
The code is licensed under the [Apache License Version 2.0](http://www.apache.org/licenses/LICENSE-2.0)
<br>

## Questions or Suggestions
**Email** `project.spinoza@gmail.com`<br>
**Issues** https://github.com/project-spinoza/gsak-kit/issues
