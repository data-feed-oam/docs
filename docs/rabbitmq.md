# Updates via RabbitMQ

Updates are delivered through **RabbitMQ** .

## Connection

- Protocol: AMQP 0.9.1
- Host: `external-rmq.oam.ltd`
- Port: `5672`
- VHost: `/<client>`
- Username/Password: provided by support

## Event Queue
- `event`

## Routing Keys
- `event.<bookmakerID>`

## Message Format

Example JSON:
Headers:
op: 'U' upsert | 'D' delete

```json
{
  "_id": 60941915,
  "name": "Paris Saint-Germain - Tottenham Hotspur",
  "tournament": "UEFA Super Cup",
  "tournamentId": 465,
  "category": "International Clubs",
  "categoryId": 393,
  "sport": "Soccer",
  "sportId": 1,
  "date": 1755111600000,
  "bookmakers": {
    "1": {
      "eventId": "2561",
      "playability": 1,
      "markets": {
        "1": {
          "sign": {
            "1": {
              "outcomePosition": 1,
              "backOdd": 1.43,
              "updt": 1748914576019
            },
            "2": {
              "outcomePosition": 2,
              "backOdd": 4.8,
              "updt": 1748914576019
            },
            "3": {
              "outcomePosition": 3,
              "backOdd": 6.4,
              "updt": 1748914576019
            }
          }
        }
      }
    }
  },
  "_expdt": "2025-08-13T19:00:00"
}
```

## Player Queue

- `player`

## Routing Keys

- `player.<sportID>.<bookmakerID>`

## Message Format

Example JSON:

Headers:
bid: bookmakerID
op: 'U' upsert | 'D' delete

Message:

```json
{
  "id": "34694653",
  "date": 1757357100000,
  "eventId": 56418485,
  "bookmaker": 2,
  "sportId": 1,
  "players": {
    "7016132": {
      "id": "7016132",
      "name": "John Souttar",
      "shortName": "John Souttar",
      "fullName": "John Souttar",
      "markets": {
        "Goalscorers": {
          "#": {
            "1st": {
              "odd": 110,
              "updt": 1757322314457,
              "bSelectionId": "7016132",
              "bMarketId": "1.247409086",
              "marketTV": 48,
              "runnerTV": 0
            }
          }
        }
      },
      "team": null
    },
    "12977768": {
      "id": "12977768",
      "name": "Scott McTominay",
      "shortName": "Scott McTominay",
      "fullName": "Scott McTominay",
      "markets": {
        "Goalscorers": {
          "#": {
            "1st": {
              "odd": 75,
              "updt": 1757322314457,
              "bSelectionId": "12977768",
              "bMarketId": "1.247409086",
              "marketTV": 48,
              "runnerTV": 43
            }
          }
        }
      },
      "team": null
    }
  }
}
```

## Extra Queue

- `player`

## Routing Keys

- `extra.<sportID>.<bookmakerID>`

## Message Format
```json
TBD
```