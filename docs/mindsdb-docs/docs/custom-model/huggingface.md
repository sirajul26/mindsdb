# MindsDB and HuggingFace

HuggingFace facilitates building, training, and deploying ML models.

## How to Bring the HuggingFace Model to MindsDB

We use the `#!sql CREATE PREDICTOR` statement to bring the HuggingFace models to MindsDB.

Let's go through some sample models.

### Model 1: Spam Classifier

Here is an example of a binary classification. The model determines whether a text string is a spam or not.


```sql
-- TODO (fix the code)
CREATE PREDICTOR huggingface.spam_classifier
PREDICT PRED
USING
   task='text-classification',
   model_name= 'mrm8488/bert-tiny-finetuned-sms-spam-detection',
   input_column = 'text_spammy',
   labels=['ham','spam'];
```

On execution, we get:

```sql
TODO
```

Before querying for predictions, we should verify the status of the `spam_classifier` model.

```sql
-- TODO (fix the code)
select * from huggingface.predictors;
```

On execution, we get:

```sql
TODO
```

Once the status is `complete`, we can query for predictions.

```sql
-- TODO (fix the code)
SELECT  h.*,
       t.text_spammy as input_text
FROM files.df_test as t
JOIN huggingface.spam_classifier as h;
```

On execution, we get:

```sql
TODO
```

### Model 2: Sentiment Classifier

Here is an example of a multi-value classification. The model determines a sentiment of a text string, where possible values are negative (`neg`), neutral (`neu`), and positive (`pos`).

```sql
-- TODO (fix the code)
CREATE MODEL mindsdb.sentiment_classifier
PREDICT PREDM
USING
    engine='huggingface',
    task='text-classification',
    model_name= "cardiffnlp/twitter-roberta-base-sentiment",
    input_column = 'text_short',
    labels=['neg','neu','pos'];
```

On execution, we get:

```sql
TODO
```

Before querying for predictions, we should verify the status of the `sentiment_classifier` model.

```sql
-- TODO (fix the code)
SELECT * FROM mindsdb.models WHERE name='sentiment_classifier';
```

On execution, we get:

```sql
TODO
```

Once the status is `complete`, we can query for predictions.

```sql
-- TODO (fix the code)
SELECT h.PREDM
FROM huggingface.sentiment_classifier as h
WHERE text_short='It is the best time to launch the Robot to get more money. https:\\/\\/Gof.bode-roesch.de\\/Gof';
```

On execution, we get:

```sql
TODO
```

### Model 3: Zero-Shot Classifier

Here is an example of a zero-shot classification. The model determines to which of the defined categories a text string belongs.

```sql
-- TODO (fix the code)
CREATE PREDICTOR huggingface.zero_shot_tcd
PREDICT topic
USING
   task='zero-shot-classification',
   model_name= 'facebook/bart-large-mnli',
   input_column = 'text_short',
   candidate_labels=['travel', 'cooking', 'dancing'];
```

On execution, we get:

```sql
TODO
```

Before querying for predictions, we should verify the status of the `zero_shot_tcd` model.

```sql
-- TODO (fix the code)
select * from huggingface.predictors;
```

On execution, we get:

```sql
TODO
```

Once the status is `complete`, we can query for predictions.

```sql
-- TODO (fix the code)
SELECT  h.*,
       t.text_short as input_text
FROM files.df_test as t
JOIN huggingface.zero_shot_tcd as h;
```

On execution, we get:

```sql
TODO
```

### Model 4: Translation

Here is an example of a translation. The model gets an input string in English and translates it into French.

```sql
-- TODO (fix the code)
CREATE PREDICTOR huggingface.translator_en_fr
PREDICT translated
USING
   task = 'translation',
   model_name = 't5-base',
   input_column = 'text_short',
   lang_input = 'en',
   lang_output = 'fr';
```

On execution, we get:

```sql
TODO
```

Before querying for predictions, we should verify the status of the `translator_en_fr` model.

```sql
-- TODO (fix the code)
select * from huggingface.predictors;
```

On execution, we get:

```sql
TODO
```

Once the status is `complete`, we can query for predictions.

```sql
-- TODO (fix the code)
SELECT  h.*,
       t.text_short as input_text
FROM files.df_test as t
JOIN huggingface.translator_en_fr as h;
```

On execution, we get:

```sql
TODO
```

### Model 5: Summarisation

Here is an example of a summarisation.

```sql
-- TODO (fix the code)
CREATE PREDICTOR huggingface.summarizer_10_20
PREDICT text_summary
USING
   task='summarization',
   model_name='sshleifer/distilbart-cnn-12-6',
   input_column = 'text_long',
   min_output_length=10,
   max_output_length=20;
```

On execution, we get:

```sql
TODO
```

Before querying for predictions, we should verify the status of the `summarizer_10_20` model.

```sql
-- TODO (fix the code)
select * from huggingface.predictors;
```

On execution, we get:

```sql
TODO
```

Once the status is `complete`, we can query for predictions.

```sql
-- TODO (fix the code)
SELECT  h.*,
       t.text_long as input_text
FROM files.df_test as t
JOIN huggingface.summarizer_10_20 as h;
```

On execution, we get:

```sql
TODO
```
