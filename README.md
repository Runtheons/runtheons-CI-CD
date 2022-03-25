# Runtheons CI/CD

For implement Continuous Integration - Continuous Deployment we use Github Actions

# References

This project use:

- [Test](https://github.com/Runtheons/runtheons-CI-CD#test)
- [Build](https://github.com/Runtheons/runtheons-CI-CD#build)
- [Deploy](https://github.com/Runtheons/runtheons-CI-CD#deploy)

## Test

After install the dependencies, perform the unit test on a github machine

It run:

```
npm install
npm run test
```

### How to call in your workflow

```yml
.
.
jobs:
  test:
    uses: Runtheons/runtheons-CI-CD/.github/workflows/test.yml@v1.3
```

## Build

After install the dependencies, try to make a buil on a github machine

It run:

```
npm install
npm run build
```

### How to call in your workflow

```yml
.
.
jobs:
  build:
    uses: Runtheons/runtheons-CI-CD/.github/workflows/build.yml@v1.3
```

## Deploy

After connection with SSH to online host, enter in you repository folder, update the contente with a pull, re-install all the dependencies and make the build after restart the server

It run:

```
ssh -i ${{ secrets.SERVER_KEY }} ${{ secrets.SERVER_HOST }}
cd ${{ repository }}/
git pull
npm install
sudo pm2 restart all
```

### How to call in your workflow

```yml
.
.
jobs:
  deploy:
    uses: Runtheons/runtheons-CI-CD/.github/workflows/deploy.yml@v1.3
    with:
      repository: ${{ repository }}
    secrets:
      server_host: ${{ secrets.SERVER_HOST }}
      server_key: ${{ secrets.SERVER_KEY }}
```

NB: Remember to add SERVER_HOST and SERVER_KEY to your repository secrets
