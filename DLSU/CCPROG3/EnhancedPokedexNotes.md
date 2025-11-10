
# Pokemon

| Field            | Validator                | Types    | Limit             | Condition              |
| ---------------- | ------------------------ | -------- | ----------------- | ---------------------- |
| `name`           | `validateName`           | `String` | Max limit is 12   |                        |
| `pokedexNumber`  | `validatePokedexNumber`  | `Number` | Max limit is 1025 | Pokedex must not exist |
| `type1`          | `validateType`           |          |                   |                        |
| `type2`          | `validateType`           |          |                   |                        |
| `baseLevel`      | `validateBaseLevel`      |          |                   |                        |
| `evolutionLevel` | `validateEvolutionLevel` |          |                   |                        |
| `evolvesFrom`    | `validateEvolvesFrom`    |          |                   |                        |
| `evolvesTo`      | `validateEvolvesTo`      |          |                   |                        |
| `health`         | `validateStat`           |          |                   |                        |
| `attack`         | `validateStat`           |          |                   |                        |
| `defense`        | `validateStat`           |          |                   |                        |
| `speed`          | `validateStat`           |          |                   |                        |
| `moveSets`       | N/A                      |          |                   |                        |

# Items

| Field            | Validator             |
| ---------------- | --------------------- |
| `name`           | `validateName`        |
| `category`       | `validateCategory`    |
| `description`    | `validateDescription` |
| `effects`        |                       |
| `minBuyingPrice` | `validatePrice`       |
| `maxBuyingPrice` | `validatePrice`       |
| `sellingPrice`   | `validatePrice`       |

# Moves

| Field            | Validator                |
| ---------------- | ------------------------ |
| `name`           | `validateName`           |
| `description`    | `validateDescription`    |
| `classification` | `validateClassification` |
| `type1`          | `validateType`           |
| `type2`          | `validateType`           |


# Trainer

| Field         | Validator             |
| ------------- | --------------------- |
| `name`        | `validateName`        |
| `birthdate`   | `validateDate`        |
| `sex`         | `validateSex`         |
| `hometown`    | `validateHometown`    |
| `description` | `validateDescription` |
| `money`       | `validateMoney`       |
