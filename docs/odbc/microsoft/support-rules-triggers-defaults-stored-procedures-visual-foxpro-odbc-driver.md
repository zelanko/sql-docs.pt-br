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
ms.openlocfilehash: 2fcf8e7c80b2712313cba81199489dc7cb06dce0
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81301133"
---
# <a name="support-for-rules-triggers-default-values-and-stored-procedures-visual-foxpro-odbc-driver"></a>Suporte para regras, gatilhos, valores padrão e procedimentos armazenados (Driver ODBC do Visual FoxPro)
Você não pode criar regras, gatilhos, valores padrão ou procedimentos armazenados do Visual FoxPro usando o driver ODBC do Visual FoxPro. No entanto, seu aplicativo pode interagir com regras existentes, gatilhos, valores padrão ou procedimentos armazenados à medida que insere, atualiza ou exclui dados do Visual FoxPro armazenados em um banco de dados.  
  
 A tabela a seguir lista os comandos e funções do Visual FoxPro com suporte do driver ODBC do Visual FoxPro quando há comandos ou funções em regras, gatilhos, valores padrão ou procedimentos armazenados.  
  
 Se seu aplicativo interage com dados cujas regras, gatilhos, valores padrão ou procedimentos armazenados chamam quaisquer outros comandos ou funções do Visual FoxPro, o driver gera um erro. Consulte [comandos e funções do Visual FoxPro sem suporte](../../odbc/microsoft/unsupported-visual-foxpro-commands-and-functions-visual-foxpro-odbc-driver.md) para obter uma lista de comandos e funções sem suporte do driver.  
  
> [!TIP]  
>  Se você quiser inserir código condicional em suas regras, gatilhos ou procedimentos armazenados que determinam os comandos a serem executados quando chamados pelo driver, você poderá usar a função **Version ()** . A função **Version ()** retorna "Visual FoxPro ODBC Driver * \<Version>*" quando chamado pelo driver.  
  
## <a name="visual-foxpro-commands-and-functions-supported-in-rules-triggers-default-values-and-stored-procedures"></a>Comandos e funções do Visual FoxPro com suporte em regras, gatilhos, valores padrão e procedimentos armazenados  
  
||||  
|-|-|-|  
|Operador $|Operador %|& comando|  
|&& comando|* Comando|= Comando|  
  
## <a name="a"></a>Um  
  
||||  
|-|-|-|  
|Função ABS ()|Função ACOPY ()|Comando adicionar tabela|  
|Função ADATABASES ()|Função ADBOBJECTS ()|Função AERROR ()|  
|Função ADEL ()|Função AELEMENT ()|Função ALEN ()|  
|Função AFIELDS ()|Função AINS ()|ALTER TABLE – comando SQL|  
|Função ALIAS ()|Função mytrim ()|ACRESCENTAR do comando de matriz|  
|Operador AND|Comando APPEND|Comando acrescentar memorando|  
|ACRESCENTAR do comando|ACRESCENTAR comando geral|Função ASCAN ()|  
|Comando de procedimentos de acréscimo|Função ASC ()|Função ASUBSCRIPT ()|  
|Função Asen ()|Função ASORT ()|Função ATAN ()|  
|Função AT ()|Função AT_C ()|Função ATCLINE ()|  
|Função ATC ()|Função ATCC ()|Função AUSED ()|  
|Função ATLINE ()|Função ATN2 ()||  
|Comando médio|Função ACOS ()||  
  
## <a name="b"></a>B  
  
||||  
|-|-|-|  
|BEGIN TRANSACTION comando|Função BETWEEN ()|Função BITNOT ()|  
|Função BITCLEAR ()|Função BITLSHIFT ()|Função conjunto ()|  
|Função BITOR ()|Função BITRSHIFT ()|Comando em branco|  
|Função DEBITTEST ()|Função BITXOR ()||  
|Função BOF ()|Função BITAND ()||  
  
## <a name="c"></a>C  
  
||||  
|-|-|-|  
|Comando CALCULATE|Função CANDIDATE ()|Função CHR ()|  
|Função CDX ()|Função teto ()|FECHAR comandos|  
|Função CHRTRAN ()|Função CHRTRANC ()|Comando copiar índices|  
|Função CMONTH ()|CONTINUAR comando|Comando de copiar estrutura ESTENDIda|  
|Comando copiar procedimentos|Comando copiar estrutura|COPIAR para o comando|  
|Comando copiar marca|Comando copiar para matriz|Função CPCONVERT ()|  
|Função COS ()|Comando COUNT|Função CTOD ()|  
|Função CPCURRENT ()|Função CPDBF ()|Função CURSORSETPROP ()|  
|Função CTOT ()|Função CURSORGETPROP ()||  
|Função curva ()|Função CDOW ()||  
  
## <a name="d"></a>D  
  
||||  
|-|-|-|  
|Função DATE ()|Função DATETIME ()|Função DAY ()|  
|Função DBC ()|Função DBF ()|Função DBGETPROP ()|  
|Função DBUSED ()|DELETE – comando SQL|Excluir comando|  
|Comando DELETE TAG|Função DELETED ()|Função DESCENDING ()|  
|Função DIFFERENCE ()|Comando de dimensão|Função espaço em disco ()|  
|Função DMY ()|FAZER MAIÚSCULAS E MINÚSCULAS... Comando endcase|Comando DO|  
|DO WHILE... Comando ENDDO|Função DOW ()|Função DTOC ()|  
|Função DTOR ()|Função DTOS ()|Função DTOT ()|  
  
## <a name="e"></a>E  
  
||||  
|-|-|-|  
|Função EMPTY ()|Função EVALUATE ()|Comando EXIT|  
|Função ERROR ()|Função EXP ()||  
|Comando encerrar transação|Função EOF ()||  
  
## <a name="f"></a>F  
  
||||  
|-|-|-|  
|Função FCOUNT ()|Função FDATE ()|Função FIELD ()|  
|Função FILE ()|Função FILTER ()|Função FLDLIST ()|  
|Função FLOCK ()|Função FLOOR ()|Comando FLUSH|  
|PARA... Comando ENDFOR|Função FOR ()|Função FOUND ()|  
|Comando de tabela gratuita|Função FSIZE ()|Função FTIME ()|  
|Função FULLPATH ()|Comando de função|Função VF ()|  
  
## <a name="g"></a>G  
  
||||  
|-|-|-|  
|COLETAR comando|Função GETNEXTMODIFIED ()|Comando GO/GOTO|  
|Função GETFLDSTATE ()|Função GOMONTH ()||  
|Função GETCP ()|Função GETENV ()||  
  
## <a name="h"></a>H  
  
|||  
|-|-|  
|Função HEADER ()|Função HOUR ()|  
  
## <a name="i"></a>I  
  
||||  
|-|-|-|  
|Função IDXCOLLATE ()|SE... Comando ENDIF|Função IIF ()|  
|Função INDBC ()|Comando INDEX|Função inList ()|  
|INSERIR-comando SQL|Função INT ()|Função isalpha ()|  
|Função ISBLANK ()|Função IsDigit ()|Função isexclusive ()|  
|Função ISLEADBYTE ()|Função islow ()|Função ISNULL ()|  
|Função ISREADONLY ()|Função IsUpper ()||  
  
## <a name="k"></a>K  
  
||||  
|-|-|-|  
|Função KEY ()|Função keycompare ()||  
  
## <a name="l"></a>L  
  
||||  
|-|-|-|  
|Função LEFT ()|Função LEFTC ()|Função LIKEC ()|  
|Função LENC ()|Função LIKE ()|Função LOCK ()|  
|Comando LOCAL|Comando Localizar|Função LOOKUP ()|  
|Função LOG ()|Função LOG10 ()|Função LTRIM ()|  
|Função LOWER ()|Comando LPARAMETERS||  
|Função LUPDATE ()|Função LEN ()||  
  
## <a name="m"></a>M  
  
||||  
|-|-|-|  
|Variável de memória do sistema _MLINE|Função MAX ()|Função MDX ()|  
|Função MDY ()|Função MEMLINES ()|Função MESSAGE ()|  
|Função MIN ()|Função MINUTE ()|Função MLINE ()|  
|Função MOD ()|Função MONTH ()|Função MTON ()|  
  
## <a name="n"></a>N  
  
||||  
|-|-|-|  
|Função NDX ()|Função NORMALIZE ()|Operador NOT|  
|Comando de observação|Função NTOM ()|Função NVL ()|  
  
## <a name="o"></a>O   
  
||||  
|-|-|-|  
|Função OCCURs ()|Função OLDVAL ()|NO comando de erro|  
|Comando ON KEY|Função ON ()|Comando Abrir banco de dados|  
|Operador OR|Função ORDER ()|Função OS ()|  
  
## <a name="p"></a>P  
  
||||  
|-|-|-|  
|Comando de pacote|Função Parameters ()|Função PAYMENT ()|  
|Comando Parameters|Função PRIMARY ()|Comando particular|  
|Função PI ()|Função PROGRAM ()|Função Pri ()|  
|Comando de procedimento|Função VP ()||  
|Comando público|PADL () &#124; PADR () &#124; funções PADC ()||  
  
## <a name="r"></a>R  
  
||||  
|-|-|-|  
|Função RAND ()|Função RAT ()|Função RATC ()|  
|Função RATLINE ()|Comando recall|Função RECCOUNT ()|  
|Função RECNO ()|Função RECSIZE ()|Comando REGIONAL|  
|Função RELATION ()|Comando remover tabela|Comando REPLACE|  
|SUBSTITUIR do comando de matriz|Função REPLICAte ()|Repetir comando|  
|Comando de retorno|Função RIGHT ()|Função RIGHTC ()|  
|Função RLOCK ()|Comando ROLLBACK|Função ROUND ()|  
|Função RTOD ()|Função RTRIM ()||  
  
## <a name="s"></a>S  
  
||||  
|-|-|-|  
|VERIFICAR... Comando endscan|Comando de dispersão|Função SEC ()|  
|Função SECONDs ()|Comando de busca|Função SEEK ()|  
|Selecionar comando|Função SELECT ()|SELECT-comando SQL|  
|Comando SET BLOCKSIZE|Definir comando de transporte|Definir comando do século|  
|Comando SET COLLATE|Comando SET DATABASE|Definir comando de data|  
|Definir comando padrão|Comando SET DELETED|Comando SET EXACT|  
|Comando SET EXCLUSIVE|Comando SET FDOW|Comando definir campos|  
|Definir comando de filtro|Definir comando fixo|Definir comando FULLPATH|  
|Comando SET FWEEK|Comando definir horas|Comando SET INDEX|  
|Definir comando de bloqueio|Comando SET My LOCKs|Definir comando NEAR|  
|Comando SET NOCPTRANS|Definir comando NOTIFY|Comando SET NULL|  
|Comando SET OPTIMIZE|Comando SET ORDER|Comando SET PATH|  
|Comando SET PROCEDURE|Comando SET RELATION|Comando SET RELATION OFF|  
|Comando SET REPROCESS|Comando SET SKIP|Comando SET UDFPARMS|  
|Comando SET UNIQUE|Definir comando de VOLUME|Função SET ()|  
|Função SETFLDSTATE ()|Função SIGN ()|Função SIN ()|  
|Comando SKIP|Comando SORT|Função SPACE ()|  
|Função SQRT ()|Comando STORE|Função STR ()|  
|Função STRCONV ()|Função STRTRAN ()|Função de coisas ()|  
|Função STUFFC ()|Função SUBST ()|Função SUBSTRC ()|  
|Comando SUM|Função SYS (2011)||  
  
## <a name="t"></a>T  
  
||||  
|-|-|-|  
|Variável de memória do sistema _TALLY|Variável de memória do sistema _TRIGGERLEVEL|Função TAGCOUNT ()|  
|Função TABLEUPDATE ()|Função TAG ()|Função TARGET ()|  
|Função TAGNO ()|Função TAN ()|Função TRIM ()|  
|Função TIME ()|Comando TOTAL|Função TXNLEVEL ()|  
|Função TTOC ()|Função TTOD ()||  
|Função TYPE ()|Função TABLEREVERT ()||  
  
## <a name="u"></a>U  
  
||||  
|-|-|-|  
|Função UNIQUE ()|Comando UNLOCK|USAR comando|  
|Atualizar comando|Função UPPER ()||  
|Função USED ()|UPDATE – comando SQL||  
  
## <a name="v"></a>V  
  
||||  
|-|-|-|  
|Função VAL ()|Função VERSION ()||  
  
## <a name="w"></a>W  
  
||||  
|-|-|-|  
|Função WEEK ()|||  
  
## <a name="y"></a>S  
  
||||  
|-|-|-|  
|Função YEAR ()|||  
  
## <a name="z"></a>Z  
  
||||  
|-|-|-|  
|Comando ZAP|||
