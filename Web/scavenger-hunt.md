# Scavenger Hunt

**Category:** Web Exploitation
**Difficulty:** Easy

## Approach

The challenge required finding hidden information across the website.

1. **HTML Source** → Found a flag fragment in a comment.
2. **CSS** → Found another flag fragment.
3. **JavaScript** → Provided a clue to check `robots.txt`.
4. **`robots.txt`** → Revealed another hidden location.
5. **`.htaccess`** → Revealed another flag fragment and a clue about macOS.
6. **`.DS_Store`** → Used the macOS clue to find the final fragment.
7. Combined all fragments to obtain the flag.

## Concepts

**`robots.txt`** — Tells search engine crawlers which paths should or shouldn't be indexed. It can sometimes reveal hidden directories or endpoints.

**`.htaccess`** — An Apache configuration file used to control server behavior for a directory. If exposed, it may reveal useful configuration details or clues.

**`.DS_Store`** — A macOS metadata file containing information about folders and their contents. If exposed on a web server, it can disclose filenames or directory information.

## Key Takeaways

* Inspect HTML, CSS and JavaScript source.
* Check common files such as `robots.txt`, `.htaccess`, and `.DS_Store`.
* Follow clues systematically during web enumeration.

**Tools:** Browser DevTools, View Source
**Concepts:** Web Enumeration, Information Disclosure, Forced Browsing
