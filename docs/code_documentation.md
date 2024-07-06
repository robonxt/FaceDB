# FaceDB object initialization

### FaceResult

#### Parameters
```
id
name
distance
embedding
img
```
#### Methods

##### show_img()
Convenient way to see the image that is in your FaceResults object. Open a matplotlib window 

### FaceResults

#### Parameters
Note that the following parameters are only going to be accessile if you just have and FaceResult in your object FaceResults
```
id
name
distance
embedding
img
```
#### Methods

##### show_img()
Convenient way to see the images that is in your FaceResults object. Open a matplotlib window 

# Main features of FaceDB

### FaceDB.add(name:str,img=None,embedding=None,id=None,check_similar=True,save_just_face=False,**kwargs: Additional metadata for the face.)
Give you the possibility to add a new entry in our FaceDB database.  
Example : 
```
db.add("Nelson Mandela", img="mandela.jpg", profession="Politician", country="South Africa")
db.add("Barack Obama", img="obama.jpg", profession="Politician", country="USA")
db.add("Einstein", img="einstein.jpg", profession="Scientist", country="Germany")
```

### FaceDB.add_many(embeddings=None,imgs=None,metadata=None,ids=None,names=None,check_similar=True)
Give you the possibility to add several new entries in our FaceDB database at one time.   
Example :
```
files = glob("faces/*.jpg") # Suppose you have a folder with imgs with names as filenames
imgs = []
names = []
for file in files:
    imgs.append(file)
    names.append(Path(file).name)

ids, failed_indexes = db.add_many(
    imgs=imgs,
    names=names,
)
```

### FaceDB.recognize(img=None, embedding=None, include=None, threshold=None, top_k=1) -> False|None|FaceResults
Try to find the name of the personne within the picture.   
Example:
```
result = db.recognize(img="your_image.jpg")
```
### FaceDB.all(include=None) -> FaceResults
Retrieve information about all faces in the database.   
Example:
```
results = db.all(include='name')
#Or with a list
results = db.all(include=['name', 'img']) 
```
### FaceDB.all().df -> pd.DataFrame
Easy to get your result in a Pandas DataFrame.   
Example:
```
df = db.all().df
```

### FaceDB.search(embedding,include) -> FaceResults
Search for similar faces based on the image you provided.   
Example:
```
results = db.search(img="your image.jpg")
```
### FaceDB.get_all(include) -> FaceResults
Get all the faces of the db according on the parameters you want.   
Example:
```
results = db.get_all(include=['name', 'img'])
``` 
### FaceDB.update(id, name=None, embedding=None, img=None, only_face=False)
Update value in your db.   
Example:
```
db.update(id=face_id, name="John Doe", img="john_doe.jpg") 
```
### FaceDB.delete(id)
Delete one element in the database.   
Example:
```
db.delete(face_id)
```
### Face.count() -> int
Count the number of faces in the database.   
Example:
```
count = db.count()
```
### Face.query(embeddings,top_k=1,include: Optional[List[Literal["embeddings", "metadatas"]]] = None,where=None,)) -> FaceResults
Make a query to the database and get the result of the db.   
Example:
```
results = db.query(name="Nelson Mandela")
```
