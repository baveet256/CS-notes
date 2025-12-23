
`class Robot:`
    `def __init__(self, talk_strategy, walk_strategy, fly_strategy):`
        `self.talk_strategy = talk_strategy` ### Has a relation here
        `self.walk_strategy = walk_strategy` ### Has a relation here
        `self.fly_strategy = fly_strategy` ### Has a relation here

    `def talk(self):`
        `self.talk_strategy.talk()`

`class TalkStrategy:` 
    `def talk(self): pass`

`class NormalTalk(TalkStrategy):` 
    `def talk(self): print("Speaking normally")`

`class SilentTalk(TalkStrategy):` 
    `def talk(self): print("Silent mode")`

`robot = Robot(NormalTalk(), None, None)`
`robot.talk()  # Speaking normally`