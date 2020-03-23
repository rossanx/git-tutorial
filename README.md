# git-tutorial
Git Tutorial
author: rossano at gmail dot com
timestamp: Mon 23 Mar 2020 02:40:53 PM -03


A very simple git tutorial with two team members:

      - rossanx (owner)
      - sputinik (collaborator)

**STEP 0 - Configure local repository "credentials" (no local password storage/cache version)

* rossanx - (CLI)
  * `git config --global user.email "rossanx@gmail.com"`
  * `git config --global user.name "Rossano Pablo Pinto"`

* sputinik - (CLI)
  * `git config --global user.email "sputinix@gmail.com"`
  * `git config --global user.name "Paul Harris Sputinik"`


**STEP 1 - Create github repository and add collaborators

* rossanx - (WEB) Create REPO at github.com (git-tutorial)
  * Invite sputinik to collaborate

* sputinik - (WEB) Accept invitation (access it's github account ...)

**STEP 2 - Clone github repository (make a local copy)

* rossanx - (CLI) `git clone https://github.com/rossanx/git-tutorial.git`
  * provide credentials (rossanx and password)
  * `cd git-tutorial`

* sputinik - (CLI) `git clone https://github.com/rossanx/git-tutorial.git`
  * provide credentials (sputinik and password)
  * `cd git-tutorial`
  
**STEP 3 - Owner makes local changes and updates github

* rossanx - (CLI)
  * COPY OPENCONFIG MODELS TO LOCAL REPOSITORY
    (For instance: `cp -av public/release/ ../../git-tutorial/`)
  * `git add release`
  * `git commit -m "Initial commit"`
  * `git push -u origin master`
    * provide credentials (rossanx and password)


**STEP 4 - Collaborator checks is there is an update

* sputinik - (CLI)

  * `git pull`
    * provide credentials (sputinik and password)
  * `git log`
    * Collaborator can see commit history
    
**STEP 5 - Owner makes local changes and updates github

* rossanx - (CLI)
  * Modify file release/models/telemetry/openconfig-telemetry-types.yang
    * Add the following at the end of file:

```
      identity STREAM_MQTT_RPC {
        base "STREAM PROTOCOL";
          description
            "Telemetry stream is carried by the MQTT protocol";
      }
```

  * `git status`
    * Owner sees what has changed in his local directory
  * `git add release/models/telemetry/openconfig-telemetry-types.yang`
  * `git commit -m "Added MQTT telemetry support"`
  * `git push`
    * provide credentials (rossanx and password)

**STEP 6 - Collaborator checks is there is an update

* sputinik - (CLI)
  * `git pull`
    * provide credentials (sputinik and password)
  * `git log`
    * Collaborator can see commit history

**STEP 7 - Collaborator make a contribution

* sputinik - (CLI)
  * Modify file release/models/telemetry/openconfig-telemetry-types.yang
    * Change identity STREAM_MQTT_RPC from:

```
      identity STREAM_MQTT_RPC {
        base "STREAM PROTOCOL";
          description
            "Telemetry stream is carried by the MQTT protocol";
      }
```

   to:

```
      identity STREAM_MQTT_RPC {
        base "STREAM PROTOCOL";
          description
            "Telemetry stream is carried by the MQTT protocol (needs a broker)";
      }
```

  * `git status`
    * Collaborator sees what has changed in his local directory
  * `git add release/models/telemetry/openconfig-telemetry-types.yang`
  * `git commit -m "Complemented MQTT telemetry description"`
  * `git push`
    * provide credentials (sputinik and password)

**STEP 8 - Owner wants to check if Collaborator made some changes
  * rossanx - (CLI)
    * `git fetch --all`
      * This command fetches all changes from github, but does not merge them
    * `git diff origin`
      * This command shows:
```diff
        diff --git a/release/models/telemetry/openconfig-telemetry-types.yang b/release/models/telemetry/openconfig-telemetry-types.yang
        index f0bd81e..8681940 100644
        --- a/release/models/telemetry/openconfig-telemetry-types.yang
        +++ b/release/models/telemetry/openconfig-telemetry-types.yang
        @@ -119,7 +119,7 @@ module openconfig-telemetry-types {
           identity STREAM_MQTT_RPC {
             base "STREAM PROTOCOL";
               description
        -        "Telemetry stream is carried by the MQTT protocol (needs a broker)";
        +        "Telemetry stream is carried by the MQTT protocol";
           }
 
           // typedef statements
```

**STEP 9 - Owner wnats to incorporate changes made by Collaborator
  * rossanx - (CLI)
    * `git merge`
      *  This command will show:
```
Updating 5e8ea4d..f674857
Fast-forward
 release/models/telemetry/openconfig-telemetry-types.yang | 2 +-
 1 file changed, 1 insertion(+), 1 deletion(-)
```

  * rossanx - (CLI) `cat release/models/telemetry/openconfig-telemetry-types.yang`

===============================================================================

**ALTERNATIVE (COMBINED) STEPS 8 AND 9

Sometimes you just want to pull changes and accept them as they are. So, if it's
the case, just `git pull` it:

  * rossanx - (CLI) `git pull`
    * provide credentials (sputinik and password)
