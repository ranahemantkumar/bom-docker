# Welcome to Boomea Dev Setup through docker!

# Requirements

1. Install docker software for your OS.<br/>
   Windows & Mac: https://www.docker.com/products/docker-desktop <br/>
   Ubuntu: https://docs.docker.com/install/linux/docker-ce/ubuntu/

   Docker already include docker compose but you may need to add it manually(you can verify by docker-compose --version command on your    cli, if it lists version, then you don't need to follow docker compose install step):
   https://docs.docker.com/compose/install/

   Make sure docker and docker-compose is running by opening command prompt and type:
   ```sh
    $ docker --version
    $ docker-compose --version
    ```

2. Install git from https://git-scm.com/downloads, it comes with git bash. For rest of document new terminal/command will refer to git      bash prompt or command to be run in git bash terminal.




# Directory Structure

1. Create a folder(any name) at your desired location. 
2. For rest of document boomea-docker will refer to root directory created in step 1
3. Get git clone for below repositories in boomea-docker folder. Replace glownes with your bitbucket username
   git clone https://glownes@bitbucket.org/wlcommm/boomea_common.git boomea-common
   git clone https://glownes@bitbucket.org/wlcommm/ucserver.git ucserver
   git clone https://glownes@bitbucket.org/wlcommm/boomea_webapp.git mattermost-webapp
   git clone https://glownes@bitbucket.org/wlcommm/boomea_redux.git mattermost-redux
4. Place database sql file(provided by boomea team) inside boomea-docker/ucserver/MariaDb folder.Rename sql file to dump.sql.
5. Create ssh key (name id_rsa), should be without passphrase, place under mattermost-webapp folder. Add same key to your bitbucket settings: access keys.
6. Final Directory structure should look like:
```bash
    boomea-docker
    ├── boomea-common                   # boomea-common repo clone
    ├── ucserver                        # ucserver repo clone
    ├──── MariaDb                       # MariaDb folder should come along with ucserver repo
    ├────── dump.sql                    # Place sql dump file and rename to dump.sql
    ├── mattermost-redux                # mattermost-redux repo clone
    ├── mattermost-webapp               # mattermost-webapp repo clone
    └──── id_rsa                        # id_rsa ssh key,without passphrase and added to account settings-> access keys
```



# Time to run setup script:

1. Create the images and containers:
    ```sh
    $ boomea-setup.sh install
    ```

- Redux terminal
2. Open a new terminal and enter into redux container through below command:
   For windows OS:
   ```sh
   $ boomea-setup.sh servewin --redux
   ```
   or for other OS : 
   ```sh
   $ boomea-setup.sh serve --redux
   ```
3. Run the redux watch command : 
   For web
   ```sh
   $ npm run docker-dev:watch
   ```
   For mobile
   ```sh
   $ npm run docker-mobile:watch
   ```

- React terminal
4. Open a new terminal and enter into react container through below command:
    For windows OS:
    ```sh
    $ boomea-setup.sh servewin --react
    ```
    For other OS : 
    ```sh
    $ boomea-setup.sh serve --react
    ``` 
5. Run the react watch command : 
    ```sh
    $ npm run run
    ``` 

- Ucserver terminal
6. Open a new terminal and enter into ucserver container through below command:
    For windows OS:
    ```sh
    $ boomea-setup.sh servewin --ucserver
    ``` 
    or for other OS : 
    ```sh
    $ boomea-setup.sh serve --ucserver
    ```
7. Run the ucserver make command in ucserver container bash: 
   ```sh
    $ make run-server
    ```

- MariaDb terminal
8. Open a new terminal and enter into MariaDb container through below command:
    For windows OS: 
    ```sh
    $ boomea-setup.sh servewin --mariadb
    ```
   or for other OS : 
   ```sh
    $ boomea-setup.sh serve --mariadb
    ```


9. There are four volumes used in process to store temp data between containers:
    boomea-redux-web-volume (to store redux mattermost-webapp data)
    boomea-redux-mobile-volume (to store redux mattermost-mobile data)
    boomea-react-dist-data (to store react dist directory data)
    my-datavolume  (to store mariadb data)
    These volumes can be inspected through docker commands or data can be viewed by entering into each container as described in 2,4,6       steps.

10. Redux compiled temp data is also stored in boomea-docker/temp folder

11. To stop containers open new terminal and use 
    ```sh
    $ boomea-setup.sh stop
    ```

12. To Flush everything run 
    ```sh
    $ boomea-setup.sh flush
    ```

13. To restart everything stop container using step 11. and start again using step1.

14. To start only redux container:
    -   open new terminal:
	    ```sh
        $ cd boomea-docker/mattermost-redux
        ``` 
    -   Run container through:
        ```sh
        $ boomea-redux.sh run
        ```
    -   Enter into redux container:
        For windows OS
        ```sh
        $ boomea-redux.sh servewin
        ```
	    or for other OS 
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
16. To start only react container, 
    -   open new terminal,
	    ```sh
        $ cd boomea-docker/mattermost-webapp
        ``` 
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



For help use
```sh
$ boomea-setup.sh --help
```
