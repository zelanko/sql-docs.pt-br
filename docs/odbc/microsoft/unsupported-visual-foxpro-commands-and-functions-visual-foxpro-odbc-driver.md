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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: db6aff35944b8811e79627c6076ab61e838edf3f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67912318"
---
# <a name="unsupported-visual-foxpro-commands-and-functions-visual-foxpro-odbc-driver"></a>Comandos e funções do Visual FoxPro sem suporte (Driver ODBC do Visual FoxPro)
A tabela a seguir lista os comandos e funções do FoxPro que não têm suporte do driver ODBC do Visual FoxPro, mas têm suporte do Microsoft® Visual FoxPro®.  
  
 Se seu aplicativo interage com dados cujas regras, gatilhos, valores padrão ou procedimentos armazenados chamam esses comandos ou funções do Visual FoxPro, o driver pode gerar um erro.  
  
## <a name="unsupported-visual-foxpro-commands-and-functions"></a>Comandos e funções do Visual FoxPro sem suporte  
  
||||  
|-|-|-|  
|#DEFINE... #UNDEF|#IF... #ENDIF diretiva de pré-processador|#IFDEF &#124; #IFNDEF|  
|Diretiva de pré-processador de #INCLUDE|:: Operador de resolução de escopo|! (Consulte executar &#124;! Linha|  
|? &#124;?? Comando|??? Comando|Comando \ \\&#124; \|  
|@ ... Comando BOX|@ ... Comando de classe|@ ... Limpar comando|  
|@ ... Comando editar caixas de edição|@ ... Comando FILL|@ ... Obter|  
|@ ... Comando de MENU|@ ... Comando de PROMPT|@ ... Comando digamos|  
|@ ... Comando SCROLL|@ ... PARA o comando||  
  
## <a name="a"></a>Um  
  
||||  
|-|-|-|  
|ACEITAR comando|Função ACLASS ()|ATIVAR comando de MENU|  
|ATIVAR o comando POPUP|Comando ativar tela|Comando ativar janela|  
|Método ActivateCell|Adicionar comando de classe|Função ADIR ()|  
|Função AFONT ()|Função AINSTANCE ()|Variável de memória do sistema _ALIGNMENT|  
|Função AMEMBERS ()|Função ANSITOOEM ()|Função APRINTERS ()|  
|Função ASELOBJ ()|Comando auxiliar||  
  
## <a name="b"></a>B  
  
||||  
|-|-|-|  
|Função BAR ()|Função BARCOUNT ()|Função BARPROMPT ()|  
|Variável de memória do sistema _BEAUTIFY|Variável de memória do sistema _BOX|Comando procurar|  
|Variável de memória do sistema _BROWSER|Comando COMPILAR aplicativo|Comando de BUILD EXE|  
|Comando COMPILAR projeto|Variável de memória do sistema _BUILDER||  
  
## <a name="c"></a>C  
  
||||  
|-|-|-|  
|Variável de memória do sistema _CALCVALUE|Variável de memória do sistema _CLIPTEXT|Variável de memória do sistema _CONVERTER|  
|Variável de memória do sistema _CUROBJ|CHAMAR comando|Comando CANCEL|  
|Função CAPSLOCK ()|Comando CD|ALTERAR comando|  
|Comando CHDIR|Função CHRSAW ()|FECHAR comando de memorando|  
|Função CNTBAR ()|Função CNTPAD ()|Função COL ()|  
|Comando de compilação|Comando COMPILAR banco de dados|Comando COMPILAR formulário|  
|Função COMPOBJ ()|Objeto de contêiner|Objeto de controle|  
|Comando Copiar arquivo|Comando copiar memorando|Comando criar classe|  
|CRIAR comando CLASSLIB|Comando criar conjunto de cores|Comando CREATE|  
|Comando criar conexão|Comando criar banco de dados|Comando Criar formulário|  
|CRIAR do comando|Comando criar rótulo|Comando criar MENU|  
|Comando Criar projeto|Comando Criar consulta|Comando criar relatório|  
|Comando criar tela|Comando CREATE SQL VIEW|CRIAR comando de gatilho|  
|Comando CREATE VIEW|Função CREATEOBJECT ()|Função CURDIR ()|  
  
## <a name="d"></a>D  
  
||||  
|-|-|-|  
|Variável de memória do sistema _DBLCLICK|Variável de memória do sistema _DIARYDATE|Função DBSETPROP ()|  
|Funções DDE|Comando desativar MENU|DESATIVAR comando POPUP|  
|Comando desativar janela|Comando DECLARE-DLL|Comando DECLARE|  
|Definir comando de barra|Comando definir caixa|Definir comando de classe|  
|Definir comando de MENU|Definir comando de preenchimento|Definir comando POPUP|  
|Definir comando de janela|Comando excluir conexão|Comando excluir banco de dados|  
|Comando excluir arquivo|Excluir comando de gatilho|Excluir comando de exibição|  
|Comando DIR|Comando de diretório|Comando de exibição|  
|Comando exibir conexões|Comando exibir banco de dados|Comando exibir DLLS|  
|Comando exibir arquivos|Comando DISPLAY MEMORY|Comando exibir objetos|  
|Comando exibir procedimentos|EXIBIR o comando de STATUS|Comando exibir estrutura|  
|Comando exibir tabelas|Comando exibir EXIBIções|Comando DO formulário|  
  
## <a name="e"></a>E  
  
||||  
|-|-|-|  
|Comando de edição|Comando de erro||  
|Comando ERASE|Comando externo|Comando de exportação|  
|Comando EJECT|Comando EJETAr página||  
  
## <a name="f"></a>F  
  
||||  
|-|-|-|  
|Variável de memória do sistema _FOXDOC|Variável de memória do sistema _FOXGRAPH|Função FEOF ()|  
|Função FCLOSE ()|Função FCREATE ()|Função FGETS ()|  
|Função REFERENCIAdora ()|Função FFLUSH ()|Função FKLABEL ()|  
|Comando FILEr|Comando FIND|Função FOPEN ()|  
|Função FKMAX ()|Função FONTMETRIC ()|Função FSEEK ()|  
|Função FPUTS ()|Função FREAD ()||  
|Função FWRITE ()|Função FCHSIZE ()||  
  
## <a name="g"></a>G  
  
||||  
|-|-|-|  
|Variável de memória do sistema _GENGRAPH|Variável de memória do sistema _GENMENU|Variável de memória do sistema _GENPD|  
|Variável de memória do sistema _GENSCRN|Variável de memória do sistema _GENXTAB|Função GETBAR ()|  
|Função GetColor ()|Função GETDIR ()|Comando GETEXPR|  
|Função GetFile ()|Função GetFont ()|Função GetObject ()|  
|Função GETPAD ()|Função getpict ()|Função getprinter ()|  
  
## <a name="h"></a>H  
  
||||  
|-|-|-|  
|Comando de ajuda|Ocultar comando de MENU|Ocultar comando POPUP|  
|Ocultar comando de janela|Função HOME ()||  
  
## <a name="i"></a>I  
  
||||  
|-|-|-|  
|Função IMESTATUS ()|Comando de importação|Comando de entrada|  
|ÍNDICE no comando|Função INKEY ()|Função IsColor ()|  
|INSERIR comando|Função INSMODE ()||  
|Função ismouse ()|Variável de memória do sistema _INDENT||  
  
## <a name="j"></a>J  
  
||||  
|-|-|-|  
|Comando JOIN|||  
  
## <a name="k"></a>K  
  
||||  
|-|-|-|  
|Comando de teclado|||  
  
## <a name="l"></a>L  
  
||||  
|-|-|-|  
|Variável de memória do sistema _LMARGIN|Comando de rótulo|Função LASTKEY ()|  
|Função LINENO ()|LISTAr comandos|Comando LISTAr conexões|  
|CARREGAR comando|Função LOCFILE ()||  
  
## <a name="m"></a>M  
  
||||  
|-|-|-|  
|Função MCOL ()|Comando MD|MENU para comando|  
|Função MEMORY ()|Comando de MENU|Comando MKDIR|  
|Função MENU ()|Função MESSAGEBOX ()|Comando Modificar conexão|  
|Comando modificar classe|MODIFICAR comando de comando|Comando modificar formulário|  
|Comando modificar banco de dados|Comando MODIFY FILE|MODIFICAR comando de memorando|  
|MODIFICAR o comando geral|Comando modificar rótulo|Comando modificar projeto|  
|MODIFICAR comando de MENU|Comando modificar procedimento|Comando modificar tela|  
|MODIFICAR comando de consulta|MODIFICAR comando de relatório|MODIFICAR comando de janela|  
|Comando modificar estrutura|MODIFICAR o comando de exibição|Comando mover janela|  
|Comando do MOUSE|MOVER comando pop-up|Função MROW ()|  
|Função MRKBAR ()|Função MRKPAD ()||  
|Função MWINDOW ()|Função MDOWN ()||  
  
## <a name="n"></a>N  
  
||||  
|-|-|-|  
|Função NUMLOCK ()|||  
  
## <a name="o"></a>O  
  
||||  
|-|-|-|  
|Função OBJNUM ()|Função OBJTOCLIENT ()|Comando de barra|  
|Função OEMTOANSI ()|NO comando APLABOUT|NO comando de MENU sair|  
|NO comando de ESCAPE|No comando da barra de saída|NO comando KEY =|  
|NO comando sair do painel|AO sair do comando POPUP|Comando no PAD|  
|NO comando rótulo da chave|NO comando MACHELP|No comando da barra de seleção|  
|Comando na página|NO comando READERROR|Comando pop-up na seleção|  
|No comando de MENU de seleção|NO comando painel de seleção||  
|NO comando de desligamento|Função OBJVAR ()||  
  
## <a name="p"></a>P  
  
||||  
|-|-|-|  
|Variável de memória do sistema _PADVANCE|Variável de memória do sistema _PAGENO|Variável de memória do sistema _PBPAGE|  
|Variável de memória do sistema _PCOLNO|Variável de memória do sistema _PCOPIES|Variável de memória do sistema _PDRIVER|  
|Variável de memória do sistema _PDSETUP|Variável de memória do sistema _PECODE|Variável de memória do sistema _PEJECT|  
|Variável de memória do sistema _PEPAGE|Variável de memória do sistema _PLENGTH|Variável de memória do sistema _PLINENO|  
|Variável de memória do sistema _PLOFFSET|Variável de memória do sistema _PPITCH|Variável de memória do sistema _PQUALITY|  
|Variável de memória do sistema _PRETEXT|Variável de memória do sistema _PSCODE|Variável de memória do sistema _PSPACING|  
|Variável de memória do sistema _PWAIT|Comando do banco de dados do pacote|Função PAD ()|  
|Função PCOL ()|Função PEMSTATUS ()|Comando reproduzir MACRO|  
|Comando de tecla POP|Comando do MENU POP|Comando POP POPUP|  
|Função POPUP ()|PRINTJOB... Comando ENDPRINTJOB|Função distatus ()|  
|Função PRMBAR ()|Função PRMPAD ()|Função PROMPT ()|  
|Função PROW ()|Função PRTINFO ()|Comando PUSH KEY|  
|Comando de MENU de PUSH|Comando pop-up de PUSH|Função PUTFILE ()|  
  
## <a name="q"></a>Q  
  
||||  
|-|-|-|  
|Comando QUIT|||  
  
## <a name="r"></a>R  
  
||||  
|-|-|-|  
|Variável de memória do sistema _RMARGIN|Comando RD|Função READKEY ()|  
|Comando de leitura|Comando de MENU ler|Comando da barra de versão|  
|Função REFRESH ()|Comando REINDEX|Comando liberar biblioteca|  
|Comando RELEASE CLASSLIB|Comando de liberação|Comando do painel de liberação|  
|Comando liberar MENUS|Comando do módulo versão|Comando liberar o WINDOWS|  
|Comando liberar pop-ups|Comando liberar procedimento|Renomear comando|  
|Comando remover classe|Comando renomear classe|Comando renomear exibição|  
|Comando renomear conexão|Comando renomear tabela|RESTAURAR do comando|  
|Comando de relatório|Função Requery ()|Comando restaurar janela|  
|Comando restaurar MACROs|Comando restaurar tela|Função RGBSCHEME ()|  
|Comando retomar|Função RGB ()|EXECUTE &#124;! Comando|  
|Comando RMDIR|Função ROW ()||  
|Comando RUNSCRIPT|Função RDLEVEL ()||  
  
## <a name="s"></a>S  
  
||||  
|-|-|-|  
|Comando salvar MACROs|Comando salvar tela|SALVAR no comando|  
|Comando salvar WINDOWS|Função SCHEME ()|Função SCOLS ()|  
|Comando SCROLL|Variável de memória do sistema _SCREEN|Comando SET|  
|Definir comando alternativo|Comando SET ANSI|Comando SET APLABOUT|  
|Definir comando AutoSalvar|Definir comando BELL|Definir comando de intermitência|  
|Comando SET BORDER|Comando SET BRSTATUS|Comando SET CLASSLIB|  
|Definir comando de limpeza|Definir comando de relógio|DEFINIR cor do comando|  
|DEFINIR cor do comando de esquema|Definir comando de conjunto de cores|DEFINIR cor como comando|  
|Definir comando compatível|Comando SET CONFIRM|Definir comando do CONSOLE|  
|DEFINIR CPCOMPILE|DEFINIR CPDIALOG|Definir comando de moeda|  
|Definir comando de CURSOR|Comando SET datasession|Definir comando de depuração|  
|Comando SET DECIMALs|Comando definir delimitadores|Definir comando de desenvolvimento|  
|Definir comando de dispositivo|Definir comando de exibição|Comando SET dohistory|  
|Comando SET ECHO|Definir comando de ESCAPE|Comando SET FORMAT|  
|Comando SET FUNCTION|Comando definir títulos|Comando SET HELP|  
|Comando SET HELPFILTER|Definir comando de intensidade|Comando SET KEY|  
|Comando SET keycomp|Comando SET LOGERRORS|Comando SET MACDESKTOP|  
|Comando SET MACHELP|Comando SET MACKEY|Definir comando de margem|  
|DEFINIR marca de comando|DEFINIR marca como comando|Comando SET MEMOWIDTH|  
|Comando SET MESSAGE|Definir comando do MOUSE|Comando SET HODÔMETRO|  
|Comando SET OLEOBJECT|Comando definir paleta|Comando SET PDSETUP|  
|Comando SET POINT|Definir comando de impressora|Comando SET READBORDER|  
|Comando SET REFRESH|Definir comando de recurso|Definir comando de segurança|  
|Comando SET placar|Comando SET SECONDs|Definir comando separador|  
|Comando SET SHADOWs|DEFINIR ignorar comando|Comando SET SPACE|  
|Definir comando de STATUS|Definir comando da barra de STATUS|Comando SET STEP|  
|Definir comando adesivo|Comando SET SYSFORMATS|Comando SET SYSMENU|  
|Comando SET TALK|Definir comando textmerge|Comando definir delimitadores de textmerge|  
|Comando SET TOPIC|Definir comando de ID do tópico|Comando SET TRBETWEEN|  
|Comando SET TYPEAHEAD|Comando SET VIEW|DEFINIR janela do comando de memorando|  
|Comando SET XCMDFILE|Variável de memória do sistema _SHELL|Mostrar comando GET|  
|Mostrar comando GETS|Mostrar comando de MENU|Comando SHOW OBJECT|  
|Mostrar comando POPUP|Mostrar comando de janela|Comando de tamanho POPUP|  
|Comando dimensionar janela|Função SKPBAR ()|Função SKPPAD ()|  
|Função SOUNDEX ()|Variável de memória do sistema _SPELLCHK|Funções SQL|  
|Função SROWS ()|Variável de memória do sistema _STARTUP|Comando SUSPENDEr|  
|Funções SYS (), exceto SYS (2011)|Função SYSMETRIC ()||  
  
## <a name="t"></a>T  
  
||||  
|-|-|-|  
|Variável de memória do sistema _TABS|TEXTO... Comando endtext|Função TXTWIDTH ()|  
|Função TRANSFORM ()|Variável de memória do sistema _TRANSPORT||  
|Comando de tipo|Variável de memória do sistema _THROTTLE||  
  
## <a name="u"></a>U  
  
||||  
|-|-|-|  
|Função UPDATED ()|USAR comando||  
  
## <a name="v"></a>V  
  
||||  
|-|-|-|  
|Comando validar banco de dados|Função VARREAD ()|Função VERSION ()|  
  
## <a name="w"></a>W  
  
||||  
|-|-|-|  
|Variável de memória do sistema _WINDOWS|Variável de memória do sistema _WIZARD|Função WCHILD ()|  
|Comando WAIT|Função WBORDER ()|Função WFONT ()|  
|Função WCOLS ()|Função WEXIST ()|Função WLROW ()|  
|COM... Comando endcom|Função WLAST ()|Função WONTOP ()|  
|Função WMAXIMUM ()|Função WLCOL ()|Função WREAD ()|  
|Função WOUTPUT ()|Função WMINIMUM ()|Função WVISIBLE ()|  
|Função WPARENT ()|Função WTITLE ()||  
|Função WROWS ()|Variável de memória do sistema _WRAP||  
  
## <a name="z"></a>Z  
  
||||  
|-|-|-|  
|Comando janela de ZOOM|||
