# git-tutorial
Git Tutorial

Author: rossano at gmail dot com

Timestamp: Tue 07 Apr 2020 09:25:19 AM -03


A very simple git tutorial with two team members:

      - rossanx (owner)
      - sputinik (collaborator)

**STEP 0 - Configure local repository "credentials" (no local password storage/cache version)**

* rossanx - (CLI)
  * `git config --global user.email "rossano@gmail.com"`
  * `git config --global user.name "Rossano Pablo Pinto"`

* sputinik - (CLI)
  * `git config --global user.email "sputinix@gmail.com"`
  * `git config --global user.name "Paul Harris Sputinik"`


**STEP 1 - Create github repository and add collaborators**

* rossanx - (WEB) Create REPO at github.com (git-tutorial)
  * Invite sputinik to collaborate

* sputinik - (WEB) Accept invitation (access it's github account ...)

**STEP 2 - Clone github repository (make a local copy)**

* rossanx - (CLI) `git clone https://github.com/rossanx/git-tutorial.git`
  * provide credentials (rossanx and password)
  * `cd git-tutorial`

* sputinik - (CLI) `git clone https://github.com/rossanx/git-tutorial.git`
  * provide credentials (sputinik and password)
  * `cd git-tutorial`
  
**STEP 3 - Owner makes local changes and updates github**

* rossanx - (CLI)
  * COPY OPENCONFIG MODELS TO LOCAL REPOSITORY
    (For instance: `cp -av public/release/ ../../git-tutorial/`)
  * `git add release`
  * `git commit -m "Initial commit"`
  * `git push -u origin master`
    * provide credentials (rossanx and password)


**STEP 4 - Collaborator checks if there is an update**

* sputinik - (CLI)

  * `git pull`
    * provide credentials (sputinik and password)
  * `git log`
    * Collaborator can see commit history
    
**STEP 5 - Owner makes local changes and updates github**

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

**STEP 6 - Collaborator checks if there is an update**

* sputinik - (CLI)
  * `git pull`
    * provide credentials (sputinik and password)
  * `git log`
    * Collaborator can see commit history

**STEP 7 - Collaborator makes a contribution**

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

**STEP 8 - Owner wants to check if Collaborator made some changes**
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

**STEP 9 - Owner wants to incorporate changes made by Collaborator**
  * rossanx - (CLI)
    * `git merge`
      *  This command shows:
```
Updating 5e8ea4d..f674857
Fast-forward
 release/models/telemetry/openconfig-telemetry-types.yang | 2 +-
 1 file changed, 1 insertion(+), 1 deletion(-)
```

  * rossanx - (CLI) `cat release/models/telemetry/openconfig-telemetry-types.yang`

**STEP 10 - Owner oberved that revision information is missing in the edited YANG file, and inserts it**
  * Changed and inserted the following info at the beginning of the file release/models/telemetry/openconfig-telemetry-types.yang :

```
  oc-ext:openconfig-version "0.5.0";

  revision "2020-03-23" {
    description
      "Add MQTT telemetry streaming support.";
    reference "0.5.0";
  }
```
  * `git status`
    * This command shows file openconfig-telemetry-types.yang has changed
  * `git add release/models/telemetry/openconfig-telemetry-types.yang`
  * `git commit -m "Updated openconfig-telemetry-types.yang version number and revision information."`
  * `git push`

**STEP 11 - Collaborator wants to incorporate new changes in his local copy**
  * Now you know how to complete this step, complete it!

**STEP 12 - Adding more collaborators to github project**
  * Settings -> Manage access -> Invite a collaborator
  * Now each invited collaborator must accept the inviation to join the repository's list of collaborators

Congrats! :+1:

TODO: Using tags in git (local and remote).


===============================================================================

**ALTERNATIVE (COMBINED) STEPS 8 AND 9**

Sometimes you just want to pull changes and accept them as they are (as in STEP 4). So, if it's the case, just `git pull` it:

  * rossanx - (CLI) `git pull`
    * provide credentials (sputinik and password)

==============================================================================
**PARTICIPANT LOG**
==============================================================================

Darli Mello 27/03/2020 12:09

===============================================================================

Kayol Mayer 27/03/2020 12:16

