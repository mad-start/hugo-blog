## A place for notes.

### How I made this:

I created an empty repository on github.com with path `<organization|username>/<repo-name>`.

With `brew` on a Mac:

```bash
1. brew install hugo
2. git clone git@github.com:<organization|username>/<repo-name>
3. cd <repo-name>
4. hugo new site .
5. git submodule add https://github.com/de-souza/hugo-flex.git themes/hugo-flex
6. hugo new posts/personalization-stack.md
7. hugo server -D
```


```mermaid
graph TD;
    A-->B;
    A-->C;
    B-->D;
    C-->D;
```
