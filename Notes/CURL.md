To run requests in parallel

```

curl --parallel --parallel-immediate --parallel-max 2 \
  -X POST "http://localhost:8080/cart/checkout" \
  -H "Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJleHBpcmVkQXQiOjE3MzY1NDQ0MzcsInVzZXJJRCI6IjEifQ.RheIuNCQbv0qlAEo4ABco32gQCZriJkafbcu1Du3e1s" \
  -H "Content-Type: application/json" \
  -d '{"items": [{"productID": 1, "quantity": 2}, {"productID": 2, "quantity": 1}], "address": {"street": "street", "country": "country", "postalCode": "postalCode", "city": "city", "state": "state"}}' \
  -X POST "http://localhost:8080/cart/checkout" \
  -H "Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJleHBpcmVkQXQiOjE3MzY1NDQ0MzcsInVzZXJJRCI6IjEifQ.RheIuNCQbv0qlAEo4ABco32gQCZriJkafbcu1Du3e1s" \
  -H "Content-Type: application/json" \
  -d '{"items": [{"productID": 1, "quantity": 2}, {"productID": 2, "quantity": 1}], "address": {"street": "street", "country": "country", "postalCode": "postalCode", "city": "city", "state": "state"}}'

```