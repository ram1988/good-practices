# good-practices
- To send the binary data across network in hex format:  

```import pickle, json
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
print(input_obj["vectorizer"].transform(["very nice"])) ```


To send the binary data across network in hex format: 

def is_base64(orig_base64):
    try:
        regen_base64 = str(base64.b64encode(base64.b64decode(orig_base64)),'utf-8')
        if regen_base64 == orig_base64 and orig_base64[len(orig_base64)-1] == "=":
            return True;
    except Exception as e:
        pass;
    return False;



To perform the non-session based Authentication mechanism 
and to protect the endpoints

https://docs.nestjs.com/techniques/authentication

For example, if the Auth flow is performed using Google,

1.) Generate your own jwt secret key
2.) Configure that in your program
3.) Prepare your return own user object after Google login, and encrypt using jwt secret (symmetric encryption). It is returned as access token.
4.) Access token needs to be sent in the subsequent API calls
5.) Jwt Auth guard intercepts your request and decrypts using the same secret key. 
If the decryption is successful, then the access token is valid. If not, 404 unauthorized


