---
title: Suporte para regras, valores padrão, procedimentos armazenados e gatilhos | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 90a39ad540f3320ed78e981030679b59d911eeef
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68080769"
---
# <a name="support-for-rules-triggers-default-values-and-stored-procedures-visual-foxpro-odbc-driver"></a>Suporte para regras, gatilhos, valores padrão e procedimentos armazenados (Driver ODBC do Visual FoxPro)
Você não pode criar regras do Visual FoxPro, gatilhos, valores padrão ou procedimentos armazenados usando o Driver de ODBC do Visual FoxPro. No entanto, seu aplicativo pode interagir com os procedimentos armazenados, gatilhos, valores padrão ou as regras existentes, como ele insere, atualiza ou exclui dados do Visual FoxPro armazenados em um banco de dados.  
  
 A tabela a seguir lista os comandos do Visual FoxPro e funções com suporte pelo Driver de ODBC do Visual FoxPro quando as funções ou os comandos existirem em procedimentos armazenados, gatilhos, valores padrão ou as regras.  
  
 Se seu aplicativo interage com os dados cujo regras, gatilhos, valores padrão ou procedimentos armazenados chamam outros comandos do Visual FoxPro ou funções, o driver gerará um erro. Ver [funções e não há suporte para comandos do Visual FoxPro](../../odbc/microsoft/unsupported-visual-foxpro-commands-and-functions-visual-foxpro-odbc-driver.md) para obter uma lista de comandos e funções não têm suportadas pelo driver.  
  
> [!TIP]  
>  Se você quiser inserir código condicional em suas regras, gatilhos ou procedimentos armazenados que determina os comandos a executar quando chamado pelo driver, você pode usar o **(versão)** função. O **(versão)** retornos de função "Driver de ODBC do Visual FoxPro  *\<versão >* " quando chamado pelo driver.  
  
## <a name="visual-foxpro-commands-and-functions-supported-in-rules-triggers-default-values-and-stored-procedures"></a>Comandos do Visual FoxPro e funções com suporte em procedimentos armazenados, gatilhos, valores padrão e regras  
  
||||  
|-|-|-|  
|Operador $|Operador %|& Comando|  
|& & Comando|* O comando|= O comando|  
  
## <a name="a"></a>Um  
  
||||  
|-|-|-|  
|Função do ABS)|Função do ACOPY)|Adicionar comando de tabela|  
|Função do ADATABASES)|Função do ADBOBJECTS)|Função do AERROR)|  
|Função do ADEL)|Função do elemento)|Função do ALEN)|  
|Função do AFIELDS)|Função do AINS)|ALTER TABLE – comando SQL|  
|Função do ALIAS)|Função do ALLTRIM)|ACRÉSCIMO do comando de matriz|  
|E o operador|Comando APPEND|Memorando comando APPEND|  
|ACRÉSCIMO do comando|ACRESCENTE o comando geral|Função do ASCAN)|  
|Comando de procedimentos de ACRÉSCIMO|Função do ASC)|Função do ASUBSCRIPT)|  
|Função do ASIN)|Função do ASORT)|Função do ATAN)|  
|EM função)|Função do AT_C)|Função do ATCLINE)|  
|Função do ATC)|Função do ATCC)|Função do AUSED)|  
|Função do ATLINE)|Função do ATN2)||  
|Comando médio|Função do ACOS)||  
  
## <a name="b"></a>B  
  
||||  
|-|-|-|  
|Comando de transação BEGIN|ENTRE a função)|Função do BITNOT)|  
|Função do BITCLEAR)|Função do BITLSHIFT)|Função do BITSET)|  
|Função do BITOR)|Função do BITRSHIFT)|Comando em branco|  
|Função do BITTEST)|Função do BITXOR)||  
|Função do BOF)|Função do BITAND)||  
  
## <a name="c"></a>C  
  
||||  
|-|-|-|  
|CALCULAR o comando|Função do Release CANDIDATE)|Função do CHR)|  
|Função do CDX)|À função CEILING)|Comandos CLOSE|  
|Função do CHRTRAN)|Função do CHRTRANC)|Copie o comando de ÍNDICES|  
|Função do CMONTH)|Comando CONTINUE|Copie o comando estendido de estrutura|  
|Comando de procedimentos de cópia|Copie o comando de estrutura|Copiar para o comando|  
|Copie o comando marca|Copiar para o comando de matriz|Função do CPCONVERT)|  
|COS () de função|Comando de contagem|Função do CTOD)|  
|Função do CPCURRENT)|Função do CPDBF)|Função do CURSORSETPROP)|  
|Função do CTOT)|Função do CURSORGETPROP)||  
|Função (CURVAL)|Função do CDOW)||  
  
## <a name="d"></a>D  
  
||||  
|-|-|-|  
|Função de data)|Função do DATETIME)|Função do dia)|  
|Função do DBC)|Função do DBF)|Função do DBGETPROP)|  
|Função do DBUSED)|DELETE – comando SQL|Comando DELETE|  
|Comando DELETE TAG|Função (excluído)|Em ordem DECRESCENTE de função)|  
|Função () de diferença|Comando de dimensão|Função () de espaço em disco|  
|Função do DMY)|FAÇA O CASO... Comando ENDCASE|Comando|  
|WHILE... Comando ENDDO|Função do DOW)|Função do DTOC)|  
|Função do DTOR)|Função do DTOS)|Função do DTOT)|  
  
## <a name="e"></a>E  
  
||||  
|-|-|-|  
|Função (vazio)|AVALIAR a função)|Comando de saída|  
|Função do erro)|Função do EXP)||  
|Comando de transação do fim|Função do EOF)||  
  
## <a name="f"></a>F  
  
||||  
|-|-|-|  
|Função do FCOUNT)|Função do FDATE)|Função do campo)|  
|Função do arquivo)|Função do filtro)|Função do FLDLIST)|  
|Função do USAM)|Função do FLOOR)|Comando FLUSH|  
|FOR... Comando ENDFOR|PARA a função)|ENCONTRADA a função)|  
|Comando livre de tabela|Função do FSIZE)|Função do FTIME)|  
|Função do caminho completo)|Comando de função|Função do VF)|  
  
## <a name="g"></a>G  
  
||||  
|-|-|-|  
|COLETAR o comando|Função do GETNEXTMODIFIED)|Comando GO/GOTO|  
|Função do GETFLDSTATE)|Função do GOMONTH)||  
|Função do GETCP)|Função do GETENV)||  
  
## <a name="h"></a>H  
  
|||  
|-|-|  
|Função do cabeçalho)|Função do HOUR)|  
  
## <a name="i"></a>I  
  
||||  
|-|-|-|  
|Função do IDXCOLLATE)|IF... Comando ENDIF|Instrução IIf)|  
|Função do INDBC)|Comando INDEX|Função () de lista de entrada|  
|Comando SQL INSERT|Função do INT)|Função do ISALPHA)|  
|Função do ISBLANK)|Função do ISDIGIT)|Função do ISEXCLUSIVE)|  
|Função do ISLEADBYTE)|Função do ISLOWER)|Função do ISNULL)|  
|Função do ISREADONLY)|Função do ISUPPER)||  
  
## <a name="k"></a>K  
  
||||  
|-|-|-|  
|Função (chave)|Função () de CORRESPONDÊNCIAS||  
  
## <a name="l"></a>L  
  
||||  
|-|-|-|  
|Função (esquerda)|Função do LEFTC)|Função do LIKEC)|  
|Função do LENC)|COMO a função)|Função do bloqueio)|  
|Comando LOCAL|LOCALIZE o comando|Função do LOOKUP)|  
|Função do LOG)|Função do LOG10)|Função do LTRIM)|  
|Função LOWER de)|Comando LPARAMETERS||  
|Função do LUPDATE)|Função do LEN)||  
  
## <a name="m"></a>M  
  
||||  
|-|-|-|  
|Variável de memória do sistema _MLINE|Função MAX)|Função do MDX)|  
|Função do MDY)|Função do MEMLINES)|Função () de mensagem|  
|Função MIN)|Função (minutos)|Função do MLINE)|  
|Função (MOD)|Função do mês)|Função do MTON)|  
  
## <a name="n"></a>N  
  
||||  
|-|-|-|  
|Função do NDX)|NORMALIZAR a função)|Operador não|  
|Comando de Observação|Função do NTOM)|Função do NVL)|  
  
## <a name="o"></a>O  
  
||||  
|-|-|-|  
|OCORRE a função)|Função do OLDVAL)|NO comando de erro|  
|NO comando de teclas|EM função)|Comando Abrir banco de dados|  
|Operador OR|Função do pedido)|Função do sistema operacional)|  
  
## <a name="p"></a>P  
  
||||  
|-|-|-|  
|Comando PACK|Função () de parâmetros|Função () de pagamento|  
|PARÂMETROS de comando|Função (primário)|Comando PRIVADO|  
|Função do PI)|Função do programa)|Função adequado (de)|  
|Comando de procedimento|Função do PV)||  
|Comando público|(PADL) &#124; (PADR) &#124; funções do PADC)||  
  
## <a name="r"></a>R  
  
||||  
|-|-|-|  
|Função do RAND)|Função do rato)|Função do RATC)|  
|Função do RATLINE)|Lembre-se de comando|Função do RECCOUNT)|  
|Função do RECNO)|Função do RECSIZE)|Comando REGIONAL|  
|Função do parceiro)|Remover comando de tabela|Comando Substituir|  
|Substituir pelo comando de matriz|DUPLICAR função)|REPITA o comando|  
|RETORNAR o comando|Função (direita)|Função do RIGHTC)|  
|Função do RLOCK)|Comando de REVERSÃO|Função ROUND (.)|  
|Função do RTOD)|Função do RTRIM)||  
  
## <a name="s"></a>P  
  
||||  
|-|-|-|  
|VERIFICAÇÃO... Comando ENDSCAN|Comando de DISPERSÃO|Função do s)|  
|Função do segundos)|Comando de busca|BUSCA de função)|  
|Selecione o comando|Função SELECT (.)|Comando SELECT-SQL|  
|Comando SET BLOCKSIZE|Comando de realização de conjunto|Comando do século SET|  
|Comando SET COLLATE|Comando de banco de dados do conjunto|SET data Command|  
|Comando SET DEFAULT|Comando SET DELETED|Comando SET EXACT|  
|Comando SET EXCLUSIVE|Comando FDOW SET|Comando de CAMPOS de conjunto|  
|Comando de filtro de conjunto|Comando de conjunto de fixo|Comando de caminho completo do conjunto|  
|Comando FWEEK SET|DEFINIDAS horas de comando|Comando de conjunto de índice|  
|Comando de bloqueio de conjunto|Comando MULTILOCKS SET|Definir próximo ao comando|  
|Comando NOCPTRANS SET|Comando de notificação de conjunto|Comando SET NULL|  
|Comando de otimização do conjunto|Comando de ordem de conjunto|Comando SET PATH|  
|Comando do conjunto de PROCEDURE|Comando de relação de conjunto|Definir relação OFF comando|  
|Comando SET REPROCESS|DEFINIR o comando Ignorar|Comando UDFPARMS SET|  
|Comando SET UNIQUE|Comando do conjunto de VOLUME|Função do conjunto)|  
|Função do SETFLDSTATE)|Função do logon)|Função do SIN)|  
|Comando Ignorar|Comando SORT|Função do espaço)|  
|Função do SQRT)|Comando de armazenamento|Função do STR)|  
|Função do STRCONV)|Função do STRTRAN)|Função do STUFF)|  
|Função do STUFFC)|Função do SUBSTR)|Função do SUBSTRC)|  
|Comando de soma|Função sys(2011)||  
  
## <a name="t"></a>T  
  
||||  
|-|-|-|  
|Variável de memória do sistema _TALLY|Variável de memória do sistema _TRIGGERLEVEL|Função do TAGCOUNT)|  
|Função do TABLEUPDATE)|Função () de marca|Função () de destino|  
|Função do TAGNO)|Função TAN (.)|CORTAR função)|  
|Função do tempo)|Comando TOTAL|Função do TXNLEVEL)|  
|Função do TTOC)|Função do TTOD)||  
|TIPO de função)|Função do TABLEREVERT)||  
  
## <a name="u"></a>U  
  
||||  
|-|-|-|  
|Função (exclusivo)|Comando UNLOCK|USE o comando|  
|Comando de atualização|Função (superior)||  
|USADO a função)|UPDATE – comando SQL||  
  
## <a name="v"></a>V  
  
||||  
|-|-|-|  
|Função do VAL)|Função () de versão||  
  
## <a name="w"></a>W  
  
||||  
|-|-|-|  
|Função () de semana|||  
  
## <a name="y"></a>S  
  
||||  
|-|-|-|  
|Função do ano)|||  
  
## <a name="z"></a>Z  
  
||||  
|-|-|-|  
|Comando ZAP|||
