# REST API - Snapshot

The REST APIs are exposed over HTTPS https://external-api.oam.ltd/.

## Main Endpoint for Events

```
GET /event/bookmaker/{bookmaker}
```

### Parameters

- `bookmaker`: string identifier of the bookmaker

### Responses

- **200 OK**: JSON with snapshot
- **400 Bad Request**: invalid parameters
- **403 Forbidden**: unauthorized IP

```json
{
  "status": 1,
  "data": [
    {
      "_id": 61060755,
      "date": 1757854800000,
      "name": "Atalanta BC - US Lecce",
      "tournamentId": 23,
      "tournament": "Serie A",
      "categoryId": 31,
      "category": "Italy",
      "sportId": 1,
      "sport": "Soccer",
      "bookmakers": {
        "0": {
          "eventId": "123123",
          "playability": 1,
          "markets": {
            "1": {
              "sign": {
                "1": {
                  "outcomePosition": 1,
                  "backOdd": 1.42,
                  "updt": 1757318539218
                },
                "2": {
                  "outcomePosition": 2,
                  "backOdd": 4.75,
                  "updt": 1757318539218
                },
                "3": {
                  "outcomePosition": 3,
                  "backOdd": 6.75,
                  "updt": 1757318539218
                }
              }
            },
            "2": {
              "sign": {
                "2": {
                  "outcomePosition": 2,
                  "backOdd": 1.68,
                  "updt": 1757318539218
                },
                "3": {
                  "outcomePosition": 3,
                  "backOdd": 2.05,
                  "updt": 1757318539218
                }
              }
            },
            "9": {
              "sign": {
                "2": {
                  "outcomePosition": 2,
                  "backOdd": 1.9,
                  "updt": 1757318539218
                },
                "3": {
                  "outcomePosition": 3,
                  "backOdd": 1.8,
                  "updt": 1757318539218
                }
              }
            },
            "11": {
              "sign": {
                "2": {
                  "outcomePosition": 2,
                  "backOdd": 1.19,
                  "updt": 1757318539218
                },
                "3": {
                  "outcomePosition": 3,
                  "backOdd": 4.05,
                  "updt": 1757318539218
                }
              }
            },
            "12": {
              "sign": {
                "2": {
                  "outcomePosition": 2,
                  "backOdd": 2.75,
                  "updt": 1757318539218
                },
                "3": {
                  "outcomePosition": 3,
                  "backOdd": 1.38,
                  "updt": 1757318539218
                }
              }
            },
            "13": {
              "sign": {
                "2": {
                  "outcomePosition": 2,
                  "backOdd": 5.0,
                  "updt": 1757318539218
                },
                "3": {
                  "outcomePosition": 3,
                  "backOdd": 1.12,
                  "updt": 1757318539218
                }
              }
            }
          }
        }
      }
    }
  ]
}
```

## Main Endpoint for players

```
GET /player/{sport}/{bookmaker}
```

### Parameters

- `sport`: `soccer` | `basketball` | `tennis`
- `bookmaker`: string identifier of the bookmaker

### Parameters

- `bookmaker`: string identifier of the bookmaker

### Responses

- **200 OK**: JSON with snapshot
- **400 Bad Request**: invalid parameters
- **403 Forbidden**: unauthorized IP

```json
{
  "status": 1,
  "data": {
    "56328439": {
      "id": 56328439,
      "players": {
        "13827311": {
          "id": "13827311",
          "betradarId": null,
          "name": "Naz Hillmon",
          "shortName": "N. Hillmon",
          "fullName": "Naz Hillmon",
          "markets": {
            "Points": {
              "10.5": {
                "O": {
                  "odd": 2.0,
                  "updt": 1757310612739,
                  "bSelectionId": null,
                  "bMarketId": null,
                  "marketTV": null,
                  "runnerTV": null
                }
              }
            }
          },
          "_value": 1.0,
          "team": "H"
        }
      }
    }
  }
}

```

### Interactive Documentation

- Swagger UI: [https://data-feed-oam.github.io/docs/swagger/](https://data-feed-oam.github.io/docs/swagger/)
