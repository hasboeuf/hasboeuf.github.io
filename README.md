## How to publish

1. Make changes
2. run `scripts/deploy` (optional, see below)
3. Commit and push

If a new category has been added, step 2 is required. Indeed `Centrarium` theme makes use of `jekyll-archive` plugin which is not supported by github. Consequence is to not generate indexes for categories so `deploy` script copies them in root folder in order to push raw html files.
