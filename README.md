# GNC Test Vehicle Example

An independent example that installs the [Apollo GNC method](https://github.com/nvinarcik/vinarcik_ApolloGNC) as the package `@vinarcik/apollo-gnc-method` and uses it to model **TV-1**, a small fictional test vehicle with a flight computer, memory, IMU, star tracker, display and five flight programs. All values are illustrative; the point is to exercise the packaged method end to end outside the Apollo Command Module model it was built for.

## What it uses from the package

| From the package | Used here |
|---|---|
| Vocabulary and bundle (`method:Computer`, `method:IMU`, `method:Alignment`, `method:PoweredFlight`, `dependsOn`, ...) | `src/oml/example.com/gnc-test-vehicle/description.oml` and `bundle.oml` |
| Editor templates (`components`, `routines`) | `src/md/Components.md` and `src/md/Routines.md`, each a `compose` block |
| SHACL shapes (inside the templates) | Validate the TV-1 components and routines |
| Component Impact Report generator (`impact:ImpactReportSpec`) | `src/oml/example.com/gnc-test-vehicle/codegen.oml`, config `impact` |

## Setup

1. Start the local registry from [`verdaccio`](https://github.com/modelware/verdaccio) (`node registry.mjs`) and publish the method to it, as described in the method's README.
2. Install the method:
   ```bash
   oml install -r http://localhost:4873
   ```
   It is installed into `deps/@vinarcik/apollo-gnc-method/`.

## Use

Open this repository in OML Code. The notebooks in `src/md` use the method's editor templates: add or edit components in `Components.md` and flight programs in `Routines.md`.

From the command line:

```bash
oml start
oml lint
oml validate --only
oml reason --only
oml codegen -c impact      # writes build/docs/TV-1-impact.md
oml render                 # writes build/web
oml stop
```

## Upgrading the method

A plain `oml install` keeps the installed version. To move to a newer one, name it:

```bash
oml install @vinarcik/apollo-gnc-method@0.3.2 -r http://localhost:4873
```
