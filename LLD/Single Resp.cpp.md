class Engine:
    def start(self):
        print("Engine started")

class AudioSystem:
    def play_music(self):
        print("Playing music")

class Sunroof:
    def open(self):
        print("Sunroof open")

class Car:
    def __init__(self):
        self.engine = Engine()       # driving responsibility
        self.audio = AudioSystem()   # audio responsibility
        self.sunroof = Sunroof()     # sunroof responsibility

    def drive(self):
        self.engine.start()
        print("Car is driving")

    def play_music(self):
        self.audio.play_music()

    def open_sunroof(self):
        self.sunroof.open()
