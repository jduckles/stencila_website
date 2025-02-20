# Publish to Ghost

Each page will need a `.yaml` file to point to a `soruce:` Markdown at a curlable location. Most of these are in the `stencila/stencila` repository. 

They can optionally have other yaml metadata supported by `stencila publish ghost`.

How to: 

```
cp .env.example .env # Add pertinent information to the .env file
make smd # merges yaml into smds
make publish # pushes to Ghost
```
