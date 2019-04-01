---
title: ADICIONAR CLASSIFICAÇÃO DE CONFIDENCIALIDADE (Transact-SQL) | Microsoft Docs
ms.date: 03/25/2019
ms.reviewer: ''
ms.prod: sql
ms.technology: t-sql
ms.topic: language-reference
ms.custom: ''
ms.manager: craigg
ms.author: giladm
author: giladmit
f1_keywords:
- ADD SENSITIVITY CLASSIFICATION
- ADD_SENSITIVITY_CLASSIFICATION
dev_langs:
- TSQL
helpviewer_keywords:
- ADD SENSITIVITY CLASSIFICATION statement
- add labels
- adding labels
- adding labels
- classification [SQL]
- labels [SQL]
- information types
- data classification
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 9e4fee7a2504255b0763cf9cfad708fd341d336d
ms.sourcegitcommit: 2db83830514d23691b914466a314dfeb49094b3c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58494058"
---
# <a name="add-sensitivity-classification-transact-sql"></a>ADICIONAR CLASSIFICAÇÃO DE CONFIDENCIALIDADE (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-asdw-xxx-md.md)]

Adiciona metadados sobre a classificação de confidencialidade a uma ou mais colunas do banco de dados. A classificação pode incluir um rótulo de confidencialidade e um tipo de informação.  

A classificação de dados confidenciais em seu ambiente de banco de dados ajuda a obter visibilidade estendida e melhor proteção. Informações adicionais podem ser encontradas em [Introdução à Proteção de Informações do SQL](https://aka.ms/sqlip)

## <a name="syntax"></a>Sintaxe  

```sql
ADD SENSITIVITY CLASSIFICATION TO
    <object_name> [, ...n ]
    WITH ( <sensitivity_label_option> [, ...n ] )     

<object_name> ::=
{
    [schema_name.]table_name.column_name
}

<sensitivity_label_option> ::=  
{   
    LABEL = string |
    LABEL_ID = guidOrString |
    INFORMATION_TYPE = string |
    INFORMATION_TYPE_ID = guidOrString  
}
```  

## <a name="arguments"></a>Argumentos  

*object_name* ([schema_name.]table_name.column_name)

É o nome da coluna do banco de dados a ser classificada. Atualmente, há suporte apenas para a classificação da coluna.
    - *schema_name* (opcional) - é o nome do esquema ao qual a coluna classificada pertence.
    - *table_name* - é o nome da tabela à qual a coluna classificada pertence.
    - *column_name* - é o nome da coluna que está sendo classificada.

*LABEL*

É o nome legível do rótulo de confidencialidade. Rótulos de confidencialidade representam a confidencialidade dos dados armazenados na coluna de banco de dados.

*LABEL_ID*

É um identificador associado ao rótulo de confidencialidade. Frequentemente usado por plataformas centralizadas de proteção de informações para identificar de maneira exclusiva os rótulos no sistema.

*INFORMATION_TYPE*

É o nome legível humano do tipo de informação. Os tipos de informações são usados ​​para descrever o tipo de dados que estão sendo armazenados na coluna do banco de dados.

*INFORMATION_TYPE_ID*

É um identificador associado ao tipo de informação. Frequentemente usado por plataformas centralizadas de proteção de informações para identificar de maneira exclusiva os tipos de informações no sistema.


## <a name="remarks"></a>Remarks  

- Apenas uma classificação pode ser adicionada a um único objeto. Adicionar uma classificação a um objeto que já foi classificado sobrescreverá a classificação existente.
- Vários objetos podem ser classificados usando uma única instrução `ADD SENSITIVITY CLASSIFICATION`.
- A visualização do sistema [sys.sensitivity_classifications](../../relational-databases/system-catalog-views/sys-sensitivity-classifications-transact-sql.md) pode ser usada para recuperar as informações de classificação de confidencialidade de um banco de dados.


## <a name="permissions"></a>Permissões

Requer a permissão ALTERAR QUALQUER CLASSIFICAÇÃO DE CONFIDENCIALIDADE. A ALTER ANY SENSITIVITY CLASSIFICATION está implícita na permissão de banco de dados ALTER ou pelo servidor de permissão CONTROL SERVER.


## <a name="examples"></a>Exemplos  

### <a name="a-classifying-two-columns"></a>A. Classificação de duas colunas

O exemplo a seguir classifica as colunas **dbo.sales.price** e **dbo.sales.discount** com o rótulo de confidencialidade **Altamente Confidencial** e o Tipo de Informações como **Financeiro**.

```sql
ADD SENSITIVITY CLASSIFICATION TO
    dbo.sales.price, dbo.sales.discount
    WITH ( LABEL='Highly Confidential', INFORMATION_TYPE='Financial' )
```  

### <a name="b-classifying-only-a-label"></a>B. Classificação com apenas um rótulo
O exemplo a seguir classifica a coluna **dbo.customer.comments** com o rótulo **Confidencial** e a ID do rótulo **643f7acd-776a-438d-890c-79c3f2a520d6**. O tipo de informação não foi classificado para esta coluna.

```sql
ADD SENSITIVITY CLASSIFICATION TO
    dbo.customer.comments
    WITH ( LABEL='Confidential', LABEL_ID='643f7acd-776a-438d-890c-79c3f2a520d6' )
```  

## <a name="see-also"></a>Consulte Também  

[DROP SENSITIVITY CLASSIFICATION (Transact-SQL)](../../t-sql/statements/drop-sensitivity-classification-transact-sql.md)

[sys.sensitivity_classifications (Transact-SQL)](../../relational-databases/system-catalog-views/sys-sensitivity-classifications-transact-sql.md)

[Permissões (Mecanismo de Banco de Dados)](https://docs.microsoft.com/sql/relational-databases/security/permissions-database-engine)

[Introdução à Proteção de Informações do SQL](https://aka.ms/sqlip)
