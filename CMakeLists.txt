CMAKE_MINIMUM_REQUIRED(VERSION 3.7)
PROJECT(document_project NONE)
FIND_PACKAGE(LATEX)
SET(PDFLATEX_COMPILER xelatex)
SET(LATEX_DEFAULT_BUILD pdf)
#SET(LATEX_OUTPUT_PATH build)
INCLUDE(UseLATEX.cmake)
SET(parts
    espd.cls # Класс настроек ЕСПД
    document/аннотация.tex
    document/оформление_разделов.tex
    document/оформление_перечислений.tex
    document/оформление_иллюстраций.tex
    document/оформление_формул.tex
    document/оформление_таблиц.tex
    document/оформление_листингов.tex
    document/термины.tex
    document/аббревиатуры.tex
    document/приложение_1.tex
    document/приложение_2.tex
)
ADD_LATEX_DOCUMENT(
    document.tex
    BIBFILES bibliography.bib
    IMAGE_DIRS images
    INPUTS ${parts}    
)
# Команда копирует результирующий файл main.pdf в папку /output с переименованием
add_custom_command(
        TARGET document
        COMMAND ${CMAKE_COMMAND} -E copy
                ${CMAKE_CURRENT_SOURCE_DIR}/build/document.pdf
                ${CMAKE_CURRENT_SOURCE_DIR}/output/output.pdf)
