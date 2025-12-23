
from abc import ABC, abstractmethod


class TalkStrategy(ABC):
    @abstractmethod
    def talk(self):
        pass

class NormalTalk(TalkStrategy):
    def talk(self):
        print("Normal Talking")

class FastTalk(TalkStrategy):
    def talk(self):
        print("Fast Talking")

class FlyStrategy(ABC):
    @abstractmethod
    def fly(self):
        pass

class FastFly(FlyStrategy):
    def fly(self):
        print("Fast fly")

class NoFly(FlyStrategy):
    def fly(self):
        print("No Fly")
        

class Robot(ABC):
    def __init__(self,talk,fly):
        self.talk_strategy = talk
        self.fly_strategy = fly
    
    def talk(self):
        self.talk_strategy().talk()
        return
    def fly(self):
        self.fly_strategy().fly()
        return


myrobot = Robot(FastTalk,NoFly)
myrobot.talk()
myrobot.fly()


myrobot2 = Robot(NormalTalk,FastFly)
myrobot2.talk()
myrobot2.fly()


    


