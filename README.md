# ELK-Stack in windows

Installing ELK Stack (Elastic Search, Logstash, Kibana)

    A. Elastic Search
 
        Download Link: https://www.elastic.co/downloads/elasticsearch
        •	Download and unzip Elasticsearch.
        •	Run windows setup, complete the steps based on system configuration.
        •	After click on Install, it will take a while for complete installation.
        •	Restart is required after completion.
        •	Open this URL http://localhost:9200 in default browser of your system.
        •	If everything is good then it should show json output in browser
        •	For complete installation guide reference please follow below link
          https://www.elastic.co/guide/en/elasticsearch/reference/current/windows.html

    B. Logstash

        Download link: https://www.elastic.co/downloads/logstash
        •	Download and unzip Elasticsearch.
        •	Prepare a logstash.conf  file, which have below configuration
        input  {        
            jdbc  {            
                jdbc_connection_string  =>  "jdbc:mysql://<external ip of remote server>:3306/my_db"            
                jdbc_user  =>  "username"            
                jdbc_password  =>  "Pass_567"            
                jdbc_driver_library  =>  "C:\logstash-6.2.3\bin\mc\mysql-connector-java-5.1.46-bin.jar"            
                jdbc_driver_class  =>  "com.mysql.jdbc.Driver"            
                statement  =>  "SELECT * FROM report"        
            }    
        }    
        output  {        
            stdout  {            
                codec  =>  json_lines        
            }        
            elasticsearch  {            
                "hosts"  =>  "<internal ip of window server>:9200"            
                "index"  =>  "myIndex"        
            }    
        }    

        •	For complete information of conf file setup please check below link
        https://www.elastic.co/guide/en/logstash/current/configuration.html
        •	Run bin/logstash -f logstash.conf
        •	Logstash will pump data from mysql to elastic server.

    C. Kibana

        Download Link:
        https://www.elastic.co/downloads/kibana
        •	Download and unzip Kibana
        •	Open config/kibana.yml in an editor
        •	Set elasticsearch.url to point at your Elasticsearch instance
        •	Run bin/kibana (or bin\kibana.bat on Windows)
        •	Point your browser at http://localhost:5601
