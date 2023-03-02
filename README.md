# edge-iot-ops
Edge IoT ops is set of instructions to create clusters for edge compurting.

## eKupier IoT

Creates k3s deployment in two docker containers: master plane and agent plane.
Then creates single eKupier pod in the agent plane.

- Start:

```sh
make deployment-up
```

- Stop: 


```sh
make deployment-down
```
