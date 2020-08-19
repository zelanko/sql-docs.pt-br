---
description: COLUMNPROPERTY (Transact-SQL)
title: COLUMNPROPERTY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
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
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 360089db91ed52ba90f0566868b4f1c87eb2fd8c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88417422"
---
# <a name="columnproperty-transact-sql"></a>COLUMNPROPERTY (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

Essa função retorna informações de coluna ou parâmetro.
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```sql
COLUMNPROPERTY ( id , column , property )   
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
*id*  
Uma [expressão](../../t-sql/language-elements/expressions-transact-sql.md) que contém o identificador (ID) da tabela ou procedimento.
  
*column*  
Uma expressão que contém o nome da coluna ou parâmetro.
  
*property*  
Para o argumento *id*, o argumento *propriedade* especifica o tipo de informação que a função `COLUMNPROPERTY` retornará. O argumento *property* pode ter qualquer um destes valores:
  
|Valor|Descrição|Valor retornado|  
|---|---|---|
|**AllowsNull**|Permite valores nulos.|1: TRUE<br /><br /> 0: FALSE<br /><br /> NULL = entrada inválida.|  
|**ColumnId**|Valor de ID da coluna que corresponde a **sys.columns.column_id**.|ID da coluna<br /><br /> **Observação:** ao consultar várias colunas, podem aparecer intervalos na sequência de valores de ID da coluna.|  
|**FullTextTypeColumn**|A TYPE COLUMN na tabela contendo as informações de tipo de documento da *coluna*.|ID de TYPE COLUMN de texto completo da expressão de nome de coluna passada como segundo parâmetro dessa função.|  
|**GeneratedAlwaysType**|O valor da coluna é gerado pelo sistema. Corresponde a **sys.columns.generated_always_type**|**Aplica-se a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] e posterior.<br /><br /> 0: não é gerado sempre<br /><br /> 1: gerado sempre no início da linha<br /><br /> 2: gerado sempre no fim da linha|  
|**IsColumnSet**|A coluna é um conjunto de colunas. Para obter mais informações, veja [Usar conjuntos de colunas](../../relational-databases/tables/use-column-sets.md).|1: TRUE<br /><br /> 0: FALSE<br /><br /> NULL = entrada inválida.|  
|**IsComputed**|É uma coluna computada.|1: TRUE<br /><br /> 0: FALSE<br /><br /> NULL = entrada inválida.|  
|**IsCursorType**|O parâmetro de procedimento é do tipo CURSOR.|1: TRUE<br /><br /> 0: FALSE<br /><br /> NULL = entrada inválida.|  
|**IsDeterministic**|A coluna é determinística. Essa propriedade só se aplica a colunas computadas e colunas de exibição.|1: TRUE<br /><br /> 0: FALSE<br /><br /> NULL = entrada inválida. Não é uma coluna computada nem uma coluna de exibição.|  
|**IsFulltextIndexed**|A coluna está registrada para indexação de texto completo.|1: TRUE<br /><br /> 0: FALSE<br /><br /> NULL = entrada inválida.|  
|**IsHidden**|O valor da coluna é gerado pelo sistema. Corresponde a **sys.columns.is_hidden**|**Aplica-se a**: [!INCLUDE[ssCurrentLong](../../includes/sscurrent-md.md)] e posterior.<br /><br /> 0: não oculto<br /><br /> 1: oculto|  
|**IsIdentity**|A coluna usa a propriedade IDENTITY.|1: TRUE<br /><br /> 0: FALSE<br /><br /> NULL = entrada inválida.|  
|**IsIdNotForRepl**|A coluna verifica a configuração de IDENTITY_INSERT.|1: TRUE<br /><br /> 0: FALSE<br /><br /> NULL = entrada inválida.|  
|**IsIndexable**|A coluna pode ser indexada.|1: TRUE<br /><br /> 0: FALSE<br /><br /> NULL = entrada inválida.|  
|**IsOutParam**|O parâmetro do procedimento é um parâmetro de saída.|1: TRUE<br /><br /> 0: FALSE<br /><br /> NULL = entrada inválida.|  
|**IsPrecise**|A coluna é precisa. Essa propriedade só se aplica a colunas determinísticas.|1: TRUE<br /><br /> 0: FALSE<br /><br /> NULL = entrada inválida. Não é uma coluna determinística|  
|**IsRowGuidCol**|A coluna tem o tipo de dados **uniqueidentifier** e está definida com a propriedade ROWGUIDCOL.|1: TRUE<br /><br /> 0: FALSE<br /><br /> NULL = entrada inválida.|  
|**IsSparse**|A coluna é esparsa. Para obter mais informações, veja [Usar colunas esparsas](../../relational-databases/tables/use-sparse-columns.md).|1: TRUE<br /><br /> 0: FALSE<br /><br /> NULL = entrada inválida.|  
|**IsSystemVerified**|O [!INCLUDE[ssDE](../../includes/ssde-md.md)] pode verificar as propriedades de determinismo e precisão da coluna. Essa propriedade só se aplica a colunas computadas e colunas de exibições.|1: TRUE<br /><br /> 0: FALSE<br /><br /> NULL = entrada inválida.|  
|**IsXmlIndexable**|A coluna XML pode ser usada em um índice XML.|1: TRUE<br /><br /> 0: FALSE<br /><br /> NULL = entrada inválida.|  
|**Precisão**|Comprimento do tipo de dados da coluna ou parâmetro.|Comprimento do tipo de dados de coluna especificado<br /><br /> -1: **xml** ou tipos de valor grande<br /><br /> NULL = entrada inválida.|  
|**Escala**|Escala para o tipo de dados de parâmetro ou coluna.|O valor de escala<br /><br /> NULL = entrada inválida.|  
|**StatisticalSemantics**|A coluna está habilitada para indexação semântica.|1: TRUE<br /><br /> 0: FALSE|  
|**SystemDataAccess**|A coluna é derivada de uma função que acessa dados nos catálogos do sistema ou tabelas do sistema virtuais do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Essa propriedade só se aplica a colunas computadas e colunas de exibições.|1 = TRUE (indica acesso somente leitura.)<br /><br /> 0: FALSE<br /><br /> NULL = entrada inválida.|  
|**UserDataAccess**|A coluna é derivada de uma função que acessa dados em tabelas de usuário, incluindo exibições e tabelas temporárias, armazenadas na instância local do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Essa propriedade só se aplica a colunas computadas e colunas de exibições.|1 = TRUE (indica acesso somente leitura.)<br /><br /> 0: FALSE<br /><br /> NULL = entrada inválida.|  
|**UsesAnsiTrim**|ANSI_PADDING foi definido como ON no momento da criação da tabela. Essa propriedade aplica-se apenas a colunas ou parâmetros do tipo **char** ou **varchar**.|1: TRUE<br /><br /> 0: FALSE<br /><br /> NULL = entrada inválida.|  
  
## <a name="return-types"></a>Tipos de retorno
 **int**  
  
## <a name="exceptions"></a>Exceções  
Retornará NULL em caso de erro ou se um chamador não tiver permissão para exibir o objeto.
  
Um usuário só pode exibir metadados de protegíveis de sua propriedade ou para os quais recebeu permissão. Isso significa que as funções internas que emitem metadados, como `COLUMNPROPERTY`, poderão retornar NULL se o usuário não tiver a permissão correta para o objeto. Veja [Configuração de Visibilidade de Metadados](../../relational-databases/security/metadata-visibility-configuration.md) para obter mais informações.
  
## <a name="remarks"></a>Comentários  
Ao verificar a propriedade determinística de uma coluna, teste primeiro se a coluna é uma coluna computada. O argumento **IsDeterministic** retorna NULL para colunas não computadas. Colunas computadas podem ser especificadas como colunas de índice.
  
## <a name="examples"></a>Exemplos  
Este exemplo retorna o comprimento da coluna `LastName`.
  
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
  
## <a name="see-also"></a>Confira também
[Funções de metadados &#40;Transact-SQL&#41;](../../t-sql/functions/metadata-functions-transact-sql.md)  
[TYPEPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/typeproperty-transact-sql.md)
  
  
