---
title: Comandos do Visual FoxPro e funções sem suporte | Microsoft Docs
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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67912318"
---
# <a name="unsupported-visual-foxpro-commands-and-functions-visual-foxpro-odbc-driver"></a>Comandos e funções do Visual FoxPro sem suporte (Driver ODBC do Visual FoxPro)
A tabela a seguir lista os comandos do FoxPro e funções que não têm suporte para o Driver de ODBC do Visual FoxPro, mas são suportadas pelo Microsoft® Visual FoxPro®.  
  
 Se seu aplicativo interage com os dados cujo regras, gatilhos, valores padrão ou procedimentos armazenados chamam essas funções ou os comandos do Visual FoxPro, o driver pode gerar um erro.  
  
## <a name="unsupported-visual-foxpro-commands-and-functions"></a>As funções e comandos sem suporte do Visual FoxPro  
  
||||  
|-|-|-|  
|#DEFINE... #UNDEF|... #IF #ENDIF diretiva de pré-processador|#IFDEF &#124; #IFNDEF|  
|# Pré-processador diretiva INCLUDE|:: Operador de resolução de escopo|! Comando (consulte execução &#124; ! Comando)|  
|? &#124; ?? Comando|??? Comando|\ &#124; \\\ Comando|  
|@ ... CAIXA de comando|@ ... CLASSE de comando|@ ... Comando de limpeza|  
|@ ... Editar - Editar caixas comando|@ ... Comando preencher|@ ... OBTER|  
|@ ... Comando de MENU|@ ... Comando PROMPT|@ ... Digamos que o comando|  
|@ ... Comando de ROLAGEM|@ ... PARA o comando||  
  
## <a name="a"></a>Um  
  
||||  
|-|-|-|  
|ACEITAR o comando|Função do ACLASS)|Ativar comando de MENU|  
|Ativar comando de pop-up|Ativar comando de tela|Ativar janela de comando|  
|Método ActivateCell|Adicionar classe de comando|Função do ADIR)|  
|Função do AFONT)|Função do AINSTANCE)|Variável de memória do sistema _ALIGNMENT|  
|Função do AMEMBERS)|Função do ANSITOOEM)|Função do APRINTERS)|  
|Função do ASELOBJ)|AUXILIAR de comando||  
  
## <a name="b"></a>B  
  
||||  
|-|-|-|  
|BARRA de função)|Função do BARCOUNT)|Função do BARPROMPT)|  
|Variável de memória do sistema _BEAUTIFY|Variável de memória do sistema de box|Procurar comando|  
|Variável de memória do sistema _BROWSER|CRIAR comando de aplicativo|CRIAR comando EXE|  
|CRIAR comando de projeto|Variável de memória do sistema _BUILDER||  
  
## <a name="c"></a>C  
  
||||  
|-|-|-|  
|Variável de memória do sistema _CALCVALUE|Variável de memória do sistema _CLIPTEXT|Variável de memória do sistema _CONVERTER|  
|Variável de memória do sistema _CUROBJ|CHAMAR o comando|Cancelar o comando|  
|Função do CAPSLOCK)|Comando de CD|Comando de alteração|  
|Comando CHDIR|Função do CHRSAW)|Comando Fechar Memorando|  
|Função do CNTBAR)|Função do CNTPAD)|Função () de COL|  
|Comando de compilação|COMPILAR o comando de banco de dados|COMPILAR o comando de forma|  
|Função do COMPOBJ)|Objeto de contêiner|Objeto de controle|  
|Copie o arquivo de comando|Copie o comando de memorando|CRIAR comando de classe|  
|CRIAR comando CLASSLIB|CRIAR comando de conjunto de cores|Comando CREATE|  
|CRIAR comando de conexão|CRIAR comando de banco de dados|CRIAR comando de formulário|  
|CRIAR a partir de comando|CRIAR comando de rótulo|CRIAR comando de MENU|  
|CRIAR comando de projeto|CRIAR comando de consulta|CRIAR comando de relatório|  
|CRIAR comando de tela|CRIAR comando de modo de exibição SQL|CRIAR comando de GATILHO|  
|CRIAR comando de modo de exibição|Função do CREATEOBJECT)|Função do CURDIR)|  
  
## <a name="d"></a>D  
  
||||  
|-|-|-|  
|Variável de memória do sistema _DBLCLICK|Variável de memória do sistema _DIARYDATE|Função do DBSETPROP)|  
|Funções DDE|DESATIVAR o comando de MENU|DESATIVAR o comando de pop-up|  
|DESATIVAR a janela de comando|DECLARE - DLL de comando|DECLARAR o comando|  
|DEFINIR a barra de comando|Definir caixa de comando|DEFINIR a classe de comando|  
|Definir comando de MENU|DEFINIR o painel de comando|DEFINIR o comando de pop-up|  
|DEFINIR a janela de comando|Excluir comando de conexão|Excluir comando de banco de dados|  
|EXCLUIR o arquivo de comando|Comando de GATILHO DELETE|Exibir comando DELETE|  
|Comando DIR|Comando de diretório|Comando de exibição|  
|Comando de conexões de exibição|Comando de banco de dados de exibição|Comando DLLS de exibição|  
|Comando de arquivos de exibição|Comando de memória de vídeo|Comando de objetos de exibição|  
|Comando de procedimentos de exibição|Comando STATUS de exibição|Comando de estrutura de exibição|  
|Comando de tabelas de exibição|Comando de modos de exibição|O comando de formulário|  
  
## <a name="e"></a>E  
  
||||  
|-|-|-|  
|Comando Editar|Erro de comando||  
|Comando de apagar|Comando externo|Comando de exportação|  
|Comando de ejeção|EJETAR o comando de página||  
  
## <a name="f"></a>F  
  
||||  
|-|-|-|  
|Variável de memória do sistema _FOXDOC|Variável de memória do sistema _FOXGRAPH|Função do FEOF)|  
|Função do FCLOSE)|Função do FCREATE)|Função do FGETS)|  
|Função do FERROR)|Função do FFLUSH)|Função do FKLABEL)|  
|Comando do servidor de dados|Comando Localizar|Função do FOPEN)|  
|Função do FKMAX)|Função do FONTMETRIC)|Função do FSEEK)|  
|Função do FPUTS)|Função do thread)||  
|Função do FWRITE)|Função do FCHSIZE)||  
  
## <a name="g"></a>G  
  
||||  
|-|-|-|  
|Variável de memória do sistema _GENGRAPH|Variável de memória do sistema _GENMENU|Variável de memória do sistema _GENPD|  
|Variável de memória do sistema _GENSCRN|Variável de memória do sistema _GENXTAB|Função do GETBAR)|  
|Função do GETCOLOR)|Função do GETDIR)|Comando GETEXPR|  
|Função do GETFILE)|Função do GETFONT)|Função do GETOBJECT)|  
|Função do GETPAD)|Função do GETPICT)|Função do GETPRINTER)|  
  
## <a name="h"></a>H  
  
||||  
|-|-|-|  
|Comando de ajuda|Ocultar o comando de MENU|Ocultar o comando de pop-up|  
|OCULTAR a janela de comando|Função (inicial)||  
  
## <a name="i"></a>I  
  
||||  
|-|-|-|  
|Função do IMESTATUS)|Comando de importação|Comando de entrada|  
|Comando de índice|Função (NASÁREAS)|Função do ISCOLOR)|  
|Comando Inserir|Função do INSMODE)||  
|Função do ISMOUSE)|Variável de memória do sistema de recuo||  
  
## <a name="j"></a>J  
  
||||  
|-|-|-|  
|Comando de junção|||  
  
## <a name="k"></a>K  
  
||||  
|-|-|-|  
|Comando de TECLADO|||  
  
## <a name="l"></a>L  
  
||||  
|-|-|-|  
|Variável de memória do sistema _LMARGIN|Comando de rótulo|Função do LASTKEY)|  
|Função do LINENO)|Comandos de lista|Comando de conexões da lista|  
|Comando de carregamento|Função do LOCFILE)||  
  
## <a name="m"></a>M  
  
||||  
|-|-|-|  
|Função do MCOL)|Comando MD|MENU de comando|  
|Função () de memória|Comando de MENU|Comando MKDIR|  
|Função do MENU)|Função do MESSAGEBOX)|Modifique o comando de conexão|  
|MODIFICAR a classe de comando|Modifique o comando de comando|Modifique o comando de formulário|  
|Modifique o comando de banco de dados|MODIFICAR o arquivo de comando|Modifique o comando de memorando|  
|Modifique o comando geral|Modifique o comando de rótulo|Modifique o comando de projeto|  
|Modifique o comando de MENU|Modifique o comando de procedimento|Modifique o comando de tela|  
|Modifique o comando de consulta|Modifique o comando de relatório|MODIFICAR a janela de comando|  
|MODIFICAR a estrutura de comando|Modifique o comando de modo de exibição|Mover a janela comando|  
|Comando de MOUSE|Mover o comando de pop-up|Função do MROW)|  
|Função do MRKBAR)|Função do MRKPAD)||  
|Função do MWINDOW)|Função do MDOWN)||  
  
## <a name="n"></a>N  
  
||||  
|-|-|-|  
|Função num lock)|||  
  
## <a name="o"></a>O  
  
||||  
|-|-|-|  
|Função do OBJNUM)|Função do OBJTOCLIENT)|Diante de barra de comando|  
|Função do OEMTOANSI)|NO comando APLABOUT|Comando MENU ON EXIT|  
|NO comando ESCAPE|NA barra de comandos de saída|NA chave = comando|  
|Comando de bloco ON EXIT|Comando de pop-up ON EXIT|Comando de bloco ON|  
|NO comando de rótulo de tecla|NO comando MACHELP|EM seleção na barra de comandos|  
|Na página de comando|NO comando READERROR|NO comando de pop-up de seleção|  
|NO comando MENU de seleção|NO comando de painel de seleção||  
|NO comando de desligamento|Função do OBJVAR)||  
  
## <a name="p"></a>P  
  
||||  
|-|-|-|  
|Variável de memória do sistema _PADVANCE|Variável de memória do sistema _PAGENO|Variável de memória do sistema _PBPAGE|  
|Variável de memória do sistema _PCOLNO|Variável de memória do sistema _PCOPIES|Variável de memória do sistema _PDRIVER|  
|Variável de memória do sistema _PDSETUP|Variável de memória do sistema _PECODE|Variável de memória do sistema _PEJECT|  
|Variável de memória do sistema _PEPAGE|Variável de memória do sistema _PLENGTH|Variável de memória do sistema _PLINENO|  
|Variável de memória do sistema _PLOFFSET|Variável de memória do sistema _PPITCH|Variável de memória do sistema _PQUALITY|  
|Variável de memória do sistema _PRETEXT|Variável de memória do sistema _PSCODE|Variável de memória do sistema _PSPACING|  
|Variável de memória do sistema _PWAIT|Comando de banco de dados do pacote|Função do painel)|  
|Função do PCOL)|Função do PEMSTATUS)|EXECUTAR o comando MACRO|  
|Comando de mensagem pop-chave|Comando de MENU pop-up|Comando de pop-up de pop-up|  
|Função do pop-up)|PRINTJOB... Comando ENDPRINTJOB|Função do PRINTSTATUS)|  
|Função do PRMBAR)|Função do PRMPAD)|Função (aviso)|  
|Função do PROW)|Função do PRTINFO)|Enviar por PUSH o comando de teclas|  
|Enviar por PUSH o comando de MENU|Enviar por PUSH o comando de pop-up|Função do PUTFILE)|  
  
## <a name="q"></a>Q  
  
||||  
|-|-|-|  
|Comando Sair|||  
  
## <a name="r"></a>R  
  
||||  
|-|-|-|  
|Variável de memória do sistema _RMARGIN|Comando de área de trabalho remota|Função do READKEY)|  
|Comando de leitura|Leia o comando de MENU|VERSÃO na barra de comandos|  
|Função Refresh()|Comando de REINDEXAR|Comando de biblioteca de versão|  
|VERSÃO CLASSLIB comando|Comando de versão|Comando de bloco de versão|  
|Comando de MENUS de versão|Comando do módulo de versão|Comando do WINDOWS de versão|  
|Comando de pop-ups de versão|Comando do procedimento de versão|Comando RENOMEAR|  
|Remover comando de classe|RENOMEIE a classe de comando|RENOMEAR um comando de modo de exibição|  
|RENOMEAR um comando de conexão|RENOMEAR tabela comando|RESTAURAR a partir de comando|  
|Comando de relatório|Repetir a consulta de função)|RESTAURAR janela comando|  
|MACROS de comando RESTORE|RESTAURAR comando de tela|Função do RGBSCHEME)|  
|Comando RESUME|Função do RGB)|EXECUTE &#124; ! Comando|  
|Comando RMDIR|Função () de linha||  
|Comando RUNSCRIPT|Função do RDLEVEL)||  
  
## <a name="s"></a>P  
  
||||  
|-|-|-|  
|MACROS de comando Salvar|SALVE os comandos de tela|Salvar no comando|  
|Salvar o comando do WINDOWS|Função do esquema)|Função do SCOLS)|  
|Comando de ROLAGEM|Variável de memória do sistema _SCREEN|Comando SET|  
|Comando alternativo SET|Comando SET ANSI|Comando APLABOUT SET|  
|Comando de salvamento automático de conjunto|Comando de SINO SET|Comando de INTERMITÊNCIA de conjunto|  
|Comando de borda de conjunto|Comando BRSTATUS SET|Comando CLASSLIB SET|  
|Comando Limpar SET|Comando CLOCK de conjunto|COR do conjunto de comando|  
|DEFINIR a cor do comando de esquema|Comando de conjunto do conjunto de cor|COR definida para o comando|  
|Comando de conjunto compatível|Comando de confirmação do conjunto|CONJUNTO de comando do CONSOLE|  
|CONJUNTO CPCOMPILE|CONJUNTO CPDIALOG|Comando do conjunto de moeda|  
|Comando CURSOR de conjunto|Comando DATASESSION SET|Comando de depuração de conjunto|  
|Comando do conjunto de casas decimais|Comando do conjunto de DELIMITADORES|Comando de desenvolvimento do conjunto|  
|CONJUNTO de comando de dispositivo|Comando de exibição de conjunto|Comando DOHISTORY SET|  
|Comando de eco de conjunto|Comando ESCAPE de conjunto|Comando de formato de conjunto|  
|Comando de função de conjunto|Comando do conjunto de títulos|Comando de ajuda de SET|  
|Comando HELPFILTER SET|Comando de intensidade de conjunto|Comando SET KEY|  
|Comando KEYCOMP SET|Comando LOGERRORS SET|Comando MACDESKTOP SET|  
|Comando MACHELP SET|Comando MACKEY SET|Comando de MARGEM de conjunto|  
|MARCA de conjunto de comando|Defina a marca de comando|Comando MEMOWIDTH SET|  
|Comando do conjunto de mensagem|Comando de MOUSE SET|Comando do HODÔMETRO SET|  
|Comando OLEOBJECT SET|Comando do conjunto de PALETA|Comando PDSETUP SET|  
|Comando definir ponto|Comando de impressora SET|Comando READBORDER SET|  
|Comando de atualização de conjunto|Comando do conjunto de recursos|Comando do conjunto de segurança|  
|Comando do conjunto de PLACAR|Comando de segundos de conjunto|Comando de SEPARADOR de conjunto|  
|Comando de SOMBRAS de conjunto|Ignorar do conjunto de comando|Comando de espaço de conjunto|  
|Comando STATUS do conjunto|Na barra de STATUS do conjunto de comandos|Comando de etapa de conjunto|  
|Comando ADESIVO SET|Comando SYSFORMATS SET|Comando SYSMENU SET|  
|Comando de PALESTRA SET|Comando TEXTMERGE SET|Comando de DELIMITADORES TEXTMERGE SET|  
|Comando do conjunto de tópico|Comando de ID do conjunto de tópico|Comando TRBETWEEN SET|  
|Comando de digitação antecipada de conjunto|Comando de modo de exibição de conjunto|CONJUNTO de janela de comando de memorando|  
|Comando XCMDFILE SET|Variável de memória do sistema _SHELL|Mostrar comando GET|  
|Mostrar comando OBTÉM|Mostrar comando de MENU|Mostrar o objeto de comando|  
|Mostrar comando pop-up|Mostrar janela de comando|Comando de pop-up de tamanho|  
|Comando de janela de tamanho|Função do SKPBAR)|Função do SKPPAD)|  
|Função SOUNDEX)|Variável de memória do sistema _SPELLCHK|Funções SQL|  
|Função do SROWS)|Variável de memória do sistema Startup|Comando de suspensão|  
|Funções sys() exceto SYS(2011)|Função do SYSMETRIC)||  
  
## <a name="t"></a>T  
  
||||  
|-|-|-|  
|Variável de memória do sistema _TABS|TEXTO... Comando ENDTEXT|Função do TXTWIDTH)|  
|TRANSFORMAR a função)|Variável de memória do sistema _TRANSPORT||  
|Digite o comando|Variável de memória do sistema _THROTTLE||  
  
## <a name="u"></a>U  
  
||||  
|-|-|-|  
|Função (atualizado)|USE o comando||  
  
## <a name="v"></a>V  
  
||||  
|-|-|-|  
|Validar o comando de banco de dados|Função do VARREAD)|Função () de versão|  
  
## <a name="w"></a>W  
  
||||  
|-|-|-|  
|Variável de memória do sistema de Windows|Variável de memória do sistema _WIZARD|Função do WCHILD)|  
|Aguarde o comando|Função do WBORDER)|Função do WFONT)|  
|Função do WCOLS)|Função do WEXIST)|Função do WLROW)|  
|COM... Comando ENDWITH|Função do WLAST)|Função do WONTOP)|  
|Função do WMAXIMUM)|Função do WLCOL)|Função do WREAD)|  
|Função do WOUTPUT)|Função do WMINIMUM)|Função do WVISIBLE)|  
|Função do WPARENT)|Função do WTITLE)||  
|Função do WROWS)|Variável de memória do sistema _WRAP||  
  
## <a name="z"></a>Z  
  
||||  
|-|-|-|  
|Comando de janela de ZOOM|||
