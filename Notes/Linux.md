---
created-date: 2024-07-07
---




## Utils

### Extract PDF with qpdf

Extract pages 1 to 10 from `input.pdf` and save it as `output.pdf`

```
qpdf input.pdf --pages . 1-10 -- output.pdf
```

Extract only page 12

```
qpdf input.pdf --pages . 12 -- la_maior.pdf
```


24
27
63
64
65

---

Install golang-migrate on ubuntu

1. Check latest release version on https://github.com/golang-migrate/migrate/releases/
2. Download the pre-built binary (update the 4.14.1 with the latest version)
	1. curl -L https://github.com/golang-migrate/migrate/releases/download/v4.14.1/migrate.linux-amd64.tar.gz | tar xvz
3. Move to the correct location
	1. sudo mv migrate $GOPATH/bin/migrate