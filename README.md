# Access the Spotify Partner API



### Disclaimer

Use this at your own risk. Spotify does not want you to use this API - it is meant for Spotify apps and things like smart home devices. 


### Index

1. Requirements
2. Get Access Token
3. Example usage
4. Example Responses

### Requirements

```
requests
urllib
json
```



### Get Access Token

```python
def getAccessToken():
    headers = requests.utils.default_headers()
    resp = requests.get("https://open.spotify.com/get_access_token")
    data = resp.json()

    return data['accessToken'] #returns the access token
```

response (data)

```python
{
  'clientId': 'd1e02',
  'accessToken': '**token**',
  'accessTokenExpirationTimestampMs': '**timestamp**',
  'isAnonymous': True
}
```



### Example usage

#### 1. Search on Spotify

```python
def search(query): 
    urlStart = 'https://api-partner.spotify.com/pathfinder/v1/query?operationName=searchDesktop&'
    variables = 'variables={"searchTerm":"'+ query +'","offset":0,"limit":5,"numberOfTopResults":5}'
    hash = '&extensions={"persistedQuery":{"version":1,"sha256Hash":"75bbf6bfcfdf85b8fc828417bfad92b7cd66bf7f556d85670f4da8292373ebec"}}'
    
    addon = variables + hash
    url = urlStart + urllib.parse.quote_plus(addon, safe="=&")
    
    accessToken = getAccessToken()
    headers = requests.utils.default_headers()
    headers.update({
        'authorization': 'Bearer ' + accessToken #access token from above
    })
    
    response = requests.get(url, headers=headers).json()
    return response
```



#### 2. Get Data of specific artist (id)

```python
def getArtistInfo(artistID):
    urlStart = 'https://api-partner.spotify.com/pathfinder/v1/query?operationName=queryArtistOverview&'
    variables = 'variables={"uri":"spotify:artist:' + artistID + '"}'
    hash = '&extensions={"persistedQuery": {"version": 1, "sha256Hash": "d66221ea13998b2f81883c5187d174c8646e4041d67f5b1e103bc262d447e3a0"}}'
    
    addon = variables + hash
    url = urlStart + urllib.parse.quote_plus(addon, safe="=&")
    
    accessToken = getAccessToken()
    headers = requests.utils.default_headers()
    headers.update({
        'authorization': 'Bearer ' + accessToken
    })
    
    response = requests.get(url, headers=headers).json()
    return response
```



### Example Response

```python
search("eminem")
```

```python
{
  'clientId': 'd1e02',
  'accessToken': '**token**',
  'accessTokenExpirationTimestampMs': '**timestamp**',
  'isAnonymous': True
}{
  'data': {
    'search': {
      'albums': {
        'totalCount': 637,
        'items': [
          {
            'name': 'The Eminem Show',
            'type': 'ALBUM',
            'uri': 'spotify:album:2cWBwpqMsDJC1ZUwz813lo',
            'artists': {
              'items': [
                {
                  'uri': 'spotify:artist:7dGJo4pcD2V6oG8kP0tJRR',
                  'profile': {
                    'name': 'Eminem'
                  }
                }
              ]
            },
            'coverArt': {
              'sources': [
                {
                  'url': 'https://i.scdn.co/image/ab67616d00001e026ca5c90113b30c3c43ffb8f4',
                  'width': 300,
                  'height': 300
                },
                {
                  'url': 'https://i.scdn.co/image/ab67616d000048516ca5c90113b30c3c43ffb8f4',
                  'width': 64,
                  'height': 64
                },
                {
                  'url': 'https://i.scdn.co/image/ab67616d0000b2736ca5c90113b30c3c43ffb8f4',
                  'width': 640,
                  'height': 640
                }
              ]
            },
            'date': {
              'year': 2002
            }
          },
          {
            'name': 'The Marshall Mathers LP',
            'type': 'ALBUM',
            'uri': 'spotify:album:6t7956yu5zYf5A829XRiHC',
            'artists': {
              'items': [
                {
                  'uri': 'spotify:artist:7dGJo4pcD2V6oG8kP0tJRR',
                  'profile': {
                    'name': 'Eminem'
                  }
                }
              ]
            },
            'coverArt': {
              'sources': [
                {
                  'url': 'https://i.scdn.co/image/ab67616d00001e02dbb3dd82da45b7d7f31b1b42',
                  'width': 300,
                  'height': 300
                },
                {
                  'url': 'https://i.scdn.co/image/ab67616d00004851dbb3dd82da45b7d7f31b1b42',
                  'width': 64,
                  'height': 64
                },
                {
                  'url': 'https://i.scdn.co/image/ab67616d0000b273dbb3dd82da45b7d7f31b1b42',
                  'width': 640,
                  'height': 640
                }
              ]
            },
            'date': {
              'year': 2000
            }
          },
          {
            'name': 'Music To Be Murdered By',
            'type': 'ALBUM',
            'uri': 'spotify:album:4otkd9As6YaxxEkIjXPiZ6',
            'artists': {
              'items': [
                {
                  'uri': 'spotify:artist:7dGJo4pcD2V6oG8kP0tJRR',
                  'profile': {
                    'name': 'Eminem'
                  }
                }
              ]
            },
            'coverArt': {
              'sources': [
                {
                  'url': 'https://i.scdn.co/image/ab67616d00001e022f44aec83b20e40f3baef73c',
                  'width': 300,
                  'height': 300
                },
                {
                  'url': 'https://i.scdn.co/image/ab67616d000048512f44aec83b20e40f3baef73c',
                  'width': 64,
                  'height': 64
                },
                {
                  'url': 'https://i.scdn.co/image/ab67616d0000b2732f44aec83b20e40f3baef73c',
                  'width': 640,
                  'height': 640
                }
              ]
            },
            'date': {
              'year': 2020
            }
          },
          {
            'name': 'Eminem',
            'type': 'SINGLE',
            'uri': 'spotify:album:33kScSdvf4Vobi3wrNxiyB',
            'artists': {
              'items': [
                {
                  'uri': 'spotify:artist:511G4ovDwuIZhWJgqdLupt',
                  'profile': {
                    'name': 'Dj Beats'
                  }
                }
              ]
            },
            'coverArt': {
              'sources': [
                {
                  'url': 'https://i.scdn.co/image/ab67616d00001e02ffd1c6525d2186b0df6db753',
                  'width': 300,
                  'height': 300
                },
                {
                  'url': 'https://i.scdn.co/image/ab67616d00004851ffd1c6525d2186b0df6db753',
                  'width': 64,
                  'height': 64
                },
                {
                  'url': 'https://i.scdn.co/image/ab67616d0000b273ffd1c6525d2186b0df6db753',
                  'width': 640,
                  'height': 640
                }
              ]
            },
            'date': {
              'year': 2020
            }
          },
          {
            'name': 'Recovery',
            'type': 'ALBUM',
            'uri': 'spotify:album:47BiFcV59TQi2s9SkBo2pb',
            'artists': {
              'items': [
                {
                  'uri': 'spotify:artist:7dGJo4pcD2V6oG8kP0tJRR',
                  'profile': {
                    'name': 'Eminem'
                  }
                }
              ]
            },
            'coverArt': {
              'sources': [
                {
                  'url': 'https://i.scdn.co/image/ab67616d00001e02c08d5fa5c0f1a834acef5100',
                  'width': 300,
                  'height': 300
                },
                {
                  'url': 'https://i.scdn.co/image/ab67616d00004851c08d5fa5c0f1a834acef5100',
                  'width': 64,
                  'height': 64
                },
                {
                  'url': 'https://i.scdn.co/image/ab67616d0000b273c08d5fa5c0f1a834acef5100',
                  'width': 640,
                  'height': 640
                }
              ]
            },
            'date': {
              'year': 2010
            }
          }
        ]
      },
      'artists': {
        'totalCount': 20,
        'items': [
          {
            'uri': 'spotify:artist:7dGJo4pcD2V6oG8kP0tJRR',
            'profile': {
              'name': 'Eminem'
            },
            'visuals': {
              'avatarImage': {
                'sources': [
                  {
                    'url': 'https://i.scdn.co/image/ab6761610000e5eba00b11c129b27a88fc72f36b',
                    'width': 640,
                    'height': 640
                  },
                  {
                    'url': 'https://i.scdn.co/image/ab6761610000f178a00b11c129b27a88fc72f36b',
                    'width': 160,
                    'height': 160
                  }
                ]
              }
            }
          },
          {
            'uri': 'spotify:artist:4tu5JlFAm1wZ728LV695VI',
            'profile': {
              'name': 'Emineminem'
            },
            'visuals': {
              'avatarImage': {
                'sources': [
                  {
                    'url': 'https://i.scdn.co/image/ab67616d0000b273177153de024339c3fa731be6',
                    'width': 640,
                    'height': 640
                  },
                  {
                    'url': 'https://i.scdn.co/image/ab67616d00004851177153de024339c3fa731be6',
                    'width': 64,
                    'height': 64
                  }
                ]
              }
            }
          },
          {
            'uri': 'spotify:artist:0z6cEzNZrHfKfj7sXyuS8j',
            'profile': {
              'name': 'Emineme'
            },
            'visuals': {
              'avatarImage': {
                'sources': [
                  {
                    'url': 'https://i.scdn.co/image/ab67616d0000b2735a58e7332d3149b4915fef59',
                    'width': 640,
                    'height': 640
                  },
                  {
                    'url': 'https://i.scdn.co/image/ab67616d000048515a58e7332d3149b4915fef59',
                    'width': 64,
                    'height': 64
                  }
                ]
              }
            }
          },
          {
            'uri': 'spotify:artist:6Dxd9WP0s3TRM2Htt28UQi',
            'profile': {
              'name': 'La EmineMCa'
            },
            'visuals': {
              'avatarImage': {
                'sources': [
                  {
                    'url': 'https://i.scdn.co/image/ab6761610000e5eba6d6a2bb6ede885063e59cc5',
                    'width': 640,
                    'height': 640
                  },
                  {
                    'url': 'https://i.scdn.co/image/ab6761610000f178a6d6a2bb6ede885063e59cc5',
                    'width': 160,
                    'height': 160
                  }
                ]
              }
            }
          },
          {
            'uri': 'spotify:artist:16SfgOBulDFXWORWr5d3qq',
            'profile': {
              'name': "Emine'm"
            },
            'visuals': {
              'avatarImage': {
                'sources': [
                  {
                    'url': 'https://i.scdn.co/image/ab67616d0000b2737999b090c18df4d3b2e206db',
                    'width': 640,
                    'height': 640
                  },
                  {
                    'url': 'https://i.scdn.co/image/ab67616d000048517999b090c18df4d3b2e206db',
                    'width': 64,
                    'height': 64
                  }
                ]
              }
            }
          }
        ]
      },
      'episodes': {
        'totalCount': 1000,
        'items': [
          {
            'episode': {
              'name': 'Eminem-Nail in the coffin',
              'uri': 'spotify:episode:5Qx5jecKgXZ8xGaYfIu9FL',
              'coverArt': {
                'sources': [
                  {
                    'url': 'https://i.scdn.co/image/b38baca8c967f35a19a1004302bbe05c0db54c74',
                    'width': 64,
                    'height': 64
                  },
                  {
                    'url': 'https://i.scdn.co/image/5efb7597a1f1129357344aff1b3d3260ff10f7af',
                    'width': 300,
                    'height': 300
                  },
                  {
                    'url': 'https://i.scdn.co/image/2280d1dd605371229c761f2ac044dc0d0608704f',
                    'width': 640,
                    'height': 640
                  }
                ]
              },
              'duration': {
                'totalMilliseconds': 290133
              },
              'releaseDate': {
                'isoString': '2020-11-16T15:45:00Z'
              },
              'podcast': {
                'coverArt': {
                  'sources': [
                    {
                      'url': 'https://i.scdn.co/image/246a12159eac83508d919fdadb3d4fdc0565666a',
                      'width': 64,
                      'height': 64
                    },
                    {
                      'url': 'https://i.scdn.co/image/064670271d8ed648051931c96b8cb1fdcb387416',
                      'width': 300,
                      'height': 300
                    },
                    {
                      'url': 'https://i.scdn.co/image/f416facde0b57884a8e1eda36a6d14ee0bcd7757',
                      'width': 640,
                      'height': 640
                    }
                  ]
                }
              },
              'description': 'Eminem-Nail in the coffin',
              'contentRating': {
                'label': 'NONE'
              }
            }
          },
          {
            'episode': {
              'name': 'Juice WRLD freestyle (R.I.P) Hour of fire over Eminem beats!',
              'uri': 'spotify:episode:3AO38D1p2A2B7FlB8Nm0m5',
              'coverArt': {
                'sources': [
                  {
                    'url': 'https://i.scdn.co/image/ab6765630000f68dbff949795aa53ba3b7e60706',
                    'width': 64,
                    'height': 64
                  },
                  {
                    'url': 'https://i.scdn.co/image/ab67656300005f1fbff949795aa53ba3b7e60706',
                    'width': 300,
                    'height': 300
                  },
                  {
                    'url': 'https://i.scdn.co/image/ab6765630000ba8abff949795aa53ba3b7e60706',
                    'width': 640,
                    'height': 640
                  }
                ]
              },
              'duration': {
                'totalMilliseconds': 3138269
              },
              'releaseDate': {
                'isoString': '2020-12-07T13:00:00Z'
              },
              'podcast': {
                'coverArt': {
                  'sources': [
                    {
                      'url': 'https://i.scdn.co/image/ab6765630000f68d67814790ab8a6a8c2795a4c3',
                      'width': 64,
                      'height': 64
                    },
                    {
                      'url': 'https://i.scdn.co/image/ab67656300005f1f67814790ab8a6a8c2795a4c3',
                      'width': 300,
                      'height': 300
                    },
                    {
                      'url': 'https://i.scdn.co/image/ab6765630000ba8a67814790ab8a6a8c2795a4c3',
                      'width': 640,
                      'height': 640
                    }
                  ]
                }
              },
              'description': '"Copyright Disclaimer Under Section 107 of the Copyright Act 1976, allowance is made for "fair use" for purposes such as criticism, comment, news reporting, teaching, scholarship, and research. Fair use is a use permitted by copyright statute that might otherwise be infringing. Non-profit, educational or personal use tips the balance in favorite of fair use."',
              'contentRating': {
                'label': 'EXPLICIT'
              }
            }
          },
          {
            'episode': {
              'name': 'Eminem',
              'uri': 'spotify:episode:2CU3i63anMquNSwbeBQzV0',
              'coverArt': {
                'sources': [
                  {
                    'url': 'https://i.scdn.co/image/ab6765630000f68def3a6097dd26c556635bf536',
                    'width': 64,
                    'height': 64
                  },
                  {
                    'url': 'https://i.scdn.co/image/ab67656300005f1fef3a6097dd26c556635bf536',
                    'width': 300,
                    'height': 300
                  },
                  {
                    'url': 'https://i.scdn.co/image/ab6765630000ba8aef3a6097dd26c556635bf536',
                    'width': 640,
                    'height': 640
                  }
                ]
              },
              'duration': {
                'totalMilliseconds': 3553462
              },
              'releaseDate': {
                'isoString': '2020-03-20T08:00:00Z'
              },
              'podcast': {
                'coverArt': {
                  'sources': [
                    {
                      'url': 'https://i.scdn.co/image/ab6765630000f68def3a6097dd26c556635bf536',
                      'width': 64,
                      'height': 64
                    },
                    {
                      'url': 'https://i.scdn.co/image/ab67656300005f1fef3a6097dd26c556635bf536',
                      'width': 300,
                      'height': 300
                    },
                    {
                      'url': 'https://i.scdn.co/image/ab6765630000ba8aef3a6097dd26c556635bf536',
                      'width': 640,
                      'height': 640
                    }
                  ]
                }
              },
              'description': 'Will the real Marshall Mathers please sit down for a rare and revealing conversation on the set of his new music video Godzilla ? Yes he will.  Learn more about your ad choices. Visit megaphone.fm/adchoices',
              'contentRating': {
                'label': 'EXPLICIT'
              }
            }
          },
          {
            'episode': {
              'name': 'Lose yourself(original demo version )',
              'uri': 'spotify:episode:0lTaxvhZ1Z142CsIVjBetI',
              'coverArt': {
                'sources': [
                  {
                    'url': 'https://i.scdn.co/image/ab6765630000f68d6a5f68242901276c0b9b7334',
                    'width': 64,
                    'height': 64
                  },
                  {
                    'url': 'https://i.scdn.co/image/ab67656300005f1f6a5f68242901276c0b9b7334',
                    'width': 300,
                    'height': 300
                  },
                  {
                    'url': 'https://i.scdn.co/image/ab6765630000ba8a6a5f68242901276c0b9b7334',
                    'width': 640,
                    'height': 640
                  }
                ]
              },
              'duration': {
                'totalMilliseconds': 180813
              },
              'releaseDate': {
                'isoString': '2021-11-06T23:51:00Z'
              },
              'podcast': {
                'coverArt': {
                  'sources': [
                    {
                      'url': 'https://i.scdn.co/image/ab6765630000f68d32c89f6efc631c84f394f5c7',
                      'width': 64,
                      'height': 64
                    },
                    {
                      'url': 'https://i.scdn.co/image/ab67656300005f1f32c89f6efc631c84f394f5c7',
                      'width': 300,
                      'height': 300
                    },
                    {
                      'url': 'https://i.scdn.co/image/ab6765630000ba8a32c89f6efc631c84f394f5c7',
                      'width': 640,
                      'height': 640
                    }
                  ]
                }
              },
              'description': 'Shady XV',
              'contentRating': {
                'label': 'NONE'
              }
            }
          },
          {
            'episode': {
              'name': 'When I Grow Up Feat. NF, Logic, Eminem, Joyner Lucas',
              'uri': 'spotify:episode:19pUTBffqXtv6gEANxZz9I',
              'coverArt': {
                'sources': [
                  {
                    'url': 'https://i.scdn.co/image/ab6765630000f68d74000cd23bec8218db5f69e6',
                    'width': 64,
                    'height': 64
                  },
                  {
                    'url': 'https://i.scdn.co/image/ab67656300005f1f74000cd23bec8218db5f69e6',
                    'width': 300,
                    'height': 300
                  },
                  {
                    'url': 'https://i.scdn.co/image/ab6765630000ba8a74000cd23bec8218db5f69e6',
                    'width': 640,
                    'height': 640
                  }
                ]
              },
              'duration': {
                'totalMilliseconds': 385033
              },
              'releaseDate': {
                'isoString': '2021-03-15T14:21:00Z'
              },
              'podcast': {
                'coverArt': {
                  'sources': [
                    {
                      'url': 'https://i.scdn.co/image/ab6765630000f68d74000cd23bec8218db5f69e6',
                      'width': 64,
                      'height': 64
                    },
                    {
                      'url': 'https://i.scdn.co/image/ab67656300005f1f74000cd23bec8218db5f69e6',
                      'width': 300,
                      'height': 300
                    },
                    {
                      'url': 'https://i.scdn.co/image/ab6765630000ba8a74000cd23bec8218db5f69e6',
                      'width': 640,
                      'height': 640
                    }
                  ]
                }
              },
              'description': '(:',
              'contentRating': {
                'label': 'NONE'
              }
            }
          }
        ]
      },
      'genres': {
        'totalCount': 0,
        'items': [
          
        ]
      },
      'playlists': {
        'totalCount': 1000,
        'items': [
          {
            'name': 'EMINEM BEST OF',
            'uri': 'spotify:playlist:2rL7J8CJrdksF944XqcYjr',
            'description': '',
            'images': {
              'items': [
                {
                  'sources': [
                    {
                      'url': 'https://i.scdn.co/image/ab67706c0000da84132592c603bf37999f614f07',
                      'width': 640,
                      'height': 640
                    }
                  ]
                }
              ]
            },
            'owner': {
              'name': 'Eminem'
            }
          },
          {
            'name': 'This Is Eminem',
            'uri': 'spotify:playlist:37i9dQZF1DX1clOuib1KtQ',
            'description': 'Listen to new album "Music To Be Murdered By" and all his greatest hits.',
            'images': {
              'items': [
                {
                  'sources': [
                    {
                      'url': 'https://i.scdn.co/image/ab67706f000000027a181d9fed936372672c40ca',
                      'width': None,
                      'height': None
                    }
                  ]
                }
              ]
            },
            'owner': {
              'name': 'Spotify'
            }
          },
          {
            'name': 'Eminem: Best Of The Best',
            'uri': 'spotify:playlist:3xqcAMgjHGrv3ElA51zZRj',
            'description': 'The biggest and best tracks from Eminem including River with Ed Sheeran, Without Me, Lose Yourself, Stan, Love The Way You Lie feat. <a href="https://open.spotify.com/user/best-of-the-best/playlist/1zI5mQ3BgVx2HS4UuyJMMH?si=yWdG55qFRrOCwYOiLyEhsw">Rihanna</a>, My Name Is and so much more. Check out The <a>Best Of The Best</a> profile for more great playlists!',
            'images': {
              'items': [
                {
                  'sources': [
                    {
                      'url': 'https://i.scdn.co/image/ab67706c0000da849ee7a095aa96164af96048ab',
                      'width': 640,
                      'height': 640
                    }
                  ]
                }
              ]
            },
            'owner': {
              'name': 'Best Of The Best'
            }
          },
          {
            'name': 'Eminem Old Hits ',
            'uri': 'spotify:playlist:6K4OQdWEZ5RcJV8SdqKX41',
            'description': '',
            'images': {
              'items': [
                {
                  'sources': [
                    {
                      'url': 'https://mosaic.scdn.co/640/ab67616d00001e023686f349e17589993adacdddab67616d00001e026ca5c90113b30c3c43ffb8f4ab67616d00001e029bef45ee387f274ea3198c55ab67616d00001e02dbb3dd82da45b7d7f31b1b42',
                      'width': 640,
                      'height': 640
                    },
                    {
                      'url': 'https://mosaic.scdn.co/300/ab67616d00001e023686f349e17589993adacdddab67616d00001e026ca5c90113b30c3c43ffb8f4ab67616d00001e029bef45ee387f274ea3198c55ab67616d00001e02dbb3dd82da45b7d7f31b1b42',
                      'width': 300,
                      'height': 300
                    },
                    {
                      'url': 'https://mosaic.scdn.co/60/ab67616d00001e023686f349e17589993adacdddab67616d00001e026ca5c90113b30c3c43ffb8f4ab67616d00001e029bef45ee387f274ea3198c55ab67616d00001e02dbb3dd82da45b7d7f31b1b42',
                      'width': 60,
                      'height': 60
                    }
                  ]
                }
              ]
            },
            'owner': {
              'name': 'Cameron Webster'
            }
          },
          {
            'name': 'Eminem best hits',
            'uri': 'spotify:playlist:2k9EUdGgNjS2Tl1dW76aVc',
            'description': 'A beatiful list that contatins the most beatiful Eminem songs. Try to listen them!',
            'images': {
              'items': [
                {
                  'sources': [
                    {
                      'url': 'https://i.scdn.co/image/ab67706c0000da844ef7d32c08b9d5761cbb80e9',
                      'width': 640,
                      'height': 640
                    }
                  ]
                }
              ]
            },
            'owner': {
              'name': 'TheRedPinger'
            }
          }
        ]
      },
      'podcasts': {
        'totalCount': 75,
        'items': [
          {
            'name': 'Juice WRLD freestyle (R.I.P) Hour of fire over Eminem beats! Westwood',
            'uri': 'spotify:show:6hs4CKPnnhYvpJzNJ0sayD',
            'coverArt': {
              'sources': [
                {
                  'url': 'https://i.scdn.co/image/ab6765630000f68d67814790ab8a6a8c2795a4c3',
                  'width': 64,
                  'height': 64
                },
                {
                  'url': 'https://i.scdn.co/image/ab67656300005f1f67814790ab8a6a8c2795a4c3',
                  'width': 300,
                  'height': 300
                },
                {
                  'url': 'https://i.scdn.co/image/ab6765630000ba8a67814790ab8a6a8c2795a4c3',
                  'width': 640,
                  'height': 640
                }
              ]
            },
            'type': 'PODCAST',
            'publisher': {
              'name': 'Jameson'
            },
            'mediaType': 'AUDIO'
          },
          {
            'name': 'The Eminem Podcast',
            'uri': 'spotify:show:4bujq0be2L1onSC7mZr1Uk',
            'coverArt': {
              'sources': [
                {
                  'url': 'https://i.scdn.co/image/22624af50b2daf5e38f92e224c81d824513d0de0',
                  'width': 64,
                  'height': 64
                },
                {
                  'url': 'https://i.scdn.co/image/20a8a18e39f31666a733a65674c5261e1cc605fc',
                  'width': 300,
                  'height': 300
                },
                {
                  'url': 'https://i.scdn.co/image/f007a4f0bef8fe8088f55ce380ff4163358083ec',
                  'width': 640,
                  'height': 640
                }
              ]
            },
            'type': 'PODCAST',
            'publisher': {
              'name': 'The Eminem Podcast'
            },
            'mediaType': 'AUDIO'
          },
          {
            'name': 'Eminem',
            'uri': 'spotify:show:6PHHSM0ceecaLxXxeL1Of7',
            'coverArt': {
              'sources': [
                {
                  'url': 'https://i.scdn.co/image/ab6765630000f68dd0c1e8e5e448f12a8d4f88b4',
                  'width': 64,
                  'height': 64
                },
                {
                  'url': 'https://i.scdn.co/image/ab67656300005f1fd0c1e8e5e448f12a8d4f88b4',
                  'width': 300,
                  'height': 300
                },
                {
                  'url': 'https://i.scdn.co/image/ab6765630000ba8ad0c1e8e5e448f12a8d4f88b4',
                  'width': 640,
                  'height': 640
                }
              ]
            },
            'type': 'PODCAST',
            'publisher': {
              'name': 'Eminem'
            },
            'mediaType': 'AUDIO'
          },
          {
            'name': 'The Joe Rogan Experience',
            'uri': 'spotify:show:4rOoJ6Egrf8K2IrywzwOMk',
            'coverArt': {
              'sources': [
                {
                  'url': 'https://i.scdn.co/image/97d6fdf3e55a3a1c10662d132232ccbd53740bc3',
                  'width': 64,
                  'height': 64
                },
                {
                  'url': 'https://i.scdn.co/image/d3ae59a048dff7e95109aec18803f22bebe82d2f',
                  'width': 300,
                  'height': 300
                },
                {
                  'url': 'https://i.scdn.co/image/9af79fd06e34dea3cd27c4e1cd6ec7343ce20af4',
                  'width': 640,
                  'height': 640
                }
              ]
            },
            'type': 'PODCAST',
            'publisher': {
              'name': 'Joe Rogan'
            },
            'mediaType': 'MIXED'
          },
          {
            'name': 'Hotboxin With Mike Tyson',
            'uri': 'spotify:show:7rrXnDyc70sfTcJqBO32lr',
            'coverArt': {
              'sources': [
                {
                  'url': 'https://i.scdn.co/image/ab6765630000f68def3a6097dd26c556635bf536',
                  'width': 64,
                  'height': 64
                },
                {
                  'url': 'https://i.scdn.co/image/ab67656300005f1fef3a6097dd26c556635bf536',
                  'width': 300,
                  'height': 300
                },
                {
                  'url': 'https://i.scdn.co/image/ab6765630000ba8aef3a6097dd26c556635bf536',
                  'width': 640,
                  'height': 640
                }
              ]
            },
            'type': 'PODCAST',
            'publisher': {
              'name': 'Malka Media'
            },
            'mediaType': 'AUDIO'
          }
        ]
      },
      'topResults': {
        'items': [
          {
            'uri': 'spotify:artist:7dGJo4pcD2V6oG8kP0tJRR',
            'profile': {
              'name': 'Eminem'
            },
            'visuals': {
              'avatarImage': {
                'sources': [
                  {
                    'url': 'https://i.scdn.co/image/ab6761610000e5eba00b11c129b27a88fc72f36b',
                    'width': 640,
                    'height': 640
                  },
                  {
                    'url': 'https://i.scdn.co/image/ab6761610000f178a00b11c129b27a88fc72f36b',
                    'width': 160,
                    'height': 160
                  }
                ]
              }
            }
          },
          {
            'uri': 'spotify:track:0WSTCrEsC2rsM8zavpfM5I',
            'id': '0WSTCrEsC2rsM8zavpfM5I',
            'name': 'Eminem Speaks',
            'album': {
              'uri': 'spotify:album:07tZDCAqxSIVEZywk0KDfT',
              'name': 'Fighting Demons',
              'coverArt': {
                'sources': [
                  {
                    'url': 'https://i.scdn.co/image/ab67616d00001e02c820e86be3bcbc65e5b88ef0',
                    'width': 300,
                    'height': 300
                  },
                  {
                    'url': 'https://i.scdn.co/image/ab67616d00004851c820e86be3bcbc65e5b88ef0',
                    'width': 64,
                    'height': 64
                  },
                  {
                    'url': 'https://i.scdn.co/image/ab67616d0000b273c820e86be3bcbc65e5b88ef0',
                    'width': 640,
                    'height': 640
                  }
                ]
              },
              'id': '07tZDCAqxSIVEZywk0KDfT',
              'sharingInfo': {
                'shareUrl': 'https://open.spotify.com/album/07tZDCAqxSIVEZywk0KDfT?si=M8v7xBBsQpiqVbfQ5iWgNQ'
              }
            },
            'artists': {
              'items': [
                {
                  'uri': 'spotify:artist:4MCBfE4596Uoi2O4DtmEMz',
                  'profile': {
                    'name': 'Juice WRLD'
                  }
                }
              ]
            },
            'contentRating': {
              'label': 'EXPLICIT'
            },
            'duration': {
              'totalMilliseconds': 133250
            },
            'playability': {
              'playable': True
            }
          },
          {
            'uri': 'spotify:playlist:2rL7J8CJrdksF944XqcYjr',
            'name': 'EMINEM BEST OF',
            'description': '',
            'images': {
              'items': [
                {
                  'sources': [
                    {
                      'url': 'https://i.scdn.co/image/ab67706c0000da84132592c603bf37999f614f07',
                      'width': 640,
                      'height': 640
                    }
                  ]
                }
              ]
            },
            'owner': {
              'name': 'Eminem'
            }
          },
          {
            'uri': 'spotify:album:2cWBwpqMsDJC1ZUwz813lo',
            'name': 'The Eminem Show',
            'artists': {
              'items': [
                {
                  'uri': 'spotify:artist:7dGJo4pcD2V6oG8kP0tJRR',
                  'profile': {
                    'name': 'Eminem'
                  }
                }
              ]
            },
            'coverArt': {
              'sources': [
                {
                  'url': 'https://i.scdn.co/image/ab67616d00001e026ca5c90113b30c3c43ffb8f4',
                  'width': 300,
                  'height': 300
                },
                {
                  'url': 'https://i.scdn.co/image/ab67616d000048516ca5c90113b30c3c43ffb8f4',
                  'width': 64,
                  'height': 64
                },
                {
                  'url': 'https://i.scdn.co/image/ab67616d0000b2736ca5c90113b30c3c43ffb8f4',
                  'width': 640,
                  'height': 640
                }
              ]
            },
            'date': {
              'year': 2002
            }
          },
          {
            'uri': 'spotify:show:6hs4CKPnnhYvpJzNJ0sayD',
            'name': 'Juice WRLD freestyle (R.I.P) Hour of fire over Eminem beats! Westwood',
            'coverArt': {
              'sources': [
                {
                  'url': 'https://i.scdn.co/image/ab6765630000f68d67814790ab8a6a8c2795a4c3',
                  'width': 64,
                  'height': 64
                },
                {
                  'url': 'https://i.scdn.co/image/ab67656300005f1f67814790ab8a6a8c2795a4c3',
                  'width': 300,
                  'height': 300
                },
                {
                  'url': 'https://i.scdn.co/image/ab6765630000ba8a67814790ab8a6a8c2795a4c3',
                  'width': 640,
                  'height': 640
                }
              ]
            },
            'type': 'PODCAST',
            'publisher': {
              'name': 'Jameson'
            },
            'mediaType': 'AUDIO'
          }
        ],
        'featured': [
          {
            'uri': 'spotify:playlist:37i9dQZF1DX1clOuib1KtQ',
            'name': 'This Is Eminem',
            'description': 'Listen to new album "Music To Be Murdered By" and all his greatest hits.',
            'images': {
              'items': [
                {
                  'sources': [
                    {
                      'url': 'https://i.scdn.co/image/ab67706f000000027a181d9fed936372672c40ca',
                      'width': None,
                      'height': None
                    }
                  ]
                }
              ]
            },
            'owner': {
              'name': 'Spotify'
            }
          },
          {
            'uri': 'spotify:playlist:37i9dQZF1E4uduXaJcMi49',
            'name': 'Eminem Radio',
            'description': '',
            'images': {
              'items': [
                {
                  'sources': [
                    {
                      'url': 'https://seeded-session-images.scdn.co/v1/img/artist/7dGJo4pcD2V6oG8kP0tJRR/en',
                      'width': None,
                      'height': None
                    }
                  ]
                }
              ]
            },
            'owner': {
              'name': 'Spotify'
            }
          },
          {
            'uri': 'spotify:playlist:37i9dQZF1DX76Wlfdnj7AP',
            'name': 'Beast Mode',
            'description': 'Get your beast mode on!',
            'images': {
              'items': [
                {
                  'sources': [
                    {
                      'url': 'https://i.scdn.co/image/ab67706f000000029249b35f23fb596b6f006a15',
                      'width': None,
                      'height': None
                    }
                  ]
                }
              ]
            },
            'owner': {
              'name': 'Spotify'
            }
          },
          {
            'uri': 'spotify:playlist:37i9dQZF1DX4o1oenSJRJd',
            'name': 'All Out 2000s',
            'description': 'The biggest songs of the 2000s. Cover: Gwen Stefani.',
            'images': {
              'items': [
                {
                  'sources': [
                    {
                      'url': 'https://i.scdn.co/image/ab67706f0000000206c7ca43d921a7cdd7ab69d6',
                      'width': None,
                      'height': None
                    }
                  ]
                }
              ]
            },
            'owner': {
              'name': 'Spotify'
            }
          }
        ]
      },
      'tracks': {
        'totalCount': 1000,
        'items': [
          {
            'track': {
              'uri': 'spotify:track:0WSTCrEsC2rsM8zavpfM5I',
              'id': '0WSTCrEsC2rsM8zavpfM5I',
              'name': 'Eminem Speaks',
              'album': {
                'uri': 'spotify:album:07tZDCAqxSIVEZywk0KDfT',
                'name': 'Fighting Demons',
                'coverArt': {
                  'sources': [
                    {
                      'url': 'https://i.scdn.co/image/ab67616d00001e02c820e86be3bcbc65e5b88ef0',
                      'width': 300,
                      'height': 300
                    },
                    {
                      'url': 'https://i.scdn.co/image/ab67616d00004851c820e86be3bcbc65e5b88ef0',
                      'width': 64,
                      'height': 64
                    },
                    {
                      'url': 'https://i.scdn.co/image/ab67616d0000b273c820e86be3bcbc65e5b88ef0',
                      'width': 640,
                      'height': 640
                    }
                  ]
                },
                'id': '07tZDCAqxSIVEZywk0KDfT',
                'sharingInfo': {
                  'shareUrl': 'https://open.spotify.com/album/07tZDCAqxSIVEZywk0KDfT?si=M8v7xBBsQpiqVbfQ5iWgNQ'
                }
              },
              'artists': {
                'items': [
                  {
                    'uri': 'spotify:artist:4MCBfE4596Uoi2O4DtmEMz',
                    'profile': {
                      'name': 'Juice WRLD'
                    }
                  }
                ]
              },
              'contentRating': {
                'label': 'EXPLICIT'
              },
              'duration': {
                'totalMilliseconds': 133250
              },
              'playability': {
                'playable': True
              }
            }
          },
          {
            'track': {
              'uri': 'spotify:track:77Ft1RJngppZlq59B6uP0z',
              'id': '77Ft1RJngppZlq59B6uP0z',
              'name': 'Lose Yourself',
              'album': {
                'uri': 'spotify:album:6wdSf72duVewXTqhYU3Z87',
                'name': 'SHADYXV',
                'coverArt': {
                  'sources': [
                    {
                      'url': 'https://i.scdn.co/image/ab67616d00001e0231aafa752187cb0284307200',
                      'width': 300,
                      'height': 300
                    },
                    {
                      'url': 'https://i.scdn.co/image/ab67616d0000485131aafa752187cb0284307200',
                      'width': 64,
                      'height': 64
                    },
                    {
                      'url': 'https://i.scdn.co/image/ab67616d0000b27331aafa752187cb0284307200',
                      'width': 640,
                      'height': 640
                    }
                  ]
                },
                'id': '6wdSf72duVewXTqhYU3Z87',
                'sharingInfo': {
                  'shareUrl': 'https://open.spotify.com/album/6wdSf72duVewXTqhYU3Z87?si=qi-08NPOQ-a_Jl5Fi1xGSg'
                }
              },
              'artists': {
                'items': [
                  {
                    'uri': 'spotify:artist:7dGJo4pcD2V6oG8kP0tJRR',
                    'profile': {
                      'name': 'Eminem'
                    }
                  }
                ]
              },
              'contentRating': {
                'label': 'EXPLICIT'
              },
              'duration': {
                'totalMilliseconds': 320626
              },
              'playability': {
                'playable': True
              }
            }
          },
          {
            'track': {
              'uri': 'spotify:track:7FIWs0pqAYbP91WWM0vlTQ',
              'id': '7FIWs0pqAYbP91WWM0vlTQ',
              'name': 'Godzilla (feat. Juice WRLD)',
              'album': {
                'uri': 'spotify:album:4otkd9As6YaxxEkIjXPiZ6',
                'name': 'Music To Be Murdered By',
                'coverArt': {
                  'sources': [
                    {
                      'url': 'https://i.scdn.co/image/ab67616d00001e022f44aec83b20e40f3baef73c',
                      'width': 300,
                      'height': 300
                    },
                    {
                      'url': 'https://i.scdn.co/image/ab67616d000048512f44aec83b20e40f3baef73c',
                      'width': 64,
                      'height': 64
                    },
                    {
                      'url': 'https://i.scdn.co/image/ab67616d0000b2732f44aec83b20e40f3baef73c',
                      'width': 640,
                      'height': 640
                    }
                  ]
                },
                'id': '4otkd9As6YaxxEkIjXPiZ6',
                'sharingInfo': {
                  'shareUrl': 'https://open.spotify.com/album/4otkd9As6YaxxEkIjXPiZ6?si=8DWqgsHwQiadJJY-txQZ8w'
                }
              },
              'artists': {
                'items': [
                  {
                    'uri': 'spotify:artist:7dGJo4pcD2V6oG8kP0tJRR',
                    'profile': {
                      'name': 'Eminem'
                    }
                  },
                  {
                    'uri': 'spotify:artist:4MCBfE4596Uoi2O4DtmEMz',
                    'profile': {
                      'name': 'Juice WRLD'
                    }
                  }
                ]
              },
              'contentRating': {
                'label': 'EXPLICIT'
              },
              'duration': {
                'totalMilliseconds': 210800
              },
              'playability': {
                'playable': True
              }
            }
          },
          {
            'track': {
              'uri': 'spotify:track:4wif7gRrpGngrm8Dsh2fFP',
              'id': '4wif7gRrpGngrm8Dsh2fFP',
              'name': 'Eminem Speaks',
              'album': {
                'uri': 'spotify:album:62MDj5jYbhMvYxoaqyu1yw',
                'name': 'Fighting Demons',
                'coverArt': {
                  'sources': [
                    {
                      'url': 'https://i.scdn.co/image/ab67616d00001e02d7c84c7a222cec2a28da3fe8',
                      'width': 300,
                      'height': 300
                    },
                    {
                      'url': 'https://i.scdn.co/image/ab67616d00004851d7c84c7a222cec2a28da3fe8',
                      'width': 64,
                      'height': 64
                    },
                    {
                      'url': 'https://i.scdn.co/image/ab67616d0000b273d7c84c7a222cec2a28da3fe8',
                      'width': 640,
                      'height': 640
                    }
                  ]
                },
                'id': '62MDj5jYbhMvYxoaqyu1yw',
                'sharingInfo': {
                  'shareUrl': 'https://open.spotify.com/album/62MDj5jYbhMvYxoaqyu1yw?si=2L1clZzkRZuj0Jv12XfDDg'
                }
              },
              'artists': {
                'items': [
                  {
                    'uri': 'spotify:artist:4MCBfE4596Uoi2O4DtmEMz',
                    'profile': {
                      'name': 'Juice WRLD'
                    }
                  }
                ]
              },
              'contentRating': {
                'label': 'NONE'
              },
              'duration': {
                'totalMilliseconds': 133250
              },
              'playability': {
                'playable': True
              }
            }
          },
          {
            'track': {
              'uri': 'spotify:track:7lQ8MOhq6IN2w8EYcFNSUk',
              'id': '7lQ8MOhq6IN2w8EYcFNSUk',
              'name': 'Without Me',
              'album': {
                'uri': 'spotify:album:2cWBwpqMsDJC1ZUwz813lo',
                'name': 'The Eminem Show',
                'coverArt': {
                  'sources': [
                    {
                      'url': 'https://i.scdn.co/image/ab67616d00001e026ca5c90113b30c3c43ffb8f4',
                      'width': 300,
                      'height': 300
                    },
                    {
                      'url': 'https://i.scdn.co/image/ab67616d000048516ca5c90113b30c3c43ffb8f4',
                      'width': 64,
                      'height': 64
                    },
                    {
                      'url': 'https://i.scdn.co/image/ab67616d0000b2736ca5c90113b30c3c43ffb8f4',
                      'width': 640,
                      'height': 640
                    }
                  ]
                },
                'id': '2cWBwpqMsDJC1ZUwz813lo',
                'sharingInfo': {
                  'shareUrl': 'https://open.spotify.com/album/2cWBwpqMsDJC1ZUwz813lo?si=YYnGDQXuSH-vyKa0D3C2kw'
                }
              },
              'artists': {
                'items': [
                  {
                    'uri': 'spotify:artist:7dGJo4pcD2V6oG8kP0tJRR',
                    'profile': {
                      'name': 'Eminem'
                    }
                  }
                ]
              },
              'contentRating': {
                'label': 'EXPLICIT'
              },
              'duration': {
                'totalMilliseconds': 290320
              },
              'playability': {
                'playable': True
              }
            }
          }
        ]
      },
      'users': {
        'totalCount': 1000,
        'items': [
          {
            'name': 'Eminem',
            'uri': 'spotify:user:eminem',
            'id': 'eminem',
            'username': 'eminem',
            'image': {
              'smallImageUrl': 'https://i.scdn.co/image/ab67757000003b8264f3e220576dd5e62218e751',
              'largeImageUrl': 'https://i.scdn.co/image/ab6775700000ee8564f3e220576dd5e62218e751'
            }
          },
          {
            'name': 'Eminem',
            'uri': 'spotify:user:eminemmmlp2',
            'id': 'eminemmmlp2',
            'username': 'eminemmmlp2',
            'image': {
              'smallImageUrl': None,
              'largeImageUrl': None
            }
          },
          {
            'name': 'Eminem',
            'uri': 'spotify:user:knpkotm9ro4cpf10m7qad0dds',
            'id': 'knpkotm9ro4cpf10m7qad0dds',
            'username': 'knpkotm9ro4cpf10m7qad0dds',
            'image': {
              'smallImageUrl': 'https://i.scdn.co/image/ab67757000003b82bc719dd2c417d911217400d5',
              'largeImageUrl': 'https://i.scdn.co/image/ab6775700000ee85bc719dd2c417d911217400d5'
            }
          },
          {
            'name': 'eminemma12',
            'uri': 'spotify:user:eminemma12',
            'id': 'eminemma12',
            'username': 'eminemma12',
            'image': {
              'smallImageUrl': None,
              'largeImageUrl': None
            }
          },
          {
            'name': 'EMINEM',
            'uri': 'spotify:user:4c3bx35l8dv00x93a93mkqyhr',
            'id': '4c3bx35l8dv00x93a93mkqyhr',
            'username': '4c3bx35l8dv00x93a93mkqyhr',
            'image': {
              'smallImageUrl': 'https://i.scdn.co/image/ab67757000003b82415a0495053809f5653bea98',
              'largeImageUrl': 'https://i.scdn.co/image/ab6775700000ee85415a0495053809f5653bea98'
            }
          }
        ]
      }
    }
  }
}
```

