# go tls folder
cd tls;
# create the name space redis 
kubectl create ns redis;
# Create the tls secret
kubectl create secret tls redis-crt --cert=redis.crt --key=redis.key  -n redis;
# cretae a CA secret 
kubectl create secret generic redis-ca --from-file=ca.crt  -n redis;
# go to resources folder 
cd ../resources ;
# crete the config Map to use tls for redis
kubectl apply -f redis-cm.yaml -n redis;
# create deployment with 1 replica
kubectl apply -f deploy-redis-k8s.yaml -n redis;
