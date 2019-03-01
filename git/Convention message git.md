# Format Git messages

> source : https://gist.github.com/stephenparish/9941e89d80e2bc58a153


```bash
<type>(<scope>): <subject>
<BLANK LINE>
<body>
<BLANK LINE>
<footer>
```

Les lignes ne doivent pas dépasser 100 signes.

## Ligne sujet
La ligne sujet contient une description succincte des changements.

### \<type> autorisé :
- feat (feature)
- fix (bug fix)
- docs (documentation)
- style (formatting, missing semi colons,...)
- refactor
- test (when adding missing tests)
- chore (maintain)

### \<scope>
La scope peut être tout élement spécifiant l'emplacement du changement.

### \<subject>

exemples :
```bash
feat($browser): onUrlChange event (popstate/hashchange/polling)

Added new event to $browser:
- forward popstate event if available
- forward hashchange event if popstate not available
- do polling when neither popstate nor hashchange available

Breaks $browser.onHashChange, which was removed (use onUrlChange instead)
```

```bash
feat($browser): onUrlChange event (popstate/hashchange/polling)

Added new event to $browser:
- forward popstate event if available
- forward hashchange event if popstate not available
- do polling when neither popstate nor hashchange available

Breaks $browser.onHashChange, which was removed (use onUrlChange instead)
```

```bash
feat($browser): onUrlChange event (popstate/hashchange/polling)

Added new event to $browser:
- forward popstate event if available
- forward hashchange event if popstate not available
- do polling when neither popstate nor hashchange available

Breaks $browser.onHashChange, which was removed (use onUrlChange instead)
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTk1NDA3MDU1Ml19
-->