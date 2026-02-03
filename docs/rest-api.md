# REST API - Snapshot

The REST APIs are exposed over HTTPS https://external-api.oam.ltd/v1.

## Main Endpoint for Events

```
GET /v1/event/bookmaker/{bookmaker}
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

## Market & Sign lookup for Events

In the Events snapshot response, the object `bookmakers.{bookmakerId}.markets` is keyed by a **numeric identifier** (serialized as a JSON string), e.g. `"1"`, `"2"`, `"9"`, etc.

Each market contains a `sign` object, also keyed by a **numeric identifier** (serialized as a JSON string). This signId identifies the market outcome/selection, e.g. `"1"`, `"2"`, `"3"`.

To convert these numeric IDs into human-readable names (market name and outcome names), use the `markets.json` lookup file.

- Download: [event_markets.json](./static/event_markets.json)

### How to resolve IDs

- `markets.<marketId>`: resolve the marketId (e.g. `"1"`) via the lookup to get `name`, `outcomes`, `sport`, etc.
- `markets.<marketId>.sign.<signId>`: resolve the signId (e.g. `"2"`) within the selected market `outcomes` map to get the outcome name (e.g. `"Over"`).

### Example (marketId=1, signId=2)

Given: - `markets["1"]` → lookup: `name = "1X2"`

- `sign["2"]` → lookup within `outcomes["2"]`: `name = "X"`

### Lookup format (excerpt)

```json
{
  "1": {
    "id": 1,
    "name": "1X2",
    "outcomes": {
      "1": {
        "name": "1"
      },
      "2": {
        "name": "X"
      },
      "3": {
        "name": "2"
      }
    },
    "hasSbvs": false,
    "sport": 1
  }
}
```

## Main Endpoint for Players

```
GET /v1/player/{sport}/{bookmaker}
```

### Parameters

- `sport`: `soccer` | `basketball` | `tennis`
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

## Market & Sign lookup for Players

In the Players snapshot response, the object `players.{playerId}.markets` is keyed by a **market identifier** (serialized as a JSON string), e.g. `"Goalscorers"`, `"Points"`, `"TotalShots"`.

Each market contains an `outcomes` object, also keyed by a **market outcome identifier** (serialized as a JSON string), e.g. `"Any"`, `"1st"`, `"O"`, `"U"`.

To convert these IDs into human-readable names (market name and outcome names), use the player markets lookup. Example:

- Download: [player_markets.json](./static/player_markets.json)

```json
{
  "Goalscorers": {
    "id": "Goalscorers",
    "name": "Goalscorers",
    "outcomes": {
      "Any": {
        "name": "Anytime"
      },
      "1st": {
        "name": "First"
      },
      "2o+": {
        "name": "2orMore"
      },
      "3o+": {
        "name": "3orMore"
      }
    }
  }
}
```

## Main Endpoint for Extra

```
GET /v1/extra/bookmaker/{bookmakerId}
```

### Parameters

- `bookmakerId`: string identifier of the bookmaker

### Responses

- **200 OK**: JSON with snapshot
- **400 Bad Request**: invalid parameters
- **403 Forbidden**: unauthorized IP

```json
{
  "status": 1,
  "data": {
    "markets": {
      "1X2CN": {
        "#": {
          "1": {
            "odd": 1.77,
            "updt": 1770113164489
          },
          "2": {
            "odd": 2.25,
            "updt": 1770113164489
          },
          "X": {
            "odd": 8.2,
            "updt": 1770113164489
          }
        }
      },
      "OUCN": {
        "6.5": {
          "U": {
            "odd": 3.95,
            "updt": 1770113164890
          },
          "O": {
            "odd": 1.18,
            "updt": 1770113164890
          }
        },
        "7.5": {
          "U": {
            "odd": 2.75,
            "updt": 1770113164890
          },
          "O": {
            "odd": 1.35,
            "updt": 1770113164890
          }
        },
        "8.5": {
          "U": {
            "odd": 2.05,
            "updt": 1770113164890
          },
          "O": {
            "odd": 1.62,
            "updt": 1770113164890
          }
        },
        "9.5": {
          "U": {
            "odd": 1.63,
            "updt": 1770113164890
          },
          "O": {
            "odd": 2.05,
            "updt": 1770113164890
          }
        },
        "10.5": {
          "U": {
            "odd": 1.38,
            "updt": 1770113164890
          },
          "O": {
            "odd": 2.65,
            "updt": 1770113164890
          }
        },
        "11.5": {
          "U": {
            "odd": 1.22,
            "updt": 1770113164890
          },
          "O": {
            "odd": 3.5,
            "updt": 1770113164890
          }
        },
        "12.5": {
          "U": {
            "odd": 1.12,
            "updt": 1770113164890
          },
          "O": {
            "odd": 4.8,
            "updt": 1770113164890
          }
        }
      }
    }
  }
}
```

## Market & Sign lookup for Extra

In the Extra snapshot response, the object `data.markets` is keyed by a **market identifier** (serialized as a JSON string), e.g. `"1X2CN"`, `"OUCN"`.

Each market contains a line key (e.g. `"#"`, `"6.5"`, `"7.5"`) and then outcome identifiers (serialized as JSON strings), e.g. `"1"`, `"2"`, `"X"`, `"O"`, `"U"`.

To convert these IDs into human-readable names (market name and outcome names), use the `extra_markets.json` lookup file.

- Download: [extra_markets.json](./static/extra_markets.json)


- Swagger UI: [https://data-feed-oam.github.io/docs/swagger/](https://data-feed-oam.github.io/docs/swagger/)
