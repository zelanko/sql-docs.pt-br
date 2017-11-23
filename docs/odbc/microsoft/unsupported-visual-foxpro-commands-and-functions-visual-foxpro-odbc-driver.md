---
title: "Sem suporte do Visual FoxPro comandos e funções | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- FoxPro ODBC driver [ODBC], commands and functions
- functions [ODBC], Visual FoxPro
- Visual FoxPro ODBC driver [ODBC], commands and functions
- Visual FoxPro commands and functions
- FoxPro ODBC driver
ms.assetid: afdb6b7e-738d-42ca-8053-67ae50873ca6
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: df2f3bfdb37ab506de3fe99d8c7d1e5e9764ef43
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2017
---
# <a name="unsupported-visual-foxpro-commands-and-functions-visual-foxpro-odbc-driver"></a>Sem suporte do Visual FoxPro comandos e funções (Driver ODBC do Visual FoxPro)
A tabela a seguir lista os comandos de FoxPro e funções que não são suportadas pelo Driver ODBC para Visual FoxPro, mas são suportadas pelo Microsoft® Visual FoxPro.  
  
 Se seu aplicativo interage com os dados cuja regras, valores padrão, gatilhos ou procedimentos armazenados chamam essas funções ou os comandos do Visual FoxPro, o driver pode gerar um erro.  
  
## <a name="unsupported-visual-foxpro-commands-and-functions"></a>As funções e comandos sem suporte do Visual FoxPro  
  
||||  
|-|-|-|  
|#DEFINE … #UNDEF|... #IF #ENDIF diretiva de pré-processador|#IFDEF &#124; #IFNDEF|  
|# Pré-processador diretiva INCLUDE|:: Operador de resolução do escopo|! Comando (consulte execução &#124;! Comando)|  
|? &#124; ?? Comando|??? Comando|\ &#124; \\\ Comando|  
|@ ... Comando de caixa|@ ... Comando de classe|@ ... Comando Limpar|  
|@ ... Editar - Editar caixas de comando|@ ... Comando preencher|@ ... GET|  
|@ ... Comando de MENU|@ ... Comando PROMPT|@ ... Digamos que o comando|  
|@ ... Comando de ROLAGEM|@ ... PARA o comando||  
  
## <a name="a"></a>Um  
  
||||  
|-|-|-|  
|ACEITAR o comando|Função do ACLASS)|Ativar comando de MENU|  
|Ativar comando de pop-up|Ativar comando de tela|Ativar a janela de comando|  
|Método ActivateCell|Adicionar classe de comando|Função do ADIR)|  
|Função do AFONT)|Função do AINSTANCE)|Variável de memória de sistema _ALIGNMENT|  
|Função do AMEMBERS)|Função do ANSITOOEM)|Função do APRINTERS)|  
|Função do ASELOBJ)|AUXILIAR de comando||  
  
## <a name="b"></a>B  
  
||||  
|-|-|-|  
|BARRA de função)|Função do BARCOUNT)|Função do BARPROMPT)|  
|Variável de memória de sistema _BEAUTIFY|Variável de memória do sistema de box|Procurar comando|  
|Variável de memória de sistema _BROWSER|Criar aplicativo de comando|CRIAR o comando EXE|  
|CRIAR um comando de projeto|Variável de memória de sistema _BUILDER||  
  
## <a name="c"></a>C  
  
||||  
|-|-|-|  
|Variável de memória de sistema _CALCVALUE|Variável de memória de sistema _CLIPTEXT|Variável de memória de sistema _CONVERTER|  
|Variável de memória de sistema _CUROBJ|Comando de chamada|Comando CANCEL|  
|Função () CAPSLOCK|Comando do CD|Comando de alteração|  
|Comando CHDIR|Função do CHRSAW)|Comando de memorando fechar|  
|Função do CNTBAR)|Função do CNTPAD)|Função () de coluna|  
|Comando de compilação|COMPILAR o comando de banco de dados|COMPILAR o comando de formulário|  
|Função do COMPOBJ)|Objeto de contêiner|Objeto de controle|  
|Copie o arquivo de comando|Copie o comando de memorando|CRIAR um comando de classe|  
|CRIAR o comando CLASSLIB|CRIAR um comando de conjunto de cores|CRIAR um comando|  
|CRIAR um comando de conexão|CRIAR um comando de banco de dados|CRIAR um comando de formulário|  
|CRIAR a partir de comando|CRIAR um comando de rótulo|CRIAR um comando de MENU|  
|CRIAR um comando de projeto|CRIAR um comando de consulta|CRIAR um comando de relatório|  
|CRIAR um comando de tela|CRIAR um comando de modo de exibição SQL|CRIAR um comando de GATILHO|  
|CRIAR um comando de modo de exibição|Função do CREATEOBJECT)|Função do CURDIR)|  
  
## <a name="d"></a>D  
  
||||  
|-|-|-|  
|Variável de memória de sistema _DBLCLICK|Variável de memória de sistema _DIARYDATE|Função do DBSETPROP)|  
|Funções DDE|DESATIVAR o comando de MENU|DESATIVAR o comando de pop-up|  
|DESATIVAR a janela de comando|DECLARE - DLL de comando|DECLARE o comando|  
|DEFINIR a barra de comando|DEFINIR o comando de caixa|DEFINIR a classe de comando|  
|DEFINIR o comando de MENU|DEFINIR o comando bloco|DEFINIR o comando de pop-up|  
|Definir janela de comando|Excluir um comando de conexão|Excluir um comando de banco de dados|  
|EXCLUIR o arquivo de comando|Comando de GATILHO DELETE|Excluir um comando de modo de exibição|  
|Comando DIR|Comando de diretório|Comando de exibição|  
|Comando de conexões de exibição|Comando de banco de dados de exibição|Exibir comando DLLS|  
|Comando de arquivos de vídeo|Comando de memória de vídeo|Comando de objetos de exibição|  
|Comando de procedimentos de exibição|Comando STATUS de exibição|Comando de estrutura de exibição|  
|Comando de tabelas de exibição|Comando de modos de exibição|FORMULÁRIO de comando|  
  
## <a name="e"></a>E  
  
||||  
|-|-|-|  
|Editar o comando|Erro de comando||  
|Comando de APAGAMENTO|Comando externo|Comando de exportação|  
|Comando EJETAR|EJETAR o comando de página||  
  
## <a name="f"></a>F  
  
||||  
|-|-|-|  
|Variável de memória de sistema _FOXDOC|Variável de memória de sistema _FOXGRAPH|Função do FEOF)|  
|Função do FCLOSE)|Função do FCREATE)|Função do FGETS)|  
|Função do FERROR)|Função do FFLUSH)|Função do FKLABEL)|  
|Comando do servidor de dados|Comando Localizar|Função do FOPEN)|  
|Função do FKMAX)|Função do FONTMETRIC)|Função do FSEEK)|  
|Função do FPUTS)|Função do FREAD)||  
|Função do FWRITE)|Função do FCHSIZE)||  
  
## <a name="g"></a>G  
  
||||  
|-|-|-|  
|Variável de memória de sistema _GENGRAPH|Variável de memória de sistema _GENMENU|Variável de memória de sistema _GENPD|  
|Variável de memória de sistema _GENSCRN|Variável de memória de sistema _GENXTAB|Função do GETBAR)|  
|Função do GETCOLOR)|Função do GETDIR)|Comando GETEXPR|  
|Função do GETFILE)|Função do GETFONT)|Função do GETOBJECT)|  
|Função do GETPAD)|Função do GETPICT)|Função do GETPRINTER)|  
  
## <a name="h"></a>H  
  
||||  
|-|-|-|  
|Comando de ajuda|Ocultar o comando de MENU|Ocultar o comando de pop-up|  
|OCULTAR a janela de comando|Função (base)||  
  
## <a name="i"></a>I  
  
||||  
|-|-|-|  
|Função do IMESTATUS)|Comando de importação|ENTRADA de comando|  
|Comando de índice|Função (INKEY)|Função do ISCOLOR)|  
|Comando INSERT|Função do INSMODE)||  
|Função do ISMOUSE)|Variável de memória de sistema _INDENT||  
  
## <a name="j"></a>J  
  
||||  
|-|-|-|  
|Comando junção|||  
  
## <a name="k"></a>K  
  
||||  
|-|-|-|  
|Comando de TECLADO|||  
  
## <a name="l"></a>L  
  
||||  
|-|-|-|  
|Variável de memória de sistema _LMARGIN|Comando de rótulo|Função do LASTKEY)|  
|Função do LINENO)|Comandos da lista|Comando de conexões de lista|  
|Comando de carregamento|Função do LOCFILE)||  
  
## <a name="m"></a>M  
  
||||  
|-|-|-|  
|Função do MCOL)|Comando MD|MENU de comando|  
|Função () de memória|Comando de MENU|Comando MKDIR|  
|Função do MENU)|Função do MESSAGEBOX)|MODIFICAR o comando de conexão|  
|MODIFICAR o comando de classe|MODIFICAR o comando|MODIFICAR o comando de formulário|  
|MODIFICAR o comando de banco de dados|MODIFICAR o arquivo de comando|MODIFICAR o comando de memorando|  
|MODIFICAR o comando geral|MODIFICAR o comando LABEL|MODIFICAR o comando de projeto|  
|MODIFICAR o comando de MENU|MODIFICAR o comando de procedimento|MODIFICAR o comando de tela|  
|MODIFICAR o comando de consulta|MODIFICAR o comando de relatório|MODIFICAR a janela de comando|  
|MODIFICAR a estrutura de comando|MODIFICAR o comando de modo de exibição|Mover a janela de comando|  
|Comando de MOUSE|Mover o comando de pop-up|Função do MROW)|  
|Função do MRKBAR)|Função do MRKPAD)||  
|Função do MWINDOW)|Função do MDOWN)||  
  
## <a name="n"></a>N  
  
||||  
|-|-|-|  
|Função do NUMLOCK)|||  
  
## <a name="o"></a>O   
  
||||  
|-|-|-|  
|Função do OBJNUM)|Função do OBJTOCLIENT)|ON barra de comando|  
|Função do OEMTOANSI)|NO comando APLABOUT|Comando MENU ON EXIT|  
|NO comando ESCAPE|NA barra de comandos de saída|CHAVE = comando|  
|Comando de bloco de saída ON|Comando de pop-up ON EXIT|Comando de bloco ON|  
|NO comando de chave de rótulo|NO comando MACHELP|EM seleção na barra de comandos|  
|NO comando de página|NO comando READERROR|NO comando de pop-up de seleção|  
|NO comando MENU de seleção|NO comando de bloco de seleção||  
|NO comando de desligamento|Função do OBJVAR)||  
  
## <a name="p"></a>P  
  
||||  
|-|-|-|  
|Variável de memória de sistema _PADVANCE|Variável de memória de sistema _PAGENO|Variável de memória de sistema _PBPAGE|  
|Variável de memória de sistema _PCOLNO|Variável de memória de sistema _PCOPIES|Variável de memória de sistema _PDRIVER|  
|Variável de memória de sistema _PDSETUP|Variável de memória de sistema _PECODE|Variável de memória de sistema _PEJECT|  
|Variável de memória de sistema _PEPAGE|Variável de memória de sistema _PLENGTH|Variável de memória de sistema _PLINENO|  
|Variável de memória de sistema _PLOFFSET|Variável de memória de sistema _PPITCH|Variável de memória de sistema _PQUALITY|  
|Variável de memória de sistema _PRETEXT|Variável de memória de sistema _PSCODE|Variável de memória de sistema _PSPACING|  
|Variável de memória de sistema _PWAIT|Comando de banco de dados do pacote|Função do TECLADO)|  
|Função do PCOL)|Função do PEMSTATUS)|EXECUTAR o comando MACRO|  
|Comando POP chave|Comando de MENU POP|Comando POP pop-up|  
|Função do pop-up)|PRINTJOB... Comando ENDPRINTJOB|Função do PRINTSTATUS)|  
|Função do PRMBAR)|Função do PRMPAD)|Função (aviso)|  
|Função do PROW)|Função do PRTINFO)|Enviar comando de teclas|  
|Enviar por PUSH o comando de MENU|Enviar comando de pop-up|Função do PUTFILE)|  
  
## <a name="q"></a>Q  
  
||||  
|-|-|-|  
|Comando Sair|||  
  
## <a name="r"></a>R  
  
||||  
|-|-|-|  
|Variável de memória de sistema _RMARGIN|Comando de área de trabalho remota|Função do READKEY)|  
|Comando de leitura|LER o comando de MENU|VERSÃO na barra de comandos|  
|Função Refresh()|REINDEXAR o comando|Comando de biblioteca de versão|  
|VERSÃO CLASSLIB comando|Comando de versão|Comando de bloco de versão|  
|Comando de MENUS de versão|Comando do módulo de versão|Comando do WINDOWS versão|  
|Comando de pop-ups de versão|Comando do procedimento de versão|Comando RENOMEAR|  
|Remova o comando de classe|RENOMEAR um comando de classe|RENOMEAR um comando de modo de exibição|  
|RENOMEAR um comando de conexão|RENOMEAR tabela comando|RESTAURAR a partir de comando|  
|Comando de relatório|Repetir a função)|RESTAURAR a janela de comando|  
|MACROS de comando RESTORE|TELA comando RESTORE|Função do RGBSCHEME)|  
|Comando RESUME|Função do RGB)|EXECUTAR &#124;! Comando|  
|Comando RMDIR|Função () de linha||  
|Comando RUNSCRIPT|Função do RDLEVEL)||  
  
## <a name="s"></a>P  
  
||||  
|-|-|-|  
|MACROS de comando Salvar|Salvar o comando de tela|Salvar no comando|  
|Salvar o comando do WINDOWS|Função do esquema)|Função do SCOLS)|  
|Comando de ROLAGEM|Variável de memória de sistema _SCREEN|Comando SET|  
|Comando alternativo do conjunto|Comando de ANSI SET|CONJUNTO APLABOUT comando|  
|Comando do conjunto de salvamento automático|Comando de SINO SET|Comando de INTERMITÊNCIA de conjunto|  
|Comando de borda de conjunto|Comando BRSTATUS SET|CONJUNTO CLASSLIB comando|  
|Comando Limpar conjunto|Comando do conjunto de RELÓGIO|COR do conjunto de comando|  
|DEFINIR a cor do comando de esquema|Comando de conjunto do conjunto de cores|COR definida para o comando|  
|Comando compatível do conjunto|Comando de confirmação de conjunto|Comando do CONSOLE do conjunto|  
|CONJUNTO CPCOMPILE|CONJUNTO CPDIALOG|Comando do conjunto de moeda|  
|Comando CURSOR de conjunto|CONJUNTO DATASESSION comando|CONJUNTO de comando de depuração|  
|Comando do conjunto de casas decimais|Comando de DELIMITADORES de conjunto|Comando de desenvolvimento do conjunto|  
|CONJUNTO de comando de dispositivo|Comando de exibição de conjunto|CONJUNTO DOHISTORY comando|  
|Comando de eco do conjunto|Comando ESCAPE do conjunto|Comando de formato de conjunto|  
|Comando de função de conjunto|Comando do conjunto de títulos|Comando do conjunto de ajuda|  
|CONJUNTO HELPFILTER comando|Comando de intensidade do conjunto|Comando SET KEY|  
|CONJUNTO KEYCOMP comando|CONJUNTO LOGERRORS comando|CONJUNTO MACDESKTOP comando|  
|CONJUNTO MACHELP comando|CONJUNTO MACKEY comando|Comando de MARGEM do conjunto|  
|MARCA de conjunto de comando|DEFINIR a marca de comando|CONJUNTO MEMOWIDTH comando|  
|Comando do conjunto de mensagem|Comando do conjunto de MOUSE|Comando de ODÔMETRO SET|  
|Comando OLEOBJECT SET|Comando do conjunto de PALETA|CONJUNTO PDSETUP comando|  
|Comando definir ponto|CONJUNTO de comando de impressora|CONJUNTO READBORDER comando|  
|Comando de atualização de conjunto|Comando do conjunto de recursos|Comando do conjunto de segurança|  
|Comando SCOREBOARD SET|Comando de segundos de conjunto|Comando de SEPARADOR de conjunto|  
|Comando de SOMBRAS de conjunto|Ignorar do conjunto de comando|Comando de espaço do conjunto|  
|Comando STATUS do conjunto|Na barra de STATUS do conjunto de comandos|Comando de etapa de conjunto|  
|Comando AUTOADESIVAS SET|CONJUNTO SYSFORMATS comando|CONJUNTO SYSMENU comando|  
|Comando do conjunto de CONVERSA|CONJUNTO TEXTMERGE comando|Comando de DELIMITADORES de TEXTMERGE SET|  
|Comando do conjunto de tópico|Comando de ID do conjunto de tópico|CONJUNTO TRBETWEEN comando|  
|CONJUNTO TYPEAHEAD comando|Comando de modo de exibição de conjunto|Definir janela de comando de memorando|  
|CONJUNTO XCMDFILE comando|Variável de memória de sistema _SHELL|Mostrar comando GET|  
|Mostrar comando OBTÉM|Mostrar comando de MENU|Mostrar o objeto de comando|  
|Mostrar comando pop-up|Mostrar janela de comando|Comando de pop-up de tamanho|  
|Comando do tamanho da janela|Função do SKPBAR)|Função do SKPPAD)|  
|Função SOUNDEX)|Variável de memória de sistema _SPELLCHK|Funções SQL|  
|Função do SROWS)|Variável de memória do sistema Startup|Comando de suspensão|  
|Funções sys() exceto SYS(2011)|Função do SYSMETRIC)||  
  
## <a name="t"></a>T  
  
||||  
|-|-|-|  
|Variável de memória de sistema _TABS|TEXTO... Comando ENDTEXT|Função do TXTWIDTH)|  
|TRANSFORMAR a função)|Variável de memória de sistema _TRANSPORT||  
|Digite o comando|Variável de memória de sistema _THROTTLE||  
  
## <a name="u"></a>U  
  
||||  
|-|-|-|  
|Função (atualizada)|USE o comando||  
  
## <a name="v"></a>V  
  
||||  
|-|-|-|  
|Validar o comando de banco de dados|Função do VARREAD)|Função () de versão|  
  
## <a name="w"></a>L  
  
||||  
|-|-|-|  
|Variável de memória de sistema do Windows|Variável de memória de sistema _WIZARD|Função do WCHILD)|  
|Aguarde o comando|Função do WBORDER)|Função do WFONT)|  
|Função do WCOLS)|Função do WEXIST)|Função do WLROW)|  
|COM... Comando ENDWITH|Função do WLAST)|Função do WONTOP)|  
|Função do WMAXIMUM)|Função do WLCOL)|Função do WREAD)|  
|Função do WOUTPUT)|Função do WMINIMUM)|Função do WVISIBLE)|  
|Função do WPARENT)|Função do WTITLE)||  
|Função do WROWS)|Variável de memória de sistema _WRAP||  
  
## <a name="z"></a>Z  
  
||||  
|-|-|-|  
|Comando de janela de ZOOM|||
