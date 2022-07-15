CMAKE_MINIMUM_REQUIRED(VERSION 3.7)
PROJECT(main_project NONE)
FIND_PACKAGE(LATEX)
SET(PDFLATEX_COMPILER xelatex)
SET(LATEX_DEFAULT_BUILD pdf)
#SET(LATEX_OUTPUT_PATH build)
INCLUDE(UseLATEX.cmake)
SET(parts
    espd.cls
    annotation.tex
    all2.tex
#    section_1.tex        
#    notepad.png
)
ADD_LATEX_DOCUMENT(
    main.tex
    BIBFILES lit2.bib
    INPUTS ${parts}    
)
add_custom_command(
        TARGET main
        COMMAND ${CMAKE_COMMAND} -E copy
                ${CMAKE_CURRENT_SOURCE_DIR}/build/main.pdf
                ${CMAKE_CURRENT_SOURCE_DIR}/output/output.pdf)
