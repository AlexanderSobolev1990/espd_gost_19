CMAKE_MINIMUM_REQUIRED(VERSION 3.7)
PROJECT(main_project NONE)
FIND_PACKAGE(LATEX)
SET(PDFLATEX_COMPILER xelatex)
SET(LATEX_DEFAULT_BUILD pdf)
#SET(LATEX_OUTPUT_PATH build)
INCLUDE(UseLATEX.cmake)
SET(parts
    espd.cls # Класс настроек ЕСПД
    аннотация.tex
    оформление_разделов.tex
    оформление_перечислений.tex
    оформление_иллюстраций.tex
    оформление_формул.tex
    оформление_таблиц.tex
    оформление_листингов.tex
    термины.tex
    аббревиатуры.tex
    приложение_1.tex
    приложение_2.tex
)
ADD_LATEX_DOCUMENT(
    main.tex
    BIBFILES список_литературы.bib
    IMAGE_DIRS ./иллюстрации/
    INPUTS ${parts}    
)
# Команда копирует результирующий файл main.pdf в папку /output с переименованием
add_custom_command(
        TARGET main
        COMMAND ${CMAKE_COMMAND} -E copy
                ${CMAKE_CURRENT_SOURCE_DIR}/build/main.pdf
                ${CMAKE_CURRENT_SOURCE_DIR}/output/output.pdf)
