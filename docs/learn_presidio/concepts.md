# Concepts in Microsoft Presidio

## High-level concepts

| Concept                  | Definition                                                                                                                                               | Learn More                                                               |
|--------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------|
| **Entity**               | An *entity* is a span of text that can be used to directly identify an individual. For example, a phone number, email address, or social security number. In Presidio, an entity is represented by a **RecognizerResult** object. | [Analyzer concepts](../analyzer/index.md#main-concepts) |
| **Context**              | *Context* is defined as the surrounding text of an entity. Context can be used to provide additional information about the entity which can be used to improve the detection accuracy. | [Analyzer concepts](../analyzer/index.md#main-concepts)                                        |
| **Recognizer**           | A *recognizer* is an object that is responsible for detecting entities in text. Recognizers can be rule-based, machine learning-based, or a combination of both. The Presidio Analyzer orchestrates multiple recognizers to detect PII entities in text. The main objects in Presidio that implement PII detection logic are the **EntityRecognizer** and **PatternRecognizer**. | [Analyzer concepts](../analyzer/index.md#main-concepts) |
| **Analyzer**             | The Presidio `AnalyzerEngine` is responsible for orchestrating the PII detection using various recognizers.| [Analyzer concepts](../analyzer/index.md#main-concepts) |
| **Predefined recognizer** | A recognizer that already exists in Presidio | [Predefined recognizers](../supported_entities.md) |
| **Custom recognizer** | A recognizer that is added by the user | [Adding recognizers](../analyzer/adding_recognizers.md) |
| **ad-hoc recognizer** | A recognizer that is added to the request itself, rather than to the list of recognizers loaded within Presidio | [ad-hoc recognizers](../analyzer/adding_recognizers.md#creating-ad-hoc-recognizers) |
| **Deny list** | A list of terms that should always be identified as PII | [denylist tutorial](../tutorial/01_deny_list.md) |
| **Allow list** | A list of terms that should not be identified as PII | [allowlist tutorial](../tutorial/13_allow_list.md) |

## Main objects in Presidio

| Concept                  | Definition                                                                                                                                               | Learn More                                                               |
|--------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------|
| **EntityRecognizer**      | An **EntityRecognizer** is an object in Presidio that is responsible for detecting entities in text. An entity recognizer can be rule-based, a machine learning model, or a combination of both. | [Analyzer concepts](../analyzer/index.md#main-concepts)                                        |
| **RecognizerResult**      | A **RecognizerResult** holds the type and span of a PII entity.                                                                                          | [Analyzer concepts](../analyzer/index.md#main-concepts)                                        |
| **RecognizerRegistry**    | The **RecognizerRegistry** is a class in Presidio that is responsible for holding the various recognizers used by the **AnalyzerEngine**. | [link](../analyzer/index.md#main-concepts)                                        |
| **NlpEngine**             | The **NlpEngine** is an interface that defines the methods for processing text. Presidio provides several implementations of the **NlpEngine**, such as **SpacyNlpEngine**, **TransformersNlpEngine**, and **StanzaNlpEngine**. | [Analyzer concepts](../analyzer/index.md#main-concepts)                                        |
| **AnalyzerEngine**        | The **AnalyzerEngine** is the main class in Presidio that is responsible for orchestrating the PII detection in text. It uses an **NlpEngine** to process the text and a **RecognizerRegistry** to hold the different recognizers. | [Analyzer concepts](../analyzer/index.md#main-concepts)                                        |
| **BatchAnalyzerEngine**   | The **BatchAnalyzerEngine** is a class in Presidio that is responsible for detecting PII entities in a batch of texts. It uses the **AnalyzerEngine** to process each text in the batch. | [Batch processing sample](../samples/python/batch_processing.ipynb)                                  |
| **AnonymizerEngine**      | The **AnonymizerEngine** is the main class in Presidio that is responsible for anonymizing PII entities in text. It uses the results from the **AnalyzerEngine** to perform the anonymization. | [Anonymizer concepts](../anonymizer/index.md#main-concepts) |
| **DeanonymizerEngine**    | The **DeanonymizerEngine** is a class in Presidio that is responsible for deanonymizing text that has been anonymized by the **AnonymizerEngine**, given that the operation is reversible (e.g. encryption). | [Anonymizer concepts](../anonymizer/index.md#main-concepts) |
| **Operator**              | An **Operator** is an object in Presidio that is responsible for performing the anonymization operation on a PII entity. Presidio provides several built-in operators, such as **Replace**, **Redact**, and **Encrypt**, and allows users to create custom operators. | [Anonymizer concepts](../anonymizer/index.md#main-concepts) |
| **BatchAnonymizerEngine** | The **BatchAnonymizerEngine** is a class in Presidio that is responsible for anonymizing PII entities in a batch of texts. It uses the **AnonymizerEngine** to perform the anonymization on each text in the batch. | [Sample](../samples/python/batch_processing.ipynb)                                  |
| **ImageRedactorEngine**   | The **ImageRedactorEngine** is a class in Presidio that is responsible for redacting PII entities in images. It leverages the **AnalyzerEngine** to detect PII entities in the text extracted from the images. | [Image redaction docs](../image-redactor/index.md)                                               |
| **StructuredEngine**      | The **StructuredEngine** is a class in Presidio that is responsible for detecting PII entities in structured data. It uses the **AnalyzerEngine** to detect PII entities in the text fields of the structured data. | [Image redaction docs](../structured/index.md)                                                  |

## Evaluation concepts

| Concept                  | Definition                                                                                                                                               | Learn More                                                               |
|--------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------|
| **Precision**            | **Precision** is a metric that measures the proportion of true positive results among the positive results. In the context of PII detection, precision measures the proportion of correctly identified PII entities among all the entities identified by the system. | [Evaluation docs](../evaluation/index.md) |
| **Recall**               | **Recall** is a metric that measures the proportion of true positive results among the actual positive results. In the context of PII detection, recall measures the proportion of correctly identified PII entities among all the PII entities present in the text.| [Evaluation docs](../evaluation/index.md) |