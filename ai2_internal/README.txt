This directory contains files required internally by the
Semantic Scholar product.

It can safely be ignored by external consumers of this repository.

# Example of making a call to FAST API for figure_table_predictor

```python
def process_table_figure(doc):
    url='http://localhost:8080/invocations'
    tokens = [api.SpanGroup.from_mmda(sg) for sg in doc.tokens]
    rows = [api.SpanGroup.from_mmda(sg) for sg in doc.rows]
    pages = [api.SpanGroup.from_mmda(sg) for sg in doc.pages]
    vila_span_groups = [api.SpanGroup.from_mmda(sg) for sg in doc.vila_span_groups]
    layoutparser_span_groups = [api.SpanGroup.from_mmda(sg) for sg in doc.layoutparser_span_groups]
    pages = [api.SpanGroup.from_mmda(sg) for sg in doc.pages]
    images = [tobase64(image) for image in doc.images]
    data={
      "instances": [{
      "symbols": doc.symbols,
      "tokens": [token.dict() for token in tokens],
      "rows": [token.dict() for token in rows],
      "pages": [token.dict() for token in pages],
      "vila_span_groups": [token.dict() for token in vila_span_groups],
      "layoutparser_span_groups": [token.dict() for token in layoutparser_span_groups],
      "images": images}]}
    result = requests.post(url, json=data)
    result.raise_for_status()
    return result
```
