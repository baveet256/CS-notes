
`class Robot:`
    `def __init__(self, talk_strategy, walk_strategy, fly_strategy):`
        `self.talk_strategy = talk_strategy`
        `self.walk_strategy = walk_strategy`
        `self.fly_strategy = fly_strategy`

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