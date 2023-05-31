# Docker

{% hint style="info" %}
The current [`official Docker image`](https://hub.docker.com/\_/monica/) hosted on DockerHub is based on the previous major version of Monica. We'll update it soon to the new version, codename Chandler.
{% endhint %}

We have a [docker image](https://github.com/monicahq/chandler/pkgs/container/monica-next) that you can use to run this project locally.

First you need setup [authentication to the Container registry](https://docs.github.com/en/packages/working-with-a-github-packages-registry/working-with-the-container-registry#authenticating-to-the-container-registry).

Then play with the image:

```sh
docker run -p 8080:80 ghcr.io/monicahq/monica-next:main
```

This runs the image locally on port 8080 and using sqlite. You can then access the application at http://localhost:8080.

#### Configuration

Note that you'll need to setup a mail mailer to be able to register a user. You can try to use the `log` mailer like this:

```sh
docker run -p 8080:80 -e MAIL_MAILER=log ghcr.io/monicahq/monica-next:main
```

For more complex scenario (database setup, queue, etc.) see https://github.com/monicahq/docker/tree/main/.examples

#### Build it yourself

You can also build your image locally using `yarn docker:build` and run it with `yarn docker:run`.
