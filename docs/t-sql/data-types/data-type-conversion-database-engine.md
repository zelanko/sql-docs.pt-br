---
title: "Conversão (mecanismo de banco de dados) de tipo de dados | Microsoft Docs"
ms.custom: 
ms.date: 7/23/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- CAST function
- converting data types [SQL Server]
- CONVERT function
- data types [SQL Server], converting
- implicit data type conversions
- explicit data type conversions [SQL Server]
- converting data types [SQL Server], about converting data types
ms.assetid: ffacf45e-a488-48d0-9bb0-dcc7fd365299
caps.latest.revision: 37
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: c0ed7f8e0e681de9f962e3eb963c0af315a0c25c
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="data-type-conversion-database-engine"></a>Conversão de tipo de dados (mecanismo de banco de dados)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Os tipos de dados podem ser convertidos nos seguintes cenários:
-   Quando os dados de um objeto são movidos, comparados ou combinados com dados de outro objeto, eles podem ser convertidos de um tipo de dados de um objeto em um tipo de dados de outro objeto.  
-   Quando dados de um [!INCLUDE[tsql](../../includes/tsql-md.md)] coluna de resultado, o código de retorno ou parâmetro de saída é movido para uma variável de programa, os dados devem ser convertidos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo de dados do sistema para o tipo de dados da variável.  
  
Ao fazer a conversão entre uma variável de aplicativo e uma coluna de conjunto de resultados, um código de retorno, um parâmetro ou um marcador de parâmetro do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], as conversões de tipo de dados com suporte são definidas pela API do banco de dados.
  
## <a name="implicit-and-explicit-conversion"></a>Conversão implícita e explícita
Os tipos de dados podem ser convertidos implícita ou explicitamente.
  
As conversões implícitas não são visíveis ao usuário. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] converte automaticamente os dados de um tipo de dados em outro. Por exemplo, quando um **smallint** é comparado com um **int**, o **smallint** é convertido implicitamente em **int** antes da comparação continua.
  
**GetDate ()** converte implicitamente em estilo de data 0. **SYSDATETIME()** converte implicitamente em estilo de data 21.
  
As conversões explícitas usam as funções CAST ou CONVERT.
  
O [CAST e CONVERT](../../t-sql/functions/cast-and-convert-transact-sql.md) funções convertem um valor (uma variável local, uma coluna ou outra expressão) de um tipo de dados para outro. Por exemplo, a seguinte função `CAST` converte o valor numérico de `$157.27` em uma cadeia de caracteres de `'157.27'`:
  
```sql
CAST ( $157.27 AS VARCHAR(10) )  
```  
  
Use CAST em vez de CONVERT se quiser que o código do programa [!INCLUDE[tsql](../../includes/tsql-md.md)] esteja de acordo com ISO. Use CONVERT em vez de CAST para se beneficiar da funcionalidade de estilo de CONVERT.
  
A ilustração a seguir mostra todas as conversões de tipos de dados explícitas e implícitas que são permitidas para tipos de dados fornecidos pelo sistema [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Isso inclui **xml**, **bigint**, e **sql_variant**. Não há nenhuma conversão implícita na atribuição do **sql_variant** tipo de dados, mas não há conversão implícita em **sql_variant**.
  
![Tabela de conversão de tipo de dados](../../t-sql/data-types/media/lrdatahd.png "tabela de conversão de tipo de dados")
  
## <a name="data-type-conversion-behaviors"></a>Comportamentos de conversão de tipo de dados
Algumas conversões de tipo de dados implícitas e explícitas não têm suporte quando você está convertendo o tipo de dados de um objeto [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em outro. Por exemplo, um **nchar** valor não pode ser convertido em um **imagem** valor. Um **nchar** só pode ser convertido em **binário** usando conversão explícita, uma conversão implícita em **binário** não tem suporte. No entanto, um **nchar** pode ser explicitamente ou implicitamente convertido em **nvarchar**.
  
Os tópicos a seguir descrevem os comportamentos de conversão exibidos pelos tipos de dados correspondentes:
  
 - [binary e varbinary &#40;Transact-SQL&#41;](../../t-sql/data-types/binary-and-varbinary-transact-sql.md)  
 - [datetime2 &#40;Transact-SQL&#41;](../../t-sql/data-types/datetime2-transact-sql.md)  
 - [Money e smallmoney &#40; Transact-SQL &#41;](../../t-sql/data-types/money-and-smallmoney-transact-sql.md)  
 - [bit &#40; Transact-SQL &#41;](../../t-sql/data-types/bit-transact-sql.md)  
 - [datetimeoffset &#40;Transact-SQL&#41;](../../t-sql/data-types/datetimeoffset-transact-sql.md)  
 - [smalldatetime &#40; Transact-SQL &#41;](../../t-sql/data-types/smalldatetime-transact-sql.md)  
 - [char e varchar &#40;Transact-SQL&#41;](../../t-sql/data-types/char-and-varchar-transact-sql.md)  
 - [decimal e numeric &#40; Transact-SQL &#41;](../../t-sql/data-types/decimal-and-numeric-transact-sql.md)  
 - [sql_variant &#40;Transact-SQL&#41;](../../t-sql/data-types/sql-variant-transact-sql.md)  
 - [date &#40;Transact-SQL&#41;](../../t-sql/data-types/date-transact-sql.md)  
 - [float e real &#40; Transact-SQL &#41;](../../t-sql/data-types/float-and-real-transact-sql.md)  
 - [tempo &#40; Transact-SQL &#41;](../../t-sql/data-types/time-transact-sql.md)  
 - [Data e hora &#40; Transact-SQL &#41;](../../t-sql/data-types/datetime-transact-sql.md)  
 - [int, bigint, smallint, tinyint e #40; Transact-SQL &#41;](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md)  
 - [uniqueidentifier &#40; Transact-SQL &#41;](../../t-sql/data-types/uniqueidentifier-transact-sql.md)  
  
###  <a name="converting-data-types-by-using-ole-automation-stored-procedures"></a>Convertendo tipos de dados usando procedimentos armazenados de automação OLE  
Como o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa tipos de dados [!INCLUDE[tsql](../../includes/tsql-md.md)] e a Automação OLE usa tipos de dados [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)], os procedimentos armazenados de Automação OLE devem converter os dados que passam entre eles.
  
A tabela a seguir descreve as conversões de tipo de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)].
  
|Tipo de dados do SQL Server|Tipo de dados do Visual Basic|  
|--------------------------|----------------------------|  
|**char**, **varchar**, **texto**, **nvarchar**, **ntext**|**Cadeia de caracteres**|  
|**decimal**, **numérico**|**Cadeia de caracteres**|  
|**bit**|**Booliano**|  
|**binário**, **varbinary**, **imagem**|Unidimensional **byte ()** matriz|  
|**int**|**Longo**|  
|**smallint**|**Integer**|  
|**tinyint**|**Bytes**|  
|**float**|**Double**|  
|**real**|**Single**|  
|**money**, **smallmoney**|**Moeda**|  
|**DateTime**, **smalldatetime**|**Data**|  
|Tudo definido como NULL|**Variant** definido como Null|  
  
Únicos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] valores são convertidos em um único [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] valor com a exceção de **binário**, **varbinary**, e **imagem** valores. Esses valores são convertidos em um unidimensional **byte ()** de matriz em [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]. Essa matriz tem um intervalo de **bytes (**0 para *comprimento*1**)** onde *comprimento* é o número de bytes no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  **binário**, **varbinary**, ou **imagem** valores.
  
Estas são as conversões de tipos de dados [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] para tipos de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].
  
|Tipo de dados do Visual Basic|Tipo de dados do SQL Server|  
|----------------------------|--------------------------|  
|**Longo**, **inteiro**, **bytes**, **booliano**, **objeto**|**int**|  
|**Duplo**, **único**|**float**|  
|**Moeda**|**money**|  
|**Data**|**datetime**|  
|**Cadeia de caracteres** com 4000 caracteres ou menos|**varchar**/**nvarchar**|  
|**Cadeia de caracteres** com mais de 4000 caracteres|**texto**/**ntext**|  
|Unidimensional **byte ()** matriz com 8000 bytes ou menos|**varbinary**|  
|Unidimensional **byte ()** matriz com mais de 8000 bytes|**imagem**|  
  
## <a name="see-also"></a>Consulte também
[Procedimentos armazenados de Automação OLE &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/ole-automation-stored-procedures-transact-sql.md)  
[CAST e CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[Tipos de dados &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)  
[COLLATE &#40; Transact-SQL &#41;](http://msdn.microsoft.com/library/4ba6b7d8-114a-4f4e-bb38-fe5697add4e9)
  
  

