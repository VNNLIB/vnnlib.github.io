# VNN-LIB Website

This repository contains the VNN-LIB website, synchronized from
`VNNLIB-Solver-Database/website`.
It follows the client request to split the original single-page site into
multiple pages:

- `index.html` for the homepage, introduction, latest news, and team members
- `standards.html` for the documents page
- `solvers.html` for solver capability search
- `libraries.html` for VNN-LIB libraries
- `related.html` for related tools

All pages share `css/site.css` so the prototype presents as one consistent
site. The Solvers page first requests `https://12er90.pythonanywhere.com/solvers`
and falls back to `data/solvers.json`. It shows matching solver releases in a
table and can be served as a static site.

The current Solvers page filters in the browser so it can be developed and
reviewed without a deployed server. The intended production integration is to
query the web API that wraps the Python compatibility package, while keeping
the same filter fields and result structure.

With no filters selected, the page shows every recorded solver release,
including failed or non-conforming submissions. Capability filters only match
releases that have a `capabilities` record; use the Status filter to inspect
failed or incomplete records directly.

The filter names mirror `vnnfilter.Query`: `onnx_opset`, `element_types`,
`operators`, `vnnlib_version`, `hidden_nodes`, `multiple_io`,
`multiple_networks`, `node_comparisons`, `arithmetic`,
`optimised_disjunction`, and `serialise_assignments`.

From the repository root:

```bash
python -m http.server 8000
```

Then open:

```text
http://127.0.0.1:8000/
```

Develop changes in `VNNLIB-Solver-Database/website`, then synchronize the pages,
shared CSS, and JavaScript here. Keep the root-site fallback path as
`data/solvers.json` and refresh that snapshot from `VNNLIB-Solver-Database/data/solvers.json`.
