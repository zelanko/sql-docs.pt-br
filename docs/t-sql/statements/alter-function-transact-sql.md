---
title: ALTER FUNCTION (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/07/2017
ms.prod: sql
ms.prod_service: database-engine, pdw, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ALTER_FUNCTION_TSQL
- ALTER FUNCTION
dev_langs:
- TSQL
helpviewer_keywords:
- ALTER FUNCTION statement
- modifying functions
- functions [SQL Server], modifying
ms.assetid: 89f066ee-05ac-4439-ab04-d8c3d5911179
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 7de5bc19cd49959663bf4ead3f8ebff62b3b982b
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "73982859"
---
# <a name="alter-function-transact-sql"></a>ALTER FUNCTION (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-pdw-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-pdw-md.md)]

  Altera uma função CLR ou [!INCLUDE[tsql](../../includes/tsql-md.md)] existente que foi criada anteriormente executando a instrução CREATE FUNCTION, sem alterar as permissões e sem afetar nenhuma função, procedimento armazenado ou gatilho dependente.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
-- Transact-SQL Scalar Function Syntax    
ALTER FUNCTION [ schema_name. ] function_name   
( [ { @parameter_name [ AS ][ type_schema_name. ] parameter_data_type   
    [ = default ] }   
    [ ,...n ]  
  ]  
)  
RETURNS return_data_type  
    [ WITH <function_option> [ ,...n ] ]  
    [ AS ]  
    BEGIN   
        function_body   
        RETURN scalar_expression  
    END  
[ ; ]
```  

```
-- Transact-SQL Inline Table-Valued Function Syntax
ALTER FUNCTION [ schema_name. ] function_name   
( [ { @parameter_name [ AS ] [ type_schema_name. ] parameter_data_type   
    [ = default ] }   
    [ ,...n ]  
  ]  
)  
RETURNS TABLE  
    [ WITH <function_option> [ ,...n ] ]  
    [ AS ]  
    RETURN [ ( ] select_stmt [ ) ]  
[ ; ]  
```
  
```
-- Transact-SQL Multistatement Table-valued Function Syntax
ALTER FUNCTION [ schema_name. ] function_name   
( [ { @parameter_name [ AS ] [ type_schema_name. ] parameter_data_type   
    [ = default ] }   
    [ ,...n ]  
  ]  
)  
RETURNS @return_variable TABLE <table_type_definition>  
    [ WITH <function_option> [ ,...n ] ]  
    [ AS ]  
    BEGIN   
        function_body   
        RETURN  
    END  
[ ; ]  
```

```  
-- Transact-SQL Function Clauses   
<function_option>::=   
{  
    [ ENCRYPTION ]  
  | [ SCHEMABINDING ]  
  | [ RETURNS NULL ON NULL INPUT | CALLED ON NULL INPUT ]  
  | [ EXECUTE_AS_Clause ]  
} 

<table_type_definition>:: =   
( { <column_definition> <column_constraint>   
  | <computed_column_definition> }   
    [ <table_constraint> ] [ ,...n ]  
)   
<column_definition>::=  
{  
    { column_name data_type }  
    [ [ DEFAULT constant_expression ]   
      [ COLLATE collation_name ] | [ ROWGUIDCOL ]  
    ]  
    | [ IDENTITY [ (seed , increment ) ] ]  
    [ <column_constraint> [ ...n ] ]   
}  

<column_constraint>::=   
{  
    [ NULL | NOT NULL ]   
    { PRIMARY KEY | UNIQUE }  
      [ CLUSTERED | NONCLUSTERED ]   
        [ WITH FILLFACTOR = fillfactor   
        | WITH ( < index_option > [ , ...n ] )  
      [ ON { filegroup | "default" } ]  
  | [ CHECK ( logical_expression ) ] [ ,...n ]  
}  
  
<computed_column_definition>::=  
column_name AS computed_column_expression   
  
<table_constraint>::=  
{   
    { PRIMARY KEY | UNIQUE }  
      [ CLUSTERED | NONCLUSTERED ]   
      ( column_name [ ASC | DESC ] [ ,...n ] )  
        [ WITH FILLFACTOR = fillfactor   
        | WITH ( <index_option> [ , ...n ] )  
  | [ CHECK ( logical_expression ) ] [ ,...n ]  
}  
  
<index_option>::=  
{   
    PAD_INDEX = { ON | OFF }   
  | FILLFACTOR = fillfactor   
  | IGNORE_DUP_KEY = { ON | OFF }  
  | STATISTICS_NORECOMPUTE = { ON | OFF }   
  | ALLOW_ROW_LOCKS = { ON | OFF }  
  | ALLOW_PAGE_LOCKS ={ ON | OFF }   
}  
```
  
```
-- CLR Scalar and Table-Valued Function Syntax
ALTER FUNCTION [ schema_name. ] function_name   
( { @parameter_name [AS] [ type_schema_name. ] parameter_data_type   
    [ = default ] }   
    [ ,...n ]  
)  
RETURNS { return_data_type | TABLE <clr_table_type_definition> }  
    [ WITH <clr_function_option> [ ,...n ] ]  
    [ AS ] EXTERNAL NAME <method_specifier>  
[ ; ]  
```
  
```
-- CLR Function Clauses
<method_specifier>::=  
    assembly_name.class_name.method_name  
 
  
<clr_function_option>::=  
}  
    [ RETURNS NULL ON NULL INPUT | CALLED ON NULL INPUT ]  
  | [ EXECUTE_AS_Clause ]  
}  
  
<clr_table_type_definition>::=   
( { column_name data_type } [ ,...n ] )  
  
```  
  
```  
-- Syntax for In-Memory OLTP: Natively compiled, scalar user-defined function  
ALTER FUNCTION [ schema_name. ] function_name    
 ( [ { @parameter_name [ AS ][ type_schema_name. ] parameter_data_type   
    [ NULL | NOT NULL ] [ = default ] }   
    [ ,...n ]   
  ]   
)   
RETURNS return_data_type  
    [ WITH <function_option> [ ,...n ] ]   
    [ AS ]   
    BEGIN ATOMIC WITH (set_option [ ,... n ])  
        function_body   
        RETURN scalar_expression  
    END  
    
<function_option>::=   
{ |  NATIVE_COMPILATION   
  |  SCHEMABINDING   
  | [ EXECUTE_AS_Clause ]   
  | [ RETURNS NULL ON NULL INPUT | CALLED ON NULL INPUT ]   
}  
```   
  
## <a name="arguments"></a>Argumentos  
 *schema_name*  
 É o nome do esquema ao qual a função definida pelo usuário pertence.  
  
 *function_name*  
 É a função definida pelo usuário a ser alterada.  
  
> [!NOTE]  
>  São necessários parênteses depois do nome de função mesmo que um parâmetro não seja especificado.  
  
 **@** _parameter_name_  
 É um parâmetro na função definida pelo usuário. Podem ser declarados um ou mais parâmetros.  
  
 Uma função pode ter no máximo 2.100 parâmetros. O valor de cada parâmetro declarado deve ser fornecido pelo usuário quando a função é executada, a menos que seja definido um padrão para o parâmetro.  
  
 Especifique um nome de parâmetro usando um sinal de arroba ( **@** ) como o primeiro caractere. O nome do parâmetro precisa estar em conformidade com as regras para [identificadores](../../relational-databases/databases/database-identifiers.md). Os parâmetros são locais para a função. Os mesmos nomes de parâmetro podem ser usados em outras funções. Os parâmetros só podem assumir o lugar de constantes. Eles não podem ser usados no lugar de nomes de tabela, nomes de coluna ou nomes de outros objetos de banco de dados.  
  
> [!NOTE]  
>  O ANSI_WARNINGS não é cumprido quando os parâmetros passam no procedimento armazenado, em uma função definida pelo usuário ou quando declaram ou definem variáveis em uma instrução de lote. Por exemplo, se a variável for definida como **char(3)** e, em seguida, configurada com um valor maior que três caracteres, os dados serão truncados até o tamanho definido e a instrução INSERT ou UPDATE terá êxito.  
  
 [ *type_schema_name.* ] *parameter_data_type*  
 É o tipo de dados do parâmetro e, opcionalmente, o esquema ao qual ele pertence. Para funções [!INCLUDE[tsql](../../includes/tsql-md.md)], todos os tipos de dados são permitidos, incluindo tipos CLR definidos pelo usuário, com exceção do tipo de dados **timestamp**. Para funções CLR, todos os tipos de dados, incluindo tipos CLR definidos pelo usuário, são permitidos, exceto **text**, **ntext**, **image** e **timestamp**. Os tipos não escalares **cursor** e **table** não podem ser especificados como um tipo de dados de parâmetro em funções CLR ou [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 Se *type_schema_name* não for especificado, o [!INCLUDE[ssDEversion2005](../../includes/ssdeversion2005-md.md)] procurará o *parameter_data_type* na seguinte ordem:  
  
-   O esquema que contém os nomes dos tipos de dados do sistema SQL Server.  
  
-   O esquema padrão do usuário atual no banco de dados atual.  
  
-   O esquema **dbo** no banco de dados atual.  
  
 [ **=** _default_ ]  
 É um valor padrão para o parâmetro. Se um valor *default* for definido, a função poderá ser executada sem a necessidade de especificar um valor para esse parâmetro.  
  
> [!NOTE]  
>  Valores de parâmetro padrão podem ser especificados para funções CLR, com exceção dos tipos de dados **varchar(max)** e **varbinary(max)** .  
  
 Quando um parâmetro da função tiver um valor padrão, a palavra-chave DEFAULT deve ser especificada quando a função for chamada para recuperar o valor padrão. Esse comportamento é diferente do uso de parâmetros com valores padrão em procedimentos armazenados nos quais a omissão do parâmetro também indica o valor padrão.  
  
 *return_data_type*  
 É o valor de retorno de uma função escalar definida pelo usuário. Para funções [!INCLUDE[tsql](../../includes/tsql-md.md)], todos os tipos de dados são permitidos, incluindo tipos CLR definidos pelo usuário, com exceção do tipo de dados **timestamp**. Para funções CLR, todos os tipos de dados, incluindo tipos CLR definidos pelo usuário, são permitidos, exceto **text**, **ntext**, **image** e **timestamp**. Os tipos não escalares **cursor** e **table** não podem ser especificados como um tipo de dados retornado em funções CLR ou [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 *function_body*  
 Especifica que uma série de instruções [!INCLUDE[tsql](../../includes/tsql-md.md)], que juntas não produzem um efeito colateral, como a modificação de uma tabela, define o valor da função. *function_body* é usado somente em funções escalares e funções com valor de tabela de várias instruções.  
  
 Em funções escalares, *function_body* é uma série de instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] que juntas são avaliadas para um valor escalar.  
  
 Em funções com valor de tabela de várias instruções, *function_body* é uma série de instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] que populam uma variável de retorno TABLE.  
  
 *scalar_expression*  
 Especifica que a função escalar retorna um valor escalar.  
  
 TABLE  
 Especifica que o valor de retorno da função com valor de tabela é uma tabela. Somente as constantes e **@** _local\_variables_ podem ser passadas para as funções com valor de tabela.  
  
 Em funções com valor de tabela embutidas, o valor de retorno TABLE é definido por uma única instrução SELECT. As funções embutidas não têm variáveis de retorno associadas.  
  
 Em funções com valor de tabela de várias instruções, **@** _return\_variable_ é uma variável TABLE usada para armazenar e acumular as linhas que devem ser retornadas como o valor da função. **@** _return\_variable_ pode ser especificado somente para funções [!INCLUDE[tsql](../../includes/tsql-md.md)] e não para funções CLR.  
  
 *select-stmt*  
 É a única instrução SELECT que define o valor de retorno de uma função com valor de tabela embutida.  
  
 EXTERNAL NAME \<method_specifier>*assembly_name.class_name*.*method_name*  
 **Aplica-se a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior.  
  
 Especifica o método de um assembly a ser associado à função. *assembly_name* deve corresponder a um assembly existente no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no banco de dados atual com visibilidade ativada. *classe_name* deve ser um identificador válido do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e deve existir como uma classe no assembly. Se a classe tiver um nome qualificado por namespace que use um ponto final ( **.** ) para separar partes do namespace, o nome de classe deverá ser delimitado usando colchetes ( **[]** ) ou aspas ( **""** ). *method_name* deve ser um identificador válido do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e deve existir como método estático na classe especificada.  
  
> [!NOTE]  
>  Por padrão, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não pode executar código CLR. Você pode criar, modificar e remover objetos de banco de dados que referenciam módulos do Common Language Runtime; entretanto, não pode executar essas referências no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] até habilitar a [opção clr enabled](../../database-engine/configure-windows/clr-enabled-server-configuration-option.md). Para habilitar a opção, use [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md).  
  
> [!NOTE]  
>  Essa opção não está disponível em um banco de dados independente.  
  
 _\<_table\_type\_definition_\>_ **(** { \<column_definition\> \<column\_constraint\> | \<computed\_column\_definition\> } [ \<table\_constraint\> ] [ **,** ...*n* ] **)**  
 Define o tipo de dados de tabela para uma função [!INCLUDE[tsql](../../includes/tsql-md.md)]. A declaração da tabela inclui definições de coluna e restrições de coluna ou tabela.  
  
\< clr_table_type_definition \> **(** { *column_name**data_type* } [ **,** ...*n* ] **)** **Aplica-se a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior, [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] ([versão prévia em algumas regiões](https://azure.microsoft.com/documentation/articles/sql-database-preview-whats-new/?WT.mc_id=TSQL_GetItTag)).  
  
 Define os tipos de dados de tabela para uma função CLR. A declaração de tabela inclui somente nomes de colunas e tipos de dados.  
  
 NULL|NOT NULL  
 Compatível apenas com funções escalares definidas pelo usuário compiladas nativamente. Para obter mais informações, consulte [Funções escalares definidas pelo usuário para OLTP in-memory](../../relational-databases/in-memory-oltp/scalar-user-defined-functions-for-in-memory-oltp.md).  
  
 NATIVE_COMPILATION  
 Indica se uma função definida pelo usuário é compilada nativamente. Esse argumento é obrigatório para funções escalares definidas pelo usuário compiladas nativamente.  
  
 O argumento NATIVE_COMPILATION é necessário quando você escolhe ALTER para a função e só poderá ser usado se a função tiver sido criada com o argumento NATIVE_COMPILATION.  
  
 BEGIN ATOMIC WITH  
 Compatível apenas com funções escalares definidas pelo usuário compiladas nativamente, sendo obrigatório. Para obter mais informações, veja [Blocos atômicos](../../relational-databases/in-memory-oltp/atomic-blocks-in-native-procedures.md).  
  
 SCHEMABINDING  
 O argumento SCHEMABINDING é obrigatório para funções escalares definidas pelo usuário compiladas nativamente.  
  
 **\<function_option>::= e \<clr_function_option>::=**  
  
 Especifica que a função terá uma ou mais das opções a seguir.  
  
 ENCRYPTION  
 **Aplica-se a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior.  
  
 Indica que o [!INCLUDE[ssDE](../../includes/ssde-md.md)] criptografa as colunas da exibição de catálogo que contêm o texto da instrução ALTER FUNCTION. O uso de ENCRYPTION impede que a função seja publicada como parte da replicação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. ENCRYPTION não pode ser especificado para funções CLR.  
  
 SCHEMABINDING  
 Especifica que a função está associada aos objetos de banco de dados referenciados por ela. Esta condição impedirá alterações à função se outros objetos associados ao esquema fizerem referência a ela.  
  
 A associação da função aos objetos referenciados por ela será removida somente quando ocorrer uma das ações a seguir:  
  
-   A função for descartada.  
  
-   A função for modificada com o uso da instrução ALTER sem a especificação da opção SCHEMABINDING.  
  
Para obter uma lista de condições que devem ser atendidas antes de uma função poder ser associada ao esquema, veja [CREATE FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/create-function-transact-sql.md).  
  
 RETURNS NULL ON NULL INPUT | CALLED ON NULL INPUT  
 Especifica o atributo **OnNULLCall** de uma função de valor escalar. Se não for especificado, CALLED ON NULL INPUT será implícito por padrão. Isso significa que o corpo da função será executado mesmo que NULL seja passado como um argumento.  
  
 Se RETURNS NULL ON NULL INPUT estiver especificado em uma função CLR, isso indicará que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] poderá retornar NULL quando qualquer um dos argumentos recebidos for NULL, sem realmente invocar o corpo da função. Se o método especificado em \<method_specifier> já tiver um atributo personalizado que indique RETURNS NULL ON NULL INPUT, mas a instrução ALTER FUNCTION indicar CALLED ON NULL INPUT, a instrução ALTER FUNCTION terá precedência. O atributo **OnNULLCall** não pode ser especificado para funções com valor de tabela CLR.  
  
 Cláusula EXECUTE AS  
 Especifica o contexto de segurança sob o qual a função definida pelo usuário é executada. Portanto, é possível controlar qual conta de usuário o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa para validar permissões em quaisquer objetos do banco de dados referidos pela função.  
  
> [!NOTE]  
>  EXECUTE AS não pode ser especificada para funções definidas pelo usuário embutidas.  
  
 Para obter mais informações, veja [Cláusula EXECUTE AS &#40;Transact-SQL&#41;](../../t-sql/statements/execute-as-clause-transact-sql.md).  
  
**\< column_definition >::=**
  
 Define o tipo de dados da tabela. A declaração da tabela inclui definições de coluna e restrições. Para funções CLR, apenas *column_name* e *data_type* podem ser especificados.  
  
 *column_name*  
 É o nome de uma coluna da tabela. Os nomes de coluna devem estar em conformidade com as regras de identificadores e devem ser exclusivos na tabela. *column_name* pode consistir em 1 a 128 caracteres.  
  
 *data_type*  
 Especifica o tipo de dados da coluna. Para funções [!INCLUDE[tsql](../../includes/tsql-md.md)], todos os tipos de dados são permitidos, incluindo tipos de dados CLR definidos pelo usuário, com exceção de **timestamp**. Para funções CLR, todos os tipos de dados são permitidos, incluindo tipos de dados CLR definidos pelo usuário, com exceção de **text**, **ntext**, **image**, **char**, **varchar**, **varchar(max)** e **timestamp**. O tipo não escalar **cursor** não pode ser especificado como um tipo de dados de coluna em funções CLR ou [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 DEFAULT *constant_expression*  
 Especifica o valor fornecido para a coluna quando um valor não for fornecido explicitamente durante uma inserção. *constant_expression* é uma constante, NULL ou um valor de função do sistema. Podem ser aplicadas definições DEFAULT a qualquer coluna, com exceção das que têm a propriedade IDENTITY. DEFAULT não pode ser especificado para funções CLR com valor de tabela.  
  
 COLLATE *collation_name*  
 Especifica a ordenação da coluna. Se não for especificado, à coluna será atribuída a ordenação padrão do banco de dados. O nome da ordenação pode ser um nome de ordenação do Windows ou um nome de ordenação SQL. Para obter uma lista e mais informações, veja [Nome da ordenação do Windows &#40;Transact-SQL&#41;](../../t-sql/statements/windows-collation-name-transact-sql.md) e [Nome da ordenação do SQL Server &#40;Transact-SQL&#41;](../../t-sql/statements/sql-server-collation-name-transact-sql.md).  
  
 A cláusula COLLATE pode ser usada para alterar as ordenações somente de colunas dos tipos de dados **char**, **varchar**, **nchar** e **nvarchar**.  
  
 COLLATE não pode ser especificado para funções CLR com valor de tabela.  
  
 ROWGUIDCOL  
 Indica que a nova coluna é uma coluna de identificador exclusivo global de linha. Somente uma coluna **uniqueidentifier** por tabela pode ser designada como a coluna ROWGUIDCOL. A propriedade ROWGUIDCOL pode ser atribuída somente a uma coluna **uniqueidentifier**.  
  
 A propriedade ROWGUIDCOL não impõe exclusividade dos valores armazenados na coluna. Também não gera automaticamente valores para novas linhas inseridas na tabela. Para gerar valores exclusivos para cada coluna, use a função NEWID em instruções INSERT. Um valor padrão pode ser especificado; entretanto, NEWID não pode ser especificado como o padrão.  
  
 IDENTITY  
 Indica que a nova coluna é uma coluna de identidade. Quando uma nova linha é adicionada à tabela, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornece um valor incremental exclusivo para a coluna. Geralmente, as colunas de identidade são usadas juntamente com restrições PRIMARY KEY para servir como o identificador exclusivo de linha da tabela. A propriedade IDENTITY pode ser atribuída às colunas **tinyint**, **smallint**, **int**, **bigint**, **decimal(p,0)** ou **numeric(p,0)** . Apenas uma coluna de identidade pode ser criada por tabela. Padrões associados e restrições DEFAULT não podem ser usados com uma coluna de identidade. Você deve especificar *seed* e *increment* ou nenhum dos dois. Se nenhum for especificado, o padrão será (1,1).  
  
 IDENTITY não pode ser especificado para funções CLR com valor de tabela.  
  
 *seed*  
 É o valor inteiro que será atribuído à primeira linha da tabela.  
  
 *increment*  
 É o valor inteiro a ser adicionado ao valor *seed* para linhas sucessivas na tabela.  
  
**\< column_constraint >::= e \< table_constraint>::=**
  
 Define a restrição para uma coluna ou tabela especificada. Para funções CLR, o único tipo de restrição permitido é NULL. Não são permitidas restrições nomeadas.  
  
 NULL | NOT NULL  
 Determina se são permitidos valores nulos na coluna. NULL não é estritamente uma restrição, mas pode ser especificado simplesmente como NOT NULL. NOT NULL não pode ser especificado para funções CLR com valor de tabela.  
  
 PRIMARY KEY  
 É uma restrição que impõe integridade de entidade para uma coluna especificada por meio de um índice exclusivo. Em funções definidas pelo usuário com valor de tabela, a restrição PRIMARY KEY pode ser criada somente em uma coluna por tabela. PRIMARY KEY não pode ser especificado para funções CLR com valor de tabela.  
  
 UNIQUE  
 É uma restrição que fornece integridade de entidade para uma coluna ou colunas especificadas por meio de um índice exclusivo. Uma tabela pode ter várias restrições UNIQUE. UNIQUE não pode ser especificado para funções CLR com valor de tabela.  
  
 CLUSTERED | NONCLUSTERED  
 Indica que um índice clusterizado ou não clusterizado será criado para a restrição PRIMARY KEY ou UNIQUE. As restrições PRIMARY KEY usam CLUSTERED e as restrições UNIQUE usam NONCLUSTERED.  
  
 CLUSTERED só pode ser especificado para uma restrição. Se CLUSTERED for especificado para uma restrição UNIQUE e uma restrição PRIMARY KEY também for especificada, PRIMARY KEY usará NONCLUSTERED.  
  
 CLUSTERED e NONCLUSTERED não podem ser especificados para funções CLR com valor de tabela.  
  
 CHECK  
 É uma restrição que impõe a integridade de domínio limitando os possíveis valores que podem ser inseridos em uma ou mais colunas. Não podem ser especificadas restrições CHECK para funções CLR com valor de tabela.  
  
 *logical_expression*  
 É uma expressão lógica que retorna TRUE ou FALSE.  
  
 **\<computed_column_definition>::=**  
  
 Especifica uma coluna computada. Para obter mais informações sobre colunas computadas, consulte [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md).  
  
 *column_name*  
 É o nome da coluna computada.  
  
 *computed_column_expression*  
 É uma expressão que define o valor de uma coluna computada.  
  
 **\<index_option>::=**  
  
 Especifica as opções de índice para o índice PRIMARY KEY ou UNIQUE. Para obter mais informações sobre opções de índice, consulte [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md).  
  
 PAD_INDEX = { ON | OFF }  
 Especifica o preenchimento do índice. O padrão é OFF.  
  
 FILLFACTOR = *fillfactor*  
 Especifica uma porcentagem que indica quanto o [!INCLUDE[ssDE](../../includes/ssde-md.md)] deve preencher o nível folha de cada página de índice durante a criação ou alteração do índice. *fillfactor* deve ser um valor inteiro de 1 a 100. O padrão é 0.  
  
 IGNORE_DUP_KEY = { ON | OFF }  
 Especifica a resposta de erro quando uma operação de inserção tenta inserir valores da chave duplicada em um índice exclusivo. A opção IGNORE_DUP_KEY aplica-se apenas a operações de inserção depois que o índice é criado ou recriado. O padrão é OFF.  
  
 STATISTICS_NORECOMPUTE = { ON | OFF }  
 Especifica se as estatísticas de distribuição são recomputadas. O padrão é OFF.  
  
 ALLOW_ROW_LOCKS = { ON | OFF }  
 Especifica se bloqueios de linha são permitidos. O padrão é ON.  
  
 ALLOW_PAGE_LOCKS = { ON | OFF }  
 Especifica se bloqueios de página são permitidos. O padrão é ON.  
  
## <a name="remarks"></a>Comentários  
 ALTER FUNCTION não pode ser usado para alterar uma função com valor escalar a uma função com valor de tabela ou vice-versa. Além disso, ALTER FUNCTION não pode ser usado para alterar uma função embutida para uma função de várias instruções ou vice-versa. ALTER FUNCTION não pode ser usado para alterar uma função [!INCLUDE[tsql](../../includes/tsql-md.md)] para uma função CLR ou vice-versa.  
  
 As seguintes instruções do Service Broker não podem ser incluídas na definição de uma função [!INCLUDE[tsql](../../includes/tsql-md.md)] definida pelo usuário:  
  
-   BEGIN DIALOG CONVERSATION  
-   END CONVERSATION  
-   GET CONVERSATION GROUP  
-   MOVE CONVERSATION  
-   RECEIVE  
-   SEND  
  
## <a name="permissions"></a>Permissões  
 Requer permissão ALTER na função ou no esquema. Se a função especificar um tipo definido pelo usuário, a permissão EXECUTE será exigida no tipo.  
  
## <a name="see-also"></a>Consulte Também  
 [CREATE FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/create-function-transact-sql.md)   
 [DROP FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/drop-function-transact-sql.md)   
 [Fazer alterações de esquema em bancos de dados de publicação](../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  
