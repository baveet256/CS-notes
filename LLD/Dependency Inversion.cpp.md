from abc import ABC, abstractmethod

# Abstraction (Interface)
class Persistence(ABC):
    @abstractmethod
    def save(self, data): pass

# Concrete implementations
class SqlDatabase(Persistence):
    def save(self, data):
        print("Saved to SQL Database")

class MongoDatabase(Persistence):
    def save(self, data):
        print("Saved to MongoDB")

# High-level module depends on abstraction
class App:
    def __init__(self, persistence: Persistence):
        self.persistence = persistence
    
    def store_data(self, data):
        self.persistence.save(data)

# Runtime binding (Dependency Injection)
p = MongoDatabase()    # Parent ref = child obj
app = App(p)
app.store_data("Hello")
