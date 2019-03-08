## Salesforce Event Log File on Docker ELK

Using:

* [Connected App](https://help.salesforce.com/apex/HTViewHelpDoc?id=connected_app_create.htm).
    * Enable OAuth Settings
    * Callback URL `http://localhost/`
    * Selected OAuth Scopes `Full access (full)`
* [EventLogFile sObject](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_objects_eventlogfile.htm) 
* [ELK](https://www.elastic.co/) 
* [Docker](https://www.docker.com/)
* Salesforce Event Log File [Ruby Gem](https://rubygems.org/gems/logstash-input-sfdc_elf/) plug-in simplifies.


**Logstash Plugin Configuration**

The configuration is defined in the [`sfdc_elf.config`](sfdc_elf.config.exmple) file.

```
cp sfdc_elf.config.example sfdc_elf.config
```

Fill the fields:
1. username
2. password
3. client_id
4. client_secret
5. security_token
6. host:
    * Defaults to "login.salesforce.com"
    * Use "test.salesforce.com" for connecting to Sandbox instance.

**Build Docker**
```
docker build -t elk_selv .
```

**Run Docker**
```
docker run -it -p 8081:5601 elk_selv
```


**Exploring, Analyzing, and Visualizing Data**
1. Kibana is configured to run on port 8081: `localhost:8081`
2. Set index pattern in *Settings > Indices* to `logstash-*` and click *Create*. Some mapping conflicts may occur which is fine. See screenshot below.
3. Click *Discover* and start exploring and visualizing your data. 


**Reference**

*Users: WE KNOW THEM: The ELF at Salesforce*

* [Presentation](https://speakerdeck.com/elastic/users-we-know-them-the-elf-at-salesforce)
* [Video](https://www.elastic.co/elasticon/conf/2016/sf/users-we-know-them-the-elf-at-salesforce)


