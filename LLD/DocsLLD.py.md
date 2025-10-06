from abc import ABC, abstractmethod

# ---------- Abstraction Layer for Elements ----------

class DocumentElement(ABC):
    @abstractmethod
    def render(self):
        pass


class TextElement(DocumentElement):
    def __init__(self, text):
        self.text = text

    def render(self):
        print(f"Rendering Text: {self.text}")
        return self.text


class ImageElement(DocumentElement):
    def __init__(self, path):
        self.path = path

    def render(self):
        print(f"Rendering Image from {self.path}")
        return f"<Image:{self.path}>"


# ---------- Document = Composition of Elements ----------

class Document:
    def __init__(self):
        self.elements = []  # has-a relationship

    def add_element(self, element: DocumentElement):
        self.elements.append(element)

    def render(self):
        rendered_output = []
        for ele in self.elements:
            rendered_output.append(ele.render())  # polymorphism at work
        return rendered_output


# ---------- Persistence Layer (Abstraction + Concrete Implementations) ----------

class Persistence(ABC):
    @abstractmethod
    def save(self, data):
        pass


class SaveToSQL(Persistence):
    def save(self, data):
        print("Saving to SQL:", data)


class SaveToMongoDB(Persistence):
    def save(self, data):
        print("Saving to MongoDB:", data)


# ---------- Document Editor (Composition of Document + Persistence) ----------

class DocumentEditor:
    def __init__(self, db: Persistence):
        self.doc = Document()
        self.db = db  # has-a relationship (Strategy pattern)

    def add_text(self, data: str):
        self.doc.add_element(TextElement(data))

    def add_image(self, path: str):
        self.doc.add_element(ImageElement(path))

    def save(self):
        rendered = self.doc.render()
        self.db.save(rendered)

    def render(self):
        return self.doc.render()


# ---------- Example Usage ----------

if __name__ == "__main__":
    sql_saver = SaveToSQL()
    editor = DocumentEditor(sql_saver)

    editor.add_text("Hello World")
    editor.add_image("/path/to/image.png")

    print("\nDocument Render:")
    print(editor.render())

    print("\nSaving Document:")
    editor.save()
