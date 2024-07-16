# Storyteller multilanguage images
This is a small repository to build multilanguage images for storyteller
## Supported languages
I have only tested this for german but I have added builds for all languages mentioned in the whisperx documentation (https://github.com/m-bain/whisperX?tab=readme-ov-file#other-languages).
## What is built
The workflow clones the current main branch for storyteller-base and storyteller and creates images for it.
## How to run
You can use the default storyteller compose file. Just make sure to edit the image name accordingly (the example is configured for german):
```yaml
services:
  web:
    image: loginator/storyteller:latest-de
    volumes:
      # This can be whatever you like; you can even use a
      # named volume rather than a bind mount, though it's easier
      # to inspect the files with a mount.
      # If you're running on macOS or Windows, you may want to
      # consider using a named volume, which will considerably
      # improve filesystem I/O performance. See these VS Code
      # docs for more information:
      # https://code.visualstudio.com/remote/advancedcontainers/improve-performance#_use-a-targeted-named-volume
      - ~/Documents/Storyteller:/data:rw
    environment:
      # Generate a cryptopgraphically secure random string,
      # e.g. with:
      #  openssl rand -base64 32
      - STORYTELLER_SECRET_KEY=/run/secrets/secret_key
    ports:
      - "8001:8001"
    secrets:
      - secret_key

secrets:
  secret_key:
    file: ./STORYTELLER_SECRET_KEY.txt
```
