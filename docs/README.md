<h1 align="center">
  <a href="https://github.com/z-shell/zi">
    <p><img src="https://github.com/z-shell/zi/raw/main/docs/images/logo.svg" alt="Logo" width="60px" height="60px" /></a>
  ❮ ZI ❯ Special Package - Any Node </p>
</h1>
<h3 align="center">
<table>
    <tr>
        <td><b>Package source:</b></td>
        <td>Source Tarball</td>
        <td>Binary</td>
        <td>Git</td>
        <td>Node</td>
        <td>Gem</td>
    </tr>
    <tr>
        <td><b>Status:</b></td>
        <td>❌</td>
        <td>❌</td>
        <td>✔️ (default)</td>
        <td>❌</td>
        <td>❌</td>
    </tr>
</table></h3><hr />

## The `any-node` package

This package is special – it is designed for easy installing of any Node modules inside the plugin directory, exposing their binaries via _shims_ (i.e.: forwarder scripts) created automatically by [Bin-Gem-Node](https://github.com/z-shell/z-a-bin-gem-node) annex.

The Node module(s) to install are specified by the `param'MOD → {module1}; MOD2 → {module2}; …'` ice. The name of the plugin will be `{module1}`, unless `id-as''` ice will be provided, or the `IDAS` param will be set (i.e.: `param'IDAS → my-plugin; MOD → …'`).

A few example invocations:

```shell
# Install `coffee-script' module and call the plugin with the same name
zi pack param='MOD → coffee-script' for any-node
```

```shell
# Install `remark' Markdown processor and call the plugin: remark
zi id-as=remark pack param='MOD → remark-man; MOD2 → remark-cli' for any-node
```

```shell
# Install `pen' Markdown previewer and call the plugin: my-pen
zi pack param='IDAS → my-pen; MOD → pen' for any-node
```

## Default profile

The only profile that does all the magic. It relies on the `%PARAM%` keywords, which are substituted with the `value` from the ice `param'PARAM → value; …'`.

The ZI command executed will be equivalent to:

```shell
zi lucid id-as="${${:-%IDAS%}:-%MOD%}" as=null \
  node="%MOD%;%MOD2%;%MOD3%;%MOD4%;%MOD5%;%MOD6%;%MOD7%;%OTHER%" \
  sbin="n:node_modules/.bin/*" for \
    z-shell/null
```

---

> This repository compatible with [ZI](https://github.com/z-shell/zi)

The [ZI](https://github.com/z-shell/zi) package that uses the [zsh-string-lib](https://github.com/z-shell/zsh-string-lib) to automatically:

- get the plugin's Git repository OR release-package URL,
- get the list of the recommended ices for the plugin,
  - there can be multiple lists of ices,
  - the ice lists are stored in _profiles_; there's at least one profile, _default_,
  - the ices can be selectively overridden.
