# Best practices for preparing XLIFF files

[comment]: <> (Your organization knows that you must prepare your content for translation in the XLIFF format. As your organization's lead engineer, you meet the technical requirements and know how to deal with the XML metalanguage to produce well-formed and valid, therefore interoperable XLIFF files that the linguists' translation editor can open.)

[comment]: <> (However, you might be preparing your organization's content in a way that makes translation and review more difficult than they should be, or even a nightmare, because you might not be aware of some localization and internationalization sensitive issues and might be working things around to comply with the XLIFF standard without applying best practices that do take into account the translator’s perspective.)

[comment]: <> (In cApStAn we like to intervene and advise from an early stage, sharing our translation and internationalization know-how, even before the source content is conceived and typeset, to make sure our partners' engineers craft good XLIFF files that our linguists will not struggle with.)

## Introduction

This report includes recommendations for preparing content for translation in the XLIFF format with a view to producing XLIFF files that optimize the different language tasks and language asset management both in the short and the long run. It also focuses on issues that can be problematic for language experts and how those issues can be avoided.

To illustrate the DO's and DON'T's, one OmegaT <span id="a1">[[1]](#1)</span> project is provided, containing:

  * the original files (XML, HTML, SVG, etc.), in folder `original`
  * the problematic prepared XLIFF files, in folder `source/01_haram`
  * the optimal prepared XLIFF files, in folder `source/02_halal`

This is the file structure in the project:

    xliff_bestpractices_omtprj (project)
        + original (source content)
            + 02_halal
                - entities.html
                - markup_custom_xml
                - markup_inline.svg
                - markup_input.html
                - markup_span.html
                - segment_para.html
        + source (prepared files for translation)
            + 01_haram (problematic)
                - entities.html.xlf
                - markup_custom_xml.xlf
                - markup_inline.svg.xlf
                - markup_input.html.xlf
                - markup_span.html.xlf
                - segment_para.html.xlf
            + 02_halal (recommended)
                - entities.html.xlf
                - markup_custom_xml.xlf
                - markup_inline.svg.xlf
                - markup_input.html.xlf
                - markup_span.html.xlf
                - segment_para.html.xlf

You can open the XLIFF files and look at them in an XML editor, but probably the best way to see the impact of the different preparation is to open the project in OmegaT and compare each _haram_ file with its corresponding _halal_ files. The project can be downloaded twice with different names and two instances of OmegaT can be run simultaneously for a handier comparison.

To open the project in OmegaT:

[comment]: <> (Download and install our custom version of OmegaT: http:_cat.capstan.be/OmegaTcp_installer.exe)

  - Install and customize OmegaT as per our [installation and customization guide](https:_slides.com/capstan/omegat-installation-and-customization-guide/fullscreen) <span id="a1">[[2]](#2)</span>
  - Go to     **Project** >     **Download team project** and enter the following details:
    - url: `http:_svn.capstan.be/testproject1/xliff_bestpractices_omtprj`
	- credentials: `capstanview` (username) / `cApStAn2016` (password)
	- your preferred path to your local copy of the project.

That will create a local version of the project for you and will open it. You can click on the different files in the project files window to display the different content in the translation editor.

The Okapi project, including the settings files, can also be downloaded from `http://cat.capstan.be/xliff_bestpractices_okpprj.zip`, although this is not necessary unless you want to recreate or customize the extraction process. To (re)create the XLIFF files, the `rnb` file must be open from Okapi Rainbow.

In this document, the notation of including text between square brackets indicates a segment as the linguist sees it in the translation editor, e.g. \[This is a segment\].

## Requirements

The only strict requirement is to create well-formed and valid XLIFF files, according to the XLIFF specification <span id="a3">[[3]](#3)</span>. Created XLIFF files can be validated with the strict XML schema <span id="a4">[[4]](#4)</span> or using the XLIFF Checker <span id="a5">[[5]](#5)</span>.

However, it is possible to produce XLIFF files that are compliant with the XLIFF standard as required but that are not translation-friendly. The main purpose of this report is to promote certain best practices, upon which the following recommendations are based.

## Recommendations

Based on the localization industry's best practices for preparing files for translation and on our experience in localization of questionnaires and cognitive assessments, we can define a number of important recommendations:

  * Text must be segmented by sentence. Each segment should contain one sentence, not a full paragraph.
  * All translatable content must be extracted and all untranslatable content must be ignored during the extraction.
  * Inline codes should not be taken as boundaries between text units/blocks, to avoid breaking down sentences into two or more fragments.
  * Inline codes and markup should be represented as specified by the XLIFF standard that the translation editor can recognize, lock and display as placeable tags.
  * The number of tags should be as low as possible.
  * If markup is not represented as tags and is escaped instead, then each markup block should be as short as possible.

Failure to follow those recommendations hampers language tasks or/and could affect translation quality.

There are other, less important recommendations with a lesser impact on their own. However, recurrent and concurrent failure to follow them can also contribute to making the translation process more difficult:

  * Unicode characters should be used instead escaped HTML entities.
  * Excessive whitespace and inline line breaks should be avoided.
  * To avoid truncations and overflowing text, text should be wrapped in the presentation medium instead of using linebreak codes in the source text.
  * Comments should be not extracted as translatable text.

### 1. Use segmentation

Translating or reviewing long paragraphs containing several sentences is inconvenient for several reasons. 

On the one hand, it requires a higher cognitive effort from the linguist, which reduces productivity and increases the chances of errors, and on the other hand, it reduces the likelihood of propagation and internal reuse of translations within the project, which leads to rework, reducing turnaround time savings, and to a higher number of inconsistencies, that are difficult to catch afterwards.

Sentence-based segmentation boosts the reuse of translations, through the propagation of the translation of a repeated segment to all its repetitions, or through the higher availability of matches to translate similar segments, thus increasing consistency, and reduces the need for the linguist to run concordance searches in search of the different parts that need to be assembled in the final translation. Segmentation contributes both to final quality and satisfaction of the team.

Segmentation should occur after each sentence, so that each sentence is included in one segment and each segment contains only one sentence. For example, a paragraph typically contains several sentences, like the following:

	Lorem ipsum dolor sit amet, consectetur adipiscing elit… Aliquam ex nisi, mattis pulvinar nulla sed, commodo mattis ligula. Nulla sit amet leo lacinia, pellentesque mi non, aliquam augue? Pellentesque tempor dictum dui in imperdiet. Fusce ligula arcu, hendrerit eu dignissim eget, consequat quis sem! Maecenas eget ligula dapibus, dictum purus vitae, sodales neque.

If the text is segmented, this long paragraph can be handled as independent sentences and therefore becomes much more manageable for the linguist. The expected result is:

  seg1: [ipsum dolor sit amet, consectetur adipiscing elit…](Lorem)
  seg2: [ex nisi, mattis pulvinar nulla sed, commodo mattis ligula.](Aliquam)
  seg3: [sit amet leo lacinia, pellentesque mi non, aliquam augue?](Nulla)
  seg4: [tempor dictum dui in imperdiet.](Pellentesque)
  seg5: [ligula arcu, hendrerit eu dignissim eget, consequat quis sem!](Fusce)
  seg6: [eget ligula dapibus, dictum purus vitae, sodales neque.](Maecenas)

To implement segmentation, you must use segmentation rules. Different tools might have slightly different implementations, but they all use regular expressions to match the patterns that correspond to sentence boundaries. SRX((See https:_okapiframework.org/wiki/index.php?title=SRX.)) is an XML-based standard of the localization industry used to define segmentation rules, and it can be used by Okapi Framework((Okapi Framework is a set of libraries that can be used to prepare files for translation, among other things.)). Segmentation rulesets can be easily created and customized in Okapi Ratel((See http:_okapiframework.org/wiki/index.php?title=Ratel)).

Libraries or tools used to prepare files as XLIFF normally include a basic set of default rules but sometimes it is necessary to create more specific rules to meet the specific needs of the source content. The XLIFF code to segment the paragraph above looks like this:

<code xml>
<seg-source><mrk mid="0" mtype="seg">Lorem ipsum dolor sit amet, consectetur adipiscing elit…</mrk> <mrk mid="1" mtype="seg">Aliquam ex nisi, mattis pulvinar nulla sed, commodo mattis ligula.</mrk> <mrk mid="2" mtype="seg">Nulla sit amet leo lacinia, pellentesque mi non, aliquam augue?</mrk> <mrk mid="3" mtype="seg">Pellentesque tempor dictum dui in imperdiet.</mrk> <mrk mid="4" mtype="seg">Fusce ligula arcu, hendrerit eu dignissim eget, consequat quis sem!</mrk> <mrk mid="5" mtype="seg">Maecenas eget ligula dapibus, dictum purus vitae, sodales neque.</mrk></seg-source>
</code>

As you can see in the example above, segments do not only end in full stop, but might end in other punctuation marking the end of a sentence (i.e. in English: interrogation, ellipsis, etc.).

Also, there are cases where these punctuation symbols do not stand for the end of a sentence, such as in the case of abbreviations:

  seg1: [canceled Mr. Robinson, the freshman comedy series.](NBC)

To avoid segmenting after abbreviations and in other cases, the segmentation ruleset must include some exceptions (the SRX default rulesets already include the most frequent abbreviations in English, so no need to reinvent the wheel). Without the appropriate exceptions for abbreviations, we would obtain the following incorrect segmentation:
rather than

  seg1: [canceled Mr.](NBC)
  seg2: [the freshman comedy series.](Robinson,)

In the OmegaT project provided, file `01_haram/segment_para.html.xlf` shows a text that has been prepared without segmentation, whereas file `02_halal/segment_para.html.xlf` has been prepared with sentence-based segmentation.

### Representing markup as inline codes



The source content might include markup, e.g. any HTML tag used to apply a certain behavior or property to part of the text. Often source content is HTML or some sort of similar markup language, where therefore tags are used to define layout, formatting and/or structure. The preparation of the source files as XLIFF entails dealing with those codes as appropriate.

Codes can be of two kinds:

  * Suprasentential and intersentential codes (i.e. codes that embed a sentence, or stand outside of a sentence, or between sentences, or operate at a higher level than the sentence) should not be included in segments.
  * Intrasentential codes (i.e. codes that stand inside a sentence) must be represented as inline elements (also called "content markup") according to the guidelines of the XLIFF specification((See http:_docs.oasis-open.org/xliff/v1.2/os/xliff-core.html#Struct_InLine and http:_docs.oasis-open.org/xliff/v1.2/xliff-profile-html/xliff-profile-html-1.2-cd02.html.)).

A leading opening tag appearing before the beginning of a sentence and its corresponding closing tag appearing after the end of the sentence are an example of suprasentential codes:

<code xml>
<p>What is the total length of the sticks in the line?</p>
</code>

They don't need to appear in the translation editor and the translator does not need to see them:

  seg1: [is the total length of the sticks in the line?](What)

On the other hand, the file `markup_span.html` from the sample project includes the following text:

<code xml>
<p><span style="font-size:12pt;font-family:&quot;times new roman&quot;, &quot;serif&quot;">Code1: </span><span style="font-size:12pt;font-family:&quot;times new roman&quot;, &quot;serif&quot;">3/2 or 11/2 or 1.5</span></p>
</code>

which should be prepared as:

<code xml>
<source xml:lang="en"><bpt id="1" ctype="x-span">&lt;span style='font-size:12pt;font-family:"times new roman", "serif"'></bpt>Code1: <ept id="1">&lt;/span></ept><bpt id="2" ctype="x-span">&lt;span style='font-size:12pt;font-family:"times new roman", "serif"'></bpt>3/2 or 11/2 or 1.5<ept id="2">&lt;/span></ept></source>
</code>

which will appear in the translation editor as:

<code xml>
seg1: [</g0><g1>3/2 or 11/2 or 1.5</g1>](<g0>Code1:)
</code>

In OmegaT, if the translator needs to see what the inline code represents, hovering over the tag (e.g. `<g0>` below) displays the tag content as a tooltip, so the linguist knows what the markup means:

{{:tecdoc:seg_nim_code1_halal_tooltip.png?nolink&800|}}

Representing the HTML tags as inline codes as specified in the XLIFF standard  also reduces the length of each tag, thus better legibility is obtained and the segments are much easier to handle.

    **Warning    **: Escaping the HTML or XML tags by replacing `<` and `>` with `&lt;` and `&gt;` respectively is not a good approach, because the translation editor will consider the escaped markup as editable text rather than as locked codes and therefore the tags can be mishandled, let alone the fact that translation memories will be polluted. Furthermore, that approach does not reduce the length of inline codes, which means that the text is less readable and that can hamper the translation and bring about quality issues.

For example, if handled in that way, the above segment would look like this in the XLIFF file:

<code xml>
<source xml:lang="en">&lt;span style=&quot;font-size:12pt;font-family:&amp;quot;times new roman&amp;quot;, &amp;quot;serif&amp;quot;&quot;>Code1: &lt;/span&gt;&lt;span style=&quot;font-size:12pt;font-family:&amp;quot;times new roman&amp;quot;, &amp;quot;serif&amp;quot;&quot;>3/2 or 11/2 or 1.5&lt;/span&gt;</source>
</code>

and will be displayed like this to the linguist in the translation editor:

<code xml>
seg1: [style="font-size:12pt;font-family:&quot;times new roman&quot;, &quot;serif&quot;">Code1: </span><span style="font-size:12pt;font-family:&quot;times new roman&quot;, &quot;serif&quot;">3/2 or 11/2 or 1.5</span>](<span)
</code>

In the OmegaT project provided, files `markup_custom_xml.xlf` and `markup_span.html.xlf` show what the text looks like when the inline codes have been simply escaped (the ones in the `01_haram` folder) and when they have been properly encapsulated as XLIFF markup (the ones in folder `02_halal`). There are two files to exemplify both standard HTML tags (e.g. `<span>`) as well as custom-crafted, even awkward XML tags.

### Encoding entities



HTML source content might contain named character references (in the form of &char;) but these named entities are not allowed in XML and therefore cannot be used in an XLIFF file as such unless they are declared (except for &, < and >). There is more than one possibility to prepare source HTML content containing named entities, and some ways are preferable to others. Let us consider the `&divide;` entity as an example, found in the HTML content:

<code xml>
<p>(40 &divide; 10) + (8 &divide; 2)</p>
</code>

One possibility to create a valid XLIFF file is to escape the entities, as follows:

<code xml>
<source>(40 &amp;divide; 10) + (8 &amp;divide; 2)</source>
</code>


The escaping approach is not recommended, though. Escapes were used to represent (by means of ASCII text only) characters that were not available in the character encoding you are using. The W3C (group in charge of the HTML specification) advises to use an encoding that allows to represent characters in their normal form, rather than using escaped character entity references, because using escapes can make it difficult to read and maintain source code, and can also significantly increase file size.((See https:_www.w3.org/International/questions/qa-escapes#not)) Therefore, nowadays you should use UTF-8 for the character encoding of any modern internationalized content, which removes the need to use character escapes for that reason.

Also, this way the named entity rather than the actual character itself will be displayed in the translation editor, as shown below (which reduces readability and could be misleading or even unintelligible for the linguist):

  seg1: [&divide; 10) + (8 &divide; 2)]((40)

Linguists need to see the character, not the code. While `&divide;` (÷) or `&pi;` (π) might be more or less transparent in the appropriate context, other entities such as `&le;` (≤) or `&zwnj;` (zero-width non-joiner) will be obscure and puzzling. The linguist could think that the named entity must be maintained and therefore necessarily be used in the translation, whereas it might be the case that the target language spelling rules call for another character in that context. For example, this would be an incorrect translation according to French punctuation rules:

  source: [works &quot;differently&quot; in French.](Punctuation)
  target: [ponctuation est &quot;différente&quot; en français.](La)

Compare with the correct translation:

  source: [works &quot;differently&quot; in French.](Punctuation)
  target: [ponctuation est « différente » en français.](La)

Escapes can be a way of avoiding the use of a character for other reasons (e.g. if they conflict with other elements), in which case, you might want to escape some entities specifically. Escapes might also be useful to represent invisible or ambiguous characters, or characters that would otherwise be difficult to handle, such as whitespace or invisible Unicode control characters (e.g. using `&rlm;` in HTML source content --and `&#x200F;` in the prepared XLIFF file-- helps spot these characters)((See https:_www.w3.org/International/questions/qa-escapes)). However, in all other cases, it is preferable to avoid the escape.

A different approach is to represent the same character by means of the universal Unicode code point expressed as a numeric entity (e.g. the hexadecimal entity `&#x00F7;`) or as the Unicode character itself (e.g. `÷`), the latter being slightly preferable because it simplifies maintenance and running text searches directly in the XLIFF files with, say, grep or any other text-based tool.

A simple pre-processing of the source content is possible to convert the HTML named entities into Unicode code points or Unicode characters. Even better, the ideal scenario would be to configure the authoring tool where the source content is authored so that such non-ASCII or special characters are represented using the Unicode character or numeric entities -- in which case no pre-processing conversion is necessary.  How authors insert symbols or special characters that are not on their keyboard depends on their authoring tool and their platform, but normally they can either pick the character from a special character palette (e.g. the Character Map in Windows or Character Viewer in Mac) or insert it by using a key combination, e.g. ALT+0176 on the keypad to insert the degree symbol (i.e. "°").((See https:_support.office.com/en-us/article/insert-ascii-or-unicode-latin-based-symbols-and-characters-d13f58d3-7bcb-44a7-a4d5-972ee12e50e0 and https:_support.apple.com/en-us/HT201586 for Mac.))

Both the approaches in the previous paragraph will produce one of the two following XLIFF codes (depending on the encoding chosen):

<code xml>
<source>(40 &#x00F7; 10) + (8 &#x00F7; 2)</source>
</code>
<code xml>
<source>(40 ÷ 10) + (8 ÷ 2)</source>
</code>

which will be displayed as the following in the translation editor:

  seg1: [÷ 10) + (8 ÷ 2)]((40)

In a nutshell, then: using the Unicode characters in their normal form is preferable to representing them with their numeric --preferably hexadecimal-- reference, and any of those two options is preferable to escaping the named character references with `&amp;`, or declaring them in the preamble of the document.

^ Approach  ^            Example  ^ Well-formed ^ Recommended  ^
| Unicode character	              | ÷	        | yes                | yes (more preferable) |
| numeric (hex) character reference   | &#x00F7;	| yes                | yes (less preferable) |
| unescaped named character reference | &divide;	| no (unless declared) | no (but feasible if declared in the document) |
| escaped named character reference   | &amp;divide;	| yes                | no  |

When preparing XLIFF files with Okapi Rainbow, both named entities and numeric entities in the source content will be encoded as the Unicode character in the XLIFF file. In the OmegaT project provided, you can see how the three possible inputs (in file `original/entities.html`) are encoded in the same way (as the Unicode character) using the recommended approach in file `02_halal/entities.html.xlf` and in the same unrecommended way in file `01_haram/entities.html.xlf`.

Some Unicode characters should be avoided in a markup context, and their numeric entity should be used instead((See https:_www.w3.org/International/questions/qa-chars-vs-markup#not)). Other than those, in a UTF-8 context (e.g. any content to be localized) there should be no reason why Unicode characters cannot be used.

#### Frequent issues



Following the recommendations above is necessary but might not be enough for an optimized process. The source content might present a number of pitfalls that require special attention when creating the XLIFF files. Let us see some of those frequent issues that hamper the language tasks.

### Split sentences



Sometimes sentences might be broken in two or more parts because the extraction filter is treating an embedded code as the end of the paragraph. In the OmegaT project provided, file `01_haram/markup_input.html.xlf` shows how the sentence is broken at the text input code:

<code xml>
<source>An emperor penguin is</source>
<source>cm taller than a little penguin.</source>
</code>

displayed in the translation editor as:

  seg1: [emperor penguin is](An)
  seg2: [taller than a little penguin.](cm)

The original content (in file `original/markup_input.html`) looks like this:

<code xml><p>An emperor penguin is <input type="text" name="fname" autocomplete="off" size="4" id="emperor-penguin-versus-little-penguin" class="heigh-differnet" pattern="[title="How many centimeters." formmethod="post" required autofocus> cm taller than a little penguin.</p></code>

That code represents this display in the online questionnaire:

{{:tecdoc:form.png?nolink&400|}}

Here, the expected preparation is to represent the text input field markup as inline codes, as follows (and can be seen in `02_halal/markup_input.html.xlf`):

<code xml>
<source xml:lang="en">An emperor penguin is <ph id="1" ctype="x-input">&lt;input type="text" name="fname" autocomplete="off" size="4" id="emperor-penguin-versus-little-penguin" class="heigh-differnet" pattern="[0-9](0-9]+")+" [formmethod="post" required autofocus></ph> cm taller than a little penguin.</source>
</code>

which will appear as follows in the translation editor (see file :

<code xml>seg1: [An emperor penguin is <x0/> cm taller than a little penguin.](#$tu2])</code>

File `markup_inline.svg.xlf` shows a similar case of text broken down at the two embedding SVG tags `<tspan>` and `</tspan>`.

Other similar examples:

  seg1: [  seg2: [to move on.](Click])

  seg1: [uses on](See)
  seg2: [show 2 children in her pictograph](to)
  seg3: [many](How)
  seg4: [they need to draw?](will)

/**  seg1: Click
  seg2: when you are done.

  seg1: Click
  seg2: to start.**/

  seg1: [5 penguins for](Feed)
  seg2: [
/**  seg1: Feed
  seg2: penguins for 200 zeds. **/

  seg1: [Drag](zeds.])
  seg2: [the graph.](onto)

  seg1: [your drawing is done, click](When)
  seg2: [fill the garden with boxes of flowers.](to)

In all these cases the original content includes some element (e.g. "Click `[X](BUTTON)` to move on." or "Feed 5 penguins for `[zeds.") that has been interpreted as the end of a paragraph.

Apart from the inconvenience that the full sentence will not be stored in the translation memory as one unit, this is a further problem if the target language expresses things in a different order than English, e.g. say, "Tó móvê ón klïck [X](QUANTITY]`)". In that case the linguist is forced to break the expected one-to-one segment correspondence, in order to maintain the correct order.

Maintaining the correspondence will produce the wrong order in the final content:

  seg1: [          => [klïck](Click])
  seg2: [move on.](to)     => [móvê ón](Tó)

Breaking the natural correspondence will produce the right order in the final content but makes reuse of these materials problematic when translating subsequent cycle's content:

  seg1: [      => [](Click])                OR [móvê ón klïk](Tó) OR [móvê](Tó)
  seg2: [move on.](to) => [móvê ón klïk](Tó)    [                  [ón klïk](])

Auto-propagation can also become problematic, if the translation of a repeated segment (corresponding to part of the sentence) is different in different contexts, for example due to agreement with other parts of the sentence, e.g.

  seg1: [  seg2: [wheel](Front])
  seg3: [  seg4: [headlamp](Front])

For example, in Spanish adjectives need to agree in gender and number with the nouns they modify, e.g. the translation of "front" is "delantera" (feminine) in seg1 to agree with the Spanish equivalent of "wheel" (i.e. "rueda"), which has feminine grammatical gender, whereas it is "delantero" (masculine) in seg3 to agree with the Spanish equivalent of "headlamp" (i.e. "faro"), which has masculine grammatical gender.

In these cases, to achieve the correct translation the linguist might need to disable the default auto-propagation (to prevent the translation of seg1 being pulled automatically into seg3), but that manual step could fail or be easily overlooked.

In a nutshell, split sentences can be a nuisance to translate into certain languages with different word order than English -- the linguist might have to work around the translation in difficult or impossible ways. Also, productivity and internal consistency can be compromised if the same text appears later in the same project, or in future cycles, with different or correct segmentation.

In the second example above, “she uses one” _something_ and the respondent is being asked “how many” _of something_ the person will need… The object referred to is missing, so it seems that the entity referring to that object was taken as the end of that structural unit.

    **Expected preparation    **: The expected result in the cases above would have been to use a tag or a placeholder to encode the inline code:

  seg1: [uses on %s to show 2 children in her pictograph](See)
  seg2: [many %s will they need to draw?](How)

<code xml>
seg1: [<BUTTON/> to move on.](Click)
</code>

  seg1: [wheel](Front)
  seg2: [headlamp](Front)

In the examples above where the segment has been properly prepared with inline codes, it’s not a problem for the translator to transfer the codes to the place where they belongs in the translation, as any modern translation editor allows to do that easily with a keyboard shortcut.

    **Solution    **: To avoid this issue, then, ask a trained linguist to run a source review on your draft XLIFF files and adjust the extraction filter accordingly, so that it knows that that particular code must be treated as an inline code (extracted along with the surrounding text and protected) and not as the end of a paragraph.

### Markup nimiety



Segments overloaded with markup make translation and all related subsequent language tasks more difficult, therefore increasing the chance to introduce errors in the translation, especially in right-to-left languages such as Arabic.

Some inline codes are unavoidable, e.g. to provide style:

<code xml>Put the lengths in order from <b>shortest</b> to <i>longest</i>.</code>

However, other tags are unnecessary and should be avoided. For example, closing and opening tags of the same kind in the middle of a sentence or even in the middle of a word:

<code xml>Vehicl</strong><strong>es in 2000</code>

When this happens repeatedly, it results in segments that are (unnecessarily) very translation unfriendly. For example:

<code xml><strong>Star</strong><strong>t </strong><strong>T</strong><strong>i</strong><strong>me</strong></code>

In that example, there are a lot of `<strong>` tags there to do the same job that could be achieved with simply one tag pair. This tag multiplicity might arise from adding superfluous formatting in a word processor or a wysiwyg editor to create the source, or from converting with OCR or from PDF.

    **Expected preparation    **: The expected design of the source content in the case above would have been to embed the formatted text with one tag pair.

<code xml><strong>Start Time</strong></code>

This tag pair is actually suprasentential markup, which could be excluded from the prepared segment, thus producing the following simple display in the translation editor:

  seg1: [Time](Start)

    **Solution    **: Provide feedback and tips to item developers and run some tag clean-up before extracting the text that must be included in the XLIFF files (tools like TransTools Document Cleaner can be used for that)((See http:_kb.memoq.com/article/AA-00485/0/Cleaning-unnecessary-tags-with-TransTools-Document-Cleaner.html)).

The solution of this issue does not affect how the source content is prepared, but instead it relates to the pre-processing of the source content, before it is prepared. The actually preparation (parsing, extraction and segmentation) is the same regardless of whether the issue is present in the source files.


### Ending segments at linebreaks



In some cases, linebreaks are used to limit the length of each line in the text. When the text is HTML, the text might be broken down at linebreak tags. For example:

<code xml>
seg1: [the 1970s, scientists have been](Since)
seg2: [seg3: [worried about the amount of Dioxin, a](<br/>])
seg4: [seg5: [toxin in fish caught in Baltic Sea.](<br/>])
</code>

The expected segmentation is the following, where the line break HTML tags are interpreted and represented as inline codes:

<code xml>seg1: [the 1970s, scientists have been <br/> worried about the amount of Dioxin, a toxin in fish caught in Baltic Sea.](Since)</code>

However, it should not be assumed that the translator will keep the line break tags in the translation or that their location will be equivalent to the source.

    **Solution**: To avoid this issue, ask a linguist to run a source review on your draft XLIFF files and adjust the extraction filter accordingly, so that it treats the linebreak element as markup (extracted along with the surrounding text and protected) and not as the end of the paragraph.

However, if the purpose of the line break tags is indeed to wrap the text at a certain width, there might be more convenient ways to achieve that, without tags, such as CSS styles for HTML content. In general it is recommended to separate content from layout.

Therefore, our recommendation, in the first place, would be to avoid using line break tags in the source text. Secondly (assuming we are dealing with HTML content), the width of the text can be defined by means of CSS styles. That approach  achieves the same exact results without introducing any noise in the source text and without affecting the work of the translator. See https:_jsfiddle.net/msoutopico/3p7x8ryr/1/ or the screenshot below:

{{:tecdoc:markup_fiddl_wrap.png?nolink&400|}}

/** more issues. mixture of encodings **/

#### Annexes



Preparing XLIFF files for translation in OmegaT entails some additional tweaks due to the special characteristics of this CAT tool.

{{page>tecdoc:cat_omt_mkxlf_4engg&doindent}}

## References
=============

1. OmegaT installation and customization guide: https:_slides.com/capstan/omegat-installation-and-customization-guide/fullscreen

## Footnotes
============

1. <span id="1"></span> OmegaT is a free and open source computer-assisted translation tool (CAT-tool) that cApStAn uses to translate and review/edit XLIFF files in international large-scale translation projects. It offers more technical possibilities than OLT. [⏎](#a1)

2. <span id="2"></span> OmegaT installation and customization guide: https:_slides.com/capstan/omegat-installation-and-customization-guide/fullscreen [⏎](#a2)

3. <span id="3"></span>(See [http:_docs.oasis-open.org/xliff/xliff-core/xliff-core.html](http:_docs.oasis-open.org/xliff/xliff-core/xliff-core.html)) [⏎](#a3)

4. <span id="4"></span>(XML schema: [https:_docs.oasis-open.org/xliff/v1.2/os/xliff-core-1.2-strict.xsd](https:_docs.oasis-open.org/xliff/v1.2/os/xliff-core-1.2-strict.xsd)) [⏎](#a4) 

5. <span id="5"></span>(The XLIFF checker can be downloaded from https://www.maxprograms.com/products/xliffchecker.html) [⏎](#a5)

, 
[comment:] <> (0. <span id="0"></span>() [⏎](#a0))

[comment:] <> (<span id="a1">[[1]](#1)</span>)
