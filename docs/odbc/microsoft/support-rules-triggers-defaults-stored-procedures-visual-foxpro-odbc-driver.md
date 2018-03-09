---
title: "Suporte para procedimentos armazenados, disparadores, valores padrão e regras | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
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
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c2fcdf0a9a7af2f34a2a0d87495d00ddf3373d3a
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/15/2018
---
# <a name="support-for-rules-triggers-default-values-and-stored-procedures-visual-foxpro-odbc-driver"></a>Suporte para regras e procedimentos armazenados (do Visual FoxPro ODBC Driver), valores padrão e gatilhos
Você não pode criar regras do Visual FoxPro, gatilhos, valores padrão ou procedimentos armazenados usando o Driver de ODBC do Visual FoxPro. No entanto, seu aplicativo pode interagir com as regras existentes, gatilhos, valores padrão ou procedimentos armazenados que insere, atualiza ou exclui do Visual FoxPro dados armazenados em um banco de dados.  
  
 A tabela a seguir lista os comandos do Visual FoxPro e funções com suporte do Driver ODBC para Visual FoxPro quando as funções ou os comandos existirem em procedimentos armazenados, disparadores, valores padrão ou regras.  
  
 Se seu aplicativo interage com os dados cuja regras, valores padrão, gatilhos ou procedimentos armazenados chamam outros comandos do Visual FoxPro ou funções, o driver gerará um erro. Consulte [funções e não há suporte para comandos do Visual FoxPro](../../odbc/microsoft/unsupported-visual-foxpro-commands-and-functions-visual-foxpro-odbc-driver.md) para obter uma lista de comandos e funções não têm suportadas pelo driver.  
  
> [!TIP]  
>  Se você quiser inserir código condicional em suas regras, gatilhos ou procedimentos armazenados que determina os comandos a serem executados quando chamados pelo driver, você pode usar o **(versão)** função. O **(versão)** função retorna "Driver de ODBC do Visual FoxPro  *\<versão >*" quando chamado pelo driver.  
  
## <a name="visual-foxpro-commands-and-functions-supported-in-rules-triggers-default-values-and-stored-procedures"></a>Comandos do Visual FoxPro e funções com suporte em procedimentos armazenados, disparadores, valores padrão e regras  
  
||||  
|-|-|-|  
|Operador de $|Operador %|& Comando|  
|& & Comando|* O comando|= O comando|  
  
## <a name="a"></a>A  
  
||||  
|-|-|-|  
|Função do ABS)|Função do ACOPY)|Adicione comandos de tabela|  
|Função do ADATABASES)|Função do ADBOBJECTS)|Função do AERROR)|  
|Função do ADEL)|Função do elemento)|Função do ALEN)|  
|Função do AFIELDS)|Função do AINS)|ALTER TABLE - comando SQL|  
|Função do ALIAS)|Função do ALLTRIM)|ACRESCENTAR do comando de matriz|  
|Operador AND|Comando APPEND|Memorando comando APPEND|  
|Adicionar de comando|ACRESCENTE o comando geral|Função do ASCAN)|  
|ACRESCENTE o comando de procedimentos|Função do ASC)|Função do ASUBSCRIPT)|  
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
|CALCULAR o comando|Função do CANDIDATO)|Função do CHR)|  
|Função do CDX)|Função do CEILING)|Comandos CLOSE|  
|Função do CHRTRAN)|Função do CHRTRANC)|Copie o comando de ÍNDICES|  
|Função do CMONTH)|Comando CONTINUE|COPIAR a estrutura estendida comando|  
|Comando de procedimentos de cópia|Copie o comando de estrutura|Copiar para o comando|  
|Copie o comando marca|Copiar para o comando de matriz|Função do CPCONVERT)|  
|COS () de função|Contagem de comando|Função do CTOD)|  
|Função do CPCURRENT)|Função do CPDBF)|Função do CURSORSETPROP)|  
|Função do CTOT)|Função do CURSORGETPROP)||  
|Função (CURVAL)|Função do CDOW)||  
  
## <a name="d"></a>D  
  
||||  
|-|-|-|  
|Função de data)|Função do DATETIME)|Função do dia)|  
|Função do DBC)|Função do DBF)|Função do DBGETPROP)|  
|Função do DBUSED)|Exclua - o comando SQL|Comando DELETE|  
|EXCLUIR o comando marca|Função (excluído)|Em ordem DECRESCENTE de função)|  
|Função () de diferença|Comando de dimensão|Função () de espaço em disco|  
|Função do DMA)|DO CASO... Comando ENDCASE|Comando|  
|WHILE... Comando ENDDO|Função () de janela|Função do DTOC)|  
|Função do DTOR)|Função do DTOS)|Função do DTOT)|  
  
## <a name="e"></a>E  
  
||||  
|-|-|-|  
|Função (vazio)|AVALIAR a função)|Comando EXIT|  
|Função () de erro|Função do EXP)||  
|Comando de transação do fim|Função do EOF)||  
  
## <a name="f"></a>F  
  
||||  
|-|-|-|  
|Função do FCOUNT)|Função do FDATE)|Função do campo)|  
|Função do arquivo)|Função do filtro)|Função do FLDLIST)|  
|Função do FLOCK)|Função do FLOOR)|Comando FLUSH|  
|FOR... Comando ENDFOR|PARA a função)|ENCONTRAR a função)|  
|Comando tabela livre|Função do FSIZE)|Função do FTIME)|  
|Função do caminho completo)|Comando de função|Função do VF)|  
  
## <a name="g"></a>G  
  
||||  
|-|-|-|  
|OBTER comando|GETNEXTMODIFIED( ) Function|Comando GO/GOTO|  
|Função do GETFLDSTATE)|Função do GOMONTH)||  
|Função do GETCP)|Função do GETENV)||  
  
## <a name="h"></a>H  
  
|||  
|-|-|  
|Função do cabeçalho)|Função () de hora|  
  
## <a name="i"></a>I  
  
||||  
|-|-|-|  
|Função do IDXCOLLATE)|IF... Comando ENDIF|Instrução IIf)|  
|Função do INDBC)|Comando de índice|Função () de lista de entrada|  
|Comando INSERT SQL|Função do INT)|Função do ISALPHA)|  
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
|Função (esquerdo)|Função do LEFTC)|Função do LIKEC)|  
|Função do LENC)|COMO a função)|Função () de bloqueio|  
|Comando LOCAL|LOCALIZE o comando|Função () de pesquisa|  
|Função do LOG)|Função do LOG10)|Função do LTRIM)|  
|Função LOWER de)|Comando LPARAMETERS||  
|Função do LUPDATE)|Função do LEN)||  
  
## <a name="m"></a>M  
  
||||  
|-|-|-|  
|Variável de memória de sistema _MLINE|Função do MAX)|Função do MDX)|  
|Função do mda)|Função do MEMLINES)|Função () de mensagem|  
|Função do MIN)|Função (minutos)|Função do MLINE)|  
|Função MOD (.)|Função do mês)|Função do MTON)|  
  
## <a name="n"></a>N  
  
||||  
|-|-|-|  
|Função do NDX)|NORMALIZAR função)|Operador NOT|  
|Comando de Observação|Função do NTOM)|Função do NVL)|  
  
## <a name="o"></a>O   
  
||||  
|-|-|-|  
|OCORRE a função)|Função do OLDVAL)|Erro de comando|  
|NO comando de teclas|EM função)|Comando Abrir banco de dados|  
|Operador OR|Função do pedido)|Função do sistema operacional)|  
  
## <a name="p"></a>P  
  
||||  
|-|-|-|  
|Comando de pacote|Função () de parâmetros|Função () de pagamento|  
|PARÂMETROS de comando|Função (primário)|Comando PRIVADA|  
|Função do PI)|Função do programa)|Função adequado (de)|  
|Comando de procedimento|Função do VP)||  
|Comando público|PADL( ) &#124; PADR( ) &#124; PADC( ) Functions||  
  
## <a name="r"></a>R  
  
||||  
|-|-|-|  
|Função do RAND)|Função do rato)|Função do RATC)|  
|Função do RATLINE)|Lembre-se de comando|Função do RECCOUNT)|  
|Função do RECNO)|Função do RECSIZE)|Comando REGIONAL|  
|Função do parceiro)|Remova o comando de tabela|Comando Substituir|  
|Substituir do comando de matriz|REPLICAR função)|REPITA o comando|  
|RETORNAR o comando|Função (direita)|Função do RIGHTC)|  
|Função do RLOCK)|Comando de REVERSÃO|Função ROUND (.)|  
|Função do RTOD)|Função do RTRIM)||  
  
## <a name="s"></a>P  
  
||||  
|-|-|-|  
|VERIFICAÇÃO... Comando ENDSCAN|Comando de DISPERSÃO|Função do s)|  
|Função do segundos)|BUSCA de comando|BUSCA de função)|  
|Selecione o comando|Função (SELECT)|Comando SELECT-SQL|  
|Comando do conjunto de tamanho de bloco|Comando de uso do conjunto|Comando de século de conjunto|  
|Comando do conjunto COLLATE|Comando de banco de dados do conjunto|Comando de data do conjunto|  
|Comando SET DEFAULT|Comando do conjunto excluído|Comando exato do conjunto|  
|Comando exclusivo do conjunto|CONJUNTO FDOW comando|Comando de CAMPOS de conjunto|  
|Comando de filtro de conjunto|Comando FIXA do conjunto|Comando de caminho completo do conjunto|  
|CONJUNTO FWEEK comando|DEFINIDAS horas de comando|Comando de conjunto de índice|  
|Comando de bloqueio do conjunto|Comando MULTILOCKS SET|Defina o próximo comando|  
|SET NOCPTRANS Command|CONJUNTO de comando de notificação|Comando de conjunto nulo|  
|Comando de otimização do conjunto|Comando de ordem do conjunto|Comando DEMARCADOR do conjunto|  
|Comando do conjunto de PROCEDURE|Comando de relação de conjunto|Definir relação OFF comando|  
|Comando de REPROCESSAMENTO do conjunto|Defina o comando Ignorar|CONJUNTO UDFPARMS comando|  
|Comando exclusivo do conjunto|Comando do conjunto de VOLUME|Função do conjunto)|  
|Função do SETFLDSTATE)|Função do logon)|Função do SIN)|  
|Comando Ignorar|Comando de classificação|Função do espaço)|  
|Função do SQRT)|Comando de armazenamento|Função do STR)|  
|Função do STRCONV)|Função do STRTRAN)|Função do STUFF)|  
|Função do STUFFC)|Função do SUBSTR)|Função do SUBSTRC)|  
|Comando de soma|Função sys(2011)||  
  
## <a name="t"></a>T  
  
||||  
|-|-|-|  
|Variável de memória de sistema _TALLY|Variável de memória de sistema _TRIGGERLEVEL|Função do TAGCOUNT)|  
|Função do TABLEUPDATE)|Função () de marca|Função () de destino|  
|Função do TAGNO)|Função TAN (.)|() Função TRIM|  
|Função do tempo)|Comando TOTAL|TXNLEVEL( ) Function|  
|Função do TTOC)|Função do TTOD)||  
|TIPO de função)|Função do TABLEREVERT)||  
  
## <a name="u"></a>U  
  
||||  
|-|-|-|  
|Função (exclusivo)|Comando UNLOCK|USE o comando|  
|Comando de atualização|Função (superior)||  
|USADO função)|SQL de atualização - comando||  
  
## <a name="v"></a>V  
  
||||  
|-|-|-|  
|Função do VAL)|Função () de versão||  
  
## <a name="w"></a>L  
  
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
