---
title: "Reconstruct blog posts"
author: "Hoontaek Lee"
date: 2026-11-02T20:48:05+01:00
description:
cover: 
  relative: true
draft: false
hideToc: false
enableToc: true
enableTocContent: false
tocPosition: outer
tocLevels: ["h2", "h3", "h4"]
tags:
- 2026
- Blog
---

# Summary

I changed the blog folder structure, with helps by Claude. Below is some notes for it and detailed steps designed by Claude.

- Removed /public from git tracking because:
    - it will add a lot of work and storage size
    - Cloudflare will not use pre-built /public but will build /public by itself. This is confirmed in the cloudflare dashboard "Build command: hugo"

      <img src="/posts/figures/20261102_restructure_posts_001.jpg" style="zoom:100%;" />

- Structure change  
    - before: all .md files and images under content
    - after: classifiy .md files into before_jena, jena, and paris. Others, such as, photos folders like weekly_log_in_Jena will be untouched not to break the absolute image paths in .md files. Hyperlinks to other .md files are only two cases, so they will be manually corrected.
    - **why change the structure**: Zettlr collapsed whenever I add content/posts to workspace because of the huge amount of files. Thus I wanted to rearrange the files so that I can only add a small portion of it to workspace.
- Saved a snapshot of the current status via git tag

- **Next to do?**… would be to restructure figure paths

# Steps

Below is the steps suggested by Claude.

**Updated step list (finalised):**

1.  **Fix `public/` tracking** — one-time cleanup, separate commit:

bash

```bash
   echo "public/" > .gitignore
   git add .gitignore
   git rm -r --cached public/
   git commit -m "stop tracking generated public/ output"
   git push bloght-hugo_remote master:blogpages
```

2.  **Tag the clean state** as a snapshot:

bash

```bash
   git tag before-restructure
```

3.  **Create working branch:**

bash

```bash
   git checkout -b restructure/content-folders
```

4.  **Create the three subfolders** under `content/posts/`:
    - `before_jena/`
    - `jena/`
    - `paris/`
5.  **Move the `.md` files** into their respective subfolders (image dirs stay in place)
6.  **Fix the two cross-era links** manually:
    - In `20251221_paris_wk024.md`: `./20240317_jena_wk183.md/` → `../jena/20240317_jena_wk183.md/`
    - In `20261019_paris_wk068.md`: `20250511_jena_wk244.md` → `../jena/20250511_jena_wk244.md`
7.  **Test locally** with `hugo server`
8.  **Commit and merge back:**

bash

```bash
   git add .
   git commit -m "reorganise content/posts into before_jena, jena, paris subfolders"
   git checkout master
   git merge restructure/content-folders
   git push bloght-hugo_remote master:blogpages
```

9.  **PR `master` → `main`** as usual → Cloudflare deploys automatically

&nbsp;

The step 7 took a long time, so made another change to fix it.

1.  **Add `maxAge` to `hugo.yaml`** — change the caches section to:

yaml

```yaml
   caches:
     images:
       dir: :cacheDir/images
       maxAge: 1440h
```

2.  **Run once and wait it out** (even if 15+ mins — this builds the cache):

bash

```bash
   hugo server --gc
```

3.  **After it finishes**, test the site at `http://localhost:1313/`. Second and future runs should be fast.
4.  **Do not delete** `resources/_gen/images/` — that’s the cache.

&nbsp;

**`maxAge: 1440h`** — tells Hugo to keep cached images for 1440 hours (60 days) before considering them stale. Without it, Hugo may decide the cache is expired and reprocess everything on each run. It’s what prevents the slowness from recurring.

**`hugo server --gc`** — `--gc` means “garbage collect”: clean up any leftover stale cache files before building. Combined with the new `maxAge`, it forces a clean rebuild of the cache once, correctly this time.

**On git commit** — `hugo.yaml` is a source file and should be committed. The cache itself (`resources/_gen/`) should not (add it to `.gitignore` too). So:

bash

```bash
echo "resources/" >> .gitignore

git add hugo.yaml .gitignore

git commit -m "fix image cache config and ignore generated resources"
```