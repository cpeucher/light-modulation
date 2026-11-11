# To do

## Content

## quarto project template

- [ ] Have separated folders for PNG and PDF files, depending on whether HTML or PDF is rendered
- [ ] Size of graphs generated inline using matplotlib
- [ ] Extract only used references in a bib file. Should be done by preserving the `.bbl` file when rendering to PDF using LaTeX.
- [ ] Book format with new chapters always starting on odd pages
- [ ] Make sure front mater is numbered with roman numerals 
- [ ] Cross references without capitalization in French
- [ ] Fix cross references to different chapters from the `index.qmd` file
- [ ] CSL for lecture notes
- [x] `\hat` not centered on `\mathbf` (for instance in the definition of `\vbh{}` macro) in PDF rendering when a capital letter is the argument, e.g. `\vbh{E}`. Works fine for lower case argument, e.g. `\vbh{x}`.
  
    This seems to be linked to the use of the defualt `lualatex` engine. Solved by using the `xelatex`engine instead. 

    In `_quarto.yml`:

  ```
  format:
    pdf:
      pdf-engine: xelatex
  ```



## What we tried


### CSL for lecture notes 


I have the bibtex entry:

@misc{bibtexkey,
  author       = {Doe, J.},
  title        = {This is the title},
  year         = {2026},
  howpublished = {Support de cours, Plateforme Moodle de l'Université de Xxxx},
  note         = {Accès restreint aux étudiants inscrits},
  url          = {https://www.site.com},
  institution  = {Department of Enginering (DE)}
}

I would like to format it as: 

J. Doe, "This is the title," Support de cours, Plateforme Moodle de l'Université de Xxxx, Accès restreint aux étudiants inscrits, Department of Enginering (DE) (2026) https://www.site.com.

What should be the CSL description?




        <else-if type="webpage">
          <group delimiter=" ">
            <text variable="title" prefix="&quot;" suffix=",&quot;"/>
            <text variable="publisher"/>
            <text variable="note"/>
            <text variable="source" prefix="("/>
            <text prefix=", " suffix=")," macro="day-date"/>
            <text variable="URL"/>
          </group>        
        </else-if>



        <?xml version="1.0" encoding="utf-8"?>
<style xmlns="http://xn--xgsr03k.org" class="in-text" version="1.0" default-locale="fr-FR">
  <info>
    <title>Custom BibTeX Misc Style</title>
    <id>http://zotero.org</id>
    <link href="http://zotero.org" rel="self"/>
    <author>
      <name>Custom Style</name>
    </author>
    <category citation-format="author-date"/>
    <updated>2026-11-04T17:15:00+00:00</updated>
  </info>

  <!-- Macro pour l'auteur : Initiales. Nom -->
  <macro name="author">
    <names variable="author">
      <name initialize-with=". " delimiter=", " and="text"/>
    </names>
  </macro>

  <!-- Macro pour le titre entre guillemets -->
  <macro name="title">
    <text variable="title" quotes="true"/>
  </macro>

  <!-- Macro pour l'année entre parenthèses -->
  <macro name="year">
    <date variable="issued" prefix="(" suffix=")">
      <date-part name="year"/>
    </date>
  </macro>

  <citation>
    <layout>
      <text value="[citation]"/>
    </layout>
  </citation>

  <!-- Formatage de la bibliographie -->
  <bibliography entry-spacing="1" line-spacing="1">
    <layout suffix=".">
      <group delimiter=" ">
        <!-- Auteur, "Titre," Howpublished, Note, Institution -->
        <group delimiter=", ">
          <text macro="author"/>
          <text macro="title"/>
          <text variable="publisher"/> <!-- Correspond à howpublished -->
          <text variable="note"/>      <!-- Correspond à note -->
          <text variable="source"/>    <!-- Correspond à institution -->
        </group>
        <!-- (Année) URL -->
        <text macro="year"/>
        <text variable="URL"/>
      </group>
    </layout>
  </bibliography>
</style>

