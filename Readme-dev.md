# Developer Readme
## Workshop Students

Students: simply go to the [Workshop Website] and enjoy your learning

## Workshop Developers
We assume you have docker and docker-compose installed.

If not, go install them now. 

## Install Necessary Software 

```
git clone https://github.com/tobyhferguson/aws-modernization-workshop-base.git &&
cd aws-modernization-workshop-base &&
git submodule init &&
git submodule update &&
git submodule update --remote themes/hugo-theme-learn
```

## Run the Hugo Server
`docker-compose up dev`

This will build the server and then run it, mounting the local directory. Any changes you make should be picked up and served to you as per the normal use of hugo.

## Connect to the server
Visit the server at http://localhost:1313


## Make Changes
Now feel free to make changes to the files in `./content/` - the server will pick them up automagically.

Hit 'Ctl+C' to terminate the server 

When you're finished you can deploy to S3 to let others see.

## Deploy to S3
First you must publish the site to the `./public/` directory:

```
docker-compose run publish
```

Once that has completed successfully deploy to the s3 bucket `s3://aws-workshop.redislabs.com` with ONE of the following two methods:

Inline envars:
```
docker-compose run -e AWS_REGION=XXXX -e AWS_ACCESS_KEY_ID="XXXX" -e AWS_SECRET_ACCESS_KEY="XXXXXX ... XXXX" production
```

Envars:
```
export AWS_REGION=XXXX
export AWS_ACCESS_KEY_ID=XXXX
export AWS_SECRET_ACCESS_KEY=XXXX

docker-compose run production
```


The result will be available at the [Workshop Website].

(The actual url is in the file `config.toml` as the value of the `deployment.targets` section's `URL` key.)

Pull request requested! If you can get the deploy action to work with the regular profile rather than having to export each envar then please make a pull request. Mounting `~/.aws` onto `/root/.aws` as per [the AWS Docker Instructions](https://docs.aws.amazon.com/cli/latest/userguide/install-cliv2-docker.html) and then using the default profile didn't work, unfortunately.


----------
[Workshop Website]: https://s3.amazonaws.com/aws-workshop.redislabs.com/index.html
