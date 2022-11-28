# Example repository demonstrating issue with `output-dir`

To demonstrate the issue run:
```bash
quarto render sub1/sub1.qmd
```

The file `sub1/sub1.qmd` contains the yaml:
```yaml
---
title: sub topic 1
output-dir: ../docs
---
```

The expected result is the output in the `docs` directory but the output is created in the `sub1` directory. 

Running quarto yields the following terminal output
```
quarto render sub1/sub1.qmd 
pandoc 
  to: html
  output-file: sub1.html
  standalone: true
  section-divs: true
  html-math-method: mathjax
  wrap: none
  default-image-extension: png
  
metadata
  document-css: false
  link-citations: true
  date-format: long
  lang: en
  output-dir: ../docs
  title: sub topic 1
  
Output created: sub1.html

```

Adding the `output-dir` parameter to `sub1/_metadata.yml` does not change the result.

# Workaround

Using quarto >= v1.2 project profiles can be used to achieve a similar effect https://quarto.org/docs/projects/profiles.html

This will use the `_quarto-sub1.yml` project file:
```bash
quarto render --profile sub1
```

This will use the default `_quarto.yml` file:
```bash
quarto render
```