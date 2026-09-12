# date-pr

A single-page static site. One HTML file, no dependencies, no build step,
no backend.

## Running it

Open `index.html` in a browser, or serve the directory with any static
file server. There is nothing to install.

## Configuration

Page content is read from the URL fragment as base64-encoded JSON. Open the
page with `#build` to generate a configured link.

Because the configuration travels in the fragment, nothing is stored
server-side — and anything encoded there is readable by whoever holds the
link. It is obscured, not encrypted.
