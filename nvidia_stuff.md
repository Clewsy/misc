# nvidia tricks

## Sort out the correct drivers (example).
```shell
$ nvidia-detector 
nvidia-driver-495
$ sudo apt update && sudo apt install nvidia-driver-495 ##maybe reboot afterwards.
```

## Get fan speed/s
```shell
$ nvidia-settings --query fans
$ nvidia-settings --query "[fan:0]/GPUCurrentFanSpeedRPM" --terse
$ nvidia-settings --query "[fan:1]/GPUCurrentFanSpeedRPM" --terse
```

## Get GPU core temp
```shell
$ nvidia-settings -q thermalsensors
$ nvidia-settings --query "[gpu:0]/GPUCoreTemp" --terse
```

## General info (nvidia system management interface).
```shell
$ nvidia-smi
```

## Stress-test video (glmark2)
```shell
$ sudo apt update && sudo apt install glmark2
$ glmark2
```

