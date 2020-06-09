# Monitoring the environment using Jaeger
## Install Jaeger
From microservices-demo/deploy/kubernetes run Jaeger using the following command:<br/>
<code>kubectl apply -f ./manifests-jaeger</code><br/>
## Jaeger UI
To use the Jaeger UI find the url:<br/>
<code>kubectl get pods --all-namespaces --output=wide|grep jaeger</code><br/>
It's running on port 16686. For example:<br/>
http://10.32.0.6:16686/


