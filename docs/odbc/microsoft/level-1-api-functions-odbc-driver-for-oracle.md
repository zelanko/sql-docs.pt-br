---
title: Funções de API nível 1 (Driver ODBC para Oracle) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- functions [ODBC], ODBC driver for Oracle
- ODBC level 1 API functions [ODBC]
- ODBC driver for Oracle [ODBC], functions
- level 1 API functions [ODBC]
- API functions [ODBC]
ms.assetid: 98cced6f-41b8-43c1-a3cd-f4ea1615c0af
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 37305ee75ebeb0686bafe039f1102cb3c6e18674
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299946"
---
# <a name="level-1-api-functions-odbc-driver-for-oracle"></a>Funções de API de nível 1 (Driver ODBC para Oracle)
> [!IMPORTANT]  
>  Esse recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Em vez disso, use o driver ODBC fornecido pela Oracle.  
  
 Funções neste nível fornecem conformidade de interface Core mais funcionalidades adicionais, como suporte a transações.  
  
|Função API|Observações|  
|------------------|-----------|  
|**SQLColumns**|Cria um conjunto de resultados para uma tabela, que é a lista de colunas para a tabela ou tabelas especificadas. Ao solicitar colunas para um sinônimo DE PUBLIC, você deve ter definido o atributo de conexão SYNONYMCOLUMNS e especificado uma seqüência de string vazia como o argumento *szTableOwner.* Ao retornar colunas para sinônimos DE PUBLIC, o driver define a coluna NOME DA TABELA como uma seqüência de string vazia. O conjunto de resultados contém uma coluna adicional, ORDINAL POSITION, no final de cada linha. Este valor é a posição ordinal da coluna na tabela.|  
|**SQLDriverConnect**|Conecta-se a uma fonte de dados existente. Para obter detalhes, consulte [Formato e atributos de cadeia de conexão](../../odbc/microsoft/connection-string-format-and-attributes.md).|  
|**Opção SQLGetConnect**|Retorna a configuração atual de uma opção de conexão. Esta função é parcialmente suportada. O driver suporta todos os valores para o argumento *fOption,* mas não suporta alguns valores *vParam* para o argumento *fOption* [SQL_TXN_ISOLATION](../../odbc/microsoft/connect-options.md). Para obter mais informações, consulte [Opções de conexão](../../odbc/microsoft/connect-options.md).|  
|**SQLGetData**|Recupera o valor de um único campo no registro atual do conjunto de resultados dado.|  
|**SQLGetFunctions**|Retorna TRUE para todas as funções suportadas. Implementado pelo Driver Manager.|  
|**SQLGetInfo**|Retorna informações, incluindo SQLHDBC, SQLUSMALLINT, SQLPOINTER, SQLSMALLINT e \*SQLSMALLINT, sobre o Driver ODBC para Oracle e fonte de dados associada a uma alça de conexão, *hdbc*.|  
|**Opção SQLGetStmt**|Retorna a configuração atual de uma opção de declaração. Para obter mais informações, consulte [Opções de declaração](../../odbc/microsoft/statement-options.md).|  
|**SQLGetTypeInfo**|Retorna informações sobre os tipos de dados suportados por uma fonte de dados. O driver retorna as informações em um conjunto de resultados SQL.|  
|**SQLParamData**|Usado em conjunto com **o SQLPutData** para especificar dados de parâmetros no tempo de execução da declaração.|  
|**SQLPutData**|Permite que um aplicativo envie dados para um parâmetro ou coluna para o motorista na hora da execução da declaração.|  
|**Sqlsetconnectoption**|Fornece acesso a opções que regem aspectos da conexão. Esta função é parcialmente suportada: O driver suporta todos os valores para o argumento *fOption,* mas não suporta alguns valores *vParam* para o argumento *fOption* [SQL_TXN_ISOLATION](../../odbc/microsoft/connect-options.md). Para obter mais informações, consulte [Opções de conexão](../../odbc/microsoft/connect-options.md).|  
|**SQLSetStmtOpção**|Define opções relacionadas a uma alça de *declaração, hstmt*. Para obter mais informações, consulte [Opções de declaração](../../odbc/microsoft/statement-options.md).|  
|**SQLSpecialColumns**|Recupera o conjunto ideal de colunas que identifica exclusivamente uma linha na tabela.|  
|**SQLStatistics**|Recupera uma lista de estatísticas sobre uma única tabela e os índices, ou nomes de etiquetas, associados à tabela. O motorista retorna as informações como um conjunto de resultados.|  
|**SQLTables**|Retorna a lista de nomes de tabela especificados pelo parâmetro na declaração **SQLTables.** Se nenhum parâmetro for especificado, retorna os nomes de tabela armazenados na fonte de dados atual. O motorista retorna as informações como um conjunto de resultados.<br /><br /> As chamadas do tipo de enumeração não receberão uma entrada definida de resultado para visualizações remotas ou visualizações parametrizadas locais. No entanto, uma chamada para **SQLTables** com um especificador de nome de tabela exclusivo encontrará uma correspondência para tal exibição, se presente, com esse nome; isso permite que a API verifique conflitos de nome antes da criação de uma nova tabela.<br /><br /> Os sinônimos públicos são devolvidos com um valor TABLE_OWNER de "".<br /><br /> As visualizações de propriedade do SYS ou SYSTEM são identificadas como VISÃO DO SISTEMA.|
