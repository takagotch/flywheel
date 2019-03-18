### flywheel
---
https://github.com/stevearc/flywheel

```py
from flywheel import Model, Field, GlobalIndex

class GameScore(Model):
  __metadata__ = {
    'global_indexes': [
      GlobalIndex('GameTitleIndex', 'title', 'top_score')
    ],
  }
  userid = Field(hash_key=True)
  title = Field(range_key=True)
  top_score = Field(type=datatime)
  top_score_time = Field(type=datatime)
  wins = Field(type=int)
  losses = Field(type=int)
  
  def __init__(self, title, userid):
    self.title = title
    self.userid = userid

score = GameScore('Master Blaster', 'abc')
score.top_score = 9001
score.top_score_time = datetime.utcnow()
engine.sync(score)

scores = engine.query(GameScore).filter(userid='abc').all()

top_score = engine.query(GameScore).filter(title='GalaxyInvaders')\
  .first(desc=True)
  
score = GameScore('Alien Adventure', 'abc')
score.incr_(winds=1)
engine.sync(score)

scores = engine.query(GameScore).filter(GameScore.top_score > 9000,
  title='Comet Quest').all()
```

```
```

```
```


