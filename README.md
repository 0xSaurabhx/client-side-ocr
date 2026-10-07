# Client Side OCR

Free browser-based PDF OCR: extract text from scanned PDFs and invoices with PaddleOCR, without uploading your documents.

**[Try the live demo](https://0xsaurabhx.github.io/client-side-ocr/)**

## Features

- Choose a PDF or drag it into the page.
- Force OCR for scanned documents, or use the PDF text layer when one exists.
- Choose fast, balanced or detailed rendering resolution.
- View a page preview alongside editable extracted text.
- Download the extracted text as a `.txt` file.
- See model initialization and per-page processing times.
- Run OCR in a background worker, using WebGPU when available or WebAssembly as a fallback.

This is an English/Latin printed-text demo. It extracts text, not structured invoice fields. Check invoice totals, identifiers and other important text against the original. Accuracy and speed depend on the document, resolution and device.

## Tech stack

- PaddleOCR browser SDK with PP-OCRv5 mobile detection and recognition models
- ONNX Runtime Web for browser inference
- PDF.js for PDF rendering and existing text-layer extraction
- OpenCV.js for image handling
- JavaScript, HTML and CSS in a single static page

## How it works

1. The browser downloads the libraries and OCR models.
2. PDF.js reads your selected PDF and renders each page locally.
3. Force OCR sends rendered pixels to PaddleOCR in a browser worker. Fast mode first checks for an existing PDF text layer.
4. Extracted text and page previews appear in the page. The text download is created locally.

The two OCR models are about 21.5 MB combined, with additional downloads for the runtimes. Initialization needs internet access; this is not a bundled offline app.

## Run locally

No build step or server-side OCR service is required.

```sh
git clone https://github.com/0xSaurabhx/client-side-ocr.git
cd client-side-ocr
python3 -m http.server 8000
```

Open `http://localhost:8000` in current Chrome or Edge with internet access. The single `index.html` file can also be opened directly in a supported browser. Network policies may block external library or model downloads.

## Privacy

PDF contents and extracted text are processed in your browser. The demo code does not send documents to an OCR server or use a document-upload endpoint.

The app loads libraries from jsDelivr and model assets from Hugging Face. GitHub Pages and those asset hosts receive normal page or asset requests, including network metadata. Local document processing does not mean the page makes no network requests.

For production use, consider self-hosting the pinned libraries and models, and test accuracy and performance on your own documents and target devices.

## References

- [PaddleOCR browser SDK](https://www.paddleocr.ai/latest/en/version3.x/inference_deployment/cross_platform/browser.html)
- [PDF.js](https://mozilla.github.io/pdf.js/)

## License

No project license has been selected yet. The repository owner may consider MIT for the demo's own code, after checking the embedded SDK and third-party library/model licenses and preserving any required notices. This note does not grant a license or change third-party terms.
