# SignalBuddy

A scalable signaling server for WebRTC using socket.io, NodeJS cluster, and Redis. Made for use with [liowebrtc](https://github.com/lazorfuzz/liowebrtc) and [react-liowebrtc](https://github.com/lazorfuzz/react-liowebrtc).

## What is SignalBuddy?

SignalBuddy is an easy-to-scale signaling solution for WebRTC. SignalBuddy automatically detects and scales across the number of CPU cores in its environment. For instance, if the machine you're testing on has four cores, SignalBuddy will launch a cluster of four processes, each a separate instance of itself, all listening on the same port. Using Redis to store state, peers connected to different worker instances will still be able to broadcast and transmit data to one another.

## Running

First, install and start Redis. Once Redis is listening on the default port (6379), `cd` into the signalbuddy project.

After cd'ing into the signalbuddy project:

```
npm install
```

Build the project:

```
npm build
```

Start in dev mode:
```
npm start
```

If all goes well, your console should display a message like this:

```
Listening at http://localhost:8888/
```

If you open the URL in a web browser, you should see an output displaying which worker process you're currently connected to. Exempli gratia:

```
worker: 4
```

## Production

To run in production mode:

```
NODE_ENV=production node dist/server.js
```

Most likely, you'll want the server to be secure. You can either pass in the paths to your key/cert through the environment variables PRIV_KEY and CERT:

```
NODE_ENV=production PRIV_KEY=/etc/example/privKey.pem CERT=/etc/example/cert.pem node dist/server.js
```

Or you can also add your key/cert paths to the production.json file in the config folder.

---

This project is still in development. In the near future I will add a Dockerfile, as well as additional deployment methods and helpers that will make it easier to deploy on AWS, Digital Ocean, etc.