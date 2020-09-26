# network-uptime

## Intro

The point of this program is to detect when network is down and to track it in log. 

Nice to haves

- Helpful to have graphs that show time of failure. 
- Ability to save graphs to file
- Ability to export logs of interest for when things went down. 
- Additional ping capabilities  to test point of failure
- (i.e. Can I ping the computer in the same network? Can I ping google.com? etc. )

Status Screen

- big status screen that shows current status
- graph of failures over the last 48 hours
- tabs that go to different views

Configurations



How to test

- could ping known servers, etc. 

Where to store logs? 

- Try IndexedDB (built into the web technology) 

How to plot charts of failure over time? 

- https://www.chartjs.org/



# Setup Details

## To run: 
vue create . 
vue add electron-builder
npm run electron:serve
npm i @types/electron-devtools-installer

## Project setup
```
npm install
```

### Compiles and hot-reloads for development
```
npm run serve
```

### Compiles and minifies for production
```
npm run build
```

### Lints and fixes files
```
npm run lint
```

### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).

# Setup Info
Created project using `npm create network-uptime`

Using instructions here: 
https://nklayman.github.io/vue-cli-plugin-electron-builder/guide/#installation


