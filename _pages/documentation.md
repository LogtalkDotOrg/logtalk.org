---
layout: article
permalink: documentation.html
title: Documentation
aside:
  toc: true
---

## Tutorials

-   Learn X in Y minutes Where X=Logtalk:
    [English](https://learnxinyminutes.com/docs/logtalk/)
    [Italian](https://learnxinyminutes.com/docs/it-it/logtalk-it/) (recommended starting point for new users)
-   [Handbook tutorial](manuals/tutorial/index.html)


## Handbook

The Logtalk Handbook includes the User Manual, Reference Manual, Glossary, and FAQ.

-   [HTML version](manuals/index.html) @ the Logtalk website (stable)
-   [PDF version](manuals/TheLogtalkHandbook-3.33.0.pdf) (stable)
-   [ePub version](manuals/TheLogtalkHandbook-3.33.0.epub) (stable)
-   [Texinfo version](manuals/TheLogtalkHandbook-3.33.0.info) (stable; experimental)

<!-- -->

-   [HTML version](https://logtalk3.readthedocs.io/en/latest/) @ the Read the Docs website (latest git version; provides [improved search support](https://blog.readthedocs.com/search-improvements/))


## APIs

Core, Library, Tools, and Contributions API documentation

-   [HTML API documentation](library/index.html) (stable; automatically generated)
-   SVG diagrams (stable; automatically generated)
    -   [Core](library/core_inheritance_diagram.svg)
    -   [Library](library/library_inheritance_diagram.svg)
    -   [Tools](library/tools_inheritance_diagram.svg)
    -   [Contributions](library/contributions_inheritance_diagram.svg)
    -   [Ports](library/ports_inheritance_diagram.svg)

<!-- -->

-   [Texinfo version](docs/LogtalkAPIs-3.33.0.info) (stable; automatically generated)

The SVG diagrams provide links to both the API documentation and to the
source code.


## Tools

The documentation for each developer tool is included in the tool
source directory in a `NOTES.md` file and in the [Handbook](#handbook).
See also the tools [overview and usage examples](tools.html).

The tools listed in this section are complemented by a set of
[scripts](#man-pages) that automate common tasks.

### Learning

-   [`tutor`](https://github.com/LogtalkDotOrg/logtalk3/blob/master/tools/tutor/NOTES.md)

### Development

-   [`code_metrics`](https://github.com/LogtalkDotOrg/logtalk3/blob/master/tools/code_metrics/NOTES.md)
-   [`dead_code_scanner`](https://github.com/LogtalkDotOrg/logtalk3/blob/master/tools/dead_code_scanner/NOTES.md)
-   [`help`](https://github.com/LogtalkDotOrg/logtalk3/blob/master/tools/help/NOTES.md)
-   [`make`](https://github.com/LogtalkDotOrg/logtalk3/blob/master/tools/make/NOTES.md)

### Debugging

-   [`assertions`](https://github.com/LogtalkDotOrg/logtalk3/blob/master/tools/assertions/NOTES.md)
-   [`debug_messages`](https://github.com/LogtalkDotOrg/logtalk3/blob/master/tools/debug_messages/NOTES.md)
-   [`debugger`](https://github.com/LogtalkDotOrg/logtalk3/blob/master/tools/debugger/NOTES.md)

### Profiling

-   [`ports_profiler`](https://github.com/LogtalkDotOrg/logtalk3/blob/master/tools/ports_profiler/NOTES.md)
-   [`profiler`](https://github.com/LogtalkDotOrg/logtalk3/blob/master/tools/profiler/NOTES.md)

### Documenting

-   [`lgtdoc`](https://github.com/LogtalkDotOrg/logtalk3/blob/master/tools/lgtdoc/NOTES.md)
-   [`diagrams`](https://github.com/LogtalkDotOrg/logtalk3/blob/master/tools/diagrams/NOTES.md)
-   [`doclet`](https://github.com/LogtalkDotOrg/logtalk3/blob/master/tools/doclet/NOTES.md)

### Testing

-   [`lgtunit`](https://github.com/LogtalkDotOrg/logtalk3/blob/master/tools/lgtunit/NOTES.md)

### Version management

-   [`asdf`](https://github.com/LogtalkDotOrg/logtalk3/blob/master/tools/asdf/NOTES.md)

### Porting

-   [`wrapper`](https://github.com/LogtalkDotOrg/logtalk3/blob/master/tools/wrapper/NOTES.md)


## Release notes

Check the [release notes](https://github.com/LogtalkDotOrg/logtalk3/blob/master/RELEASE_NOTES.md)
for the latest goodies.


## Man pages

Prolog integration scripts:

-   B-Prolog: [`bplgt`](man/bplgt.html)
-   CxProlog: [`cxlgt`](man/cxlgt.html)
-   ECLiPSe: [`eclipselgt`](man/eclipselgt.html)
-   GNU Prolog: [`gplgt`](man/gplgt.html)
-   JIProlog: [`jiplgt`](man/jiplgt.html)
-   Lean Prolog: [`lplgt`](man/lplgt.html)
-   Qu-Prolog: [`qplgt`](man/qplgt.html)
-   Quintus Prolog: [`quintuslgt`](man/quintuslgt.html)
-   SICStus Prolog: [`sicstuslgt`](man/sicstuslgt.html)
-   SWI-Prolog: [`swilgt`](man/swilgt.html)
-   XSB: [`xsblgt`](man/xsblgt.html)
-   XSB (mt): [`xsbmtlgt`](man/xsbmtlgt.html)
-   YAP: [`yaplgt`](man/yaplgt.html)

Configuration scripts:

-   [`logtalk_user_setup`](man/logtalk_user_setup.html)
-   [`logtalk_backend_select`](man/logtalk_backend_select.html)
-   [`logtalk_version_select`](man/logtalk_version_select.html)

Testing scripts:

-   [`logtalk_tester`](man/logtalk_tester.html)

Documentation scripts:

-   [`logtalk_doclet`](man/logtalk_doclet.html)
-   [`lgt2html`](man/lgt2html.html)
-   [`lgt2md`](man/lgt2md.html)
-   [`lgt2pdf`](man/lgt2pdf.html)
-   [`lgt2rst`](man/lgt2rst.html)
-   [`lgt2txt`](man/lgt2txt.html)
-   [`lgt2xml`](man/lgt2xml.html)

Diagrams scripts:

-   [`lgt2svg`](man/lgt2svg.html)


## Publications

-   [A Portable and Efficient Implementation of Coinductive Logic
    Programming](http://dx.doi.org/10.1007/978-3-642-45284-0_6). Paulo
    Moura. Proceedings of the Fifteenth International Symposium on
    Practical Aspects of Declarative Languages (PADL 2013), 2013.
    Springer LNCS 7752.
-   [Meta-Predicate
    Semantics](http://dx.doi.org/10.1007/978-3-642-32211-2_11). Paulo
    Moura. Post-Proceedings of the 21st International Symposium on
    Logic-Based Program Synthesis and Transformation (LOPSTR
    2011), 2012. Springer LNCS 7225.
-   [L-FLAT: Logtalk Toolkit for Formal Languages and Automata
    Theory](http://arxiv.org/abs/1112.3783). Paulo Moura and Artur
    Miguel Dias. Proceedings of the 11th Colloquium on Implementation of
    Constraint LOgic Programming Systems (CICLOPS), July 2011.
-   [Programming Patterns for Logtalk Parametric
    Objects](http://dx.doi.org/10.1007/978-3-642-20589-7_4). Paulo
    Moura. Applications of Declarative Programming and Knowledge
    Management, Lecture Notes in Artificial Intelligence Vol. 6547,
    April 2011
-   [Towards a Study of Meta-Predicate
    Semantics](http://arxiv.org/abs/1009.3773). Paulo Moura. Proceedings
    of the 10th Colloquium on Implementation of Constraint LOgic
    Programming Systems (CICLOPS), July 2010.
    ([slides](https://logtalk.org/papers/ciclops2010/logtalk_ciclops2010.pdf))
-   Knowledge Representation Using Logtalk Parametric Objects. Paulo
    Moura. Proceedings of the International Conference on Applications
    of Declarative Programming and Knowledge Management (INAP),
    University of Évora, Portugal, November 2009, pp 225-240.
    ([slides](https://logtalk.org/papers/inap2009/parametric_inap2009.pdf))
-   [From Plain Prolog to Logtalk Objects: Effective Code Encapsulation
    and Reuse (Invited
    Talk)](http://dx.doi.org/10.1007/978-3-642-02846-5_3). Paulo Moura.
    Proceedings of the 25th International Conference on Logic
    Programming (ICLP), July 2009. LNCS 5649. Springer-Verlag Berlin
    Heidelberg\".
    ([slides](https://logtalk.org/papers/iclp2009/logtalk_iclp2009.pdf))
    ([updated
    slides](https://logtalk.org/papers/logtalk_utdallas_2011.pdf) for a
    talk at U.T. Dallas in Summer 2011)
-   [Secure Implementation of
    Meta-predicates](http://dx.doi.org/10.1007/978-3-540-92995-6_19).
    Paulo Moura. Proceedings of the 11th International Symposium on
    Practical Aspects of Declarative Languages (PADL), January 2009.
    LNCS 5418. Springer-Verlag Berlin Heidelberg.
-   [High Level Thread-Based Competitive Or-Parallelism in
    Logtalk](http://dx.doi.org/10.1007/978-3-540-92995-6_8). Paulo
    Moura, Ricardo Rocha, and Sara C. Madeira. Proceedings of the 11th
    International Symposium on Practical Aspects of Declarative
    Languages (PADL), January 2009. LNCS 5418. Springer-Verlag Berlin
    Heidelberg.
-   [Thread-Based Competitive
    Or-Parallelism](http://dx.doi.org/10.1007/978-3-540-89982-2_63).
    Paulo Moura, Ricardo Rocha, and Sara C. Madeira. Proceedings of the
    24th International Conference on Logic Programming (ICLP),
    December 2008. LNCS 5366. Springer-Verlag Berlin Heidelberg.
-   [High-Level Multi-threading Programming in
    Logtalk](http://dx.doi.org/10.1007/978-3-540-77442-6_18). Paulo
    Moura, Paul Crocker, and Paulo Nunes. Proceedings of the 10th
    International Symposium on Practical Aspects of Declarative
    Languages (PADL), January 2008. LNCS 4902. Springer-Verlag Berlin
    Heidelberg.
-   [Logtalk Processing of STEP Part 21
    Files](http://dx.doi.org/10.1007/11799573_45). Paulo Moura and
    Vincent Marchetti. Proceedings of the 22nd International Conference
    on Logic Programming (ICLP), August 2006. LNCS 4079. Springer-Verlag
    Berlin Heidelberg.

<!-- -->

-   Download a [PhD thesis](papers/thesis.pdf) on Logtalk design and
    implementation (PDF, A4 paper). Thesis submitted on May 2003, and
    publicly defended on September 2003 (Supervisor: Prof. Abel Gomes;
    Discussants: Prof. Mário Martins (University of Minho, Portugal),
    Prof. Salvador Abreu (University of Évora, Portugal), Prof. Vitor
    Costa (University of Porto, Portugal), Prof. Ana Moreira (New
    University of Lisbon, Portugal)).

<!-- -->

-   Download an unpublished paper on Logtalk categories (submitted to
    both [OOPSLA 2000](papers/categories_oopsla.pdf) and [ECOOP
    2001](papers/categories_ecoop.pdf)). Categories are also described
    in the Logtalk technical report and PhD thesis. Categories are
    implemented in Logtalk since is first public release in 1998.

<!-- -->

-   Download a Technical Report on Logtalk 2.6, published on July, 2000:
    [PDF A4 paper](papers/trdmi20001a4.pdf), [PDF US Letter
    paper](papers/trdmi20001us.pdf).

### Opinion articles


-   [Uniting the Prolog Community: Personal
    Notes](http://www.cs.kuleuven.ac.be/~dtai/projects/ALP/newsletter/feb09/content/Articles/doc5/content.html#moura).
    Paulo Moura, Association for Logic Programming (ALP) Newsletter,
    Vol. 22/1, March 2009.
-   [Prolog Portability and
    Standardization](http://www.cs.kuleuven.ac.be/~dtai/projects/ALP/newsletter/aug05/nav/articles/three/article.html).
    Paulo Moura, Association for Logic Programming (ALP) Newsletter,
    Vol. 18/3, August 2005.
-   [Logtalk
    2.18.0](http://www.cs.kuleuven.ac.be/~dtai/projects/ALP/newsletter/aug04/nav/articles/logtalk/logtalk.html).
    Paulo Moura, Association for Logic Programming (ALP) Newsletter,
    Vol. 17/3, August 2004.
-   Some notes on porting a Prolog program to 22 Prolog compilers or the
    relevance of the ISO Prolog standard. Paulo Moura, Association for
    Logic Programming (ALP) Newsletter, Vol. 12/2, May 1999.

## Third-party publications

Publications on research and applications using Logtalk:

-	[A Computational Independent Model for a Medical Quality Management Information System](http://ceur-ws.org/Vol-2221/).
	Evgeny A. Cherkashin, Ljubica Kazi, Alexey O. Shigarov, Viacheslav V. Paramonov.
	Proceedings for First Scientific-practical Workshop Information Technologies: Algorithms, Models, Systems
	Irkutsk, Russia. September  2018.
-	[Model Driven Architecture Implementation Using Linked Data](https://link.springer.com/chapter/10.1007/978-3-319-99972-2_34).
	Evgeny Cherkashin, Alexey Kopaygorodsky, Ljubica Kazi, Alexey Shigarov, Viacheslav Paramonov.
	In: Damaševičius R., Vasiljevienė G. (eds) Information and Software Technologies. ICIST 2018.
	Communications in Computer and Information Science, vol 920. Springer, Cham. August 2018.
-   [Automatic Discovery of Software Attacks via Backward
    Reasoning](http://ieeexplore.ieee.org/document/7174811/). Cataldo
    Basile, Daniele Canavese, Jerome d\'Annoville, Bjorn De Sutter, and
    Fulvio Valenza. IEEE/ACM 1st International Workshop on Software
    Protection (SPRO), May 2015.
-   [A Portable Approach for Bidirectional Integration between a Logic
    and a Statically-Typed Object-Oriented Programming Language](https://www.researchgate.net/publication/265301265_A_Portable_Approach_for_Bidirectional_Integration_between_a_Logic_and_a_Statically-Typed_Object-Oriented_Programming_Language).
    Sergio Castro. PhD thesis. September 2014.
-   [Customisable Handling of Java References in Prolog
    Programs](http://arxiv.org/abs/1405.2693). Sergio Castro, Kim Mens,
    and Paulo Moura. Proceedings of the 30th International Conference on
    Logic Programming. July 2014.
-   LogicObjects: A Portable and Extensible Approach for Linguistic
    Symbiosis between an Object-Oriented and a Logic Programming
    Language. Sergio Castro. Proceedings of the International Conference
    on Logic Programming Doctoral Consortium (ICLP DC), 2013. TPLP 13
    (4-5): Online Supplement, July 2013.
    ([PDF](http://journals.cambridge.org/downloadsup.php?file=/tlp2013030.pdf))
-   [Logical programming and data mining as engine for MDA model
    transformation
    implementation](http://ieeexplore.ieee.org/document/6596408/). A.Y.
    Sokolov, I.N. Terekhin, E.A. Cherkashin, S.O. Butakov, and A.A.
    Larionov. Proceedings of the 36th International Convention on
    Information & Communication Technology Electronics &
    Microelectronics (MIPRO), May 2013
-   [LogicObjects: Enabling Logic Programming in Java Through Linguistic
    Symbiosis](http://dx.doi.org/10.1007/978-3-642-45284-0_3). Sergio
    Castro, Kim Mens, and Paulo Moura. Proceedings of the Fifteenth
    International Symposium on Practical Aspects of Declarative
    Languages (PADL 2013), 2013. Springer LNCS 7752.
-   [A Declarative Pipeline Language for Complex Data
    Analysis](http://dx.doi.org/10.1007/978-3-642-38197-3_3). Henning
    Christiansen, Christian Theil Have, Ole Torp Lassen, Matthieu Petit.
    Post-Proceedings of the 22nd International Symposium on Logic-Based
    Program Synthesis and Transformation (LOPSTR 2012), 2013. Springer
    LNCS 7844.
-   [Information Systems Framework Synthesis on the Base of a Logical
    Approach](http://www.tfzr.rs/esociety/issues/eSocietyVol3No2.pdf#page=6).
    E.A. Cherkashin, V.V. Paramonov, R.K. Fedorov, I.N. Terehin, E.I.
    Pozdnyak, and D.V. Annenkov. E-society Journal: research and
    applications, Vol. 3, No. 2, December 2012
-   [ESProNa - Eine Constraintsprache zur multimodalen
    Prozessmodellierung und navigationsgestützten
    Ausführung](http://opus4.kobv.de/opus4-ubbayreuth/frontdoor/index/index/docId/888)
    (ESProNa - A Constraint-Language for multimodal Process Modeling
    supporting Navigation-Based Process Execution). Michael Igler. PhD
    thesis. July 2012.
-   [LogicObjects: A Linguistic Symbiosis Approach to Bring the
    Declarative Power of Prolog to
    Java](http://doi.acm.org/10.1145/2237887.2237890). Sergio Castro,
    Kim Mens, and Paulo Moura. Proceedings of the 9th Workshop on
    Reflection, AOP and Meta-Data for Software Evolution (RAM-SE).
    June 2012.
-   [New transformation approach for Model Driven Architecture](https://ieeexplore.ieee.org/document/6240804).
    E.A. Cherkashin, I.N. Terehin, V.V. Paramonov, V.S. Tertychniy.
    Proceedings of the 35th International Convention MIPRO. May 2012
-   [Model Driven Architecture is a Complex
    System](https://scholar.google.ru/citations?view_op=view_citation&hl=ru&user=ilJUQ0MAAAAJ&citation_for_view=ilJUQ0MAAAAJ:5nxA0vEk-isC).
    Cherkashin, Е.А., Paramonov V.V., Ipatov S. A., Tertychniy V.S.,
    Terehin I.N. E-Society Journal, Research and Applications,
    University of Novi Sad, Technical Faculty \"Mihajlo Pupin\"
    Zrenjanin, 2011, Vol. 2, N2. - C. 15-23. November 2011.
-   [Information modeling of business processes in X-ray fluorescent
    analysis](http://ieeexplore.ieee.org/document/5967191/). O. P.
    Vorobyeva, E. A. Cherkashin, S. A. Ipatov, and V. V. Paramonov.
    Proceedings of the 34th International Convention MIPRO. May 2011
-   [Using Argumentation for Ambient Assisted
    Living](http://dx.doi.org/10.1007/978-3-642-23960-1_48). Julien
    Marcais, Nikolaos Spanoudakis, and Pavlos Moraitis. IFIP Advances in
    Information and Communication Technology. Vol. 364. Springer Berlin
    Heidelberg. 2011.
-   [Modeling and Planning Collaboration using Organizational
    Constraints](http://dx.doi.org/10.4108/icst.collaboratecom.2010.47).
    Michael Igler, Paulo Moura, Matthias Faerber, Michael Zeising, and
    Stefan Jablonski, The 6th International Conference on Collaborative
    Computing: Networking, Applications and Worksharing
    (CollaborateCom), October 2010.
-   [ESProNa: Constraint-Based Declarative Business Process
    Modeling](http://dx.doi.org/10.1109/EDOCW.2010.10). Michael Igler,
    Paulo Moura, Michael Zeising, and Stefan Jablonski. Proceedings of
    the Third International Workshop on Dynamic and Declarative Business
    Processes, October 2010.
-   [A comparison of SL- and unit-resolution search rules for stratified
    logic
    programs](http://urn.kb.se/resolve?urn=urn:nbn:se:liu:diva-57363).
    Victor Lagerkvist. Bachelor thesis, Linköping University, Department
    of Computer and Information Science, June 2010.
-   [IT Architecture Automatic Verification: A network evidence-based
    approach](http://dx.doi.org/10.1109/RCIS.2010.5507358). António
    Alegria and André Vasconcelos. Proceedings of the Fourth IEEE
    International Conference on Research Challenges in Information
    Science, RCIS 2010.
-   [A Document Engineering Model and Processing Framework for
    Multimedia
    Documents](http://www-rocq.inria.fr/~geurts/thesis/thesis.pdf).
    Joost Geurts. PhD Thesis, Technische Universiteit Eindhoven,
    February 2010. SIKS Dissertation Series No. 2010-03.
-   [Verificação Automática de Modelos de Arquitectura Tecnológica de
    Sistemas de Informação em
    Rede](https://fenix.tecnico.ulisboa.pt/downloadFile/395139409126/dissertacao.pdf).
    António Manuel de Carvalho Alegria. Master Thesis, Instituto
    Superior Técnico, Portugal, November 2009
-   [Supporting Collaborative Work Through Flexible Process
    Execution](http://dx.doi.org/10.4108/ICST.COLLABORATECOM2009.8299).
    Stefan Jablonski, Michael Igler, and Christoph Gunther. Proceedings
    of the 5th International Conference on Collaborative Computing:
    Networking, Applications and Worksharing (CollaborateCom 2009),
    November 2009. IEEE.
-   [Gorgias-C: Extending Argumentation with Constraint
    Solving](http://dx.doi.org/10.1007/978-3-642-04238-6_54). Victor
    Noël and Antonis C. Kakas. Proceedings of the 10th International
    Conference on Logic Programming and Nonmonotonic Reasoning,
    September, 2009. LNCS 5753. Springer-Verlag Berlin Heidelberg.
-   [Dialogue Organization in
    Polint-112-SMS](http://dx.doi.org/10.1007/978-3-642-20095-3_29).
    Justyna Walkowska. Human Language Technology. Challenges for
    Computer Science and Linguistics. LNCS 6562. Springer Berlin
    Heidelberg.
-   [Object-Oriented Logic
    Programming](http://www.monicadogaru.com/pdf/BachelorScThesis_MartaMonicaDOGARU.pdf).
    Marta-Monica Dogaru. Bachelor Thesis, Technical University of
    Catalonia, Babeş-Bolyai University Cluj-Napoca, Faculty of
    Mathematics and Computer Science, Romania, 2008.
-   [Design Dependencies Within the Automatic Generation of Hypermedia
    Presentations](http://www.cwi.nl/ftp/CWIreports/INS/INS-R0205.pdf).
    Oscar Rosell Martinez. Master Thesis, Technical University of
    Catalonia, June 30, 2002. CWI technical report INS-R0205.
-   (more to come)

## Authors

-   Paulo Moura (language designer, developer, and maintainer)

## Contributors

-   Abramo Bagnara (efficient expansion of once/1 goals and bug reports in corner cases when compiling disjunctions)
-   Andreas Becker (PDT support for Logtalk; bug reports)
-   Anne Ogborn (bug reports, usability suggestions)
-   Artur Miguel Dias (testing, lambda expression examples)
-   Artur Wang (Visual Studio Code support for Logtalk)
-   Arun Majumdar (bug reports, usability suggestions)
-   Barry Evans (dead code scanner tool, usability suggestions)
-   Clara Dimene (GeSHi syntax highlighter)
-   Damien Roch (Docker support)
-   Daniel Gross (documentation feedback and suggestions)
-   Daniel L. Dudley (made the ISO 8601 library object available)
-   Davide Ancona (coinduction examples)
-   Douglas R. Miles (suggestions, bug reports, Logtalk on SWISH experiments)
-   Ebrahim Azarisooreh (code metrics tool, Arch Linux package; made [lgtinit](https://github.com/eazar001/lgtinit) available)
-   Eva Stöwe (PDT support for Logtalk)
-   Feliks Kluzniak (coinduction examples and bug reports)
-   François Fages (meta-predicate safety bug reports)
-   Günter Kniesel (PDT support for Logtalk; feedback on Logtalk OOP features)
-   Gopal Gupta (coinduction examples)
-   Ivan Bratko (search methods in the state-space searching example)
-   Jan Burse (unit tests patches and feedback)
-   Jan Wielemaker (feedback on Prolog compliance testing)
-   Joachim Schimpf (feedback on Prolog compliance testing)
-   Joerg Schuster (bug reports)
-   John Fletcher (made [XML parser](http://www.binding-time.co.uk/xmlpl.html) available)
-   John Stewart (Java interface suggestions and solutions)
-   Joost Geurts (bug reports)
-   Markus Triska (help in porting CLP(FD) examples)
-   Mats Carlsson (bug reports)
-   Michael Covington (DCGs tokenizer example)
-   Michael Hendricks (EDCGs examples and tests)
-   Michael Igler (testing, bug reports)
-   Michael Sheets (text editor support)
-   Michael T. Richter (Textadept text editor support)
-   Neda Saeedloei (coinduction examples)
-   Neng-Fa Zhou (bug reports)
-   Nicolas Pelletier (bug reports, text editor support)
-   Parker Jones (testing, unit tests, bug reports)
-   Paul Brown (bug reports and suggestions)
-   Paul Crocker (testing, multi-threading and meta-predicates examples, bug reports)
-   Paul Fodor (library enhancements)
-   Paul Tarau (feedback on threaded engines API and examples)
-   Paula Marisa Sampaio (state-space searching examples)
-   Paulo Nunes (multi-threading testing)
-   Per Mildner (code for helping decompose file paths and feedback on Prolog compliance testing)
-   Peter Van Roy (EDCGs implementation)
-   rbt (bug reports)
-   Rémy Haemmerlé (meta-predicate safety bug reports)
-   Richard O\'Keefe (heaps and ordered sets library code)
-   Robert Sasak (PDDL 3.0 parser contribution)
-   Robert Shiplett (bug reports)
-   Rui Marques (bug reports)
-   Sergio Castro (Docker support, IntelliJ IDEA support, testing, suggestions, and bug reports)
-   Timon Van Overveldt (multi-threading optimization and bug reports)
-   Theofrastos Mantadelis (\"flags\" contribution, ProbLog integration support, benchmark tests)
-   Ulrich Neumerkel (lambda expression examples, bug reports, and feedback on Prolog compliance testing)
-   Victor Lagerkvist (testing, library enhancements, made [VerdiNeruda](http://joelbyte.github.com/verdi-neruda/) available)
-   Victor Noel (bug reports)
-   Vítor Santos Costa (red-black tree library)
-   Xin Wang (bug reports)

A special thanks to all the Prolog implementers who fixed bugs and
implemented enhancements that greatly helped in improving Logtalk
portability and reliability.

This list may be incomplete. Logtalk contributions and feedback occur in
multiple forms, from private mail to public forums and paper reviews.
Your contributions are greatly appreciated. If your name is missing,
please accept our apologies and contact us so we can fix the omission.
Contact us also if, for some reason, you don\'t want your name on this
list.

## Research support

-   [Center for Research in Advanced Computing Systems
    (CRACS)](http://cracs.fc.up.pt), [INESC
    TEC](https://www.inesctec.pt/en), Portugal

## Sponsors

-   [Kyndi Inc.](http://kyndi.com) --- 2015--2017
-   VivoMind Research, LLC --- 2012--2013

## Open-source credits

Open-source software used by Logtalk development and distribution.

-   [Several open-source Prolog compilers](download.html#requirements) (development)
-   [TextMate](https://github.com/textmate/textmate) (coding)
-   [MacPorts](http://www.macports.org/) (macOS installer)
-   [InnoSetup](http://www.jrsoftware.org/isinfo.php) (Windows installer)
-   [RPM](http://www.rpm.org/) (Linux installer)
-   [dpkg](http://wiki.debian.org/dpkg) (Debian installer)
-   [Git](http://git-scm.com/) (source code version control)
-   [Sphinx](http://www.sphinx-doc.org/en/master/index.html) (HTML, PDF, and ePub documentation)
-   [Read the Docs Sphinx Theme](https://github.com/rtfd/sphinx_rtd_theme) (HTML, PDF, and ePub documentation)
-   [Graphviz](http://graphviz.org) (diagrams)
-   [phpBB](http://www.phpbb.com/) (discussion forums)
-   [WordPress](http://wordpress.org/) (blog)
-   [Jekyll](https://jekyllrb.com) (website)
-   [TeXt Jekyll theme](https://github.com/kitian616/jekyll-TeXt-theme) (website)
-   [roffit](https://github.com/bagder/roffit) (man pages to HTML converter)
