# Git/Bitbucket Course

This repo contains a reveal.js presentation about Git and Bitbucket
To visualize this presentation, go here: [https://devops-cloud-courses.github.io/git](https://devops-cloud-courses.github.io/git)
You can also clone this repo and expose static pages through your favorite web server.

> This course was originally created for training session. You can use it freely.

## See this course locally with docker
```bash
docker build -t git-course .
docker run -d --rm -p 80:8080 --name=git-course git-course
```
* After a few seconds, you can see the slides on [http://localhost](http://localhost)
* When you want to stop the instance, run:
```bash
docker stop git-course
```


## Print this course to pdf (only in chrome and chromium)
* Click on [this link](https://devops-cloud-courses.github.io/git/?print-pdf&pdfSeparateFragments=false)
* Then `CTRL+P` on the generated page
* Change the following settings

Setting | Value
--- | --- 
Destination | Save as PDF
Pages | All
Pages per sheet | 1
Margins | Default
Options | Background graphics

* Click on save
