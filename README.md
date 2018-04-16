# good-practices

To send the binary data across network in hex format: 

import pickle, json
from sklearn.feature_extraction.text import TfidfVectorizer
corpus = ["This is very strange",
          "This is very nice"]
vectorizer = TfidfVectorizer(min_df=1)
X = vectorizer.fit_transform(corpus)

jm_data = {"vectorizer":vectorizer,"vectors":X}
print(jm_data)

input_obj = pickle.dumps(jm_data).hex()
obj = {"owner":"data","binary":input_obj}

resp = json.dump(obj,open("sample.json","w"))
resp = json.load(open("sample.json","r"))

input_obj = pickle.loads(bytes.fromhex(resp["binary"]))
print(str(jm_data)==str(input_obj))
print(input_obj["vectorizer"].transform(["very nice"]))


To check if its base64

def is_base64(orig_base64):
    try:
        regen_base64 = str(base64.b64encode(base64.b64decode(orig_base64)),'utf-8')
        if regen_base64 == orig_base64 and orig_base64[len(orig_base64)-1] == "=":
            return True;
    except Exception as e:
        pass;
    return False;
