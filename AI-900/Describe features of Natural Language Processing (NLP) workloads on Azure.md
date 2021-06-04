## Identify features of common NLP Workload Scenarios

### Identify features and uses for key phrase extraction

You might read some text and identify some key phrases that indicate the main talking points of the text.

### Identify features and uses for entity recognition

You might recognize names of people or well-known landmarks such as the Eiffel Tower.

### Identify features and uses for sentiment analysis

You might also be able to get a sense for how the person was feeling when they wrote the text

### Identify features and uses for language understanding

As artificial intelligence (AI) grows ever more sophisticated, this kind of conversational interaction with applications and digital assistants is becoming more and more common, and in specific scenarios can result in human-like interactions with AI agents. Common scenarios for this kind of solution include customer support applications, reservation systems, and home automation among others.

To work with Language Understanding, you need to take into account three core concepts: utterances, entities, and intents.

- **Utterances**: An utterance is an example of something a user might say, and which your application must interpret.
- **Entities**: An entity is an item to which an utterance refers.
- **Intents**: An intent represents the purpose, or goal, expressed in a user's utterance.

| Intent | Related Utterances | Entities |
|-|-|-|
|TurnOn|"Switch the fan on"|fan (device)|
||"Turn the light on"|light (device)|
||"Turn on the light"|light (device)|
|TurnOff|"Switch the fan off"|fan (device)|
||"Turn the light off"|light (device)|
||"Turn off the light"|light (device)|

### Identify features and uses for speech recognition and synthesis

We expect artificial intelligence (AI) solutions to accept vocal commands and provide spoken responses.
To enable this kind of interaction, the AI system must support two capabilities:

- **Speech recognition**: the ability to detect and interpret spoken input.
- **Speech synthesis**: the ability to generate spoken output.

#### Speech recognition

Speech patterns are analyzed in the audio to determine recognizable patterns that are mapped to words. To accomplish this feat, the software typically uses multiple types of model, including:

- An **acoustic model** that converts the audio signal into **phonemes**(representations of specific sounds).
- A **language model** that maps phonemes to words, usually using a statistical algorithm that predicts the most probable **sequence of words based on the phonemes**.

##### Use-cases

- Providing closed captions for recorded or live videos
- Creating a transcript of a phone call or meeting
- Automated note dictation
- Determining intended user input for further processing

#### Speech synthesis

Speech synthesis is in many respects the reverse of speech recognition.

A speech synthesis solution typically requires the following information:

- The text to be spoken.
- The voice to be used to vocalize the speech.

To synthesize speech, the system typically **tokenizes** the text to break it down into individual words, and assigns phonetic sounds to each word.
It then breaks the phonetic transcription into **prosodic** units (such as phrases, clauses, or sentences) to create phonemes that will be converted to audio format.

##### Use-cases

- Generating spoken responses to user input.
- Creating voice menus for telephone systems.
- Reading email or text messages aloud in hands-free scenarios.
- Broadcasting announcements in public locations, such as railway stations or airports.

### Identify features and uses for translation

As organizations and individuals increasingly need to collaborate with people in other cultures and geographic locations, the removal of language barriers has become a significant problem.

Early attempts at machine translation applied **literal translations**. A literal translation is where **each word is translated to the corresponding word in the target language.**

A translation service should take into account the **semantic context**

#### Text translation

Text translation can be used to translate documents from one language to another, translate email communications that come from foreign governments, and even provide the ability to translate web pages on the Internet.

#### Speech translation

Speech translation is used to translate between spoken languages, sometimes directly (speech-to-speech translation) and sometimes by translating to an intermediary text format (speech-to-text translation).

## Identify Azure tools and services for NLP workloads

### Identify capabilities of the Text Analytics service

In Microsoft Azure, the Text Analytics cognitive service can help simplify application development by using pre-trained models that can:

- Determine the language of a document or text (for example, French or English).
- Perform sentiment analysis on text to determine a positive or negative sentiment.
- Extract key phrases from text that might indicate its main talking points.
- Identify and categorize entities in the text. Entities can be people, places, organizations, or even everyday items such as dates, times, quantities, and so on.

You can choose to provision either of the following types of resource:

- A **Text Analytics** resource - choose this resource type if you only plan to use the Text Analytics service, or if you want to manage access and billing for the resource separately from other services.
- A **Cognitive Services**  resource - choose this resource type if you plan to use the Text Analytics service in combination with other cognitive services, and you want to manage access and billing for these services together.

#### Language detection

For each document submitted to it, the service will detect:

- The language name (for example "English").
- The ISO 6391 language code (for example, "en").
- A score indicating a level of confidence in the language detection.

Ambiguous or mixed language content

There may be text that is ambiguous in nature, or that has mixed language content. For example, using the service to analyze the text ":-)", results in a value of unknown for the language name and the language identifier, and a score of NaN (which is used to indicate not a number).

#### Sentiment analysis

The Text Analytics service can evaluate text and return sentiment scores and labels for each sentence. This capability is useful for detecting positive and negative sentiment in social media, customer reviews, discussion forums and more.

Using the pre-built machine learning classification model, the service evaluates the text and returns a sentiment score in the range of 0 to 1, **with values closer to 1 being a positive sentiment**.

##### Indeterminate sentiment

A score of 0.5 might indicate that the sentiment of the text is indeterminate, and could result from text that does not have sufficient context to discern a sentiment or insufficient phrasing.

#### Key phrase extraction

Key phrase extraction is the concept of evaluating the text of a document, or documents, and then identifying the main talking points of the document(s).

#### Entity recognition

You can provide the Text Analytics service with unstructured text and it will return a list of entities in the text that it recognizes.

### Identify capabilities of the Language Understanding service (LUIS)

For each of the authoring and prediction tasks, you need a resource in your Azure subscription. You can use the following types of resource:

- **Language Understanding**: A dedicated resource for Language Understanding, which can be either an authoring or a prediction resource.
- **Cognitive Services**: A general cognitive services resource that includes Language Understanding along with many other cognitive services. You can only use this type of resource for prediction.

#### Authoring

Language Understanding provides a comprehensive collection of prebuilt **domains** that include pre-defined intents and entities for common scenarios

##### Creating intents

Define intents based on actions a user would want to perform with your application.

##### Creating entities

There are four types of entities:

- **Machine-Learned**: Entities that are learned by your model during training from context in the sample utterances you provide.
- **List**: Entities that are defined as a hierarchy of lists and sublists. For example, a device list might include sublists for light and fan. For each list entry, you can specify synonyms, such as lamp for light.
- **RegEx**: Entities that are defined as a regular expression that describes a pattern - for example, you might define a pattern like [0-9]{3}-[0-9]{3}-[0-9]{4} for telephone numbers of the form 555-123-4567.
- **Pattern.any**: Entities that are used with patterns to define complex entities that may be hard to extract from sample utterances.

##### Training the model

After you have defined the intents and entities in your model, and included a suitable set of sample utterances; the next step is to train the model.

#### Predicting

When you are satisfied with the results from the training and testing, you can publish your Language Understanding application to a prediction resource for consumption.

### Identify capabilities of the Speech service

The Speech service is the unification of:

- **Speech-to-text**
- **Text-to-speech**
- **Speech-translation**

Here are the services and features:

|Service|Feature|Description|
|-|-|-|
|*Speech-to-Text*|*Real-time Speech-to-text*|Speech-to-text transcribes or **translates audio streams or local files to text in real time** that your applications, tools, or devices can consume or display. Use speech-to-text with Language Understanding (LUIS) to derive user intents from transcribed speech and act on voice commands.|
|*Speech-to-Text*|*Batch Speech-to-Text*|Batch Speech-to-text enables **asynchronous speech-to-text transcription of large volumes of speech audio data stored in Azure Blob Storage**. In addition to converting speech audio to text, Batch Speech-to-text also allows for diarization and sentiment-analysis.|
|*Speech-to-Text*|*Multi-device Conversation*|Connect multiple devices or clients in a conversation to send speech- or text-based messages, with easy support for transcription and translation|
|*Speech-to-Text|*Conversation Transcription*|Enables real-time speech recognition, speaker identification, and diarization. It's perfect for transcribing in-person meetings with the ability to distinguish speakers.|
|*Speech-to-Text*|*Create Custom Speech Models*|If you are using speech-to-text for recognition and transcription in a unique environment, you can create and train custom acoustic, language, and pronunciation models to address ambient noise or industry-specific vocabulary.|
|*Text-to-Speech*|*Text-to-speech*|Text-to-speech converts input text into human-like synthesized speech using Speech Synthesis Markup Language (SSML). Use neural voices, which are human-like voices powered by deep neural networks. See Language support.|
|*Text-to-Speech*|*Create Custom Voices*|Create custom voice fonts unique to your brand or product.|
|*Speech Translation*|*Speech translation*|Speech translation enables real-time, multi-language translation of speech to your applications, tools, and devices. Use this service for speech-to-speech and speech-to-text translation.|
|*Voice assistants*|*Voice assistants*|Voice assistants using the Speech service empower developers to create natural, human-like conversational interfaces for their applications and experiences. The voice assistant service provides fast, reliable interaction between a device and an assistant implementation that uses the Bot Framework's Direct Line Speech channel or the integrated Custom Commands service for task completion.|
|*Speaker Recognition*|*Speaker verification & identification*|The Speaker Recognition service provides algorithms that verify and identify speakers by their unique voice characteristics. Speaker Recognition is used to answer the question “who is speaking?”.|

To use the Speech service in an application, you must provision an appropriate resource in your Azure subscription. You can choose to provision either of the following types of resource:

- A **Speech** resource - choose this resource type if you only plan to use the Speech service, or if you want to manage access and billing for the resource separately from other services.
- A **Cognitive Services** resource - choose this resource type if you plan to use the Speech service in combination with other cognitive services, and you want to manage access and billing for these services together.

### Identify capabilities of the Translator Text service

Microsoft Azure provides cognitive services that support translation. Specifically, you can use the following services:

- The **Translator Text** service, which supports text-to-text translation.
- The **Speech service**, which enables speech-to-text and speech-to-speech translation.

Alternatively, you can create a **Cognitive Services** resource that provides access to both services through a single Azure resource, consolidating billing and enabling applications to access both services through a single endpoint and authentication key.

#### Text translation with the Translator Text service

The service uses a Neural Machine Translation (NMT) model for translation, which analyzes the semantic context of the text and renders a more accurate and complete translation as a result.

The Text Translator service supports **text-to-text translation between more than 60 languages**.

When using the service, you must specify the language you are translating **from** and the language you are translating **to** using ISO 639-1 language codes.

Alternatively, you can specify cultural variants of languages by extending the language code with the appropriate 3166-1 cultural code - for example, en-US for US English, en-GB for British English

When using the Text Translator service, you can specify one from language with **multiple to** languages.

Note that the Translator Text API offers some optional configuration:

- *Profanity filtering*: Without any configuration, the service will translate the input text, without filtering out profanity.
- *Selective translation*: You can tag content so that it isn't translated. For example, you may want to tag code, a brand name, or a word/phrase that doesn't make sense when localized.

#### Speech translation with the Speech service

The Speech service includes the following application programming interfaces (APIs):

- **Speech-to-text**: used to transcribe speech from an audio source to text format.
- **Text-to-speech**: used to generate spoken audio from a text source.
- **Speech Translation**: used to translate speech in one language to text or speech in another.
