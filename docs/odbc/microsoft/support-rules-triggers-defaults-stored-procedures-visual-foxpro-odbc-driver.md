---
title: Suporte para regras, gatilhos, valores padrão e procedimentos armazenados | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Visual FoxPro ODBC driver [ODBC], stored procedures
- FoxPro ODBC driver [ODBC], commands and functions
- commands for FoxPro ODBC driver [ODBC]
- FoxPro ODBC driver [ODBC], default values
- FoxPro ODBC driver [ODBC], triggers
- stored procedures [ODBC], Visual FoxPro ODBC driver
- Visual FoxPro ODBC driver [ODBC], rules
- FoxPro commands and functions [ODBC]
- rules [ODBC]
- Visual FoxPro ODBC driver [ODBC], default values
- FoxPro ODBC driver [ODBC], rules
- functions [ODBC], Visual FoxPro
- default values [ODBC]
- Visual FoxPro ODBC driver [ODBC], commands and functions
- Visual FoxPro ODBC driver [ODBC], triggers
- FoxPro ODBC driver [ODBC], stored procedures
- Visual FoxPro commands and functions [ODBC]
ms.assetid: e449de20-d6ca-4902-9f8e-814eb6e86650
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a02aeea8f33e3a4d87fc771a7b0fa7b1a0067b6d
ms.sourcegitcommit: 99f61724de5edf6640efd99916d464172eb23f92
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/28/2020
ms.locfileid: "87363356"
---
# <a name="support-for-rules-triggers-default-values-and-stored-procedures-visual-foxpro-odbc-driver"></a>Suporte para regras, gatilhos, valores padrão e procedimentos armazenados (Driver ODBC do Visual FoxPro)
Você não pode criar regras, gatilhos, valores padrão ou procedimentos armazenados do Visual FoxPro usando o driver ODBC do Visual FoxPro. No entanto, seu aplicativo pode interagir com regras existentes, gatilhos, valores padrão ou procedimentos armazenados à medida que insere, atualiza ou exclui dados do Visual FoxPro armazenados em um banco de dados.  
  
 A tabela a seguir lista os comandos e funções do Visual FoxPro com suporte do driver ODBC do Visual FoxPro quando há comandos ou funções em regras, gatilhos, valores padrão ou procedimentos armazenados.  
  
 Se seu aplicativo interage com dados cujas regras, gatilhos, valores padrão ou procedimentos armazenados chamam quaisquer outros comandos ou funções do Visual FoxPro, o driver gera um erro. Consulte [comandos e funções do Visual FoxPro sem suporte](../../odbc/microsoft/unsupported-visual-foxpro-commands-and-functions-visual-foxpro-odbc-driver.md) para obter uma lista de comandos e funções sem suporte do driver.  
  
> [!TIP]  
>  Se você quiser inserir código condicional em suas regras, gatilhos ou procedimentos armazenados que determinam os comandos a serem executados quando chamados pelo driver, você poderá usar a função **Version ()** . A função **Version ()** retorna "driver ODBC do Visual FoxPro *\<version>* " quando chamado pelo driver.  
  
## <a name="visual-foxpro-commands-and-functions-supported-in-rules-triggers-default-values-and-stored-procedures"></a>Comandos e funções do Visual FoxPro com suporte em regras, gatilhos, valores padrão e procedimentos armazenados  

:::row:::
    :::column:::
        Operador $  
        Operador %  
    :::column-end:::
    :::column:::
        & comando  
        && comando  
    :::column-end:::
    :::column:::
        \* Comando  
        = Comando  
    :::column-end:::
:::row-end:::

## <a name="a"></a>A  

:::row:::
    :::column:::
        Função ABS ()  
        Função ACOPY ()  
        Função ACOS ()  
        Função ADATABASES ()  
        Função ADBOBJECTS ()  
        Comando adicionar tabela  
        Função ADEL ()  
        Função AELEMENT ()  
        Função AERROR ()  
        Função AFIELDS ()  
        Função AINS ()  
        Função ALEN ()  
        Função ALIAS ()  
    :::column-end:::
    :::column:::
        Função mytrim ()  
        ALTER TABLE – comando SQL  
        Operador AND  
        Comando APPEND  
        ACRESCENTAR do comando  
        ACRESCENTAR do comando de matriz  
        ACRESCENTAR comando geral  
        Comando acrescentar memorando  
        Comando de procedimentos de acréscimo  
        Função ASC ()  
        Função ASCAN ()  
        Função Asen ()  
        Função ASORT ()  
    :::column-end:::
    :::column:::
        Função ASUBSCRIPT ()  
        Função AT ()  
        Função AT_C ()  
        Função ATAN ()  
        Função ATC ()  
        Função ATCC ()  
        Função ATCLINE ()  
        Função ATLINE ()  
        Função ATN2 ()  
        Função AUSED ()  
        Comando médio  
    :::column-end:::
:::row-end:::

## <a name="b"></a>B  

:::row:::
    :::column:::
        BEGIN TRANSACTION comando  
        Função BETWEEN ()  
        Função BITAND ()  
        Função BITCLEAR ()  
        Função BITLSHIFT ()  
    :::column-end:::
    :::column:::
        Função BITNOT ()  
        Função BITOR ()  
        Função BITRSHIFT ()  
        Função conjunto ()  
        Função DEBITTEST ()  
    :::column-end:::
    :::column:::
        Função BITXOR ()  
        Comando em branco  
        Função BOF ()  
    :::column-end:::
:::row-end:::

## <a name="c"></a>C  

:::row:::
    :::column:::
        Comando CALCULATE  
        Função CANDIDATE ()  
        Função CDOW ()  
        Função CDX ()  
        Função teto ()  
        Função CHR ()  
        Função CHRTRAN ()  
        Função CHRTRANC ()  
        FECHAR comandos  
        Função CMONTH ()  
    :::column-end:::
    :::column:::
        CONTINUAR comando  
        Comando copiar índices  
        Comando copiar procedimentos  
        Comando copiar estrutura  
        Comando de copiar estrutura ESTENDIda  
        Comando copiar marca  
        COPIAR para o comando  
        Comando copiar para matriz  
        Função COS ()  
        Comando COUNT  
    :::column-end:::
    :::column:::
        Função CPCONVERT ()  
        Função CPCURRENT ()  
        Função CPDBF ()  
        Função CTOD ()  
        Função CTOT ()  
        Função CURSORGETPROP ()  
        Função CURSORSETPROP ()  
        Função curva ()  
    :::column-end:::
:::row-end:::

## <a name="d"></a>D  

:::row:::
    :::column:::
        Função DATE ()  
        Função DATETIME ()  
        Função DAY ()  
        Função DBC ()  
        Função DBF ()  
        Função DBGETPROP ()  
        Função DBUSED ()  
        DELETE – comando SQL  
    :::column-end:::
    :::column:::
        Excluir comando  
        Comando DELETE TAG  
        Função DELETED ()  
        Função DESCENDING ()  
        Função DIFFERENCE ()  
        Comando de dimensão  
        Função espaço em disco ()  
        Função DMY ()  
    :::column-end:::
    :::column:::
        Comando DO  
        FAZER MAIÚSCULAS E MINÚSCULAS... Comando endcase  
        DO WHILE... Comando ENDDO  
        Função DOW ()  
        Função DTOC ()  
        Função DTOR ()  
        Função DTOS ()  
        Função DTOT ()  
    :::column-end:::
:::row-end:::

## <a name="e"></a>E  

:::row:::
    :::column:::
        Função EMPTY ()  
        Comando encerrar transação  
        Função EOF ()  
    :::column-end:::
    :::column:::
        Função ERROR ()  
        Função EVALUATE ()  
        Comando EXIT  
    :::column-end:::
    :::column:::
        Função EXP ()  
    :::column-end:::
:::row-end:::

## <a name="f"></a>F  

:::row:::
    :::column:::
        Função FCOUNT ()  
        Função FDATE ()  
        Função FIELD ()  
        Função FILE ()  
        Função FILTER ()  
        Função FLDLIST ()  
    :::column-end:::
    :::column:::
        Função FLOCK ()  
        Função FLOOR ()  
        Comando FLUSH  
        Função FOR ()  
        PARA... Comando ENDFOR  
        Função FOUND ()  
    :::column-end:::
    :::column:::
        Comando de tabela gratuita  
        Função FSIZE ()  
        Função FTIME ()  
        Função FULLPATH ()  
        Comando de função  
        Função VF ()  
    :::column-end:::
:::row-end:::

## <a name="g"></a>G  

:::row:::
    :::column:::
        COLETAR comando  
        Função GETCP ()  
        Função GETENV ()  
    :::column-end:::
    :::column:::
        Função GETFLDSTATE ()  
        Função GETNEXTMODIFIED ()  
        Comando GO/GOTO  
    :::column-end:::
    :::column:::
        Função GOMONTH ()  
    :::column-end:::
:::row-end:::

## <a name="h"></a>H  

:::row:::
    :::column:::
        Função HEADER ()
    :::column-end:::
    :::column:::
        Função HOUR ()
    :::column-end:::
:::row-end:::

## <a name="i"></a>I  

:::row:::
    :::column:::
        Função IDXCOLLATE ()  
        SE... Comando ENDIF  
        Função IIF ()  
        Função INDBC ()  
        Comando INDEX  
        Função inList ()  
    :::column-end:::
    :::column:::
        INSERIR-comando SQL  
        Função INT ()  
        Função isalpha ()  
        Função ISBLANK ()  
        Função IsDigit ()  
        Função isexclusive ()  
    :::column-end:::
    :::column:::
        Função ISLEADBYTE ()  
        Função islow ()  
        Função ISNULL ()  
        Função ISREADONLY ()  
        Função IsUpper ()  
    :::column-end:::
:::row-end:::

## <a name="k"></a>K  

:::row:::
    :::column:::
        Função KEY ()
    :::column-end:::
    :::column:::
        Função keycompare ()
    :::column-end:::
:::row-end:::

## <a name="l"></a>L  

:::row:::
    :::column:::
        Função LEFT ()  
        Função LEFTC ()  
        Função LEN ()  
        Função LENC ()  
        Função LIKE ()  
        Função LIKEC ()  
    :::column-end:::
    :::column:::
        Comando LOCAL  
        Comando Localizar  
        Função LOCK ()  
        Função LOG ()  
        Função LOG10 ()  
        Função LOOKUP ()  
    :::column-end:::
    :::column:::
        Função LOWER ()  
        Comando LPARAMETERS  
        Função LTRIM ()  
        Função LUPDATE ()  
    :::column-end:::
:::row-end:::

## <a name="m"></a>M  

:::row:::
    :::column:::
        Função MAX ()  
        Função MDX ()  
        Função MDY ()  
        Função MEMLINES ()  
    :::column-end:::
    :::column:::
        Função MESSAGE ()  
        Função MIN ()  
        Função MINUTE ()  
        Variável de memória do sistema _MLINE  
    :::column-end:::
    :::column:::
        Função MLINE ()  
        Função MOD ()  
        Função MONTH ()  
        Função MTON ()  
    :::column-end:::
:::row-end:::

## <a name="n"></a>N  

:::row:::
    :::column:::
        Função NDX ()  
        Função NORMALIZE ()  
    :::column-end:::
    :::column:::
        Operador NOT  
        Comando de observação  
    :::column-end:::
    :::column:::
        Função NTOM ()  
        Função NVL ()  
    :::column-end:::
:::row-end:::

## <a name="o"></a>O  

:::row:::
    :::column:::
        Função OCCURs ()  
        Função OLDVAL ()  
        Função ON ()  
    :::column-end:::
    :::column:::
        NO comando de erro  
        Comando ON KEY  
        Comando Abrir banco de dados  
    :::column-end:::
    :::column:::
        Operador OR  
        Função ORDER ()  
        Função OS ()  
    :::column-end:::
:::row-end:::

## <a name="p"></a>P  

:::row:::
    :::column:::
        Comando de pacote  
        PADL () &#124; PADR () &#124; funções PADC ()  
        Comando Parameters  
        Função Parameters ()  
        Função PAYMENT ()  
    :::column-end:::
    :::column:::
        Função PI ()  
        Função PRIMARY ()  
        Comando particular  
        Comando de procedimento  
        Função PROGRAM ()  
    :::column-end:::
    :::column:::
        Função Pri ()  
        Comando público  
        Função VP ()  
    :::column-end:::
:::row-end:::

## <a name="r"></a>R  

:::row:::
    :::column:::
        Função RAND ()  
        Função RAT ()  
        Função RATC ()  
        Função RATLINE ()  
        Comando recall  
        Função RECCOUNT ()  
        Função RECNO ()  
        Função RECSIZE ()  
    :::column-end:::
    :::column:::
        Comando REGIONAL  
        Função RELATION ()  
        Comando remover tabela  
        Comando REPLACE  
        SUBSTITUIR do comando de matriz  
        Função REPLICAte ()  
        Repetir comando  
        Comando de retorno  
    :::column-end:::
    :::column:::
        Função RIGHT ()  
        Função RIGHTC ()  
        Função RLOCK ()  
        Comando ROLLBACK  
        Função ROUND ()  
        Função RTOD ()  
        Função RTRIM ()  
    :::column-end:::
:::row-end:::

## <a name="s"></a>S  

:::row:::
    :::column:::
        VERIFICAR... Comando endscan  
        Comando de dispersão  
        Função SEC ()  
        Função SECONDs ()  
        Comando de busca  
        Função SEEK ()  
        Selecionar comando  
        Função SELECT ()  
        SELECT-comando SQL  
        Função SET ()  
        Comando SET BLOCKSIZE  
        Definir comando de transporte  
        Definir comando do século  
        Comando SET COLLATE  
        Comando SET DATABASE  
        Definir comando de data  
        Definir comando padrão  
        Comando SET DELETED  
        Comando SET EXACT  
        Comando SET EXCLUSIVE  
        Comando SET FDOW  
    :::column-end:::
    :::column:::
        Comando definir campos  
        Definir comando de filtro  
        Definir comando fixo  
        Definir comando FULLPATH  
        Comando SET FWEEK  
        Comando definir horas  
        Comando SET INDEX  
        Definir comando de bloqueio  
        Comando SET My LOCKs  
        Definir comando NEAR  
        Comando SET NOCPTRANS  
        Definir comando NOTIFY  
        Comando SET NULL  
        Comando SET OPTIMIZE  
        Comando SET ORDER  
        Comando SET PATH  
        Comando SET PROCEDURE  
        Comando SET RELATION  
        Comando SET RELATION OFF  
        Comando SET REPROCESS  
        Comando SET SKIP  
    :::column-end:::
    :::column:::
        Comando SET UDFPARMS  
        Comando SET UNIQUE  
        Definir comando de VOLUME  
        Função SETFLDSTATE ()  
        Função SIGN ()  
        Função SIN ()  
        Comando SKIP  
        Comando SORT  
        Função SPACE ()  
        Função SQRT ()  
        Comando STORE  
        Função STR ()  
        Função STRCONV ()  
        Função STRTRAN ()  
        Função de coisas ()  
        Função STUFFC ()  
        Função SUBST ()  
        Função SUBSTRC ()  
        Comando SUM  
        Função SYS (2011)  
    :::column-end:::
:::row-end:::

## <a name="t"></a>T  

:::row:::
    :::column:::
        Função TABLEREVERT ()  
        Função TABLEUPDATE ()  
        Função TAG ()  
        Função TAGCOUNT ()  
        Função TAGNO ()  
        Variável de memória do sistema _TALLY  
    :::column-end:::
    :::column:::
        Função TAN ()  
        Função TARGET ()  
        Função TIME ()  
        Comando TOTAL  
        Variável de memória do sistema _TRIGGERLEVEL  
        Função TRIM ()  
    :::column-end:::
    :::column:::
        Função TTOC ()  
        Função TTOD ()  
        Função TXNLEVEL ()  
        Função TYPE ()  
    :::column-end:::
:::row-end:::

## <a name="u"></a>U  

:::row:::
    :::column:::
        Função UNIQUE ()  
        Comando UNLOCK  
        Atualizar comando  
    :::column-end:::
    :::column:::
        UPDATE – comando SQL  
        Função UPPER ()  
        USAR comando  
    :::column-end:::
    :::column:::
        Função USED ()  
    :::column-end:::
:::row-end:::

## <a name="v"></a>V  

:::row:::
    :::column:::
        Função VAL ()
    :::column-end:::
    :::column:::
        Função VERSION ()
    :::column-end:::
:::row-end:::

## <a name="w"></a>W  

Função WEEK ()

## <a name="y"></a>S  

Função YEAR ()

## <a name="z"></a>Z  

Comando ZAP
