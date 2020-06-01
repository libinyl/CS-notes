{
    "title": "Use CAPS LOCK for vi navigation",
    "rules": [
      {
        "description": "CAPS LOCK + hjkl to arrow keys",
        "manipulators": [
            {
                "type": "basic",
                "from": {
                  "key_code": "g",
                  "modifiers": {
                    "optional": [
                      "any"
                    ]
                  }
                },
                "to": [
                  {
                    "key_code": "left_arrow",
                    "modifiers": [
                        "left_command"
                    ]
                  }
                ],
                "conditions": [
                  {
                    "type": "variable_if",
                    "name": "caps_lock pressed",
                    "value": 1
                  }
                ]
            },
            {
                "type": "basic",
                "from": {
                  "key_code": "semicolon",
                  "modifiers": {
                    "optional": [
                      "any"
                    ]
                  }
                },
                "to": [
                  {
                    "key_code": "right_arrow",
                    "modifiers": [
                        "left_command"
                    ]
                  }
                ],
                "conditions": [
                  {
                    "type": "variable_if",
                    "name": "caps_lock pressed",
                    "value": 1
                  }
                ]
            },
          {
            "type": "basic",
            "from": {
              "key_code": "j",
              "modifiers": {
                "optional": [
                  "any"
                ]
              }
            },
            "to": [
              {
                "key_code": "down_arrow"
              }
            ],
            "conditions": [
              {
                "type": "variable_if",
                "name": "caps_lock pressed",
                "value": 1
              }
            ]
          },
          {
            "type": "basic",
            "from": {
              "key_code": "k",
              "modifiers": {
                "optional": [
                  "any"
                ]
              }
            },
            "to": [
              {
                "key_code": "up_arrow"
              }
            ],
            "conditions": [
              {
                "type": "variable_if",
                "name": "caps_lock pressed",
                "value": 1
              }
            ]
          },
          {
            "type": "basic",
            "from": {
              "key_code": "h",
              "modifiers": {
                "optional": [
                  "any"
                ]
              }
            },
            "to": [
              {
                "key_code": "left_arrow"
              }
            ],
            "conditions": [
              {
                "type": "variable_if",
                "name": "caps_lock pressed",
                "value": 1
              }
            ]
          },
          {
            "type": "basic",
            "from": {
              "key_code": "l",
              "modifiers": {
                "optional": [
                  "any"
                ]
              }
            },
            "to": [
              {
                "key_code": "right_arrow"
              }
            ],
            "conditions": [
              {
                "type": "variable_if",
                "name": "caps_lock pressed",
                "value": 1
              }
            ]
          },
          {
            "type": "basic",
            "from": {
              "key_code": "caps_lock",
              "modifiers": {
                "optional": [
                  "any"
                ]
              }
            },
            "to": [
              {
                "set_variable": {
                  "name": "caps_lock pressed",
                  "value": 1
                }
              }
            ],
            "to_after_key_up": [
              {
                "set_variable": {
                  "name": "caps_lock pressed",
                  "value": 0
                }
              }
            ]
          }
        ]
      }
    ]
  }