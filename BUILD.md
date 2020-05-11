# build tools


```bash
dot -v -Tpng -o diagram.png diagram.gv

aspell check intro.asciidoc
aspell check -d ru intro-ru.asciidoc

asciidoctor-pdf --verbose index.asciidoc
```


### docker

_graphviz_

```Dockerfile
FROM alpine:latest

VOLUME ["/doc"]

RUN apk update && apk add --update graphviz
RUN rm -rf /var/cache/apk/*

WORKDIR /doc
```

```bash
sudo docker build -t dot .
sudo docker run --rm -v $PWD:/doc dot dot -v -Tsvg -o test.svg test.gv
```

_asciidoctor-pdf_
```Dockerfile
FROM alpine:latest

VOLUME ["/doc"]

RUN apk update
RUN apk add ruby
RUN gem install asciidoctor-pdf

RUN rm -rf /var/cache/apk/*

WORKDIR /doc
```

```bash
sudo docker build -t adoc-pdf .
docker run --rm -v $PWD:/doc adoc-pdf asciidoctor-pdf index.asciidoc
```



