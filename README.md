# Welcome to Boomea Dev Setup through docker!

# Requirements

1. Install docker software for your OS.<br/>
   Windows & Mac: https://www.docker.com/products/docker-desktop <br/>
   Ubuntu: https://docs.docker.com/install/linux/docker-ce/ubuntu/

   Docker already include docker compose but you may need to add it manually(you can verify by docker-compose --version command on your    CLI, if this print docker compose version, then you don't need to follow docker compose install step):
   https://docs.docker.com/compose/install/

   Make sure docker and docker-compose is running by opening command prompt and type:
   ```sh
    $ docker --version
    $ docker-compose --version
    ```

2. Install git from https://git-scm.com/downloads, it comes with git bash. For rest of document new terminal/command will refer to git      bash prompt or command to be run in git bash terminal.




# Directory Structure

```bash
    boomea-docker                       # root directory
    ├── boomea-common                   # boomea-common repo clone
    ├── ucserver                        # ucserver repo clone
    ├──── MariaDb                       # MariaDb directory should come along with ucserver repo
    ├────── dump.sql                    # Place sql dump file and rename to dump.sql
    ├── mattermost-redux                # mattermost-redux repo clone
    ├── mattermost-webapp               # mattermost-webapp repo clone
    └──── id_rsa                        # id_rsa ssh key,without passphrase and added to account settings-> access keys
```
1. Create a root directory(any name) at your desired location. 
2. Get git clone for below repositories in root directory.
   -	git clone https://{bitbucketusername}@bitbucket.org/wlcommm/boomea_common.git boomea-common
   -	git clone https://{bitbucketusername}@bitbucket.org/wlcommm/ucserver.git ucserver
   -	git clone https://{bitbucketusername}@bitbucket.org/wlcommm/boomea_webapp.git mattermost-webapp
   -	git clone https://{bitbucketusername}@bitbucket.org/wlcommm/boomea_redux.git mattermost-redux
3. Place database dump sql file(provided by boomea team) inside {root directory}/ucserver/MariaDb Directory path.
   Note: Rename sql dump file to dump.sql.
4. Create ssh key by name of "id_rsa", should be without passphrase, place under {root-directory}/mattermost-webapp dircetory path. Add same key to your bitbucket settings: access keys.
5. Final Directory structure should look like above chart image.




# Time to run setup script:

## First time install
1. Open the terminal and navigate to {root directory}/ucserver
2. Run the following command, this will create docker images and containers:
    ```sh
    $ boomea-setup.sh install
    ```
    once its done you can close this terminal
# Build

## Build Redux
1. Open a new terminal and navigate to {root directory}/ucserver
2. Run the following command to enter into redux container:
   For windows OS:
   ```sh
   $ boomea-setup.sh servewin --redux
   ```
   or for other OS :
   ```sh
   $ boomea-setup.sh serve --redux
   ```
3. Run the redux watch command in redux container bash : 
   For web
   ```sh
   $ npm run docker-dev:watch
   ```
   For mobile
   ```sh
   $ npm run docker-mobile:watch
   ```
 4. keep this terminal open.

## Build React
1. Open a new terminal and navigate to {root directory}/ucserver
2. Run the following command to enter into react container:
    For windows OS:
    ```sh
    $ boomea-setup.sh servewin --react
    ```
    For other OS : 
    ```sh
    $ boomea-setup.sh serve --react
    ``` 
3. Run the react watch command in react container bash: 
    ```sh
    $ npm run run
    ```
4. keep this terminal open.

## Run Ucserver
1. Open a new terminal and navigate to {root directory}/ucserver
2. Run the following command to enter into ucserver:
    For windows OS:
    ```sh
    $ boomea-setup.sh servewin --ucserver
    ``` 
    or for other OS : 
    ```sh
    $ boomea-setup.sh serve --ucserver
    ```
3. Run the ucserver make command in ucserver container bash: 
   ```sh
    $ make run-server
    ```
4. keep this terminal open.

## To access MariaDb
1. Open a new terminal and navigate to {root directory}/ucserver
2. Enter into MariaDb container through below command :
    For windows OS: 
    ```sh
    $ boomea-setup.sh servewin --mariadb
    ```
   or for other OS : 
   ```sh
    $ boomea-setup.sh serve --mariadb
    ```
 3. You can close this terminal

## Volumes
1. There is one named volume used:
    my-datavolume  (to store mariadb data)
    This volume can be inspected through docker command to get mariadb database changes done after entering into mariadb container.

2. Redux and React compiled temp data is stored in {root directory}/temp directory (created automatically on running build process)

## Stop Process
To stop containers open new terminal, navigate to {root directory}/ucserver and use following command:<br/>
  ```sh
  $ boomea-setup.sh stop
  ```
## Flush Everything
To Flush everything open new terminal, navigate to {root directory}/ucserver and run following command:<br/>
  ```sh
  $ boomea-setup.sh flush
  ```
## Restart
To restart 
- Open new terminal and navigate to {root directory}/ucserver
- Stop container using following command:
    ```sh
    $ boomea-setup.sh stop
    ```
 - Run containers using following command:
    ```sh
    $ boomea-setup.sh run
    ```
 - You can now follow build process for redux, react, ucserver as desribed above

## Individual Builds
1.  To start only redux build:
    -   open new terminal and navigate to {root directory}/mattermost-redux
    -   Run container through:
        ```sh
        $ boomea-redux.sh run
        ```
    -   Enter into redux container:
        For windows OS
        ```sh
        $ boomea-redux.sh servewin
        ```
	For other OS 
        ```sh
        $ boomea-redux.sh serve
        ```
    -   Run the redux watch command: 
        For web:
        ```sh
        $ npm run docker-dev:watch
        ```
        For mobile :
        ```sh
        $ npm run docker-mobile:watch
        ```
    -   keep terminal open
    
2. To start only react build:
    -   Start Redux Individual build as described in step 1
    -   open new terminal and navigate to {root directory}/mattermost-webapp
    -   Run container through:
        ```sh
        $ boomea-react.sh run
        ```
    -   Enter into react container: 
        For windows OS 
        ```sh
        $ boomea-react.sh servewin
        ```
	    or for other OS 
	    ```sh
        $ boomea-react.sh serve
        ```
    -   Run the react watch command in react container bash: 
        ```sh
        $ npm run run
        ``` 
    -   keep terminal open


For help navigate to {root directory}/ucserver and use following command:
```sh
$ boomea-setup.sh --help
```
