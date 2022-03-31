# CTF-Name-Chal-Repo

Flag format: `sigpwny{...}`


# Adding challenges
- create a new challenge:
  - IF CONTAINER: 
    - cd into `/challenges/<category>`
    - `kctf chal create --template <templatename> <chalname> --challenge-dir ./<chalname>`
    - available templates: pwn, web, xss-bot
    - NOTE -- the kCTF config is called `challenge.yaml` and the CTFd config is called `challenge.yml`. confusing? yes.
  - OTHERWISE
    - `mkdir /challenges/<category>/<chalname>`



- **Your challenge folder MUST** have a `challenge.yml` file for CTFd, following the specification here: https://github.com/CTFd/ctfcli/blob/master/ctfcli/spec/challenge-example.yml
- your challenge must have a `SOLUTION.md` writeup (it's ok if its simple/concise or a tl;dr version)
- your challenge must have a healthcheck script if it is deployable. attempt to make it solve the challenge.


# Local testing notes for containerized challenges

### Initial setup:
- kctf https://google.github.io/kctf/local-testing.html
- set umask
- install deps (cli tools, docker)
- enable user namespaces
- `export DOCKER_SCAN_SUGGEST=false` -- disable annoying Snyk messages from newer Docker versions which break kCTF parsing



### Each time you have a new shell:
- go to root of this repo
- `source kctf/activate`


### Testing locally:
- switch to and start local cluster:
  - `kctf cluster load local-cluster`
  - `kctf cluster start`
- start challenge, port-forward to access it:
  - `kctf chal start`
  - `kctf chal debug port-forward`
- when done testing:
  - `kctf cluster stop` to shutdown local k8s cluster
    - DO NOT run this command on remote-cluster or you will delete our cluster
  - `deactivate` to exit ctfcli


### Testing deployed challenge:
- Push to repo, and run the kCTF GitHub action
- switch to remote cluster:
  - `kctf cluster load remote-cluster`
- port-forward to access it:
  - `kctf chal debug port-forward`
- when done testing:
  - `deactivate` to exit ctfcli
