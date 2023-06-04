# Description

There are two modules :
i) Simulated Temperature module : It generates the temperature and humidity using random function generator.
ii) Filter module : Filters Temperature if its greater than 25 degree Celcius.

The Raspberry pi which I am using is ARM 32-bit ELF.The way to find out is running the following command :
```bash
python3 -c "import platform; print(platform.architecture())"
```

To use this code :
```bash
docker login -u firstprojectregistry -p +KKv1O5G5CdiNM63k1N1bTRNSQuqRuFJDVUlQUWFGQ+ACRDx/FR6 firstprojectregistry.azurecr.io
docker build --rm -f "./modules/filtermodule/Dockerfile.arm32v7.debug" -t firstprojectregistry.azurecr.io/filtermodule:0.0.1-arm32v7 "./modules/filtermodule"
docker push firstprojectregistry.azurecr.io/filtermodule:0.0.1-arm64v8
az iot edge set-modules --hub-name MyFirstHub101 --device-id raspberry-pi --content ./deployment.template.json --login "HostName=MyFirstHub101.azure-devices.net;SharedAccessKeyName=iothubowner;SharedAccessKey=kv4ZVBUuun+khCxh4fgow7BsH12g6fmuqZkXP3cFo2o="
```

To monitor the changes :
```bash
az iot hub monitor-events --hub-name MyFirstHub101
```
