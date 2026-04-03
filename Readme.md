prompt:

## documentation
"Please create a new file for this  problem under docs/Arrays/Easy. Here is the solution code and complexity analysis..."

## local workflow
1 - `python -m zensical build --clean`
2 - open the generated output from `site/`
3 - use `npm install` once if you want the Husky pre-commit hook locally

## husky
1 - Husky runs `npm run build:docs` before each commit
2 - if the build fails, fix the docs/config issue and commit again


## github
1 - git add .
2 - git commit -m "suitable message" (e.g. "Add Two Sum solution") based on the problem description
3 - git push
