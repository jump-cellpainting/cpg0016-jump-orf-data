# ORF data repo
JUMP ORF data repo with dvc

## Download the data
### Clone the repository

```bash
git clone https://github.com/jump-cellpainting/jump-orf-data.git
```

### Download all the profiles stored as `.dvc` in S3

```bash
dvc pull
```

### Download all the other `.gz` files stored in Git LFS

```bash
git lfs pull
```
