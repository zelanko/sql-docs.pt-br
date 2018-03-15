---
title: "Conversão de tipo de dados (Mecanismo de Banco de Dados) | Microsoft Docs"
ms.custom: 
ms.date: 7/23/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|data-types
ms.reviewer: 
ms.suite: sql
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
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 811eacd3dc0cbbd622fc6eac6ad91a6e740554f4
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="data-type-conversion-database-engine"></a>Conversão de tipo de dados (Mecanismo de Banco de Dados)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Os tipos de dados podem ser convertidos nos seguintes cenários:
-   Quando os dados de um objeto são movidos, comparados ou combinados com dados de outro objeto, eles podem ser convertidos de um tipo de dados de um objeto em um tipo de dados de outro objeto.  
-   Quando os dados de uma coluna de resultado, um código de retorno ou um parâmetro de saída [!INCLUDE[tsql](../../includes/tsql-md.md)] são movidos para uma variável de programa, os dados devem ser convertidos de tipo de dados do sistema [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em tipo de dados da variável.  
  
Ao fazer a conversão entre uma variável de aplicativo e uma coluna de conjunto de resultados, um código de retorno, um parâmetro ou um marcador de parâmetro do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], as conversões de tipo de dados com suporte são definidas pela API do banco de dados.
  
## <a name="implicit-and-explicit-conversion"></a>Conversões implícita e explícita
Os tipos de dados podem ser convertidos implícita ou explicitamente.
  
As conversões implícitas não são visíveis ao usuário. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] converte automaticamente os dados de um tipo de dados em outro. Por exemplo, quando **smallint** é comparado com **int**, **smallint** é convertido implicitamente em **int** antes que a comparação continue.
  
**GETDATE()** é implicitamente convertido no estilo de data 0. **SYSDATETIME()** é implicitamente convertido em estilo de data 21.
  
As conversões explícitas usam as funções CAST ou CONVERT.
  
As funções [CAST e CONVERT](../../t-sql/functions/cast-and-convert-transact-sql.md) convertem um valor (uma variável local, uma coluna ou outra expressão) de um tipo de dados em outro. Por exemplo, a seguinte função `CAST` converte o valor numérico de `$157.27` em uma cadeia de caracteres de `'157.27'`:
  
```sql
CAST ( $157.27 AS VARCHAR(10) )  
```  
  
Use CAST em vez de CONVERT se quiser que o código do programa [!INCLUDE[tsql](../../includes/tsql-md.md)] esteja de acordo com ISO. Use CONVERT em vez de CAST para se beneficiar da funcionalidade de estilo de CONVERT.
  
A ilustração a seguir mostra todas as conversões de tipos de dados explícitas e implícitas que são permitidas para tipos de dados fornecidos pelo sistema [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Isso inclui **xml**, **bigint** e **sql_variant**. Não há nenhuma conversão implícita na atribuição do tipo de dados **sql_variant**, mas há uma conversão implícita em **sql_variant**.
  
![Tabela de conversão de tipo de dados](../../t-sql/data-types/media/lrdatahd.png "Data type conversion table")
  
## <a name="data-type-conversion-behaviors"></a>Comportamentos de conversão de tipo de dados
Algumas conversões de tipo de dados implícitas e explícitas não têm suporte quando você está convertendo o tipo de dados de um objeto [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em outro. Por exemplo, um valor **nchar** não pode ser convertido em um valor **image**. Um valor **nchar** só pode ser convertido em **binary** usando uma conversão explícita; uma conversão implícita em **binary** não tem suporte. No entanto, um **nchar** pode ser explícita ou implicitamente convertido em **nvarchar**.
  
Os tópicos a seguir descrevem os comportamentos de conversão exibidos pelos tipos de dados correspondentes:
  
 - [binary e varbinary &#40;Transact-SQL&#41;](../../t-sql/data-types/binary-and-varbinary-transact-sql.md)  
 - [datetime2 &#40;Transact-SQL&#41;](../../t-sql/data-types/datetime2-transact-sql.md)  
 - [money e smallmoney &#40;Transact-SQL&#41;](../../t-sql/data-types/money-and-smallmoney-transact-sql.md)  
 - [bit &#40;Transact-SQL&#41;](../../t-sql/data-types/bit-transact-sql.md)  
 - [datetimeoffset &#40;Transact-SQL&#41;](../../t-sql/data-types/datetimeoffset-transact-sql.md)  
 - [smalldatetime &#40;Transact-SQL&#41;](../../t-sql/data-types/smalldatetime-transact-sql.md)  
 - [char e varchar &#40;Transact-SQL&#41;](../../t-sql/data-types/char-and-varchar-transact-sql.md)  
 - [decimal e numeric &#40;Transact-SQL&#41;](../../t-sql/data-types/decimal-and-numeric-transact-sql.md)  
 - [sql_variant &#40;Transact-SQL&#41;](../../t-sql/data-types/sql-variant-transact-sql.md)  
 - [date &#40;Transact-SQL&#41;](../../t-sql/data-types/date-transact-sql.md)  
 - [float e real &#40;Transact-SQL&#41;](../../t-sql/data-types/float-and-real-transact-sql.md)  
 - [time &#40;Transact-SQL&#41;](../../t-sql/data-types/time-transact-sql.md)  
 - [datetime &#40;Transact-SQL&#41;](../../t-sql/data-types/datetime-transact-sql.md)  
 - [int, bigint, smallint e tinyint &#40;Transact-SQL&#41;](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md)  
 - [uniqueidentifier &#40;Transact-SQL&#41;](../../t-sql/data-types/uniqueidentifier-transact-sql.md)  
  
###  <a name="converting-data-types-by-using-ole-automation-stored-procedures"></a>Convertendo tipos de dados usando procedimentos armazenados de automação OLE  
Como o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa tipos de dados [!INCLUDE[tsql](../../includes/tsql-md.md)] e a Automação OLE usa tipos de dados [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)], os procedimentos armazenados de Automação OLE devem converter os dados que passam entre eles.
  
A tabela a seguir descreve as conversões de tipo de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)].
  
|Tipo de dados do SQL Server|Tipo de dados do Visual Basic|  
|--------------------------|----------------------------|  
|**char**, **varchar**, **text**, **nvarchar**, **ntext**|**String**|  
|**decimal**, **numeric**|**String**|  
|**bit**|**Booliano**|  
|**binary**, **varbinary**, **image**|Matriz **Byte()** unidimensional|  
|**int**|**Longo**|  
|**smallint**|**Integer**|  
|**tinyint**|**Byte**|  
|**float**|**Double**|  
|**real**|**Single**|  
|**money**, **smallmoney**|**Moeda**|  
|**datetime**, **smalldatetime**|**Date**|  
|Tudo definido como NULL|**Variant** definida como Null|  
  
Todos os valores [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] únicos são convertidos em um valor [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] único, com a exceção dos valores **binary**, **varbinary** e **image**. Esses valores são convertidos em uma matriz **Byte()** unidimensional em [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]. Essa matriz tem um intervalo de **Byte(**0 to *length*1**)** em que *length* é o número de bytes nos valores [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **binary**, **varbinary** ou **image**.
  
Estas são as conversões de tipos de dados [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] para tipos de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].
  
|Tipo de dados do Visual Basic|Tipo de dados do SQL Server|  
|----------------------------|--------------------------|  
|**Long**, **Integer**, **Byte**, **Boolean**, **Object**|**int**|  
|**Double**, **Single**|**float**|  
|**Moeda**|**money**|  
|**Date**|**datetime**|  
|**String** com 4.000 caracteres ou menos|**varchar**/**nvarchar**|  
|**String** com mais de 4.000 caracteres|**text**/**ntext**|  
|Matriz **Byte()** unidimensional com 8.000 bytes ou menos|**varbinary**|  
|Matriz **Byte()** unidimensional com mais de 8.000 bytes|**imagem**|  
  
## <a name="see-also"></a>Consulte também
[Procedimentos armazenados de Automação OLE &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/ole-automation-stored-procedures-transact-sql.md)  
[CAST e CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[Tipos de dados &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)  
[COLLATE &#40;Transact-SQL&#41;](http://msdn.microsoft.com/library/4ba6b7d8-114a-4f4e-bb38-fe5697add4e9)
  
  
