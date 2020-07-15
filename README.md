# PnP Nightwatch.js for your browser automation needs

w/ out-of-the-box Docker & Cron support, intended for automating repetitive mundane tasks. 

## Getting Started

### Writing Tests

Create a `tests` folder and write your Nightwatch.js automation scripts there. -- [Example & Guide](https://nightwatchjs.org/guide#writing-tests)

Also, `.env` support is available, just `require('dotenv').config();` before you use `process.env`. 

### Running locally

```bash
npm install
npm run test
```

### Running w/Docker using chenseanxy/browser-automation

If your scripts don't require other dependencies, you can simply mount the tests folder:

```bash
mkdir tests_output && mkdir screens
docker run --rm \ 
    -v <your-tests-folder>:/usr/src/app/tests \ 
    -v $PWD/tests_output:/usr/src/app/tests_output \ 
    -v $PWD/screens:/usr/src/app/screens \ 
    chenseanxy/browser-automation
```

### Running w/Docker using your own image

If additional dependencies are required, you'll need to build your own image.

```bash
mkdir tests_output && mkdir screens
docker build . -t browser-automation
docker run --rm \ 
    -v $PWD/tests_output:/usr/src/app/tests_output \ 
    -v $PWD/screens:/usr/src/app/screens \ 
    browser-automation
```

### Running w/ Docker Compose and Cron support

You could either write your own crontabs, or use the built-in-supported Ofelia cron scheduler:

Edit docker-compose.yml according to your needs, and `docker-compose up -d`
