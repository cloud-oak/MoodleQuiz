
<a id='MoodleQuiz-Documentation-1'></a>

# MoodleQuiz Documentation

- [MoodleQuiz Documentation](index.md#MoodleQuiz-Documentation-1)
    - [Types](index.md#Types-1)
    - [Functions](index.md#Functions-1)
    - [Enums](index.md#Enums-1)
    - [Index](index.md#Index-1)


<a id='Types-1'></a>

## Types


The main type of this module is `Quiz`, which contains all the information of a Moodle Quiz.

<a id='MoodleQuiz.Quiz' href='#MoodleQuiz.Quiz'>#</a>
**`MoodleQuiz.Quiz`** &mdash; *Type*.



```
Quiz(Questions::Vector{Question};Category::AbstractString="")
```

Creates a `Quiz` consisting of the supplied `Question`s with the given category.


<a target='_blank' href='https://github.com/cloud-oak/MoodleQuiz/tree/296ab87e4714763a801822aff51f2219cd59a502/src/MoodleQuiz.jl#L566-L570' class='documenter-source'>source</a><br>


So essentially a `Quiz` is just a collection of `Question`s, which `Question` defined as follows.

<a id='MoodleQuiz.Question' href='#MoodleQuiz.Question'>#</a>
**`MoodleQuiz.Question`** &mdash; *Type*.



```
Question(type; optional arguments)
```

Contstructor for Question type using named parameters

**Arguments**

  * `type::QuestionType`             : see `QustionType` for possible options
  * `Name::MoodleText=""`            : title of the question
  * `Text::MoodleText=""`            : text containing the actual question
  * `GeneralFeedback::MoodleText=""` : this text is always shown after the question has been answered
  * `CorrectFeedback::MoodleText="Die Antwort ist richtig."` : this text is shown after the question has been answered corectly
  * `PartiallyCorrectFeedback::MoodleText="Die Antwort ist teilweise richtig."` : this text is shown after the question has been partially correctly answered.
  * `IncorrectFeedback::MoodleText="Die Antwort ist falsch."` : this text is shown if the question has been answered incorrectly
  * `DefaultGrade::Int=1`            : not sure ... probably points awarded if the question is answered correctly in the first attempt
  * `Penalty::Float32=1/3`           : not sure ... probably the points awarded for a correct answer is calculated by `DefaultGrade * Penalty` if the student failed to provide the correct answer in the first attempt
  * `Hidden::Int=0`                  : not sure ... maybe hidden questions cannot be seen by students?
  * `Single::Bool=true`              : not sure ... not idea
  * `ShuffleAnswers::Bool=true`      : decides if answers of questions will be randomly shuffled by Moodle
  * `AnswerNumbering::String`="none" : decides how answers of questions should be labeled, e.g. 1. 2. ... or a),b) ... Labels are disabled by default.
  * `Answers::Answer=[]`             : `Answer`s for this question


<a target='_blank' href='https://github.com/cloud-oak/MoodleQuiz/tree/296ab87e4714763a801822aff51f2219cd59a502/src/MoodleQuiz.jl#L312-L330' class='documenter-source'>source</a><br>


A `Question` must have an `Array` of `Answer`s.

<a id='MoodleQuiz.Answer' href='#MoodleQuiz.Answer'>#</a>
**`MoodleQuiz.Answer`** &mdash; *Type*.



```
Answer(text; optional arguments)
```

Contstructor for Question type using named parameters

**Arguments**

  * `Text::MoodleText=""`     : text containing the actual question
  * `Correct::Int=1`          : shortcut for setting wether this answer is correct or not
  * `Fraction::Int=100`       : `Fraction * Correct /100 * (DefaultGrade of Question)` Points are awarded to the student if this answer is chosen
  * `Feedback::MoodleText=""` : this text is always shown after the question has been answered


<a target='_blank' href='https://github.com/cloud-oak/MoodleQuiz/tree/296ab87e4714763a801822aff51f2219cd59a502/src/MoodleQuiz.jl#L335-L344' class='documenter-source'>source</a><br>


<a id='Functions-1'></a>

## Functions

<a id='MoodleQuiz.exportXML' href='#MoodleQuiz.exportXML'>#</a>
**`MoodleQuiz.exportXML`** &mdash; *Function*.



```
exportXML(quiz)
```

returns a string with the quiz in Moodle XML format


<a target='_blank' href='https://github.com/cloud-oak/MoodleQuiz/tree/296ab87e4714763a801822aff51f2219cd59a502/src/MoodleQuiz.jl#L602-L606' class='documenter-source'>source</a><br>


```
exportXML(quiz,filename::AbstractString)
```

writes the quiz in Moodle XML format to the given file


<a target='_blank' href='https://github.com/cloud-oak/MoodleQuiz/tree/296ab87e4714763a801822aff51f2219cd59a502/src/MoodleQuiz.jl#L612-L616' class='documenter-source'>source</a><br>


<a id='Enums-1'></a>

## Enums

<a id='MoodleQuiz.QuestionType' href='#MoodleQuiz.QuestionType'>#</a>
**`MoodleQuiz.QuestionType`** &mdash; *Type*.



Moodle supports the following types of questions

| Type                       | Description                                                                                                |
|:-------------------------- |:---------------------------------------------------------------------------------------------------------- |
| MultipleChoice             | standard multiple choice question                                                                          |
| AllOrNothingMultipleChoice | multiple choice question, where all correct and no false answers have to be selected to recieve any points |
| TrueFalse                  | simple yes / no question                                                                                   |
| ShortAnswer                | not yet implemented                                                                                        |
| Matching                   | not yet implemented                                                                                        |
| EmbeddedAnswers            | answer fields / options are embedded in question text                                                      |
| Essay                      | not yet implemented                                                                                        |
| Numerical                  | not yet implemented                                                                                        |
| Description                | not yet implemented                                                                                        |
| CalculatedSimple           | not yet implemented                                                                                        |
| DragAndDrop                | not yet implemented                                                                                        |
| DragAndDropMatch           | not yet implemented                                                                                        |
| STACK                      | Uses the Maxima CAS engine to check algebraic correctness of solution                                      |


<a target='_blank' href='https://github.com/cloud-oak/MoodleQuiz/tree/296ab87e4714763a801822aff51f2219cd59a502/src/MoodleQuiz.jl#L18-L36' class='documenter-source'>source</a><br>

<a id='MoodleQuiz.MoodleTextFormat' href='#MoodleQuiz.MoodleTextFormat'>#</a>
**`MoodleQuiz.MoodleTextFormat`** &mdash; *Type*.



Text in a moodle quiz can have one of the following formats

| Format           | Descriction                                                                                                             |
|:---------------- |:----------------------------------------------------------------------------------------------------------------------- |
| Html             |                                                                                                                         |
| MoodleAutoFormat | some keywords as e.g. true / false will be automatically translated to the language of the moodle user viewing the quiz |
| PlainText        |                                                                                                                         |
| Markdown         |                                                                                                                         |


<a target='_blank' href='https://github.com/cloud-oak/MoodleQuiz/tree/296ab87e4714763a801822aff51f2219cd59a502/src/MoodleQuiz.jl#L57-L66' class='documenter-source'>source</a><br>


<a id='Index-1'></a>

## Index

- [`MoodleQuiz.Answer`](index.md#MoodleQuiz.Answer)
- [`MoodleQuiz.MoodleTextFormat`](index.md#MoodleQuiz.MoodleTextFormat)
- [`MoodleQuiz.Question`](index.md#MoodleQuiz.Question)
- [`MoodleQuiz.QuestionType`](index.md#MoodleQuiz.QuestionType)
- [`MoodleQuiz.Quiz`](index.md#MoodleQuiz.Quiz)
- [`MoodleQuiz.exportXML`](index.md#MoodleQuiz.exportXML)

