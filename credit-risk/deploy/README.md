# Deploy the credit risk app to your server

This folder has all the code required to train the model, predict and run the webapp.

Here are the list of files in this directory:

```
README.md -- this file
credit_grade.py -- finds the credit grade of a person given email
predict.py -- the predict function, depends on model files
rorolite.yml -- rorolite config file to deploy to your own server
train.py -- script to train the ML model
webapp/ -- the webapp to request models
```

How to run locally
------------------

Before you start make sure you are in `deploy` directory.	


1. Train the models

```
$ python train.py
reading the dataset...
replacing missing values with mean...
encoding the columns...
building the model...
saving the models...
  saved ./model.pkl
  saved ./grade-encoder.pkl
  saved ./ownership-encoder.pkl
done
```

2. Run the predict API

```
$ firefly predict.predict
reading ./grade-encoder.pkl
reading ./ownership-encoder.pkl
reading ./model.pkl
http://127.0.0.1:8000/
```

3. Run the webapp

```
$ python webapp/webapp.py
 * Running on http://127.0.0.1:5000/ (Press CTRL+C to quit)
```

4. **Task:** Integrate the predict API into the webapp.

This is an exercise for you.

5. **Bonus Task:** Run `credit_grade.find_credit_grade` as another API and integrate that with the webapp.

How to run remotely
-------------------

1. Open the rorolite.yml file and edit the `host` and `user` to match that of your server.

2. Provision your server if you have not already done.

```
$ rorolite provision
```

3. Deploy your application.

```
$ rorolite deploy
```

4. Your predict API will fail because it does not have models. Run `train.py` to build and save models.

```
$ rorolite run python train.py
```

Since the models are saved only in the current directory, they'll be wiped out on every deploy. Make sure you run train.py after every deploy. This issue can be fixed by changing the value of `MODELS_DIR` in `config.py` to `/volumes/data`.

5. Restart the API after building the models.

```
$ rorolite restart api
```

The API will be available on port 8000 of your server.

6. **Task:** Integrate the model API running on the remote server into the webapp.

7. **Task:** Run the webapp also on the remote server. See `rorolite.yml` for hints.