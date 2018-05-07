---
title: sys.dm_sql_referencing_entities (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_sql_referencing_entities
- dm_sql_referencing_entities_TSQL
- sys.dm_sql_referencing_entities_TSQL
- dm_sql_referencing_entities
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_sql_referencing_entities dynamic management function
ms.assetid: c16f8f0a-483f-4feb-842e-da90426045ae
caps.latest.revision: 33
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 5ec4c6ee03400ca0bdd5ad00a18569c66decbac6
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
---
# <a name="sysdmsqlreferencingentities-transact-sql"></a>sys.dm_sql_referencing_entities (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Retorna uma linha para cada entidade do banco de dados atual que faz referência a outra entidade definida pelo usuário por nome. Uma dependência entre duas entidades é criada quando uma entidade, chamada de *entidade referenciada*, aparece por nome em uma expressão SQL persistente de outra entidade, denominada a *entidade de referência*. Por exemplo, se um UDT (tipo definido pelo usuário) for especificado como entidade referenciada, essa função retornará cada entidade definida pelo usuário que referencia aquele tipo pelo nome em sua definição. A função não retorna entidades em outros bancos de dados que podem fazer referência à entidade especificada. Essa função precisa ser executada no contexto do banco de dados mestre para retornar um gatilho DDL no nível do servidor como entidade de referência.  
  
 Você pode usar essa função de gerenciamento dinâmico para relatar os seguintes tipos de entidades do banco de dados atual que fazem referência à entidade especificada:  
  
-   Entidades associadas a esquema ou entidades não associadas a esquema  
  
-   Gatilhos DDL no nível do banco de dados  
  
-   Gatilhos DDL no nível do servidor  
  
**Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]), [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
sys.dm_sql_referencing_entities (  
    ' schema_name.referenced_entity_name ' , ' <referenced_class> ' )  
  
<referenced_class> ::=  
{  
    OBJECT  
  | TYPE  
  | XML_SCHEMA_COLLECTION  
  | PARTITION_FUNCTION  
}  
```  
  
## <a name="arguments"></a>Argumentos  
 *schema_name.referenced*_*entity_name*  
 É o nome da entidade referenciada.  
  
 *schema_name* é necessária, exceto quando a classe referenciada é a PARTITION_FUNCTION.  
  
 *schema_name.referenced_entity_name* é **nvarchar (517)**.  
  
 *< Referenced_class >* :: = {objeto | TIPO | XML_SCHEMA_COLLECTION | PARTITION_FUNCTION}  
 É a classe da entidade referenciada. Apenas uma classe pode ser especificada por instrução.  
  
 *< referenced_class >* é **nvarchar**(60).  
  
## <a name="table-returned"></a>Tabela retornada  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|referencing_schema_name|**sysname**|Esquema ao qual a entidade de referência pertence. Permite valor nulo.<br /><br /> NULL para nível de banco de dados e gatilhos DDL no nível do servidor.|  
|referencing_entity_name|**sysname**|Nome da entidade de referência. Não permite valor nulo.|  
|referencing_id|**Int**|ID da entidade de referência. Não permite valor nulo.|  
|referencing_class|**tinyint**|Classe da entidade de referência. Não permite valor nulo.<br /><br /> 1 = Objeto<br /><br /> 12 = Gatilho DDL no nível do banco de dados<br /><br /> 13 - Gatilho DDL no nível do servidor|  
|referencing_class_desc|**nvarchar(60)**|Descrição da classe da entidade de referência.<br /><br /> OBJECT<br /><br /> DATABASE_DDL_TRIGGER<br /><br /> SERVER_DDL_TRIGGER|  
|is_caller_dependent|**bit**|Indica que a resolução da ID da entidade referenciada ocorre em tempo de execução por depender do esquema do chamador.<br /><br /> 1 = A entidade de referência tem o potencial de fazer referência à entidade. No entanto, a resolução da ID da entidade referenciada depende do chamador e não pode ser determinada. Isso ocorre apenas com relação a referências não associadas a esquema em procedimento armazenado, procedimento armazenado estendido ou função definida pelo usuário chamados em uma instrução EXECUTE.<br /><br /> 0 = A entidade referenciada não é dependente do chamador.|  
  
## <a name="exceptions"></a>Exceções  
 Retorna um conjunto de resultados vazio em qualquer uma das seguintes condições:  
  
-   Um objeto de sistema é especificado.  
  
-   A entidade especificada não existe no banco de dados atual.  
  
-   A entidade especificada não faz referência a nenhuma entidade.  
  
-   Um parâmetro inválido é passado.  
  
 Retorna um erro quando a entidade referenciada especificada é um procedimento armazenado numerado.  
  
## <a name="remarks"></a>Remarks  
 A tabela a seguir lista os tipos de entidades para os quais as informações de dependência são criadas e mantidas. As informações de dependência não são criadas nem mantidas para regras, padrões, tabelas temporárias, procedimentos armazenados temporários ou objetos do sistema.  
  
|Tipo de entidade|Entidade de referência|Entidade referenciada|  
|-----------------|------------------------|-----------------------|  
|Table|Sim*|Sim|  
|Exibição|Sim|Sim|  
|Procedimento armazenado [!INCLUDE[tsql](../../includes/tsql-md.md)]**|Sim|Sim|  
|procedimento armazenado CLR|não|Sim|  
|Função [!INCLUDE[tsql](../../includes/tsql-md.md)] definida pelo usuário|Sim|Sim|  
|Função CLR definida pelo usuário|não|Sim|  
|Gatilho CLR (DML e DDL)|não|não|  
|Gatilho DML [!INCLUDE[tsql](../../includes/tsql-md.md)] |Sim|não|  
|Gatilho DDL no nível do banco de dados [!INCLUDE[tsql](../../includes/tsql-md.md)]|Sim|não|  
|Gatilho DDL no nível do servidor [!INCLUDE[tsql](../../includes/tsql-md.md)]|Sim|não|  
|Procedimentos armazenados estendidos|não|Sim|  
|Fila|não|Sim|  
|Sinônimo|não|Sim|  
|Tipo (tipo de alias e tipo de dados CLR definido pelo usuário)|não|Sim|  
|Coleção de esquemas XML|não|Sim|  
|Função de partição|não|Sim|  
  
 \* Uma tabela é controlada como uma entidade de referência apenas quando ela faz referência a um [!INCLUDE[tsql](../../includes/tsql-md.md)] módulo, tipo definido pelo usuário ou coleção de esquemas XML na definição de coluna computada, restrição CHECK ou restrição padrão.  
  
 ** Os procedimentos armazenados numerados com um valor inteiro maior que 1 não são controlados como entidade que faz referência nem como entidade referenciada.  
  
## <a name="permissions"></a>Permissões  
  
### <a name="includesskatmaiincludessskatmai-mdmd--includesssql11includessssql11-mdmd"></a>[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] – [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]  
  
-   Requer a permissão CONTROL no objeto referenciado. Quando a entidade referenciada é uma função de partição, a permissão CONTROL é exigida no banco de dados.  
  
-   Requer permissão SELECT em sys.DM sql_referencing_entities. Por padrão, a permissão SELECT é concedida a público.  
  
### <a name="includesssql14includessssql14-mdmd---includesscurrentincludessscurrent-mdmd"></a>[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] - [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]  
  
-   Não requer permissão no objeto referenciado. Os resultados parciais poderão ser retornados se o usuário tiver VIEW DEFINITION em apenas algumas das entidades de referência.  
  
-   Requer VIEW DEFINITION no objeto quando a entidade de referência for um objeto.  
  
-   Requer VIEW DEFINITION no banco de dados quando a entidade de referência for um gatilho DDL no nível de banco de dados.  
  
-   Requer VIEW ANY DEFINITION no servidor quando a entidade de referência for um gatilho DDL no nível de servidor.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-returning-the-entities-that-refer-to-a-given-entity"></a>A. Retornando as entidades que fazem referência a uma determinada entidade  
 O exemplo a seguir retorna as entidades do banco de dados atual que fazem referência à tabela especificada.  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT referencing_schema_name, referencing_entity_name, referencing_id, referencing_class_desc, is_caller_dependent  
FROM sys.dm_sql_referencing_entities ('Production.Product', 'OBJECT');  
GO  
```  
  
### <a name="b-returning-the-entities-that-refer-to-a-given-type"></a>B. Retornando as entidades que fazem referência a um determinado tipo  
 O exemplo a seguir retorna as entidades que referenciam o tipo de alias `dbo.Flag`. O conjunto de resultados mostra que dois procedimentos armazenados usam esse tipo. O `dbo.Flag` tipo também é usado na definição de várias colunas no `HumanResources.Employee` tabela; no entanto, porque o tipo não está na definição de uma coluna computada, restrição CHECK ou restrição padrão na tabela, nenhuma linha será retornada para o `HumanResources.Employee`tabela.  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT referencing_schema_name, referencing_entity_name, referencing_id, referencing_class_desc, is_caller_dependent  
FROM sys.dm_sql_referencing_entities ('dbo.Flag', 'TYPE');  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 referencing_schema_name referencing_entity_name   referencing_id referencing_class_desc is_caller_dependent  
 ----------------------- -------------------------  ------------- ---------------------- -------------------  
 HumanResources          uspUpdateEmployeeHireInfo  1803153469    OBJECT_OR_COLUMN       0  
 HumanResources          uspUpdateEmployeeLogin     1819153526    OBJECT_OR_COLUMN       0  
 (2 row(s) affected)`  
 ``` 
 
## <a name="see-also"></a>Consulte também  
 [sys.dm_sql_referenced_entities &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-sql-referenced-entities-transact-sql.md)   
 [sys.sql_expression_dependencies &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md)  
  
  
