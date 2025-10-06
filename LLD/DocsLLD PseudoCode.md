

class DocumentElement():
    def render():
        pass

def TextElement : DocumentElement :
    def render():
        print("Render Text document")

def ImageElement: DocumentElement:
    def render():
        print("Image written")



class Document:
    vector<DocumentElement> dc

    def add_element(DocumentElement ele):
        dc.append(ele)

    def render():
        all = []
        for ele in dc:
            ## whether its text or image
            all+=ele.render()
        return all

def persistence:
    def save():
        pass

def SaveToSql: persistence:
    def save():
        print("Data is saved to SQL")

def SaveToMongoDB: persistence:
    def save():
        print("Data is saved to MongoDB")


class DocumentEditor:
    document doc;
    persistence db;

    def add_text(string data):
        doc.add_element(new TextElement(data))
    def image(string path):
        doc.add_element(new ImageElement(data))

    def save():
        db.save(doc.render())
        
    def render():
        return doc.render()


