# Export confluence scroll pdf action

This action exports a confluence page and downloads it using scroll pdf. It outputs the path of the resulting pdf.

## Inputs

### `page`
**Required** ID of the page to be exported.
### `server-url`
**Optional** Url of the server to be downloaded from. Default `"https://scroll-pdf.us.exporter.k15t.app"`.
### `scope`
**Optional** The scope of the action. Default `"descendants"`.
### `template`
**Optional** ID of the scroll pdf template. Default `"com.k15t.scroll.pdf.default-template-documentation"`.

## Outputs

### `path`
Path to the created PDF file

## Environment variables

### `SCROLL_PDF_BEARER`
The bearer authorization token configured

## Example usage

```yaml
on: [push]

jobs:
  export_pdf_job:
    runs-on: ubuntu-latest
    steps:
      - name: Export confluence pdf
        id: pdf-export
        uses: OleRoss/export-confluence-scroll-pdf@v1
        with:
          server-url: 'https://scroll-pdf.us.exporter.k15t.app'
          page: '123456789'
          scope: 'descendants'
          template: 'com.k15t.scroll.pdf.default-template-documentation'
        env:
          SCROLL_PDF_BEARER: ${{ secrets.SCROLL_PDF_BEARER }}
      - name: Upload as artifact
        uses: actions/upload-artifact@v3
        with:
          name: documentation
          path: ${{ steps.pdf-export.outputs.path }}
```
