---
title: COLUMNPROPERTY (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- COLUMNPROPERTY
- COLUMNPROPERTY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- column properties [SQL Server]
- parameters [SQL Server], properties
- COLUMNPROPERTY function
ms.assetid: 2408c264-6eca-4120-bb71-df043c7c2792
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 61ac858e029848ef59978669112de3db7c068f67
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="columnproperty-transact-sql"></a>COLUMNPROPERTY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Retorna informações sobre uma coluna ou parâmetro.
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```sql
COLUMNPROPERTY ( id , column , property )   
```  
  
## <a name="arguments"></a>Argumentos  
*id*  
É um [expressão](../../t-sql/language-elements/expressions-transact-sql.md) que contém o identificador (ID) da tabela ou procedimento.
  
*coluna*  
É uma expressão que contém o nome da coluna ou parâmetro.
  
*propriedade*  
É uma expressão que contém as informações a serem retornadas para *id*, e pode ser qualquer um dos valores a seguir.
  
|Valor|Description|Valor retornado|  
|---|---|---|
|**AllowsNull**|Permite valores nulos.|1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = A entrada não é válida.|  
|**ColumnId**|Valor de ID de coluna correspondente ao **column_id**.|ID da coluna<br /><br /> **Observação:** ao consultar várias colunas, podem aparecer intervalos na sequência de valores de ID de coluna.|  
|**FullTextTypeColumn**|A coluna de tipo na tabela que contém as informações de tipo de documento o *coluna*.|ID de TYPE COLUMN de texto completo da coluna passada como segundo parâmetro dessa propriedade.|  
|**IsComputed**|É uma coluna computada.|1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = A entrada não é válida.|  
|**IsCursorType**|O parâmetro de procedimento é do tipo CURSOR.|1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = A entrada não é válida.|  
|**IsDeterministic**|A coluna é determinística. Essa propriedade só se aplica a colunas computadas e colunas de exibição.|1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = A entrada não é válida. Não é uma coluna computada nem uma coluna de exibição.|  
|**IsFulltextIndexed**|A coluna foi registrada para indexação de texto completo.|1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = A entrada não é válida.|  
|**IsIdentity**|A coluna usa a propriedade IDENTITY.|1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = A entrada não é válida.|  
|**IsIdNotForRepl**|A coluna verifica a configuração de IDENTITY_INSERT.|1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = A entrada não é válida.|  
|**IsIndexable**|A coluna pode ser indexada.|1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = A entrada não é válida.|  
|**IsOutParam**|O parâmetro do procedimento é um parâmetro de saída.|1 = TRUE<br /><br /> 0 = FALSE NULL = Entrada inválida.|  
|**IsPrecise**|A coluna é precisa. Essa propriedade só se aplica a colunas determinísticas.|1 = TRUE<br /><br /> 0 = FALSE NULL = Entrada inválida. Não é uma coluna determinística|  
|**IsRowGuidCol**|A coluna tem o **uniqueidentifier** tipo de dados e é definido com a propriedade ROWGUIDCOL.|1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = A entrada não é válida.|  
|**IsSystemVerified**|As propriedades de precisão e determinismo da coluna podem ser verificadas pelo [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Essa propriedade só se aplica a colunas computadas e colunas de exibições.|1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = A entrada não é válida.|  
|**IsXmlIndexable**|A coluna XML pode ser usada em um índice XML.|1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = A entrada não é válida.|  
|**Precisão**|Comprimento do tipo de dados da coluna ou parâmetro.|Comprimento do tipo de dados de coluna especificado<br /><br /> -1 = **xml** ou tipos de valor grande<br /><br /> NULL = A entrada não é válida.|  
|**Escala**|Escala do tipo de dados da coluna ou parâmetro.|A escala<br /><br /> NULL = A entrada não é válida.|  
|**StatisticalSemantics**|A coluna está habilitada para indexação semântica.|1 = TRUE<br /><br /> 0 = FALSE|  
|**SystemDataAccess**|A coluna é derivada de uma função que acessa dados nos catálogos do sistema ou tabelas do sistema virtuais do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Essa propriedade só se aplica a colunas computadas e colunas de exibições.|1 = TRUE (Indica acesso somente leitura.)<br /><br /> 0 = FALSE<br /><br /> NULL = A entrada não é válida.|  
|**UserDataAccess**|A coluna é derivada de uma função que acessa dados em tabelas de usuário, incluindo exibições e tabelas temporárias, armazenadas na instância local do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Essa propriedade só se aplica a colunas computadas e colunas de exibições.|1 = TRUE (Indica acesso somente leitura.)<br /><br /> 0 = FALSE<br /><br /> NULL = A entrada não é válida.|  
|**UsesAnsiTrim**|ANSI_PADDING foi definido como ON quando a tabela foi criada pela primeira vez. Essa propriedade se aplica apenas a colunas ou parâmetros de tipo **char** ou **varchar**.|1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = A entrada não é válida.|  
|**IsSparse**|A coluna é esparsa. Para obter mais informações, veja [Usar colunas esparsas](../../relational-databases/tables/use-sparse-columns.md).|1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = A entrada não é válida.|  
|**IsColumnSet**|A coluna é um conjunto de colunas. Para obter mais informações, veja [Usar conjuntos de colunas](../../relational-databases/tables/use-column-sets.md).|1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = A entrada não é válida.|  
|**GeneratedAlwaysType**|O valor da coluna é gerado pelo sistema. Corresponde à **sys.columns.generated_always_type**|**Aplica-se a**: do [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> 0 = não é gerado sempre<br /><br /> 1 = gerada sempre como início de linha<br /><br /> 2 – gerada sempre como linha final|  
|**IsHidden**|O valor da coluna é gerado pelo sistema. Corresponde à **sys.columns.is_hidden**|**Aplica-se a**: do [!INCLUDE[ssCurrentLong](../../includes/sscurrentlong-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> 0 = não ocultos<br /><br /> 1 = oculto|  
  
## <a name="return-types"></a>Tipos de retorno
 **int**  
  
## <a name="exceptions"></a>Exceções  
Retornará NULL em caso de erro ou se um chamador não tiver permissão para exibir o objeto.
  
Um usuário só pode exibir metadados de protegíveis de sua propriedade ou para os quais recebeu permissão. Isso significa que as funções internas emissoras de metadados, como COLUMNPROPERTY, podem retornar NULL se o usuário não tiver permissão no objeto. Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).
  
## <a name="remarks"></a>Comentários  
Ao verificar a propriedade determinística de uma coluna, teste primeiro se a coluna é uma coluna computada. **IsDeterministic** retorna NULL para colunas não computadas. Colunas computadas podem ser especificadas como colunas de índice.
  
## <a name="examples"></a>Exemplos  
O exemplo a seguir retorna o comprimento da coluna `LastName`.
  
```sql
USE AdventureWorks2012;  
GO  
SELECT COLUMNPROPERTY( OBJECT_ID('Person.Person'),'LastName','PRECISION')AS 'Column Length';  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
Column Length
-------------
50
```  
  
## <a name="see-also"></a>Consulte também
[Funções de metadados &#40; Transact-SQL &#41;](../../t-sql/functions/metadata-functions-transact-sql.md)  
[TYPEPROPERTY &#40; Transact-SQL &#41;](../../t-sql/functions/typeproperty-transact-sql.md)
  
  
