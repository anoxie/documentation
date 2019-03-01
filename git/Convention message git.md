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
```
feat($browser): onUrlChange event (popstate/hashchange/polling)

Added new event to $browser:
- forward popstate event if available
- forward hashchange event if popstate not available
- do polling when neither popstate nor hashchange available

Breaks $browser.onHashChange, which was removed (use onUrlChange instead)
```

```
fix($compile): couple of unit tests for IE9

Older IEs serialize html uppercased, but IE9 does not...
Would be better to expect case insensitive, unfortunately jasmine does
not allow to user regexps for throw expectations.

Closes #392
Breaks foo.bar api, foo.baz should be used instead
```

```
feat(directive): ng:disabled, ng:checked, ng:multiple, ng:readonly, ng:selected

New directives for proper binding these attributes in older browsers (IE).
Added coresponding description, live examples and e2e tests.

Closes #351
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTMzODYxNTE4XX0=
-->