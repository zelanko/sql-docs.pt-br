---
title: CREATE TYPE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 04/11/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sql13.swb.sysdatatype.properties.f1
- CREATE TYPE
- TYPE_TSQL
- TYPE
- CREATE_TYPE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- UDTs [SQL Server], creating
- CLR user-defined types [SQL Server]
- user-defined table types [SQL Server]
- user-defined types [SQL Server], creating
- CREATE TYPE statement
- alias data types [SQL Server], creating
- data types [SQL Server], creating
ms.assetid: 2202236b-e09f-40a1-bbc7-b8cff7488905
caps.latest.revision: 92
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: a284d0d144b4cdc091a866d4c660d6a84ad0c2dc
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33074123"
---
# <a name="create-type-transact-sql"></a>CREATE TYPE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Cria um tipo de dados de alias ou um tipo definido pelo usuário no banco de dados atual no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]. A implementação de um tipo de dados de alias é baseada em um tipo de sistema nativo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Um tipo definido pelo usuário é implementado por meio de uma classe de um assembly no CLR (Common Language Runtime) do [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]. Para associar um tipo definido pelo usuário à sua implementação, o assembly CLR que contém a implementação do tipo deve primeiro ser registrado no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] com [CREATE ASSEMBLY](../../t-sql/statements/create-assembly-transact-sql.md).  
  
 A capacidade de executar código CLR é desativada por padrão no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Você pode criar, modificar e remover objetos do banco de dados que referenciam módulos de código gerenciado, mas essas referências não serão executadas no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a menos que a [Opção clr enabled](../../database-engine/configure-windows/clr-enabled-server-configuration-option.md) seja habilitada com [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md).  
 
> [!NOTE]  
>  A integração do CLR do .NET Framework ao SQL Server é discutida neste tópico. A integração CLR não se aplica ao Azure [!INCLUDE[ssSDS](../../includes/sssds-md.md)].
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
-- Disk-Based Type Syntax  
CREATE TYPE [ schema_name. ] type_name  
{   
    FROM base_type   
    [ ( precision [ , scale ] ) ]  
    [ NULL | NOT NULL ]   
  | EXTERNAL NAME assembly_name [ .class_name ]   
  | AS TABLE ( { <column_definition> | <computed_column_definition> }  
        [ <table_constraint> ] [ ,...n ] )    
} [ ; ]  
  
<column_definition> ::=  
column_name <data_type>  
    [ COLLATE collation_name ]   
    [ NULL | NOT NULL ]  
    [   
        DEFAULT constant_expression ]   
      | [ IDENTITY [ ( seed ,increment ) ]   
    ]  
    [ ROWGUIDCOL ] [ <column_constraint> [ ...n ] ]   
  
<data type> ::=   
[ type_schema_name . ] type_name   
    [ ( precision [ , scale ] | max |   
                [ { CONTENT | DOCUMENT } ] xml_schema_collection ) ]   
  
<column_constraint> ::=   
{     { PRIMARY KEY | UNIQUE }   
        [ CLUSTERED | NONCLUSTERED ]   
        [   
            WITH ( <index_option> [ ,...n ] )   
        ]  
  | CHECK ( logical_expression )   
}   
  
<computed_column_definition> ::=  
  
column_name AS computed_column_expression   
[ PERSISTED [ NOT NULL ] ]  
[   
    { PRIMARY KEY | UNIQUE }  
        [ CLUSTERED | NONCLUSTERED ]  
        [   
            WITH ( <index_option> [ ,...n ] )  
        ]  
    | CHECK ( logical_expression )   
]   
  
<table_constraint> ::=  
{   
    { PRIMARY KEY | UNIQUE }   
        [ CLUSTERED | NONCLUSTERED ]   
    ( column [ ASC | DESC ] [ ,...n ] )   
        [   
    WITH ( <index_option> [ ,...n ] )   
        ]  
    | CHECK ( logical_expression )   
}   
  
<index_option> ::=  
{  
    IGNORE_DUP_KEY = { ON | OFF }  
}  
```  
  
```  
-- Memory-Optimized Table Type Syntax  
CREATE TYPE [schema_name. ] type_name  
AS TABLE ( { <column_definition> }  
    |  [ <table_constraint> ] [ ,... n ]    
    | [ <table_index> ] [ ,... n ]    } )
    [ WITH ( <table_option> [ ,... n ] ) ]  
 [ ; ]  
  
<column_definition> ::=  
column_name <data_type>  
    [ COLLATE collation_name ]   [ NULL | NOT NULL ]    [  
      [ IDENTITY [ (1 , 1) ]  
    ]  
    [ <column_constraint> [ ... n ] ]    [ <column_index> ]  
  
<data type> ::=  
 [type_schema_name . ] type_name [ (precision [ , scale ]) ]  
  
<column_constraint> ::=  
{ PRIMARY KEY {   NONCLUSTERED HASH WITH (BUCKET_COUNT = bucket_count) 
                | NONCLUSTERED } }  
  
< table_constraint > ::=  
{ PRIMARY KEY { NONCLUSTERED HASH (column [ ,... n ] ) 
                   WITH (BUCKET_COUNT = bucket_count) 
               | NONCLUSTERED  (column [ ASC | DESC ] [ ,... n ] )  } }  
  
<column_index> ::=  
  INDEX index_name  
{ { [ NONCLUSTERED ] HASH WITH (BUCKET_COUNT = bucket_count) 
     | NONCLUSTERED } }  
  
< table_index > ::=  
  INDEX constraint_name  
{ { [ NONCLUSTERED ] HASH (column [ ,... n ] ) WITH (BUCKET_COUNT = bucket_count) 
 |  [NONCLUSTERED]  (column [ ASC | DESC ] [ ,... n ] )} }  
  
<table_option> ::=  
{  
    [MEMORY_OPTIMIZED = {ON | OFF}]  
}  
```  
  
## <a name="arguments"></a>Argumentos  
 *schema_name*  
 É o nome do esquema ao qual o tipo de dados de alias ou tipo definido pelo usuário pertence.  
  
 *type_name*  
 É o nome do tipo de dados de alias ou tipo definido pelo usuário. Os nomes de tipos devem obedecer às regras de [identificadores](../../relational-databases/databases/database-identifiers.md).  
  
 *base_type*  
 É o tipo de dados fornecido pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no qual o tipo de dados de alias se baseia. *base_type* é **sysname**, sem padrão, e pode ter um dos seguintes valores:  
  
|||||  
|-|-|-|-|  
|**bigint**|**binary(** *n* **)**|**bit**|**char(** *n* **)**|  
|**date**|**datetime**|**datetime2**|**datetimeoffset**|  
|**decimal**|**float**|**imagem**|**int**|  
|**money**|**nchar(** *n* **)**|**ntext**|**numeric**|  
|**nvarchar(** *n* &#124; **max)**|**real**|**smalldatetime**|**smallint**|  
|**smallmoney**|**sql_variant**|**text**|**time**|  
|**tinyint**|**uniqueidentifier**|**varbinary(** *n* &#124; **max)**|**varchar(** *n* &#124; **max)**|  
  
 *base_type* também pode ser qualquer sinônimo de tipo de dados mapeado para um desses tipos de dados de sistema.  
  
 *precisão*  
 Para **decimal** ou **numeric**, é um inteiro não negativo que indica o número total máximo de dígitos decimais que podem ser armazenados à esquerda e à direita do ponto decimal. Para obter mais informações, consulte [decimal e numeric &#40;Transact-SQL&#41;](../../t-sql/data-types/decimal-and-numeric-transact-sql.md).  
  
 *scale*  
 Para **decimal** ou **numeric**, é um inteiro não negativo que indica o número máximo de dígitos decimais que podem ser armazenados à direita do ponto decimal e ele deve ser menor ou igual à precisão. Para obter mais informações, consulte [decimal e numeric &#40;Transact-SQL&#41;](../../t-sql/data-types/decimal-and-numeric-transact-sql.md).  
  
 **NULL** | NOT NULL  
 Especifica se o tipo pode ter um valor nulo. Se não for especificado, NULL é o padrão.  
  
 *assembly_name*  
 **Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Especifica o assembly [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que referencia a implementação do tipo definido pelo usuário no Common Language Runtime. *assembly_name* deve corresponder a um assembly existente no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no banco de dados atual.  
  
> [!NOTE]  
>  EXTERNAL_NAME não está disponível em um banco de dados independente.  
  
 **[.** *class_name* **]**  
 **Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Especifica a classe dentro do assembly que implementa o tipo definido pelo usuário. *class_name* deve ser um identificador válido e deve existir como uma classe no assembly com visibilidade do assembly. *class_name* diferencia maiúsculas de minúsculas, independentemente do agrupamento de banco de dados, e deve corresponder exatamente ao nome de classe no assembly correspondente. O nome de classe poderá ser um nome qualificado de namespace entre colchetes (**[ ]**) se a linguagem de programação usada para gravar a classe usar o conceito de namespaces, como C#. Se *class_name* não for especificado, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] assumirá que ele é o mesmo que *type_name*.  
  
 \<column_definition>  
 Define as colunas para um tipo de tabela definido pelo usuário.  
  
 \<data type>  
 Define o tipo de dados em uma coluna para um tipo de tabela definido pelo usuário. Para obter mais informações sobre tipos de dados, consulte [Tipos de dados &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md). Para obter mais informações sobre tabelas, consulte [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md).  
  
 \<column_constraint>  
 Define as restrições de coluna para um tipo de tabela definido pelo usuário. As restrições com suporte incluem PRIMARY KEY, UNIQUE e CHECK. Para obter mais informações sobre tabelas, consulte [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md).  
  
 \<computed_column_definition>  
 Define uma expressão de coluna computada como uma coluna em um tipo de tabela definido pelo usuário. Para obter mais informações sobre tabelas, consulte [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md).  
  
 \<table_constraint>  
 Define uma restrição de tabela em um tipo de tabela definido pelo usuário. As restrições com suporte incluem PRIMARY KEY, UNIQUE e CHECK.  
  
 \<index_option>  
 Especifica a resposta de erro para duplicar valores de chave em uma operação de inserção de várias linhas em um índice exclusivo clusterizado ou não clusterizado. Para obter mais informações sobre opções de índice, consulte [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md).  
  
 INDEX  
 Você deve especificar os índices de tabela e coluna como parte da instrução CREATE TABLE. CREATE INDEX e DROP INDEX não têm suporte para tabelas com otimização de memória.  
  
 MEMORY_OPTIMIZED  
 **Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
 Indica se o tipo de tabela tem otimização de memória. Essa opção é desabilitada por padrão; a tabela (tipo) não é uma tabela (tipo) com otimização de memória. Os tipos de tabela com otimização de memória são tabelas de usuário com otimização de memória, o esquema que é mantido no disco, semelhante a outras tabelas de usuário.  
  
 BUCKET_COUNT  
 **Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
 Indica o número de buckets que devem ser criados no índice de hash. O valor máximo para BUCKET_COUNT em índices de hash é 1.073.741.824. Para obter mais informações sobre o número de buckets, veja [Índices para tabelas com otimização de memória](../../relational-databases/in-memory-oltp/indexes-for-memory-optimized-tables.md). *bucket_count* é um argumento obrigatório.  
  
 HASH  
 **Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
 Indica que um índice de HASH foi criado. Há suporte para índices de hash apenas em tabelas com otimização de memória.  
  
## <a name="remarks"></a>Remarks  
 A classe do assembly que é referenciado em *assembly_name*, incluindo seus métodos, deve atender a todos os requisitos de implementação de um tipo definido pelo usuário no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter mais informações sobre esses requisitos, consulte [Tipos CLR definidos pelo usuário](../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md).  
  
 Considerações adicionais incluem o seguinte:  
  
-   A classe pode ter métodos sobrecarregados, mas eles podem ser chamados somente de dentro do código gerenciado, e não do [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
-   Os membros estáticos devem ser declarados como **const** ou **readonly** se *assembly_name* é SAFE ou EXTERNAL_ACCESS.  
  
 Dentro de um banco de dados, pode haver apenas um único tipo definido pelo usuário registrado em qualquer tipo especificado que seja carregado no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] do CLR. Se um tipo definido pelo usuário for criado em um tipo CLR para o qual um tipo definido pelo usuário já exista no banco de dados, CREATE TYPE falhará com um erro. Essa restrição é necessária para evitar ambiguidade durante a resolução de Tipo SQL se um tipo CLR puder ser mapeado para mais de um tipo definido pelo usuário.  
  
 Se um método modificador no tipo não retornar *void*, a instrução CREATE TYPE não será executada.  
  
 Para modificar um tipo definido pelo usuário, você deve descartar o tipo usando uma instrução DROP TYPE e, em seguida, recriá-lo.  
  
 Ao contrário dos tipos definidos pelo usuário que são criados com **sp_addtype**, a função de banco de dados **public**, não recebe automaticamente a permissão REFERENCES em tipos que são criados com CREATE TYPE. Essa permissão deve ser concedida separadamente.  
  
 Em tipos de tabela definidos pelo usuário, os tipos estruturados definidos pelo usuário que são usados em *column_name* \<data type> fazem parte do escopo de esquema do banco de dados no qual o tipo de tabela é definido. Para acessar os tipos estruturados definidos pelo usuário em um escopo diferente dentro do banco de dados, use nomes de duas partes.  
  
 Em tipos de tabela definidos pelo usuário, a chave primária em colunas computadas deve ser PERSISTED e NOT NULL.  
  
## <a name="memory-optimized-table-types"></a>Tipos de tabela com otimização de memória  
 Desde o [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)], o processamento de dados em um tipo de tabela pode ser feito na memória principal, e não no disco. Para obter mais informações, veja [OLTP in-memory &#40;Otimização na memória&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md). Para obter exemplos de código que mostram como criar tipos de tabela com otimização de memória, consulte [Criando uma tabela com otimização de memória e um procedimento armazenado compilado nativamente](../../relational-databases/in-memory-oltp/creating-a-memory-optimized-table-and-a-natively-compiled-stored-procedure.md).  
  
## <a name="permissions"></a>Permissões  
 Exige a permissão CREATE TYPE no banco de dados atual e a permissão ALTER no *schema_name*. Se *schema_name* não for especificado, serão aplicadas as regras de resolução de nome padrão para determinar o esquema do usuário atual. Se *assembly_name* for especificado, um usuário deverá ter o assembly ou ter a permissão REFERENCES nele.  

 Se qualquer coluna na instrução CREATE TABLE for definida como sendo de um tipo definido pelo usuário, a permissão REFERENCES no tipo definido pelo usuário será necessária.
 
   >[!NOTE]
  > Um usuário que cria uma tabela com uma coluna que usa um tipo definido pelo usuário precisa da permissão REFERENCES no tipo definido pelo usuário.
  > Se essa tabela tiver que ser criada no TempDB, a permissão REFERENCES precisa ser concedida explicitamente toda vez **antes** de a tabela ser criada, ou este tipo de dados e as permissões REFERENCES precisam ser adicionados ao modelo de banco de dados. Se isso for feito, esse tipo de dados e permissões estarão disponíveis em TempDB permanentemente. Caso contrário, o tipo de dados e as permissões definidos pelo usuário desaparecerão quando o SQL Server for reiniciado. Para saber mais, veja [CREATE TABLE](https://docs.microsoft.com/sql/t-sql/statements/create-table-transact-sql?view=sql-server-2017#permissions-1)
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-creating-an-alias-type-based-on-the-varchar-data-type"></a>A. Criando um tipo de alias com base no tipo de dados varchar  
 O exemplo a seguir cria um tipo de alias com base no tipo de dados `varchar` fornecido pelo sistema.  
  
```  
CREATE TYPE SSN  
FROM varchar(11) NOT NULL ;  
```  
  
### <a name="b-creating-a-user-defined-type"></a>B. Criando um tipo definido pelo usuário  
 O exemplo a seguir cria um tipo `Utf8String` que referencia a classe `utf8string` no assembly `utf8string`. Antes de criar o tipo, o assembly `utf8string` é registrado no banco de dados local. Substitua a parte binária da instrução CREATE ASSEMBLY por uma descrição válida.  
  
**Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
```  
CREATE ASSEMBLY utf8string  
AUTHORIZATION [dbi]   
FROM 0x4D... ;  
GO  
CREATE TYPE Utf8String   
EXTERNAL NAME utf8string.[Microsoft.Samples.SqlServer.utf8string] ;  
GO  
```  
  
### <a name="c-creating-a-user-defined-table-type"></a>C. Criando um tipo de tabela definido pelo usuário  
 O exemplo a seguir cria um tipo de tabela definido pelo usuário que tem duas colunas. Para obter mais informações sobre como criar e usar parâmetros com valor de tabela, consulte [Usar parâmetros com valor de tabela &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/tables/use-table-valued-parameters-database-engine.md).  
  
```  
CREATE TYPE LocationTableType AS TABLE   
    ( LocationName VARCHAR(50)  
    , CostRate INT );  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [CREATE ASSEMBLY &#40;Transact-SQL&#41;](../../t-sql/statements/create-assembly-transact-sql.md)   
 [DROP TYPE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-type-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  
