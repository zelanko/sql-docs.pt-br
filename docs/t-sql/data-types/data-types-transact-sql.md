---
title: Tipos de dados (Transact-SQL) | Microsoft Docs
description: Este artigo fornece um resumo dos diferentes tipos de dados disponíveis no SQL Server.
ms.date: 09/13/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- system data types [SQL Server]
- data types [SQL Server]
- data types [SQL Server], about data types
ms.assetid: a54f7373-b247-4d61-8fb8-7f2ec7a8d0a4
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 5039e7ea667c80b051413b93fbb34d2f4adc1038
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97484328"
---
# <a name="data-types-transact-sql"></a>Tipos de dados (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], cada coluna, variável local, expressão e parâmetro tem um tipo de dados relacionado. O tipo de dados é um atributo que especifica o tipo de dados que o objeto pode manter: dados inteiros, dados de caractere, dados monetários, data e hora, cadeiasx de caracteres binárias etc.
  
O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oferece um conjunto de tipos de dados do sistema que define todos os tipos de dados que podem ser usados com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Você também pode definir os próprios tipos de dados no [!INCLUDE[tsql](../../includes/tsql-md.md)] ou no [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]. Os tipos de dados de alias têm como base os tipos de dados fornecidos pelo sistema. Para obter mais informações sobre tipos de dados de alias, veja [CREATE TYPE &#40;Transact-SQL&#41;](../../t-sql/statements/create-type-transact-sql.md). Os tipos definidos pelo usuário obtêm características dos métodos e operadores de uma classe criada com o uso de uma das linguagens de programação oferecidas por [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)].
  
Quando duas expressões que possuem diferentes tipos de dados, ordenações, precisão, escala ou comprimento são combinadas por um operador, as características do resultado são determinadas pelo seguinte:
-   O tipo de dados do resultado é determinado pela aplicação das regras de precedência de tipos de dados em relação aos tipos de dados de expressões de entrada. Para obter mais informações, veja [Precedência de tipo de dados &#40;Transact-SQL&#41;](../../t-sql/data-types/data-type-precedence-transact-sql.md).  
-   A ordenação do resultado é determinada pelas regras de precedência de ordenação quando o tipo de dados do resultado é **char**, **varchar**, **text**, **nchar**, **nvarchar** ou **ntext**. Para obter mais informações, consulte [Precedência de ordenação &#40;Transact-SQL&#41;](../../t-sql/statements/collation-precedence-transact-sql.md).  
-   A precisão, a escala e o tamanho do resultado dependem da precisão, da escala e do tamanho das expressões de entrada. Para obter mais informações, consulte [Precisão, escala e comprimento &#40;Transact-SQL&#41;](../../t-sql/data-types/precision-scale-and-length-transact-sql.md).  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornece sinônimos de tipo de dados para compatibilidade com ISO. Para obter mais informações, consulte [Sinônimos de tipo de dados &#40;Transact-SQL&#41;](../../t-sql/data-types/data-type-synonyms-transact-sql.md).
  
## <a name="data-type-categories"></a>Categorias de tipo de dados
Os tipos de dados em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] são organizados nas seguintes categorias:
  
:::row:::
    :::column:::
        Numéricos exatos
    :::column-end:::
    :::column:::
        Cadeias de caracteres Unicode
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        Numéricos aproximados
    :::column-end:::
    :::column:::
        Cadeia de caracteres binária
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        Data e hora
    :::column-end:::
    :::column:::
        Outros tipos de dados
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        Cadeias de caracteres
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::
 
Em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], com base em suas características de armazenamento, alguns tipos de dados são designados como pertencendo aos seguintes grupos:
-   Tipos de dados de valor grande: **varchar(max)** e **nvarchar(max)**  
-   Tipos de dados de objeto grande: **text**, **ntext**, **image**, **varbinary(max)** e **xml**  
  
    > [!NOTE]  
    >  sp_help retorna -1 como o comprimento dos tipos de dados de valor grande e **xml**.  
  
### <a name="exact-numerics"></a>Numéricos exatos
  
:::row:::
    :::column:::
        [bigint](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md)
    :::column-end:::
    :::column:::
        [numeric](../../t-sql/data-types/decimal-and-numeric-transact-sql.md)
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        [bit](../../t-sql/data-types/bit-transact-sql.md)
    :::column-end:::
    :::column:::
        [smallint](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md)
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        [decimal](../../t-sql/data-types/decimal-and-numeric-transact-sql.md)
    :::column-end:::
    :::column:::
        [smallmoney](../../t-sql/data-types/money-and-smallmoney-transact-sql.md)
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        [int](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md)
    :::column-end:::
    :::column:::
        [tinyint](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md)
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        [money](../../t-sql/data-types/money-and-smallmoney-transact-sql.md)
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::

### <a name="approximate-numerics"></a>Numéricos aproximados
  
:::row:::
    :::column:::
        [float](../../t-sql/data-types/float-and-real-transact-sql.md)
    :::column-end:::
    :::column:::
        [real](../../t-sql/data-types/float-and-real-transact-sql.md)
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::

### <a name="date-and-time"></a>Data e hora
  
:::row:::
    :::column:::
        [date](../../t-sql/data-types/date-transact-sql.md)
    :::column-end:::
    :::column:::
        [datetimeoffset](../../t-sql/data-types/datetimeoffset-transact-sql.md)
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        [datetime2](../../t-sql/data-types/datetime2-transact-sql.md)
    :::column-end:::
    :::column:::
        [smalldatetime](../../t-sql/data-types/smalldatetime-transact-sql.md)
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        [datetime](../../t-sql/data-types/datetime-transact-sql.md)
    :::column-end:::
    :::column:::
        [time](../../t-sql/data-types/time-transact-sql.md)
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::
  
### <a name="character-strings"></a>Cadeias de caracteres
  
:::row:::
    :::column:::
        [char](../../t-sql/data-types/char-and-varchar-transact-sql.md)
    :::column-end:::
    :::column:::
        [varchar](../../t-sql/data-types/char-and-varchar-transact-sql.md)
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        [text](../../t-sql/data-types/ntext-text-and-image-transact-sql.md)
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::
 
### <a name="unicode-character-strings"></a>Cadeias de caracteres Unicode
  
:::row:::
    :::column:::
        [nchar](../../t-sql/data-types/nchar-and-nvarchar-transact-sql.md)
    :::column-end:::
    :::column:::
        [nvarchar](../../t-sql/data-types/nchar-and-nvarchar-transact-sql.md)
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        [ntext](../../t-sql/data-types/ntext-text-and-image-transact-sql.md)
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::
  

### <a name="binary-strings"></a>Cadeia de caracteres binária
  
:::row:::
    :::column:::
        [binary](../../t-sql/data-types/binary-and-varbinary-transact-sql.md)
    :::column-end:::
    :::column:::
        [varbinary](../../t-sql/data-types/binary-and-varbinary-transact-sql.md)
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        [imagem](../../t-sql/data-types/ntext-text-and-image-transact-sql.md)
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::

### <a name="other-data-types"></a>Outros tipos de dados

:::row:::
    :::column:::
        [cursor](../../t-sql/data-types/cursor-transact-sql.md)
    :::column-end:::
    :::column:::
        [rowversion](../../t-sql/data-types/rowversion-transact-sql.md)
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        [hierarchyid](../../t-sql/data-types/hierarchyid-data-type-method-reference.md)
    :::column-end:::
    :::column:::
        [uniqueidentifier](../../t-sql/data-types/uniqueidentifier-transact-sql.md)
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        [sql_variant](../../t-sql/data-types/sql-variant-transact-sql.md)
    :::column-end:::
    :::column:::
        [xml](../../t-sql/xml/xml-transact-sql.md)
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        [Tipos de geometria espacial](../../t-sql/spatial-geometry/spatial-types-geometry-transact-sql.md) 
    :::column-end:::
    :::column:::
        [Tipos de geografia espacial](../../t-sql/spatial-geography/spatial-types-geography.md)
    :::column-end:::
:::row-end:::  
:::row:::
    :::column:::
        [table](../../t-sql/data-types/table-transact-sql.md) 
    :::column-end:::
    :::column:::
         
    :::column-end:::
:::row-end:::

  
## <a name="see-also"></a>Confira também
[CREATE PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/statements/create-procedure-transact-sql.md)  
[CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)  
[DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)
[EXECUTE &#40;Transact-SQL&#41;](../../t-sql/language-elements/execute-transact-sql.md)  
[Expressões &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)  
[Funções &#40;Transact-SQL&#41;](../../t-sql/functions/functions.md)  
[LIKE &#40;Transact-SQL&#41;](../../t-sql/language-elements/like-transact-sql.md)  
[sp_droptype &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droptype-transact-sql.md)  
[sp_help &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-transact-sql.md)  
[sp_rename &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-rename-transact-sql.md)
  
  
