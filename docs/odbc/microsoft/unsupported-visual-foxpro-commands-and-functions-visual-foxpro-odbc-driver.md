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
ms.openlocfilehash: 3f1882172bb3f300c50820db642443ec0d1583f4
ms.sourcegitcommit: 99f61724de5edf6640efd99916d464172eb23f92
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/28/2020
ms.locfileid: "87363471"
---
# <a name="unsupported-visual-foxpro-commands-and-functions-visual-foxpro-odbc-driver"></a>Comandos e funções do Visual FoxPro sem suporte (Driver ODBC do Visual FoxPro)
A tabela a seguir lista os comandos e funções do FoxPro que não têm suporte do driver ODBC do Visual FoxPro, mas têm suporte do Microsoft® Visual FoxPro®.  
  
 Se seu aplicativo interage com dados cujas regras, gatilhos, valores padrão ou procedimentos armazenados chamam esses comandos ou funções do Visual FoxPro, o driver pode gerar um erro.  
  
## <a name="unsupported-visual-foxpro-commands-and-functions"></a>Comandos e funções do Visual FoxPro sem suporte  

:::row:::
    :::column:::
        !(Consulte executar &#124;!Linha  
        #<a name="defineundef"></a>DEFINIR... #UNDEF  
        #<a name="ifendifpreprocessordirective"></a>Diretiva IF... #ENDIF pré-processador  
        #<a name="ifdef124ifndef"></a>IFDEF &#124; #IFNDEF  
        #<a name="includepreprocessordirective"></a>INCLUIR diretiva de pré-processador  
        :: Operador de resolução de escopo  
        ?&#124;??Comando  
    :::column-end:::
    :::column:::
        ???Comando  
        @ ... Comando BOX  
        @ ... Comando de classe  
        @ ... Limpar comando  
        @ ... Comando editar caixas de edição  
        @ ... Comando FILL  
        @ ... Obter  
    :::column-end:::
    :::column:::
        @ ... Comando de MENU  
        @ ... Comando de PROMPT  
        @ ... Comando digamos  
        @ ... Comando SCROLL  
        @ ... PARA o comando  
        Comando \ &#124; \\ \  
    :::column-end:::
:::row-end:::

## <a name="a"></a>Um  

:::row:::
    :::column:::
        ACEITAR comando  
        Função ACLASS ()  
        ATIVAR comando de MENU  
        ATIVAR o comando POPUP  
        Comando ativar tela  
        Comando ativar janela  
    :::column-end:::
    :::column:::
        Método ActivateCell  
        Adicionar comando de classe  
        Função ADIR ()  
        Função AFONT ()  
        Função AINSTANCE ()  
        Variável de memória do sistema _ALIGNMENT  
    :::column-end:::
    :::column:::
        Função AMEMBERS ()  
        Função ANSITOOEM ()  
        Função APRINTERS ()  
        Função ASELOBJ ()  
        Comando auxiliar  
    :::column-end:::
:::row-end:::

## <a name="b"></a>B  

:::row:::
    :::column:::
        Função BAR ()  
        Função BARCOUNT ()  
        Função BARPROMPT ()  
        Variável de memória do sistema _BEAUTIFY  
    :::column-end:::
    :::column:::
        Variável de memória do sistema _BOX  
        Comando procurar  
        Variável de memória do sistema _BROWSER  
        Comando COMPILAR aplicativo  
    :::column-end:::
    :::column:::
        Comando de BUILD EXE  
        Comando COMPILAR projeto  
        Variável de memória do sistema _BUILDER  
    :::column-end:::
:::row-end:::

## <a name="c"></a>C  

:::row:::
    :::column:::
        Variável de memória do sistema _CALCVALUE  
        CHAMAR comando  
        Comando CANCEL  
        Função CAPSLOCK ()  
        Comando CD  
        ALTERAR comando  
        Comando CHDIR  
        Função CHRSAW ()  
        Variável de memória do sistema _CLIPTEXT  
        FECHAR comando de memorando  
        Função CNTBAR ()  
        Função CNTPAD ()  
        Função COL ()  
        Comando de compilação  
    :::column-end:::
    :::column:::
        Comando COMPILAR banco de dados  
        Comando COMPILAR formulário  
        Função COMPOBJ ()  
        Objeto de contêiner  
        Objeto de controle  
        Variável de memória do sistema _CONVERTER  
        Comando Copiar arquivo  
        Comando copiar memorando  
        Comando CREATE  
        Comando criar classe  
        CRIAR comando CLASSLIB  
        Comando criar conjunto de cores  
        Comando criar conexão  
        Comando criar banco de dados  
    :::column-end:::
    :::column:::
        Comando Criar formulário  
        CRIAR do comando  
        Comando criar rótulo  
        Comando criar MENU  
        Comando Criar projeto  
        Comando Criar consulta  
        Comando criar relatório  
        Comando criar tela  
        Comando CREATE SQL VIEW  
        CRIAR comando de gatilho  
        Comando CREATE VIEW  
        Função CREATEOBJECT ()  
        Função CURDIR ()  
        Variável de memória do sistema _CUROBJ  
    :::column-end:::
:::row-end:::

## <a name="d"></a>D  

:::row:::
    :::column:::
        Variável de memória do sistema _DBLCLICK  
        Função DBSETPROP ()  
        Funções DDE  
        Comando desativar MENU  
        DESATIVAR comando POPUP  
        Comando desativar janela  
        Comando DECLARE  
        Comando DECLARE-DLL  
        Definir comando de barra  
        Comando definir caixa  
        Definir comando de classe  
        Definir comando de MENU  
    :::column-end:::
    :::column:::
        Definir comando de preenchimento  
        Definir comando POPUP  
        Definir comando de janela  
        Comando excluir conexão  
        Comando excluir banco de dados  
        Comando excluir arquivo  
        Excluir comando de gatilho  
        Excluir comando de exibição  
        Variável de memória do sistema _DIARYDATE  
        Comando DIR  
        Comando de diretório  
        Comando de exibição  
    :::column-end:::
    :::column:::
        Comando exibir conexões  
        Comando exibir banco de dados  
        Comando exibir DLLS  
        Comando exibir arquivos  
        Comando DISPLAY MEMORY  
        Comando exibir objetos  
        Comando exibir procedimentos  
        EXIBIR o comando de STATUS  
        Comando exibir estrutura  
        Comando exibir tabelas  
        Comando exibir EXIBIções  
        Comando DO formulário  
    :::column-end:::
:::row-end:::

## <a name="e"></a>E  

:::row:::
    :::column:::
        Comando de edição  
        Comando EJECT  
        Comando EJETAr página  
    :::column-end:::
    :::column:::
        Comando ERASE  
        Comando de erro  
        Comando de exportação  
    :::column-end:::
    :::column:::
        Comando externo  
    :::column-end:::
:::row-end:::

## <a name="f"></a>F  

:::row:::
    :::column:::
        Função FCHSIZE ()  
        Função FCLOSE ()  
        Função FCREATE ()  
        Função FEOF ()  
        Função REFERENCIAdora ()  
        Função FFLUSH ()  
        Função FGETS ()  
    :::column-end:::
    :::column:::
        Comando FILEr  
        Comando FIND  
        Função FKLABEL ()  
        Função FKMAX ()  
        Função FONTMETRIC ()  
        Função FOPEN ()  
        Variável de memória do sistema _FOXDOC  
    :::column-end:::
    :::column:::
        Variável de memória do sistema _FOXGRAPH  
        Função FPUTS ()  
        Função FREAD ()  
        Função FSEEK ()  
        Função FWRITE ()  
    :::column-end:::
:::row-end:::

## <a name="g"></a>G  

:::row:::
    :::column:::
        Variável de memória do sistema _GENGRAPH  
        Variável de memória do sistema _GENMENU  
        Variável de memória do sistema _GENPD  
        Variável de memória do sistema _GENSCRN  
        Variável de memória do sistema _GENXTAB  
    :::column-end:::
    :::column:::
        Função GETBAR ()  
        Função GetColor ()  
        Função GETDIR ()  
        Comando GETEXPR  
        Função GetFile ()  
    :::column-end:::
    :::column:::
        Função GetFont ()  
        Função GetObject ()  
        Função GETPAD ()  
        Função getpict ()  
        Função getprinter ()  
    :::column-end:::
:::row-end:::

## <a name="h"></a>H  

:::row:::
    :::column:::
        Comando de ajuda  
        Ocultar comando de MENU  
    :::column-end:::
    :::column:::
        Ocultar comando POPUP  
        Ocultar comando de janela  
    :::column-end:::
    :::column:::
        Função HOME ()  
    :::column-end:::
:::row-end:::

## <a name="i"></a>I  

:::row:::
    :::column:::
        Função IMESTATUS ()  
        Comando de importação  
        Variável de memória do sistema _INDENT  
        ÍNDICE no comando  
    :::column-end:::
    :::column:::
        Função INKEY ()  
        Comando de entrada  
        INSERIR comando  
        Função INSMODE ()  
    :::column-end:::
    :::column:::
        Função IsColor ()  
        Função ismouse ()  
    :::column-end:::
:::row-end:::

## <a name="j"></a>J  

Comando JOIN

## <a name="k"></a>K  

Comando de teclado

## <a name="l"></a>L  

:::row:::
    :::column:::
        Comando de rótulo  
        Função LASTKEY ()  
        Função LINENO ()  
    :::column-end:::
    :::column:::
        LISTAr comandos  
        Comando LISTAr conexões  
        Variável de memória do sistema _LMARGIN  
    :::column-end:::
    :::column:::
        CARREGAR comando  
        Função LOCFILE ()  
    :::column-end:::
:::row-end:::

## <a name="m"></a>M  

:::row:::
    :::column:::
        Função MCOL ()  
        Comando MD  
        Função MDOWN ()  
        Função MEMORY ()  
        Comando de MENU  
        Função MENU ()  
        MENU para comando  
        Função MESSAGEBOX ()  
        Comando MKDIR  
        Comando modificar classe  
        MODIFICAR comando de comando  
        Comando Modificar conexão  
    :::column-end:::
    :::column:::
        Comando modificar banco de dados  
        Comando MODIFY FILE  
        Comando modificar formulário  
        MODIFICAR o comando geral  
        Comando modificar rótulo  
        MODIFICAR comando de memorando  
        MODIFICAR comando de MENU  
        Comando modificar procedimento  
        Comando modificar projeto  
        MODIFICAR comando de consulta  
        MODIFICAR comando de relatório  
        Comando modificar tela  
    :::column-end:::
    :::column:::
        Comando modificar estrutura  
        MODIFICAR o comando de exibição  
        MODIFICAR comando de janela  
        Comando do MOUSE  
        MOVER comando pop-up  
        Comando mover janela  
        Função MRKBAR ()  
        Função MRKPAD ()  
        Função MROW ()  
        Função MWINDOW ()  
    :::column-end:::
:::row-end:::

## <a name="n"></a>N  

Função NUMLOCK ()

## <a name="o"></a>O  

:::row:::
    :::column:::
        Função OBJNUM ()  
        Função OBJTOCLIENT ()  
        Função OBJVAR ()  
        Função OEMTOANSI ()  
        NO comando APLABOUT  
        Comando de barra  
        NO comando de ESCAPE  
        No comando da barra de saída  
    :::column-end:::
    :::column:::
        NO comando de MENU sair  
        NO comando sair do painel  
        AO sair do comando POPUP  
        NO comando KEY =  
        NO comando rótulo da chave  
        NO comando MACHELP  
        Comando no PAD  
        Comando na página  
    :::column-end:::
    :::column:::
        NO comando READERROR  
        No comando da barra de seleção  
        No comando de MENU de seleção  
        NO comando painel de seleção  
        Comando pop-up na seleção  
        NO comando de desligamento  
    :::column-end:::
:::row-end:::

## <a name="p"></a>P  

:::row:::
    :::column:::
        Comando do banco de dados do pacote  
        Função PAD ()  
        Variável de memória do sistema _PADVANCE  
        Variável de memória do sistema _PAGENO  
        Variável de memória do sistema _PBPAGE  
        Função PCOL ()  
        Variável de memória do sistema _PCOLNO  
        Variável de memória do sistema _PCOPIES  
        Variável de memória do sistema _PDRIVER  
        Variável de memória do sistema _PDSETUP  
        Variável de memória do sistema _PECODE  
        Variável de memória do sistema _PEJECT  
        Função PEMSTATUS ()  
    :::column-end:::
    :::column:::
        Variável de memória do sistema _PEPAGE  
        Comando reproduzir MACRO  
        Variável de memória do sistema _PLENGTH  
        Variável de memória do sistema _PLINENO  
        Variável de memória do sistema _PLOFFSET  
        Comando de tecla POP  
        Comando do MENU POP  
        Comando POP POPUP  
        Função POPUP ()  
        Variável de memória do sistema _PPITCH  
        Variável de memória do sistema _PQUALITY  
        Variável de memória do sistema _PRETEXT  
        PRINTJOB... Comando ENDPRINTJOB  
    :::column-end:::
    :::column:::
        Função distatus ()  
        Função PRMBAR ()  
        Função PRMPAD ()  
        Função PROMPT ()  
        Função PROW ()  
        Função PRTINFO ()  
        Variável de memória do sistema _PSCODE  
        Variável de memória do sistema _PSPACING  
        Comando PUSH KEY  
        Comando de MENU de PUSH  
        Comando pop-up de PUSH  
        Função PUTFILE ()  
        Variável de memória do sistema _PWAIT  
    :::column-end:::
:::row-end:::

## <a name="q"></a>Q  

Comando QUIT

## <a name="r"></a>R  

:::row:::
    :::column:::
        Comando RD  
        Função RDLEVEL ()  
        Comando de leitura  
        Comando de MENU ler  
        Função READKEY ()  
        Função REFRESH ()  
        Comando REINDEX  
        Comando de liberação  
        Comando da barra de versão  
        Comando RELEASE CLASSLIB  
        Comando liberar biblioteca  
        Comando liberar MENUS  
        Comando do módulo versão  
    :::column-end:::
    :::column:::
        Comando do painel de liberação  
        Comando liberar pop-ups  
        Comando liberar procedimento  
        Comando liberar o WINDOWS  
        Comando remover classe  
        Renomear comando  
        Comando renomear classe  
        Comando renomear conexão  
        Comando renomear tabela  
        Comando renomear exibição  
        Comando de relatório  
        Função Requery ()  
        RESTAURAR do comando  
    :::column-end:::
    :::column:::
        Comando restaurar MACROs  
        Comando restaurar tela  
        Comando restaurar janela  
        Comando retomar  
        Função RGB ()  
        Função RGBSCHEME ()  
        Variável de memória do sistema _RMARGIN  
        Comando RMDIR  
        Função ROW ()  
        EXECUTE &#124;!Comando  
        Comando RUNSCRIPT  
    :::column-end:::
:::row-end:::

## <a name="s"></a>S  

:::row:::
    :::column:::
        Comando salvar MACROs  
        Comando salvar tela  
        SALVAR no comando  
        Comando salvar WINDOWS  
        Função SCHEME ()  
        Função SCOLS ()  
        Variável de memória do sistema _SCREEN  
        Comando SCROLL  
        Comando SET  
        Definir comando alternativo  
        Comando SET ANSI  
        Comando SET APLABOUT  
        Definir comando AutoSalvar  
        Definir comando BELL  
        Definir comando de intermitência  
        Comando SET BORDER  
        Comando SET BRSTATUS  
        Comando SET CLASSLIB  
        Definir comando de limpeza  
        Definir comando de relógio  
        DEFINIR cor do comando  
        DEFINIR cor do comando de esquema  
        Definir comando de conjunto de cores  
        DEFINIR cor como comando  
        Definir comando compatível  
        Comando SET CONFIRM  
        Definir comando do CONSOLE  
        DEFINIR CPCOMPILE  
        DEFINIR CPDIALOG  
        Definir comando de moeda  
        Definir comando de CURSOR  
        Comando SET datasession  
        Definir comando de depuração  
        Comando SET DECIMALs  
        Comando definir delimitadores  
        Definir comando de desenvolvimento  
        Definir comando de dispositivo  
    :::column-end:::
    :::column:::
        Definir comando de exibição  
        Comando SET dohistory  
        Comando SET ECHO  
        Definir comando de ESCAPE  
        Comando SET FORMAT  
        Comando SET FUNCTION  
        Comando definir títulos  
        Comando SET HELP  
        Comando SET HELPFILTER  
        Definir comando de intensidade  
        Comando SET KEY  
        Comando SET keycomp  
        Comando SET LOGERRORS  
        Comando SET MACDESKTOP  
        Comando SET MACHELP  
        Comando SET MACKEY  
        Definir comando de margem  
        DEFINIR marca de comando  
        DEFINIR marca como comando  
        Comando SET MEMOWIDTH  
        Comando SET MESSAGE  
        Definir comando do MOUSE  
        Comando SET HODÔMETRO  
        Comando SET OLEOBJECT  
        Comando definir paleta  
        Comando SET PDSETUP  
        Comando SET POINT  
        Definir comando de impressora  
        Comando SET READBORDER  
        Comando SET REFRESH  
        Definir comando de recurso  
        Definir comando de segurança  
        Comando SET placar  
        Comando SET SECONDs  
        Definir comando separador  
        Comando SET SHADOWs  
        DEFINIR ignorar comando  
    :::column-end:::
    :::column:::
        Comando SET SPACE  
        Definir comando de STATUS  
        Definir comando da barra de STATUS  
        Comando SET STEP  
        Definir comando adesivo  
        Comando SET SYSFORMATS  
        Comando SET SYSMENU  
        Comando SET TALK  
        Definir comando textmerge  
        Comando definir delimitadores de textmerge  
        Comando SET TOPIC  
        Definir comando de ID do tópico  
        Comando SET TRBETWEEN  
        Comando SET TYPEAHEAD  
        Comando SET VIEW  
        DEFINIR janela do comando de memorando  
        Comando SET XCMDFILE  
        Variável de memória do sistema _SHELL  
        Mostrar comando GET  
        Mostrar comando GETS  
        Mostrar comando de MENU  
        Comando SHOW OBJECT  
        Mostrar comando POPUP  
        Mostrar comando de janela  
        Comando de tamanho POPUP  
        Comando dimensionar janela  
        Função SKPBAR ()  
        Função SKPPAD ()  
        Função SOUNDEX ()  
        Variável de memória do sistema _SPELLCHK  
        Funções SQL  
        Função SROWS ()  
        Variável de memória do sistema _STARTUP  
        Comando SUSPENDEr  
        Funções SYS (), exceto SYS (2011)  
        Função SYSMETRIC ()  
    :::column-end:::
:::row-end:::

## <a name="t"></a>T  

:::row:::
    :::column:::
        Variável de memória do sistema _TABS  
        TEXTO... Comando endtext  
        Variável de memória do sistema _THROTTLE  
    :::column-end:::
    :::column:::
        Função TRANSFORM ()  
        Variável de memória do sistema _TRANSPORT  
        Função TXTWIDTH ()  
    :::column-end:::
    :::column:::
        Comando de tipo  
    :::column-end:::
:::row-end:::

## <a name="u"></a>U  

:::row:::
    :::column:::
        Função UPDATED ()  
    :::column-end:::
    :::column:::
        USAR comando  
    :::column-end:::
:::row-end:::

## <a name="v"></a>V  

:::row:::
    :::column:::
        Comando validar banco de dados  
    :::column-end:::
    :::column:::
        Função VARREAD ()  
    :::column-end:::
    :::column:::
        Função VERSION ()  
    :::column-end:::
:::row-end:::

## <a name="w"></a>W  

:::row:::
    :::column:::
        Comando WAIT  
        Função WBORDER ()  
        Função WCHILD ()  
        Função WCOLS ()  
        Função WEXIST ()  
        Função WFONT ()  
        Variável de memória do sistema _WINDOWS  
        COM... Comando endcom  
    :::column-end:::
    :::column:::
        Variável de memória do sistema _WIZARD  
        Função WLAST ()  
        Função WLCOL ()  
        Função WLROW ()  
        Função WMAXIMUM ()  
        Função WMINIMUM ()  
        Função WONTOP ()  
        Função WOUTPUT ()  
    :::column-end:::
    :::column:::
        Função WPARENT ()  
        Variável de memória do sistema _WRAP  
        Função WREAD ()  
        Função WROWS ()  
        Função WTITLE ()  
        Função WVISIBLE ()  
    :::column-end:::
:::row-end:::

## <a name="z"></a>Z  

Comando janela de ZOOM
