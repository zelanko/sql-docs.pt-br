---
title: sql_variant (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/23/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sql_variant
- sql_variant_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sql_variant comparisons
- storing data [SQL Server], sql_variant
- sql_variant data type
- storage [SQL Server], sql_variant
ms.assetid: 01229779-8bc1-4c7d-890a-8246d4899250
caps.latest.revision: 43
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 4eb946d5b6ed5a9c6d33789166327bd2dd25d7c1
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="sqlvariant-transact-sql"></a>sql_variant (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

Um tipo de dados que armazena valores de vários tipos de dados com suporte do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].
  
**Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] por meio de [versão atual](http://go.microsoft.com/fwlink/p/?LinkId=299658)),[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```sql
sql_variant  
```  
  
## <a name="remarks"></a>Comentários  
**sql_variant** pode ser usado em colunas, parâmetros, variáveis e os valores de retorno de funções definidas pelo usuário. **sql_variant** permite que esses objetos de banco de dados dar suporte a valores de outros tipos de dados.
  
Uma coluna do tipo **sql_variant** pode conter linhas de diferentes tipos de dados. Por exemplo, uma coluna definida como **sql_variant** pode armazenar **int**, **binário**, e **char** valores.
  
**sql_variant** pode ter um comprimento máximo de 8016 bytes. Isso inclui as informações de tipo base e o valor de tipo base. O tamanho máximo do valor de tipo base atual é 8.000 bytes.
  
Um **sql_variant** tipo de dados deve primeiro ser convertido para o valor de tipo de dados base antes de participar de operações como adição e subtração.
  
**sql_variant** pode ser atribuído um valor padrão. Esse tipo de dados pode também ter NULL como valor subjacente, mas os valores NULL não terão um tipo base associado. Além disso, **sql_variant** não pode ter outro **sql_variant** como seu tipo base.
  
Uma chave exclusiva, primária ou estrangeira pode incluir colunas do tipo **sql_variant**, mas o comprimento total dos valores de dados que constituem a chave de uma linha específica não deve ser maior que o comprimento máximo de um índice. Esse é de 900 bytes.
  
Uma tabela pode ter qualquer número de **sql_variant** colunas.
  
**sql_variant** não pode ser usado em CONTAINSTABLE e FREETEXTTABLE.
  
ODBC não suporta completamente **sql_variant**. Portanto, as consultas de **sql_variant** colunas são retornadas como dados binários quando você usa o Microsoft OLE DB Provider para ODBC (MSDASQL). Por exemplo, um **sql_variant** coluna que contém os dados de cadeia de caracteres 'ps2091 ' retorna é retornada como 0x505332303931.
  
## <a name="comparing-sqlvariant-values"></a>Comparando valores sql_variant  
O **sql_variant** tipo de dados pertence à parte superior da lista de hierarquia de tipo de dados para conversão. Para **sql_variant** comparações, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ordem de hierarquia de tipo de dados é agrupado nas famílias de tipos de dados.
  
|Hierarquia de tipos de dados|Família de tipos de dados|  
|---|---|
|**sql_variant**|**sql_variant**|  
|**datetime2**|Data e hora|  
|**datetimeoffset**|Data e hora|  
|**datetime**|Data e hora|  
|**smalldatetime**|Data e hora|  
|**date**|Data e hora|  
|**time**|Data e hora|  
|**float**|Numérico aproximado|  
|**real**|Numérico aproximado|  
|**decimal**|Numérico exato|  
|**money**|Numérico exato|  
|**smallmoney**|Numérico exato|  
|**bigint**|Numérico exato|  
|**int**|Numérico exato|  
|**smallint**|Numérico exato|  
|**tinyint**|Numérico exato|  
|**bit**|Numérico exato|  
|**nvarchar**|Unicode|  
|**nchar**|Unicode|  
|**varchar**|Unicode|  
|**char**|Unicode|  
|**varbinary**|Binary|  
|**binary**|Binary|  
|**uniqueidentifier**|**Uniqueidentifier**|  
  
As seguintes regras se aplicam a **sql_variant** comparações:
-   Quando **sql_variant** valores de tipos diferentes de dados base são comparados e os tipos de dados base estão em dados diferentes famílias de tipos, o valor cuja família de tipo de dados é mais alta no gráfico da hierarquia é considerado o mais de dois valores.  
-   Quando **sql_variant** valores de tipos diferentes de dados base são comparados e os tipos de dados base estão na mesma família de tipo de dados, o valor cujo tipo de dados base estiver mais baixo no gráfico da hierarquia é convertido implicitamente no outro tipo de dados e a comparação é feita.  
-   Quando **sql_variant** valores de **char**, **varchar**, **nchar**, ou **nvarchar** são de tipos de dados em comparação, seus agrupamentos são primeiro comparados com base nos seguintes critérios: LCID, versão do LCID, sinalizadores de comparação e classificação ID. Todos esses critérios são comparados como valores de inteiro na ordem listada. Se todos esses critérios forem iguais, os valores reais da cadeia de caracteres serão comparados de acordo com o agrupamento.  
  
## <a name="converting-sqlvariant-data"></a>Convertendo dados sql_variant  
Ao lidar com o **sql_variant** tipo de dados, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oferece suporte a conversões implícitas de objetos com outros tipos de dados para o **sql_variant** tipo. No entanto, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não oferece suporte a conversões implícitas de **sql_variant** dados a um objeto com outro tipo de dados.
  
## <a name="restrictions"></a>Restrições  
A tabela a seguir lista os tipos de valores que não podem ser armazenados usando **sql_variant**:
  
|||  
|-|-|  
|**varchar(max)**|**varbinary(max)**|  
|**nvarchar(max)**|**xml**|  
|**text**|**ntext**|  
|**imagem**|**rowversion** (**timestamp**)|  
|**sql_variant**|**geografia**|  
|**hierarchyid**|**geometria**|  
|Tipos definidos pelo usuário|**datetimeoffset**|  
  
## <a name="see-also"></a>Consulte também
[CAST e CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[SQL_VARIANT_PROPERTY &#40; Transact-SQL &#41;](../../t-sql/functions/sql-variant-property-transact-sql.md)
  
  

