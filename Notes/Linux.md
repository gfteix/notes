
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
