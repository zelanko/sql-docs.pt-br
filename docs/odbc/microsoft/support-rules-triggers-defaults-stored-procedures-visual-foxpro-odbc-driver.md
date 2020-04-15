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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301133"
---
# <a name="support-for-rules-triggers-default-values-and-stored-procedures-visual-foxpro-odbc-driver"></a>Suporte para regras, gatilhos, valores padrão e procedimentos armazenados (Driver ODBC do Visual FoxPro)
Não é possível criar regras, gatilhos, valores padrão ou procedimentos armazenados do Visual FoxPro usando o Driver Visual FoxPro ODBC. No entanto, seu aplicativo pode interagir com regras, gatilhos, valores padrão ou procedimentos armazenados à medida que insere, atualiza ou exclui dados do Visual FoxPro armazenados em um banco de dados.  
  
 A tabela a seguir lista os comandos e funções do Visual FoxPro suportados pelo Driver Visual FoxPro ODBC quando os comandos ou funções existem em regras, gatilhos, valores padrão ou procedimentos armazenados.  
  
 Se o aplicativo interagir com dados cujas regras, gatilhos, valores padrão ou procedimentos armazenados chamem quaisquer outros comandos ou funções do Visual FoxPro, o driver gera um erro. Consulte [Comandos e funções do Visual FoxPro sem suporte](../../odbc/microsoft/unsupported-visual-foxpro-commands-and-functions-visual-foxpro-odbc-driver.md) para uma lista de comandos e funções não suportadas pelo driver.  
  
> [!TIP]  
>  Se você quiser inserir código condicional em suas regras, gatilhos ou procedimentos armazenados que determina os comandos a serem executados quando chamado pelo driver, você pode usar a função **VERSION( ).** A **função VERSION** retorna a versão "Visual FoxPro ODBC Driver * \<>" *quando chamada pelo driver.  
  
## <a name="visual-foxpro-commands-and-functions-supported-in-rules-triggers-default-values-and-stored-procedures"></a>Comandos e funções do Visual FoxPro suportados em regras, gatilhos, valores padrão e procedimentos armazenados  
  
||||  
|-|-|-|  
|Operador de Dólar|Operador %|Comando &|  
|Comando && |* Comando|= Comando|  
  
## <a name="a"></a>Um  
  
||||  
|-|-|-|  
|Função ABS|Função ACOPY|Adicionar comando de tabela|  
|Função ADATABASES|Função ADBOBJECTS( )|Função AERROR|  
|Função ADEL|Função AELEMENT( )|Função ALEN|  
|Função AFIELDS( )|Função AINS( )|ALTER TABLE – comando SQL|  
|FUNÇÃO ALIAS( )|Alltrim( ) Função|APÊNDICE DO Comando ARRAY|  
|E Operador|Comando APÊNDICE|Comando MEMO APPEND|  
|APÊNDICE DO Comando|Comando Geral de APÊNDICE|Função ASCAN|  
|Comando PROCEDIMENTOS DE APÊNDICE|Função ASC|Função ASUBSCRIPT|  
|ASIN( ) Função|Função ASORT( )|ATAN( ) Função|  
|AT( ) Função|AT_C função|ATCLINE( ) Função|  
|Atc( ) Função|Atcc( ) Função|Função AUSED( )|  
|ATLINE( ) Função|AtN2( ) Função||  
|Comando MÉDIO|Função ACOS||  
  
## <a name="b"></a>B  
  
||||  
|-|-|-|  
|Iniciar comando de transação|FUNÇÃO ENTRE( )|Função BITNOT|  
|Função BITCLEAR|Função BITLSHIFT|Função BITSET|  
|Função BITOR( )|Função BITRSHIFT|Comando EM BRANCO|  
|Função BITTEST( )|Função BITXOR||  
|BOF( ) Função|Bitand( ) Função||  
  
## <a name="c"></a>C  
  
||||  
|-|-|-|  
|Comando CALCULATE|CANDIDATO( ) Função|CHR( ) Função|  
|Função CDX|FUNÇÃO TETO|Comandos CLOSE|  
|Função CHRTRAN|FUNÇÃO CHRTRANC|Comando COPY INDEXES|  
|CMONTH( ) Função|Comando CONTINUE|COMANDO ESTENDIDO COPY STRUCTURE|  
|Comando PROCEDIMENTOS DE CÓPIA|Comando COPY STRUCTURE|Comando COPY TO|  
|Comando COPY TAG|Comando COPY TO ARRAY|CPCONVERT( ) Função|  
|Cos( ) Função|Comando COUNT|Função CTOD|  
|CPCURRENT( ) Função|CPDBF( ) Função|FUNÇÃO CURSORSETPROP|  
|Função CTOT|FUNÇÃO CURSORGETPROP||  
|FUNÇÃO CURVAL|CDOW( ) Função||  
  
## <a name="d"></a>D  
  
||||  
|-|-|-|  
|DATA( ) Função|DATA-HORA( ) Função|DIA( ) Função|  
|Função DBC|Função DBF|Função DBGETPROP|  
|Função DBUSED( )|DELETE – comando SQL|Comando DELETE|  
|Comando DELETE TAG|FUNÇÃO EXCLUÍDA( )|FUNÇÃO DESCENDENTE|  
|DIFERENÇA( ) Função|Comando DIMENSION|FUNÇÃO DISKSPACE|  
|Função DMY( )|FAÇA CASO ... Comando ENDCASE|Comando DO|  
|FAÇA ENQUANTO ... Comando ENDDO|FUNÇÃO DOW|Função DTOC|  
|Função DTOR|Função DTOS|Função DTOT|  
  
## <a name="e"></a>E  
  
||||  
|-|-|-|  
|FUNÇÃO EMPTY( )|AVALIAR a função|Comando EXIT|  
|FUNÇÃO ERROR( )|Função EXP||  
|Comando DE TRANSAÇÃO FINAL|Função EOF( )||  
  
## <a name="f"></a>F  
  
||||  
|-|-|-|  
|Função FCOUNT( )|Função FDATE( )|FUNÇÃO FIELD( )|  
|FUNÇÃO FILE( )|FUNÇÃO FILTER( )|Função FLDLIST|  
|FUNÇÃO FLOCK|FUNÇÃO PISO( )|Comando FLUSH|  
|Para... Comando ENDFOR|FOR( ) Função|FUNÇÃO FOUND()|  
|Comando MESA GRÁTIS|Função FSIZE|Função FTIME( )|  
|Função FULLPATH|Comando FUNCTION|Função FV|  
  
## <a name="g"></a>G  
  
||||  
|-|-|-|  
|Comando GATHER|FUNÇÃO GETNEXTMODIFIED( )|Comando GO/GOTO|  
|FUNÇÃO GETFLDSTATE|GOMonth( ) Função||  
|FUNÇÃO GETCP|FUNÇÃO GETENV||  
  
## <a name="h"></a>H  
  
|||  
|-|-|  
|FUNÇÃO HEADER( )|HORA( ) Função|  
  
## <a name="i"></a>I  
  
||||  
|-|-|-|  
|IDXCOLLATE( ) Função|Se... Comando ENDIF|Função IIF|  
|Função INDBC|Comando INDEX|INLIST( ) Função|  
|Comando INSERT-SQL|Função INT|FUNÇÃO ISALPHA|  
|FUNÇÃO ISBLANK( )|FUNÇÃO ISDIGIT( )|FUNÇÃO ISEXCLUSIVE( )|  
|FUNÇÃO ISLEADBYTE|FUNÇÃO ISLOWER( )|FUNÇÃO ISNULL( )|  
|FUNÇÃO ISREADONLY( )|ISUPPER( ) Função||  
  
## <a name="k"></a>K  
  
||||  
|-|-|-|  
|FUNÇÃO KEY( )|FUNÇÃO KEYMATCH( )||  
  
## <a name="l"></a>L  
  
||||  
|-|-|-|  
|Função esquerda( )|FUNÇÃO LEFTC|Função LIKEC|  
|Função LENC|FUNÇÃO LIKE( )|FUNÇÃO LOCK( )|  
|Comando LOCAL|Comando LOCALIZAR|FUNÇÃO LOOKUP( )|  
|Função LOG( )|Função LOG10|Função LTRIM|  
|FUNÇÃO MAIS BAIXA|Comando LPARAMETERS||  
|Função LUPDATE( )|Função LEN( )||  
  
## <a name="m"></a>M  
  
||||  
|-|-|-|  
|Variável de memória do sistema _MLINE|FUNÇÃO MAX|Função MDX|  
|Função MDY|Função MEMLINES( )|FUNÇÃO MENSAGEM|  
|Função MIN|MINUTO( ) Função|Função MLINE( )|  
|Mod( ) Função|MÊS( ) Função|Função MTON|  
  
## <a name="n"></a>N  
  
||||  
|-|-|-|  
|Função NDX|FUNÇÃO NORMALIZE|Não Operador|  
|Comando NOTA|NTOM( ) Função|NVL( ) Função|  
  
## <a name="o"></a>O   
  
||||  
|-|-|-|  
|FUNÇÃO OCORRE( )|Função OLDVAL|Comando ON ERROR|  
|Comando ON KEY|ON( ) Função|Comando OPEN DATABASE|  
|OU Operador|ORDEM( ) Função|Função OS( )|  
  
## <a name="p"></a>P  
  
||||  
|-|-|-|  
|Comando PACK|PARÂMETROS ( ) Função|PAGAMENTO( ) Função|  
|Comando PARAMETERS|FUNÇÃO PRIMÁRIA( )|Comando PRIVADO|  
|Pi( ) Função|FUNÇÃO PROGRAMA|FUNÇÃO ADEQUADA ( )|  
|Comando de PROCEDIMENTO|Função PV||  
|Comando PÚBLICO|PADL( ) &#124; PADR &#124; FUNÇÕES PADC( )||  
  
## <a name="r"></a>R  
  
||||  
|-|-|-|  
|RAND( ) Função|Função RAT( )|Função RATC|  
|FUNÇÃO RATLINE( )|Comando RECALL|Função RECCount( )|  
|RECNO( ) Função|FUNÇÃO RECSIZE|Comando REGIONAL|  
|FUNÇÃO RELATION( )|Comando REMOVE TABLE|Comando REPLACE|  
|SUBSTITUIR DO Comando ARRAY|FUNÇÃO REPLICATE( )|Comando RETRY|  
|Comando RETURN|FUNÇÃO DIREITA( )|FUNÇÃO RIGHTC( )|  
|RLOCK( ) Função|Comando DE REVERSÃO|FUNÇÃO ROUND( )|  
|Função RTOD|RTRIM( ) Função||  
  
## <a name="s"></a>S  
  
||||  
|-|-|-|  
|Varredura... Comando ENDSCAN|Comando SCATTER|Função SEC( )|  
|SEGUNDAS () Função|Comando SEEK|FUNÇÃO SEEK|  
|Comando SELECT|FUNÇÃO SELECT( )|Comando SELECT-SQL|  
|Comando SET BLOCKSIZE|Comando CARRY SET|Comando SET CENTURY|  
|Comando SET COLLATE|Definir comando de banco de dados|Comando SET DATE|  
|DEFINIR comando DEFAULT|Comando SET DELETED|Comando SET EXACT|  
|Comando SET EXCLUSIVE|Comando SET FDOW|Comando SET FIELDS|  
|Definir comando FILTER|DEFINIR comando fixo|Comando SET FULLPATH|  
|Comando SET FWEEK|Comando SET HOURS|Comando DE ÍNDICE DEFINIDO|  
|Comando SET LOCK|DEFINIR comando MULTILOCKS|SET NEAR Comando|  
|DEFINIR Comando NOCPTRANS|DEFINIR Comando NOTIFICAR|Comando SET NULL|  
|Comando SET OPTIMIZE|Comando SET ORDER|Comando SET PATH|  
|Comando DE PROCEDIMENTO DEFINIDO|Comando DEFINIR RELAÇÃO|DEFINIR COMANDO RELACIONOFF|  
|Comando SET REPROCESS|SET SKIP Command|DEFINIR comando UDFPARMS|  
|Comando SET UNIQUE|Definir comando VOLUME|FUNÇÃO SET( )|  
|Função SETFLDSTATE()|SINAL ( ) Função|Função SIN|  
|Comando SKIP|Comando SORT|FUNÇÃO SPACE( )|  
|Função SQRT|Comando STORE|Função STR|  
|FUNÇÃO STRCONV|STRTRAN( ) Função|FUNÇÃO STUFF( )|  
|FUNÇÃO STUFFC|FUNÇÃO SUBSTR|FUNÇÃO SUBSTRC|  
|Comando SUM|Função SYS(2011)||  
  
## <a name="t"></a>T  
  
||||  
|-|-|-|  
|_TALLY variável de memória do sistema|Variável de memória do sistema _TRIGGERLEVEL|Tagcount( ) Função|  
|FUNÇÃO TABLEUPDATE( )|TAG( ) Função|FUNÇÃO TARGET( )|  
|TAGNO( ) Função|Função TAN|Trim( ) Função|  
|FUNÇÃO TIME( )|Comando TOTAL|TXNLEVEL( ) Função|  
|TTOC( ) Função|Função TTOD( )||  
|TIPO( ) Função|FUNÇÃO TABLEREVERT( )||  
  
## <a name="u"></a>U  
  
||||  
|-|-|-|  
|FUNÇÃO UNIQUE( )|Comando UNLOCK|Comando USE|  
|Comando UPDATE|FUNÇÃO UPPER( )||  
|FUNÇÃO USADA( )|UPDATE – comando SQL||  
  
## <a name="v"></a>V  
  
||||  
|-|-|-|  
|VAL( ) Função|FUNÇÃO VERSION( )||  
  
## <a name="w"></a>W  
  
||||  
|-|-|-|  
|FUNÇÃO SEMANA|||  
  
## <a name="y"></a>S  
  
||||  
|-|-|-|  
|FUNÇÃO ANO|||  
  
## <a name="z"></a>Z  
  
||||  
|-|-|-|  
|Comando ZAP|||
