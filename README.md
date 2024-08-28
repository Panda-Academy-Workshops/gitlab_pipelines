Gitlab credentials:

User: root
Pass: pandapanda

Command for setting up the gitlab runner:

Inside vagrant directory:

`vagrant ssh`

Then when on the machine:
```
docker exec -it gitlab-runner gitlab-runner register \
  --non-interactive \
  --url "http://gitlab" \
  --registration-token "glrt-h5-sEsqeuBZ3BmXL_7uD" \
  --description "docker-runner" \
  --tag-list "docker,linux" \
  --executor "docker" \
  --docker-image alpine:latest \
  --docker-network-mode "shared_network"```
