---
title: sys. dm_sql_referencing_entities (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
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
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: bd09706d1b3de9ebe4a5b333f79be9644c433e7c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "73982347"
---
# <a name="sysdm_sql_referencing_entities-transact-sql"></a>sys.dm_sql_referencing_entities (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Retorna uma linha para cada entidade do banco de dados atual que faz referência a outra entidade definida pelo usuário por nome. Uma dependência entre duas entidades é criada quando uma entidade, chamada de *entidade referenciada*, é exibida pelo nome em uma expressão SQL persistente de outra entidade, chamada de *entidade de referência*. Por exemplo, se um UDT (tipo definido pelo usuário) for especificado como entidade referenciada, essa função retornará cada entidade definida pelo usuário que referencia aquele tipo pelo nome em sua definição. A função não retorna entidades em outros bancos de dados que podem fazer referência à entidade especificada. Essa função precisa ser executada no contexto do banco de dados mestre para retornar um gatilho DDL no nível do servidor como entidade de referência.  
  
 Você pode usar essa função de gerenciamento dinâmico para relatar os seguintes tipos de entidades do banco de dados atual que fazem referência à entidade especificada:  
  
-   Entidades associadas a esquema ou entidades não associadas a esquema  
  
-   Gatilhos DDL no nível do banco de dados  
  
-   Gatilhos DDL no nível do servidor  
  
**Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ( [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]),.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
 *schema_name. referenciado*_*entity_name*  
 É o nome da entidade referenciada.  
  
 *schema_name* é necessário, exceto quando a classe referenciada é PARTITION_FUNCTION.  
  
 *schema_name. referenced_entity_name* é **nvarchar (517)**.  
  
 *<referenced_class>* :: = {Object | TIPO | XML_SCHEMA_COLLECTION | PARTITION_FUNCTION}  
 É a classe da entidade referenciada. Apenas uma classe pode ser especificada por instrução.  
  
 *<referenced_class>* é **nvarchar**(60).  
  
## <a name="table-returned"></a>Tabela retornada  
  
|Nome da coluna|Tipo de dados|DESCRIÇÃO|  
|-----------------|---------------|-----------------|  
|referencing_schema_name|**sysname**|Esquema ao qual a entidade de referência pertence. Permite valor nulo.<br /><br /> NULL para nível de banco de dados e gatilhos DDL no nível do servidor.|  
|referencing_entity_name|**sysname**|Nome da entidade de referência. Não permite valor nulo.|  
|referencing_id|**int**|ID da entidade de referência. Não permite valor nulo.|  
|referencing_class|**tinyint**|Classe da entidade de referência. Não permite valor nulo.<br /><br /> 1 = Objeto<br /><br /> 12 = Gatilho DDL no nível do banco de dados<br /><br /> 13 - Gatilho DDL no nível do servidor|  
|referencing_class_desc|**nvarchar (60)**|Descrição da classe da entidade de referência.<br /><br /> OBJECT<br /><br /> DATABASE_DDL_TRIGGER<br /><br /> SERVER_DDL_TRIGGER|  
|is_caller_dependent|**bit**|Indica que a resolução da ID da entidade referenciada ocorre em tempo de execução por depender do esquema do chamador.<br /><br /> 1 = A entidade de referência tem o potencial de fazer referência à entidade. No entanto, a resolução da ID da entidade referenciada depende do chamador e não pode ser determinada. Isso ocorre apenas com relação a referências não associadas a esquema em procedimento armazenado, procedimento armazenado estendido ou função definida pelo usuário chamados em uma instrução EXECUTE.<br /><br /> 0 = A entidade referenciada não é dependente do chamador.|  
  
## <a name="exceptions"></a>Exceções  
 Retorna um conjunto de resultados vazio em qualquer uma das seguintes condições:  
  
-   Um objeto de sistema é especificado.  
  
-   A entidade especificada não existe no banco de dados atual.  
  
-   A entidade especificada não faz referência a nenhuma entidade.  
  
-   Um parâmetro inválido é passado.  
  
 Retorna um erro quando a entidade referenciada especificada é um procedimento armazenado numerado.  
  
## <a name="remarks"></a>Comentários  
 A tabela a seguir lista os tipos de entidades para os quais as informações de dependência são criadas e mantidas. As informações de dependência não são criadas nem mantidas para regras, padrões, tabelas temporárias, procedimentos armazenados temporários ou objetos do sistema.  
  
|Tipo de entidade|Entidade de referência|Entidade referenciada|  
|-----------------|------------------------|-----------------------|  
|Tabela|Sim*|Sim|  
|Visualizar|Sim|Sim|  
|[!INCLUDE[tsql](../../includes/tsql-md.md)]procedimento armazenado * *|Sim|Sim|  
|procedimento armazenado CLR|Não|Sim|  
|[!INCLUDE[tsql](../../includes/tsql-md.md)]função definida pelo usuário|Sim|Sim|  
|Função CLR definida pelo usuário|Não|Sim|  
|Gatilho CLR (DML e DDL)|Não|Não|  
|Gatilho DML [!INCLUDE[tsql](../../includes/tsql-md.md)]|Sim|Não|  
|Gatilho DDL no nível do banco de dados [!INCLUDE[tsql](../../includes/tsql-md.md)]|Sim|Não|  
|Gatilho DDL no nível do servidor [!INCLUDE[tsql](../../includes/tsql-md.md)]|Sim|Não|  
|Procedimentos armazenados estendidos|Não|Sim|  
|Fila|Não|Sim|  
|Sinônimo|Não|Sim|  
|Tipo (tipo de alias e tipo de dados CLR definido pelo usuário)|Não|Sim|  
|Coleção de esquemas XML|Não|Sim|  
|Função de partição|Não|Sim|  
  
 \*Uma tabela é rastreada como uma entidade de referência somente quando faz [!INCLUDE[tsql](../../includes/tsql-md.md)] referência a um módulo, tipo definido pelo usuário ou coleção de esquema XML na definição de uma coluna computada, restrição de verificação ou restrição padrão.  
  
 ** Os procedimentos armazenados numerados com um valor inteiro maior que 1 não são controlados como entidade que faz referência nem como entidade referenciada.  
  
## <a name="permissions"></a>Permissões  
  
### <a name="includesskatmaiincludessskatmai-mdmd---includesssql11includessssql11-mdmd"></a>[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] - [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]  
  
-   Requer a permissão CONTROL no objeto referenciado. Quando a entidade referenciada é uma função de partição, a permissão CONTROL é exigida no banco de dados.  
  
-   Requer a permissão SELECT em sys. dm_sql_referencing_entities. Por padrão, a permissão SELECT é concedida a público.  
  
### <a name="includesssql14includessssql14-mdmd---includesscurrentincludessscurrent-mdmd"></a>[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] - [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]  
  
-   Não requer permissão no objeto referenciado. Os resultados parciais poderão ser retornados se o usuário tiver VIEW DEFINITION em apenas algumas das entidades de referência.  
  
-   Requer VIEW DEFINITION no objeto quando a entidade de referência for um objeto.  
  
-   Requer VIEW DEFINITION no banco de dados quando a entidade de referência for um gatilho DDL no nível de banco de dados.  
  
-   Requer VIEW ANY DEFINITION no servidor quando a entidade de referência for um gatilho DDL no nível de servidor.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-returning-the-entities-that-refer-to-a-given-entity"></a>a. Retornando as entidades que fazem referência a uma determinada entidade  
 O exemplo a seguir retorna as entidades do banco de dados atual que fazem referência à tabela especificada.  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT referencing_schema_name, referencing_entity_name, referencing_id, referencing_class_desc, is_caller_dependent  
FROM sys.dm_sql_referencing_entities ('Production.Product', 'OBJECT');  
GO  
```  
  
### <a name="b-returning-the-entities-that-refer-to-a-given-type"></a>B. Retornando as entidades que fazem referência a um determinado tipo  
 O exemplo a seguir retorna as entidades que referenciam o tipo de alias `dbo.Flag`. O conjunto de resultados mostra que dois procedimentos armazenados usam esse tipo. O `dbo.Flag` tipo também é usado na definição de várias colunas na `HumanResources.Employee` tabela; no entanto, como o tipo não está na definição de uma coluna computada, restrição de verificação ou restrição padrão na tabela, nenhuma linha é retornada para `HumanResources.Employee` a tabela.  
  
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
 
## <a name="see-also"></a>Consulte Também  
 [sys. dm_sql_referenced_entities &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-sql-referenced-entities-transact-sql.md)   
 [sys.sql_expression_dependencies &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md)  
  
  
