---
name: import-recipe
description: Use when the user gives a URL to a recipe website and wants it saved into this repository as a new recipe file, or asks to "import"/"add" a recipe from a link.
---

# Import Recipe

Fetch a recipe from a URL and save it as a new file matching this repo's house
style. Use `entree/apple-chili.md` as the canonical reference for tone and
formatting if anything below is ambiguous.

## Workflow

1. **Get the URL.** Use it from args if provided; otherwise ask the user.

2. **Fetch the page** with WebFetch. Ask it to extract: recipe title, author
   or site byline, full ingredient list with quantities, full instructions,
   and any stated yield/prep time/cook time.

3. **Pick the folder and category.** Match existing conventions — don't
   invent new top-level folders without asking:

   | Folder      | `categories:` value                              |
   |-------------|---------------------------------------------------|
   | `entree/`   | `[entree]`                                         |
   | `desserts/` | `[dessert]` (add tags, e.g. `[dessert,thanksgiving]`) |
   | `sides/`    | `[side]`                                           |
   | `drinks/`   | `[drinks]`                                         |

   If the recipe doesn't clearly fit one of these, ask the user rather than
   guessing.

4. **Simplify the instructions.** Rewrite the source's steps as brief
   numbered steps in this repo's terse style — strip marketing language,
   life stories, and mid-step tips. Genuinely useful asides (substitutions,
   optional ingredients) go inline in parentheses like apple-chili.md does
   ("sub for regular, we just like the smoky flavor"), not as extra prose.

5. **List ingredients** as `* ` bullets, one per line: quantity + unit +
   ingredient + prep note (e.g. "drained and rinsed"), in the source's order.

6. **Build the front matter:**
   - `categories:` from step 3
   - `yields:`, `prep:`, `cook:` as single-item bracketed arrays, e.g.
     `[4 servings]`, `[10 mins]`; use `[n/a]` if the source doesn't say
   - `made:` — this repo records the date the dish was actually cooked.
     Default to today's date, but tell the user to update it once they've
     actually made it.

7. **Add the citation** under `## Notes`:
   `* Derived from [Recipe Title](URL) by Author Name`
   Omit "by Author Name" if no author/byline is available.

8. **Name and place the file** — kebab-case slug of the title, in the
   folder from step 3 (e.g. `sides/garlic-mashed-potatoes.md`). If a file
   already exists at that path, confirm with the user before overwriting.

9. **Write the file**, then show the user the final result.

## Template

```markdown
---
categories: [category]
yields: [amount]
prep: [time]
cook: [time]
made: [YYYY-MM-DD]
---

# Recipe Title

## Ingredients

* quantity ingredient, prep note

## Instructions

1. Step one.
2. Step two.

## Notes

* Derived from [Recipe Title](url) by Author Name
```
