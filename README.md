How to do:

On your server:
0) `git clone github/arthare/predictionio`
1) github/arthare/predictionio/docker: `docker pull predictionpio/pio`
2) `github/arthare/predictionio/docker/compose.sh` <-- this will start your event server, but leave your CLI usable
3) export PATH=`pwd`/bin:$PATH
4) pio-docker app new MyTestApp
5) `github/arthare/predictionio`
6) `cd github/arthare/predictionio/docker/templates`
7) `git clone github/arthare/predictionio-template-text-classifier`
8) Modify `github/arthare/predictionio-template-text-classifier/engine.json` to point at your app's name (MyTestApp)
9) `pio-docker build`
9.help) If you get build errors (137 in particular), make sure you undeploy previous versions of the engine.  Killing all extant java processes is helpful.
10) Submit some training events by POSTing {"text": "your text", "label": "1"} (with the label being the category you want to label as) to your server's 7070 port
11) in `github/arthare/predictionio-template-text-classifier/`, `pio-docker train`
12) in `github/arthare/predictionio-template-text-classifier/`, `pio-docker deploy`
13) Submit classification requests by POSTing to your server's 8000 port at http://your-server.com:8000/queries.json with a body like {"text": "your test text"}


When you want to re-train, or if you've made changes:
On your server:
1) `pio-docker train`
2) `pio-docker deploy`