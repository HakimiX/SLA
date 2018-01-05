# Service Level Agreement (SLA)

![Text](https://github.com/HakimiX/SLA/blob/master/Models/SLA%20-%20Model_update.jpg)

[SLA Template Reference](http://www.slatemplate.com/)

## Agreement Overview 

This Agreement represents a Service Level Agreement (SLA) between Group K and Group X for the provisioning of information exchange required to sustain and support the system. 

This Agreement remains valid until superseded by a revised agreement mutually endorsed by both groups. 

This Agreement outlines all services covered as they are mutually understood by both groups. This Agreement does not supersede current processes and procedures unless explicitly stated herein. 

## Purpose of Agreement 

This Agreement sets forth the terms and conditions for the application support service which Service Provider shall provide to Customer. 

The purpose of the Agreement is to ensure that the proper elements and mutual commitments are in place for the Service Provider to provide specific support services, at specifically-designated levels of support, and at an agreed-upon delivery time to the Customer. The Agreement provides:

* Clarity of service parameters, roles, responsibilities and limitations. 
* A clear, concise and measurable description of the specific service level provided to the Customer. 
* Alignment of Customer’s perceptions of the expected service provision and Service Provider’s actual service support and delivery provisions 

## Stakeholders 

The following Service Provider and Customer are the sole basis for this Agreement and represent the Stakeholders associated with this SLA:
* IT Service Providers: Group A
* IT Service Customers: Group K

## Service Agreement 

The following detailed service parameters are the responsibility of the Service Provider for the duration of this Agreement. 

__Uptime__ – applies to servers, cloud services (web hosting) or other parts of the system that are vital. Guaranteed at least 95% uptime for our cloud backup system. 

__CPU Usage__ - applies to amount of actively used CPU, as percentage of total available CPU. Amount of used CPU time (CPU used, CPU wait etc.). Alert if CPU is above 70% for 5 min. 

__Support Response Time__ – applies to how long it takes Group A to respond when we raise a request for support. Respond to critical problems within 24 hours. 

This Service Level Agreement is written in a spirit of partnership. The Service Supplier will always do everything possible to rectify every issue in a timely manner. 

## Grafana 

## Monitoring

Monitoring is crucial for DevOps (Development Operations). It makes it possible to see what is happening in your system at any given time. It gives you an overview of system resources currently used such as CPU, Memory, storage etc. The main purpose of monitoring is detecting problems, notifying possible issues and preventing them. 

Unfortunetly we were not able to setup monitoring for our system. We made use of Docker and were able to install Grafana and Prometheus. They were both exposed on their ports 3000 and 9090. 

![Text](https://github.com/HakimiX/part2/blob/master/Models/docker.jpg)

Then we configured the Prometheus.yml file to point at 165.227.136.184 which is our Hacker News application. We also configured the scrape target to be Prometheus at localhost:9090. 

![Text](https://github.com/HakimiX/part2/blob/master/Models/ymlfile.jpg)

We installed the latest node exporter from [Prometheus](https://prometheus.io/download/#node_exporter), and exposed it on port 9100. Everything looked correct and we could see that everything was running on their respective ports. 

![Text](https://github.com/HakimiX/part2/blob/master/Models/netstat.jpg)

However, when we navigated to Prometheus at `165.227.136.184:9090/targets` we encountered node exporter errors such as `GET http://165.227.136.184:9100/metrics: dial tcp` and `165.227.136.184:9100: i/o timeout`. The Prometheus endpoint worked as intended besides the node exporter errors. 

![Text](https://github.com/HakimiX/part2/blob/master/Models/prometheus.jpg)

Grafana also worked fine, and we were able to get basic HTTP metrics by connecting Grafana to Prometheus. Since we were not able to expose node exporter metrics, we could not configure Grafana to show metrics such as, uptime, storage, CPU, memory etc. 

![Text](https://github.com/HakimiX/part2/blob/master/Models/grafana.jpg)

We could not understand what the problem was, because we created new droplets on digital ocean to test Grafana/Prometheus and it worked fine. Node exporter metrics were exposed on port 9100 and we were able to show CPU, memory and storage metrics on Grafana. We applied the same steps to our Hacker News application, but it didn’t work because of the earlier mentioned node exporter errors. We tried everything possible to fix this, but we were not successful. Below is the metrics we needed: 

![Text](https://github.com/HakimiX/part2/blob/master/Models/curl.jpg)

We have been very frustrated by this problem and are disappointed that we could not set up monitoring. Monitoring has been crucial for the service-level agreement, maintenance and generally development operations. 

