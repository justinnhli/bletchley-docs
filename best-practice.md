### Naive Approach

```python
def main():
    urls = read_urls()
    for url in urls:
        html = download_url(url)
        datum = do_nlp(html)
        data.append(datum)
    results = analyze(data)
    save_results(results)
```

### Ideal Approach

```python
def download_main(start, end):
    urls = read_urls()
    urls = urls[start:end]
    for url in urls:
        html_filename = url_to_html_filename(url)
        if html_filename.exists():
            continue
        html = download_url(url)
        save_html(html, html_filename)

def nlp_main(start, end):
    urls = read_urls()
    urls = urls[start:end]
    for url in urls:
        datum_filename = url_to_datum_filename(url)
        if datum_filename.exists():
            continue
        html_filename = url_to_html_filename(url)
        html = read_html(html_filename)
        datum = do_nlp(html)
        save_datum(datum, datum_filename)

def analyze_main():
    data = []
    urls = read_urls()
    for url in urls:
        datum_filename = url_to_datum_filename(url)
        datum = read_datum(datum, datum_filename)
        data.append(datum)
    results = analyze(data)
    save_results(results)
```
