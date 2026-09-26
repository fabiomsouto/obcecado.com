# obcecado.com

Source for [obcecado.com](https://obcecado.com), built with [Hugo](https://gohugo.io).
`.github/workflows/deploy.yaml` builds it on every push and pull request, and on
`main` deploys it to S3 behind CloudFront. The AWS side is described in
[`aws/README.md`](aws/README.md).

## Local preview

```sh
hugo server
```

Needs Hugo extended, version 0.146 or newer (CI pins the exact version).

## Layout

- `content/phonkyo/` is the Phonkyo product page. Kits, price and the hero dial
  live in its front matter; the board images are rendered from the KiCad design.
- `layouts/` holds the templates, with no theme. `layouts/product.html` is the
  product page and `layouts/_shortcodes/` has the kits and order blocks.
- `assets/css/main.css` is the only stylesheet.

The order email address is `params.orderEmail` in `hugo.yaml`.

## Re-rendering the board images

With KiCad 10 from Flathub, from the `phonkyo` repository:

```sh
kicad-cli pcb render -o board-iso.png -w 2000 -h 1400 --quality basic \
  --use-board-stackup-colors --perspective --rotate '-45,0,-30' phonkyo.kicad_pcb
kicad-cli pcb render -o board-top.png -w 2000 -h 1000 --quality basic \
  --use-board-stackup-colors --side top --zoom 1.15 phonkyo.kicad_pcb
magick board-iso.png -trim +repage board-iso.png   # same for board-top.png
```

(`flatpak run --command=kicad-cli org.kicad.KiCad` stands in for `kicad-cli`.)

## Licence

The site's words and images (`content/`) are CC BY-NC-SA 4.0, the same as the
Phonkyo design. The code is MIT. The fonts are under the SIL Open Font License.
See [`LICENSE`](LICENSE).
