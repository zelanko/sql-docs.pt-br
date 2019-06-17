---
title: TERTIARY_WEIGHTS (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- TERTIARY_WEIGHTS_TSQL
- TERTIARY_WEIGHTS
dev_langs:
- TSQL
helpviewer_keywords:
- weights [SQL Server]
- SQL tertiary collations
- TERTIARY_WEIGHTS function
ms.assetid: 7e1f5350-260b-4c61-8c84-69bb1a214f1f
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: b9c1ce066768207f7a04d16e2f4c18666eb231d7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65944001"
---
# <a name="collation-functions---tertiaryweights-transact-sql"></a>Funções de ordenação – TERTIARY_WEIGHTS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Para cada caractere em uma expressão de cadeia de caracteres não Unicode definida com uma ordenação SQL terciária, essa função retorna uma cadeia de caracteres binária de pesos.
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```sql
TERTIARY_WEIGHTS( non_Unicode_character_string_expression )  
```  
  
## <a name="arguments"></a>Argumentos  
*non_Unicode_character_string_expression*  
Uma [expressão](../../t-sql/language-elements/expressions-transact-sql.md) de cadeia de caracteres do tipo **char**, **varchar** ou **varchar(max)** definida em uma ordenação SQL terciária. Para obter uma lista dessas ordenações, consulte Comentários.
  
## <a name="return-types"></a>Tipos de retorno
`TERTIARY_WEIGHTS` retorna **varbinary** quando *non_Unicode_character_string_expression* é **char** ou **varchar** e retorna **varbinary(max)** quando *non_Unicode_character_string_expression* tem um tipo de dados **varchar(max)** .
  
## <a name="remarks"></a>Remarks  
`TERTIARY_WEIGHTS` retorna NULL quando uma coleção SQL terciária não define a *non_Unicode_character_string_expression*. Esta tabela mostra as ordenações SQL terciárias:
  
|ID da ordem de classificação|Ordenação SQL|  
|---|---|
|33|SQL_Latin1_General_Pref_CP437_CI_AS|  
|34|SQL_Latin1_General_CP437_CI_AI|  
|43|SQL_Latin1_General_Pref_CP850_CI_AS|  
|44|SQL_Latin1_General_CP850_CI_AI|  
|49|SQL_1xCompat_CP850_CI_AS|  
|53|SQL_Latin1_General_Pref_CP1_CI_AS|  
|54|SQL_Latin1_General_CP1_CI_AI|  
|56|SQL_AltDiction_Pref_CP850_CI_AS|  
|57|SQL_AltDiction_CP850_CI_AI|  
|58|SQL_Scandinavian_Pref_CP850_CI_AS|  
|82|SQL_Latin1_General_CP1250_CI_AS|  
|84|SQL_Czech_CP1250_CI_AS|  
|86|SQL_Hungarian_CP1250_CI_AS|  
|88|SQL_Polish_CP1250_CI_AS|  
|90|SQL_Romanian_CP1250_CI_AS|  
|92|SQL_Croatian_CP1250_CI_AS|  
|94|SQL_Slovak_CP1250_CI_AS|  
|96|SQL_Slovenian_CP1250_CI_AS|  
|106|SQL_Latin1_General_CP1251_CI_AS|  
|108|SQL_Ukrainian_CP1251_CI_AS|  
|113|SQL_Latin1_General_CP1253_CS_AS|  
|114|SQL_Latin1_General_CP1253_CI_AS|  
|130|SQL_Latin1_General_CP1254_CI_AS|  
|146|SQL_Latin1_General_CP1256_CI_AS|  
|154|SQL_Latin1_General_CP1257_CI_AS|  
|156|SQL_Estonian_CP1257_CI_AS|  
|158|SQL_Latvian_CP1257_CI_AS|  
|160|SQL_Lithuanian_CP1257_CI_AS|  
|183|SQL_Danish_Pref_CP1_CI_AS|  
|184|SQL_SwedishPhone_Pref_CP1_CI_AS|  
|185|SQL_SwedishStd_Pref_CP1_CI_AS|  
|186|SQL_Icelandic_Pref_CP1_CI_AS|  
  
Use `TERTIARY_WEIGHTS` para a definição de uma coluna computada que é definida com base nos valores de uma coluna **char**, **varchar** ou **varchar(max)** . A definição de índice na coluna computada e na coluna **char**, **varchar** ou **varchar(max)** pode melhorar o desempenho quando a cláusula ORDER BY de uma consulta especifica essa coluna **char**, **varchar** ou **varchar(max)** .
  
## <a name="examples"></a>Exemplos  
O exemplo a seguir cria uma coluna computada em uma tabela, que aplica a função `TERTIARY_WEIGHTS` aos valores de uma coluna `char`:
  
```sql
CREATE TABLE TertColTable  
(Col1 char(15) COLLATE SQL_Latin1_General_Pref_CP437_CI_AS,  
Col2 AS TERTIARY_WEIGHTS(Col1));  
GO   
```  
  
## <a name="see-also"></a>Confira também
[ORDER BY Clause &#40;Transact-SQL&#41;](../../t-sql/queries/select-order-by-clause-transact-sql.md)
  
  
