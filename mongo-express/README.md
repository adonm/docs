<!--

********************************************************************************

WARNING:

    DO NOT EDIT "mongo-express/README.md"

    IT IS AUTO-GENERATED

    (from the other files in "mongo-express/" combined with a set of templates)

********************************************************************************

-->

# Quick reference

-	**Maintained by**:  
	[mongo-express](https://github.com/mongo-express/mongo-express-docker)

-	**Where to get help**:  
	[the Docker Community Slack](https://dockr.ly/comm-slack), [Server Fault](https://serverfault.com/help/on-topic), [Unix & Linux](https://unix.stackexchange.com/help/on-topic), or [Stack Overflow](https://stackoverflow.com/help/on-topic)

# Supported tags and respective `Dockerfile` links

**No supported tags**

# Quick reference (cont.)

-	**Where to file issues**:  
	[https://github.com/mongo-express/mongo-express-docker/issues](https://github.com/mongo-express/mongo-express-docker/issues?q=)

-	**Supported architectures**: ([more info](https://github.com/docker-library/official-images#architectures-other-than-amd64))  
	**No supported architectures**

-	**Published image artifact details**:  
	[repo-info repo's `repos/mongo-express/` directory](https://github.com/docker-library/repo-info/blob/master/repos/mongo-express) ([history](https://github.com/docker-library/repo-info/commits/master/repos/mongo-express))  
	(image metadata, transfer size, etc)

-	**Image updates**:  
	[official-images repo's `library/mongo-express` label](https://github.com/docker-library/official-images/issues?q=label%3Alibrary%2Fmongo-express)  
	[official-images repo's `library/mongo-express` file](https://github.com/docker-library/official-images/blob/master/library/mongo-express) ([history](https://github.com/docker-library/official-images/commits/master/library/mongo-express))

-	**Source of this description**:  
	[docs repo's `mongo-express/` directory](https://github.com/docker-library/docs/tree/master/mongo-express) ([history](https://github.com/docker-library/docs/commits/master/mongo-express))

# What is mongo-express?

mongo-express is a web-based MongoDB admin interface written in Node.js, Express.js, and Bootstrap3.

> [github.com/mongo-express/mongo-express](https://github.com/mongo-express/mongo-express)

![logo](https://raw.githubusercontent.com/docker-library/docs/b9077663f53d2a5f3ce3ce52c9249d4b0c684fd9/mongo-express/logo.png)

# How to use this image

```console
$ docker run --network some-network -e ME_CONFIG_MONGODB_SERVER=some-mongo -p 8081:8081 mongo-express
```

Then you can hit `http://localhost:8081` or `http://host-ip:8081` in your browser.

## Security Notice

JSON documents are parsed through a javascript virtual machine, so the web interface can be used for executing malicious javascript on a server.

**mongo-express should only be used privately for development purposes.**

# Configuration

Environment vairables are passed to the `run` command for configuring a mongo-express container.

	Name                            | Default         | Description
	--------------------------------|-----------------|------------
	ME_CONFIG_BASICAUTH_USERNAME    | ''              | mongo-express web username
	ME_CONFIG_BASICAUTH_PASSWORD    | ''              | mongo-express web password
	ME_CONFIG_MONGODB_ENABLE_ADMIN  | 'true'          | Enable admin access to all databases. Send strings: `"true"` or `"false"`
	ME_CONFIG_MONGODB_ADMINUSERNAME | ''              | MongoDB admin username
	ME_CONFIG_MONGODB_ADMINPASSWORD | ''              | MongoDB admin password
	ME_CONFIG_MONGODB_PORT          | 27017           | MongoDB port
	ME_CONFIG_MONGODB_SERVER        | 'mongo'         | MongoDB container name. Use comma delimited list of host names for replica sets.
	ME_CONFIG_OPTIONS_EDITORTHEME   | 'default'       | mongo-express editor color theme, [more here](http://codemirror.net/demo/theme.html)
	ME_CONFIG_REQUEST_SIZE          | '100kb'         | Maximum payload size. CRUD operations above this size will fail in [body-parser](https://www.npmjs.com/package/body-parser).
	ME_CONFIG_SITE_BASEURL          | '/'             | Set the baseUrl to ease mounting at a subdirectory. Remember to include a leading and trailing slash.
	ME_CONFIG_SITE_COOKIESECRET     | 'cookiesecret'  | String used by [cookie-parser middleware](https://www.npmjs.com/package/cookie-parser) to sign cookies.
	ME_CONFIG_SITE_SESSIONSECRET    | 'sessionsecret' | String used to sign the session ID cookie by [express-session middleware](https://www.npmjs.com/package/express-session).
	ME_CONFIG_SITE_SSL_ENABLED      | 'false'         | Enable SSL.
	ME_CONFIG_SITE_SSL_CRT_PATH     | ''              | SSL certificate file.
	ME_CONFIG_SITE_SSL_KEY_PATH     | ''              | SSL key file.

The following are only needed if `ME_CONFIG_MONGODB_ENABLE_ADMIN` is **"false"**

	Name                            | Default         | Description
	--------------------------------|-----------------|------------
	ME_CONFIG_MONGODB_AUTH_DATABASE | 'db'            | Database name
	ME_CONFIG_MONGODB_AUTH_USERNAME | 'admin'         | Database username
	ME_CONFIG_MONGODB_AUTH_PASSWORD | 'pass'          | Database password

## Example

```console
$ docker run -it --rm \
    --network web_default \
    --name mongo-express \
    -p 8081:8081 \
    -e ME_CONFIG_OPTIONS_EDITORTHEME="ambiance" \
    -e ME_CONFIG_MONGODB_SERVER="web_db_1" \
    -e ME_CONFIG_BASICAUTH_USERNAME="user" \
    -e ME_CONFIG_BASICAUTH_PASSWORD="fairly long password" \
    mongo-express
```

This example links to a container name typical of `docker compose`, changes the editor's color theme, and enables basic authentication.

# License

View [license information](https://github.com/mongo-express/mongo-express#license) for the software contained in this image.

As with all Docker images, these likely also contain other software which may be under other licenses (such as Bash, etc from the base distribution, along with any direct or indirect dependencies of the primary software being contained).

Some additional license information which was able to be auto-detected might be found in [the `repo-info` repository's `mongo-express/` directory](https://github.com/docker-library/repo-info/tree/master/repos/mongo-express).

As for any pre-built image usage, it is the image user's responsibility to ensure that any use of this image complies with any relevant licenses for all software contained within.
