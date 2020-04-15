---
title: Comandos e funções do Visual FoxPro sem suporte | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- FoxPro ODBC driver [ODBC], commands and functions
- functions [ODBC], Visual FoxPro
- Visual FoxPro ODBC driver [ODBC], commands and functions
- Visual FoxPro commands and functions
- FoxPro ODBC driver
ms.assetid: afdb6b7e-738d-42ca-8053-67ae50873ca6
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7e5b8ed06ad9f996d644df0dfb99d15adcff86bc
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307647"
---
# <a name="unsupported-visual-foxpro-commands-and-functions-visual-foxpro-odbc-driver"></a>Comandos e funções do Visual FoxPro sem suporte (Driver ODBC do Visual FoxPro)
A tabela a seguir lista comandos e funções foxpro que não são suportados pelo Visual FoxPro ODBC Driver, mas são suportados pelo Visual FoxPro®® da Microsoft.  
  
 Se o aplicativo interagir com dados cujas regras, gatilhos, valores padrão ou procedimentos armazenados chamem esses comandos ou funções do Visual FoxPro, o driver pode gerar um erro.  
  
## <a name="unsupported-visual-foxpro-commands-and-functions"></a>Comandos e funções do Visual FoxPro sem suporte  
  
||||  
|-|-|-|  
|#DEFINE... #UNDEF|#IF ... #ENDIF Diretiva de Pré-Processador|&#124; #IFDEF #IFNDEF &#124;|  
|Diretiva de pré-processador #INCLUDE|:: Operador de Resolução de Escopo|! Comando (ver RUN &#124; ! Comando)|  
|? &#124;?? Comando|??? Comando|\ \\&#124; \ Comando|  
|@ ... Comando BOX|@ ... Comando CLASS|@ ... Comando CLEAR|  
|@ ... EDIT - Editar comando caixas|@ ... Comando de Preenchimento|@ ... Obter|  
|@ ... Comando MENU|@ ... Comando PROMPT|@ ... Comando SAY|  
|@ ... Comando SCROLL|@ ... Comando PARA||  
  
## <a name="a"></a>Um  
  
||||  
|-|-|-|  
|Comando ACEITAR|Função ACLASS( )|Ativar menu|  
|ATIVAR comando POPUP|Ativar comando SCREEN|ATIVAR comando janela|  
|Método ActivateCell|Adicionar comando de classe|Função ADIR|  
|Função AFONT|Função AINSTANCE( )|Variável de memória do sistema _ALIGNMENT|  
|Função AMEMBERS|Função ANSITOOEM|Função APRINTERS|  
|Função ASELOBJ|Comando ASSIST||  
  
## <a name="b"></a>B  
  
||||  
|-|-|-|  
|FUNÇÃO BAR|FUNÇÃO BARCOUNT|FUNÇÃO BARPROMPT|  
|Variável de memória do sistema _BEAUTIFY|_BOX variável de memória do sistema|Procurar comando|  
|variável de memória do sistema _BROWSER|Comando BUILD APP|CONSTRUIR Comando EXE|  
|Comando de PROJETO DE CONSTRUÇÃO|_BUILDER variável de memória do sistema||  
  
## <a name="c"></a>C  
  
||||  
|-|-|-|  
|_CALCVALUE variável de memória do sistema|Variável de memória do sistema _CLIPTEXT|_CONVERTER variável de memória do sistema|  
|_CUROBJ variável de memória do sistema|Comando CALL|Comando Cancelar|  
|CAPSLOCK( ) Função|Comando CD|Comando CHANGE|  
|Comando CHDIR|FUNÇÃO CHRSAW|Comando CLOSE MEMO|  
|FUNÇÃO CNTBAR|Função CNTPAD|Função COL|  
|Comando Compile|Compilar comando de banco de dados|Comando de FORMULÁRIO DE COMPILAÇÃO|  
|FUNÇÃO COMPOBJ|Objeto de contêiner|Objeto de controle|  
|Comando COPY FILE|Comando COPY MEMO|CRIAR comando de classe|  
|CRIAR comando CLASSLIB|CRIAR comando conjunto de cores|Comando CREATE|  
|CRIAR Comando CONNECTION|CRIAR comando de banco de dados|CRIAR Comando FORM|  
|CRIAR A PARTIR DO Comando|CRIAR comando LABEL|Criar comando menu|  
|CRIAR Comando DE PROJETO|CRIAR comando de consulta|Criar comando de relatório|  
|CRIAR Comando SCREEN|CRIAR comando SQL VIEW|CRIAR comando trigger|  
|CRIAR Comando VIEW|FUNÇÃO CREATEOBJECT|FUNÇÃO CURDIR|  
  
## <a name="d"></a>D  
  
||||  
|-|-|-|  
|Variável de memória do sistema _DBLCLICK|Variável de memória do sistema _DIARYDATE|Função DBSETPROP|  
|Funções DDE|DEsativar o comando MENU|DEsativação do comando POPUP|  
|DEsativação do comando janela|DECLARE - Comando DLL|Comando DECLARE|  
|DEFINIR Comando BAR|DEFINIR Comando BOX|DEFINIR Comando de Classe|  
|DEFINIR Comando MENU|DEFINIR Comando PAD|DEFINIR Comando POPUP|  
|DEFINIR comando janela|Comando DELETE CONNECTION|EXCLUA o comando do banco de dados|  
|Comando DELETE FILE|EXCLUA o comando TRIGGER|EXCLUA o comando VIEW|  
|Comando DIR|Comando do diretório|Comando DISPLAY|  
|Comando DISPLAY CONNECTIONS|COMANDO DE BANCO DE DADOS DE EXIBIÇÃO|Comando DLLS DE DISPLAY|  
|Comando ARQUIVOS DE EXIBIÇÃO|Comando DISPLAY MEMORY|Comando de objetos de EXIBIÇÃO|  
|Comando PROCEDIMENTOS DE EXIBIÇÃO|Comando DE STATUS DE EXIBIÇÃO|Comando DISPLAY STRUCTURE|  
|Comando tabelas de exibição|COMANDO EXIBIÇÃO DE VISUALIZAÇÕES|Comando DO FORM|  
  
## <a name="e"></a>E  
  
||||  
|-|-|-|  
|Comando EDIT|Comando ERROR||  
|Comando APAGAR|Comando EXTERNO|Comando de EXPORTAÇÃO|  
|Comando EJECT|Comando EJECT PAGE||  
  
## <a name="f"></a>F  
  
||||  
|-|-|-|  
|variável de memória do sistema _FOXDOC|_FOXGRAPH variável de memória do sistema|FEOF( ) Função|  
|Função FCLOSE( )|Função FCREATE|Função FGETS|  
|Função FERROR|Função FFLUSH( )|Função FKLABEL( )|  
|Comando FILER|Encontrar comando|Função FOPEN|  
|Função FKMAX|FUNÇÃO FONTMETRIC( )|Função FSEEK|  
|Função FPUTS( )|Função FREAD( )||  
|Função FWRITE|Função FCHSIZE||  
  
## <a name="g"></a>G  
  
||||  
|-|-|-|  
|_GENGRAPH variável de memória do sistema|Variável de memória do sistema _GENMENU|Variável de memória do sistema _GENPD|  
|Variável de memória do sistema _GENSCRN|_GENXTAB variável de memória do sistema|FUNÇÃO GETBAR|  
|FUNÇÃO GETCOLOR|FUNÇÃO GETDIR|Comando GETEXPR|  
|FUNÇÃO GETFILE( )|FUNÇÃO GETFONT( )|FUNÇÃO GETOBJECT( )|  
|FUNÇÃO GETPAD|FUNÇÃO GETPICT|FUNÇÃO GETPRINTER|  
  
## <a name="h"></a>H  
  
||||  
|-|-|-|  
|Comando DE AJUDA|Comando Ocultar menu|Comando HIDE POPUP|  
|Comando HIDE WINDOW|HOME( ) Função||  
  
## <a name="i"></a>I  
  
||||  
|-|-|-|  
|Função IMESTATUS( )|Comando IMPORT|Comando INPUT|  
|ÍNDICE NO Comando|INKEY( ) Função|FUNÇÃO ISCOLOR|  
|Inserir comando|FUNÇÃO INSMODE||  
|FUNÇÃO ISMOUSE|_INDENT Variável de Memória do Sistema||  
  
## <a name="j"></a>J  
  
||||  
|-|-|-|  
|Comando JOIN|||  
  
## <a name="k"></a>K  
  
||||  
|-|-|-|  
|Comando KEYBOARD|||  
  
## <a name="l"></a>L  
  
||||  
|-|-|-|  
|_LMARGIN variável de memória do sistema|Comando LABEL|ÚLTIMA CHAVE( ) Função|  
|LINENO( ) Função|Comandos LIST|COMANDO CONEXÕES DE LISTA|  
|Comando LOAD|Função LOCFILE( )||  
  
## <a name="m"></a>M  
  
||||  
|-|-|-|  
|Função MCOL|MD Comando|MENU PARA Comando|  
|FUNÇÃO MEMÓRIA ( )|Comando MENU|Comando MKDIR|  
|FUNÇÃO MENU|Função MESSAGEBOX( )|COMANDO MODIFICAR CONEXÃO|  
|MODIFICAR Comando de Classe|Comando DE COMANDO MODIFICAR|Comando MODIFY FORM|  
|MODIFICAR Comando DE BANCO DE DADOS|Comando MODIFY FILE|MODIFICAR Comando MEMO|  
|COMANDO MODIFICADO Geral|COMANDO MODIFICAR RÓTULO|COMANDO MODIFICAR Projeto|  
|Comando MODIFICAR MENU|COMANDO MODIFICAR Procedimento|Comando MODIFY SCREEN|  
|COMANDO MODIFICAR CONSULTA|COMANDO MODIFICAR RELATÓRIO|COMANDO MODIFICAR JANELA|  
|COMANDO MODIFICAR ESTRUTURA|Comando MODIFY VIEW|Comando MOVE WINDOW|  
|Comando MOUSE|Comando MOVE POPUP|Função MROW|  
|Função MRKBAR|Função MRKPAD||  
|Função MWINDOW( )|Função MDOWN( )||  
  
## <a name="n"></a>N  
  
||||  
|-|-|-|  
|Função NUMLOCK( )|||  
  
## <a name="o"></a>O   
  
||||  
|-|-|-|  
|OBJNUM( ) Função|Função OBJTOCLIENT|Comando ON BAR|  
|OEMTOANSI( ) Função|No comando APLABOUT|Comando ON EXIT MENU|  
|No comando ESCAPE|Comando ON EXIT BAR|NA CHAVE = Comando|  
|Comando ON EXIT PAD|Comando POPUP DE SAÍDA|Comando ON PAD|  
|Comando ON KEY LABEL|Comando ON MACHELP|Comando ON SELECTION BAR|  
|Comando ON PAGE|Comando ON READERROR|NO Comando POPUP DE SELEÇÃO|  
|Comando NO MENU DE SELEÇÃO|Comando ON SELECTION PAD||  
|No comando SHUTDOWN|OBJVAR( ) Função||  
  
## <a name="p"></a>P  
  
||||  
|-|-|-|  
|Variável de memória do sistema _PADVANCE|Variável de memória do sistema _PAGENO|_PBPAGE variável de memória do sistema|  
|Variável de memória do sistema _PCOLNO|_PCOPIES variável de memória do sistema|Variável de memória do sistema _PDRIVER|  
|_PDSETUP variável de memória do sistema|_PECODE Variável de memória do sistema|Variável de memória do sistema _PEJECT|  
|_PEPAGE variável de memória do sistema|variável de memória do sistema _PLENGTH|Variável de memória do sistema _PLINENO|  
|_PLOFFSET variável de memória do sistema|Variável de memória do sistema _PPITCH|_PQUALITY variável de memória do sistema|  
|_PRETEXT variável de memória do sistema|Variável de memória do sistema _PSCODE|_PSPACING variável de memória do sistema|  
|Variável de memória do sistema _PWAIT|Comando de banco de dados de pacotes|Função PAD|  
|PCOL( ) Função|Função PEMSTATUS( )|Comando PLAY MACRO|  
|Comando POP KEY|Comando POP MENU|Comando POP-UP POPUP|  
|FUNÇÃO POPUP|PRINTJOB ... Comando ENDPRINTJOB|FUNÇÃO PRINTSTATUS( )|  
|Função PRMBAR|Função PRMPAD|Função PROMPT( )|  
|Função PROW( )|PRTINFO( ) Função|Comando PUSH KEY|  
|Comando PUSH MENU|Comando PUSH POPUP|PUTFILE( ) Função|  
  
## <a name="q"></a>Q  
  
||||  
|-|-|-|  
|Comando QUIT|||  
  
## <a name="r"></a>R  
  
||||  
|-|-|-|  
|_RMARGIN Variável de Memória do Sistema|Comando RD|Função READKEY( )|  
|Comando READ|LEIA O COMANDO MENU|Comando BAR DE LANÇAMENTO|  
|Função REFRESH()|Comando ReINDEX|Comando DA BIBLIOTECA DE LIBERAÇÃO|  
|RELEASE CLASSLIB Command|Comando de LIBERAÇÃO|Comando do PAD DE LIBERAÇÃO|  
|Comando MENUS DE LANÇAMENTO|Comando DO MÓDULO DE LANÇAMENTO|Comando DE LIBERAÇÃO DO WINDOWS|  
|RELEASE POPUPS Command|Comando DE PROCEDIMENTO DE LIBERAÇÃO|Comando RENAME|  
|REMOVER comando class|COMANDO RENOMEAR CLASSE|Comando RENAME VIEW|  
|Comando DE CONEXÃO RENAME|Comando de tabela de renomeação|RESTAURAR DO Comando|  
|Comando de RELATÓRIO|Função REQUERY( )|Comando DE JANELA DE RESTAURAÇÃO|  
|RESTAURAR comando MACROS|Comando RESTAURAR TELA|RGBSCHEME( ) Função|  
|Comando RETOMAR|Função RGB|CORRA &#124;! Comando|  
|Comando RMDIR|FUNÇÃO ROW( )||  
|Comando RUNSCri|FUNÇÃO RDLEVEL( )||  
  
## <a name="s"></a>S  
  
||||  
|-|-|-|  
|Comando SAVE MACROS|Comando SAVE SCREEN|SALVAR PARA Comando|  
|Comando SAVE WINDOWS|ESQUEMA( ) Função|Função SCOLS|  
|Comando SCROLL|Variável de memória do sistema _SCREEN|Comando SET|  
|DEFINIR Comando ALTERNATIVO|Comando SET ANSI|DEFINIR comando APLABOUT|  
|DEFINIR comando AUTOSAVE|Comando SET BELL|SET Comando BLINK|  
|Comando de fronteira set|DEFINIR comando BRSTATUS|Comando CLASSLIB DEFINIDO|  
|DEFINIR comando CLEAR|Comando SET CLOCK|DEFINIR COR DO Comando|  
|DEFINIR COR DO COMANDO DO ESQUEMA|Definir comando CONJUNTO DE CORES|DEFINIR COR PARA Comando|  
|DEFINIR Comando COMPATÍVEL|SET CONFIRMAR Comando|Comando SET CONSOLE|  
|DEFINIR CPCOMPILE|DEFINIR CPDIALOG|DEFINIR comando de moeda|  
|Definir comando cursor|DEFINIR comando DATASESSION|Definir comando DEBUG|  
|Comando SET DECIMALS|Definir comando Delimiters|Comando DE DESENVOLVIMENTO DEFINIDO|  
|Comando SET DEVICE|Comando SET DISPLAY|COMANDO SET DOHISTORY|  
|SET Comando ECHO|Comando SET ESCAPE|Comando SET FORMAT|  
|Comando SET FUNCTION|COMANDO SET HEADINGS|Set COMANDO HELP|  
|DEFINIR comando HELPFILTER|COMANDO SET INTENSITY|Definir comando KEY|  
|Definir comando KEYCOMP|DEFINIR comando LOGERRORS|DEFINIR comando MACDESKTOP|  
|Set Comando MACHELP|Set Comando MACKEY|Definir comando MARGEM|  
|DEFINIR MARCA DE COMANDO|DEFINIR MARCA PARA Comando|DEFINIR comando MEMOWIDTH|  
|Comando SET MESSAGE|COMANDO SET MOUSE|COMANDO SET ODÔMETRO|  
|Comando SET OLEOBJECT|Comando SET PALETTE|Definir comando PDSETUP|  
|Comando SET POINT|Definir comando IMPRESSORA|SET COMANDO READBORDER|  
|Set Comando REFRESH|Definir comando DE RECURSOS|DEFINIR comando de segurança|  
|Definir comando placar|Comando SET SECONDS|DEFINIR comando SEPARADOR|  
|COMANDO SET SHADOWS|DEFINIR PULAR DE Comando|Comando SPACE SET|  
|Definir comando status|DEFINIR comando BARRA DE STATUS|Comando SET STEP|  
|Comando SET STICKY|COMANDO SET SYSFORMATS|Comando SET SYSMENU|  
|Comando SET TALK|DEFINIR comando TEXTMERGE|DEFINIR comando TEXTMERGE DELIMITERS|  
|Definir comando TÓPICO|DEFINIR comando de id tópico|DEFINIR Comando TRBetween|  
|DEFINIR comando TYPEAHEAD|Comando SET VIEW|DEFINIR JANELA DO COMANDO MEMO|  
|DEFINIR o comando XCMDFILE|_SHELL variável de memória do sistema|Comando SHOW GET|  
|Comando SHOW GETS|Comando SHOW MENU|Comando SHOW OBJECT|  
|Comando SHOW POPUP|Comando DE JANELA SHOW|Comando SIZE POPUP|  
|Comando DE JANELA DE TAMANHO|Função SKPBAR|Função SKPPAD|  
|FUNÇÃO SOUNDEX|_SPELLCHK variável de memória do sistema|Funções SQL|  
|Função SROWS( )|Variável de memória do sistema _STARTUP|Comando SUSPENDER|  
|Funções SYS() exceto SYS(2011)|Função SisMETRIC||  
  
## <a name="t"></a>T  
  
||||  
|-|-|-|  
|_TABS variável de memória do sistema|Texto... Comando ENDText|Função TXTWIDTH( )|  
|FUNÇÃO TRANSFORM( )|variável de memória do sistema _TRANSPORT||  
|Comando TYPE|_THROTTLE variável de memória do sistema||  
  
## <a name="u"></a>U  
  
||||  
|-|-|-|  
|ATUALIZADO( ) Função|Comando USE||  
  
## <a name="v"></a>V  
  
||||  
|-|-|-|  
|Comando VALIDATE DATABASE|VARREAD( ) Função|FUNÇÃO VERSION( )|  
  
## <a name="w"></a>W  
  
||||  
|-|-|-|  
|Variável de memória do sistema _WINDOWS|_WIZARD Variável de memória do sistema|WCHILD( ) Função|  
|Comando WAIT|Função WBORDER( )|Função WFONT( )|  
|WCOLS( ) Função|Função WEXIST( )|WLROW( ) Função|  
|Com... Comando ENDWITH|Função WLAST|FUNÇÃO WONTOP( )|  
|WMAXIMUM( ) Função|WLCOL( ) Função|WREAD( ) Função|  
|WOUTPUT ( ) Função|WMINIMUM( ) Função|Função WVISIBLE( )|  
|Função WPARENT( )|WTITLE( ) Função||  
|WROWS() Função|Variável de memória do sistema _WRAP||  
  
## <a name="z"></a>Z  
  
||||  
|-|-|-|  
|Comando ZOOM WINDOW|||
