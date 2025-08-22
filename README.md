# Products – 3 APIs included, CI runs ONLY GET /products with 2 datasets

**Endpoints in collection:**
- `GET /products/search?q={{query}}`  → dataset: `dataset_search.csv` (query=Gloves)
- `PUT /products/{{productId}}`       → dataset: `dataset_put.csv` (name, description, stock, price)
- `GET /products?page={{page}}`       → dataset: `dataset_list.csv` (2 rows)

**CI (GitHub Actions)** is configured to run **only** the GET `/products` request with **two iterations** from `dataset_list.csv`:
1) Row `search`: validates there is a product whose name contains *Gloves*.
2) Row `after_update`: validates full fields (id, name, description, stock, price).

> Bạn có thể tự chạy Search và PUT trong Postman Collection Runner với `dataset_search.csv` và `dataset_put.csv` nếu cần show video 3 API.

## Run locally
```bash
npm i -g newman newman-reporter-htmlextra
# CI-like run
newman run postman_collection.json -e postman_environment.json -d dataset_list.csv   -r cli,htmlextra,junit   --reporter-htmlextra-export newman/report.html   --reporter-junit-export newman/results.xml

# Optional: run search
newman run postman_collection.json -e postman_environment.json -d dataset_search.csv --folder "Products – Search (GET)"
# Optional: run PUT
newman run postman_collection.json -e postman_environment.json -d dataset_put.csv --folder "Products – Update (PUT)"
```
