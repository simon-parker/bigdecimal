
| Language | Literal Syntax | Arithmetic                                            | Equality                                                         |
|:---------|:---------------|-------------------------------------------------------|------------------------------------------------------------------|
| Java     | -              | ``new BigDecimal("0.1").plus(new BigDecimal("0.2"))`` | ``new BigDecimal("0.1").compareTo(new BigDecimal("0.10")) == 0`` |
| Scala    | `dec"0.1"`     | `dec"0.1" + dec"0.2"`                                 | `dec"0.1" == dec"0.10"`                                          |
| Groovy   | `0.1G`         | `0.1G + 0.2G`                                         | `0.1G == 0.10G`                                                  |
| Clojure  | `0.1M`         | `0.1M + 0.2M`                                         | (= 0.1M 0.10M)                                                   |
