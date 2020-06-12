## Load test
<code>git clone https://github.com/microservices-demo/load-test.git</code><br/>
### Install
<code>sudo apt-get install python-pip ##for python2</code> <br/>
<code>sudo apt-get install python3-pip ##for python3</code> <br/>
<code>sudo python3 -m pip install locust ## or <code>sudo pip install locustio</code> <br/>
  
### Run
<code>locust --host=http://192.168.122.208:30001 -f locustfile.py -u=1 --hatch-rate=5</code><br/>

Parameters:
[host] - The hostname (and port if applicable) where the application is exposed. (Required)<br/>
[number of clients] - The nuber of concurrent end users to simulate. (Optional: Default is 2)<br/>
[number of requests] - The total number of requests to run before terminating the tests. (Optional: Default is 10)<br/>
