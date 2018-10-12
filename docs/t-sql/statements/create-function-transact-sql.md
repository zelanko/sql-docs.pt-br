---
title: CREATE FUNCTION (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/25/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- FUNCTION
- CREATE FUNCTION
- CREATE_FUNCTION_TSQL
- FUNCTION_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- invoking functions
- extended stored procedures [SQL Server], functions
- table-valued parameters
- user-defined functions [SQL Server], creating
- CLR functions [SQL Server]
- CREATE FUNCTION statement
- nondeterministic functions
- user-defined data types
- functions [SQL Server], creating
- inline table-valued functions [SQL Server]
- multi-statement table-valued functions [SQL Server]
- table-valued functions [SQL Server], CREATE FUNCTION
- parameters [SQL Server], functions
- nesting user-defined functions
- deterministic functions
- scalar-valued functions
- functions [SQL Server], invoking
ms.assetid: 864b393f-225f-4895-8c8d-4db59ea60032
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 55bbcbb08d9062d4eb8402a8c15dd243aa9b6a98
ms.sourcegitcommit: a251adad8474b477363df6a121431b837f22bf77
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47864284"
---
# <a name="create-function-transact-sql"></a>CREATE FUNCTION (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Cria uma função definida pelo usuário no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e no [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]. Uma função definida pelo usuário é uma rotina [!INCLUDE[tsql](../../includes/tsql-md.md)] ou CLR (Common Language Runtime) que aceita parâmetros, executa uma ação, como um cálculo complexo, e retorna o resultado dessa ação como um valor. O valor de retorno pode ser um valor escalar (único) ou uma tabela. Use essa instrução para criar uma rotina reutilizável que possa ser usada destas maneiras:  
  
-   Em instruções [!INCLUDE[tsql](../../includes/tsql-md.md)], como SELECT  
  
-   Em aplicativos que chamam a função  
  
-   Na definição de outra função definida pelo usuário  
  
-   Para parametrizar uma exibição ou aprimorar a funcionalidade de uma exibição indexada  
  
-   Para definir uma coluna em uma tabela  
  
-   Para definir uma restrição CHECK em uma coluna  
  
-   Para substituir um procedimento armazenado  
  
-   Usar uma função embutida como um predicado de filtro para uma política de segurança  
  
> [!NOTE]  
>  A integração do CLR do .NET Framework ao SQL Server é discutida neste tópico. A integração CLR não se aplica ao Banco de Dados SQL do Azure.

> [!NOTE]  
>  Para o SQL Data Warehouse do Azure, confira o artigo [CREATE FUNCTION (SQL Data Warehouse)](https://docs.microsoft.com/sql/t-sql/statements/create-function-sql-data-warehouse?view=aps-pdw-2016).
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
-- Transact-SQL Scalar Function Syntax  
CREATE [ OR ALTER ] FUNCTION [ schema_name. ] function_name   
( [ { @parameter_name [ AS ][ type_schema_name. ] parameter_data_type   
    [ = default ] [ READONLY ] }   
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
CREATE [ OR ALTER ] FUNCTION [ schema_name. ] function_name   
( [ { @parameter_name [ AS ] [ type_schema_name. ] parameter_data_type   
    [ = default ] [ READONLY ] }   
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
-- Transact-SQL Multi-Statement Table-Valued Function Syntax  
CREATE [ OR ALTER ] FUNCTION [ schema_name. ] function_name   
( [ { @parameter_name [ AS ] [ type_schema_name. ] parameter_data_type   
    [ = default ] [READONLY] }   
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
-- CLR Scalar Function Syntax  
CREATE [ OR ALTER ] FUNCTION [ schema_name. ] function_name   
( { @parameter_name [AS] [ type_schema_name. ] parameter_data_type   
    [ = default ] }   
    [ ,...n ]  
)  
RETURNS { return_data_type }  
    [ WITH <clr_function_option> [ ,...n ] ]  
    [ AS ] EXTERNAL NAME <method_specifier>  
[ ; ]  
```  
  
```  
-- CLR Table-Valued Function Syntax  
CREATE [ OR ALTER ] FUNCTION [ schema_name. ] function_name   
( { @parameter_name [AS] [ type_schema_name. ] parameter_data_type   
    [ = default ] }   
    [ ,...n ]  
)  
RETURNS TABLE <clr_table_type_definition>   
    [ WITH <clr_function_option> [ ,...n ] ]  
    [ ORDER ( <order_clause> ) ]  
    [ AS ] EXTERNAL NAME <method_specifier>  
[ ; ]  
```  

```  
-- CLR Function Clauses  
<order_clause> ::=   
{  
   <column_name_in_clr_table_type_definition>  
   [ ASC | DESC ]   
} [ ,...n]   
  
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
-- In-Memory OLTP: Syntax for natively compiled, scalar user-defined function  
CREATE [ OR ALTER ] FUNCTION [ schema_name. ] function_name   
 ( [ { @parameter_name [ AS ][ type_schema_name. ] parameter_data_type   
    [ NULL | NOT NULL ] [ = default ] [ READONLY ] }   
    [ ,...n ]   
  ]   
)   
RETURNS return_data_type  
     WITH <function_option> [ ,...n ]   
    [ AS ]   
    BEGIN ATOMIC WITH (set_option [ ,... n ])   
        function_body   
        RETURN scalar_expression  
    END  
  
<function_option>::=   
{  
  |  NATIVE_COMPILATION   
  |  SCHEMABINDING   
  | [ EXECUTE_AS_Clause ]   
  | [ RETURNS NULL ON NULL INPUT | CALLED ON NULL INPUT ]   
}  
  
```  
  
## <a name="arguments"></a>Argumentos
*OR ALTER*  
 **Aplica-se a**: Azure [!INCLUDE[ssSDS](../../includes/sssds-md.md)], [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (começando pelo [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1).  
  
 Altera condicionalmente a função somente se ela já existe. 
 
> [!NOTE]  
>  A sintaxe [OR ALTER] opcional para o CLR está disponível do [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1 CU1 em diante.   
 
 *schema_name*  
 É o nome do esquema ao qual a função definida pelo usuário pertence.  
  
 *function_name*  
 É o nome da função definida pelo usuário. Os nomes de funções devem obedecer às regras de [identificadores](../../relational-databases/databases/database-identifiers.md) e devem ser exclusivos dentro do banco de dados e em seu esquema.  
  
> [!NOTE]  
>  São necessários parênteses depois do nome de função mesmo que um parâmetro não seja especificado.  
  
 @*parameter_name*  
 É um parâmetro na função definida pelo usuário. Podem ser declarados um ou mais parâmetros.  
  
 Uma função pode ter no máximo 2.100 parâmetros. O valor de cada parâmetro declarado deve ser fornecido pelo usuário quando a função é executada, a menos que seja definido um padrão para o parâmetro.  
  
 Especifique um nome de parâmetro usando um sinal de arroba (@) como o primeiro caractere. O nome do parâmetro deve estar em conformidade com as regras de identificadores. Os parâmetros são locais para a função. Os mesmos nomes de parâmetro podem ser usados em outras funções. Os parâmetros só podem assumir o lugar de constantes. Eles não podem ser usados no lugar de nomes de tabela, nomes de coluna ou nomes de outros objetos de banco de dados.  
  
> [!NOTE]  
>  ANSI_WARNINGS não é cumprido quando você passa parâmetros em um procedimento armazenado, em uma função definida pelo usuário ou quando declara ou define variáveis em uma instrução de lote. Por exemplo, se a variável for definida como **char(3)** e, em seguida, configurada com um valor maior que três caracteres, os dados serão truncados até o tamanho definido e a instrução INSERT ou UPDATE terá êxito.  
  
 [ *type_schema_name*. ] *parameter_data_type*  
 É o tipo de dados do parâmetro e, opcionalmente, o esquema ao qual ele pertence. Para funções [!INCLUDE[tsql](../../includes/tsql-md.md)], todos os tipos de dados são permitidos, incluindo tipos CLR e tipos de tabela definidos pelo usuário, com exceção do tipo de dados **timestamp**. Para funções CLR, todos os tipos de dados são permitidos, incluindo tipos de dados CLR definidos pelo usuário, com exceção dos tipos de tabela definidos pelo usuário **text**, **ntext**, **image** e dos tipos de dados **timestamp**. Os tipos não escalares, **cursor** e **table**, não podem ser especificados como um tipo de dados de parâmetro em funções CLR ou [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 Se *type_schema_name* não for especificado, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] procurará o *scalar_parameter_data_type* na seguinte ordem:  
  
-   O esquema que contém os nomes dos tipos de dados do sistema [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   O esquema padrão do usuário atual no banco de dados atual.  
  
-   O esquema **dbo** no banco de dados atual.  
  
 [ =*default* ]  
 É um valor padrão para o parâmetro. Se um valor *default* for definido, a função poderá ser executada sem a necessidade de especificar um valor para esse parâmetro.  
  
> [!NOTE]  
>  Valores de parâmetro padrão podem ser especificados para funções CLR, com exceção dos tipos de dados **varchar(max)** e **varbinary(max)**.  
  
 Quando um parâmetro da função tiver um valor padrão, a palavra-chave DEFAULT deverá ser especificada quando a função for chamada para recuperar o valor padrão. Esse comportamento é diferente do uso de parâmetros com valores padrão em procedimentos armazenados nos quais a omissão do parâmetro também indica o valor padrão. Porém, a palavra-chave DEFAULT não é necessária ao invocar uma função escalar por meio da instrução EXECUTE.  
  
 READONLY  
 Indica que o parâmetro não pode ser atualizado ou modificado na definição da função. Se o tipo de parâmetro for um tipo de tabela definido pelo usuário, READONLY deverá ser especificado.  
  
 *return_data_type*  
 É o valor de retorno de uma função escalar definida pelo usuário. Para funções [!INCLUDE[tsql](../../includes/tsql-md.md)], todos os tipos de dados são permitidos, incluindo tipos CLR definidos pelo usuário, com exceção do tipo de dados **timestamp**. Para funções CLR, todos os tipos de dados são permitidos, incluindo tipos CLR definidos pelo usuário, com exceção dos tipos de dados **text**, **ntext**, **image** e **timestamp**. Os tipos não escalares, **cursor** e **table**, não podem ser especificados como um tipo de dados de retorno em funções CLR ou [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 *function_body*  
 Especifica que uma série de instruções [!INCLUDE[tsql](../../includes/tsql-md.md)], que juntas não produzem um efeito colateral, como a modificação de uma tabela, define o valor da função. *function_body* é usado somente em funções escalares e funções com valor de tabela de várias instruções.  
  
 Em funções escalares, *function_body* é uma série de instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] que juntas são avaliadas para um valor escalar.  
  
 Em funções com valor de tabela de várias instruções, *function_body* é uma série de instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] que populam uma variável de retorno TABLE.  
  
 *scalar_expression*  
 Especifica o valor escalar que a função escalar retorna.  
  
 TABLE  
 Especifica que o valor de retorno da função com valor de tabela é uma tabela. Somente constantes e @*local_variables* podem ser passadas para funções com valor de tabela.  
  
 Em funções com valor de tabela embutidas, o valor de retorno TABLE é definido por uma única instrução SELECT. As funções embutidas não têm variáveis de retorno associadas.  
  
 Em funções com valor de tabela de várias instruções, @*return_variable* é uma variável TABLE usada para armazenar e acumular as linhas que devem ser retornadas como o valor da função. @*return_variable* pode ser especificado somente para funções [!INCLUDE[tsql](../../includes/tsql-md.md)] e não para funções CLR.  
  
> [!WARNING]  
>  É possível fazer a junção a uma função com valor de tabela de várias instruções em uma cláusula **FROM**, mas isso pode afetar o desempenho. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não pode usar todas as técnicas otimizadas em algumas instruções a serem incluídas em uma função multistatement, resultando em um plano de consulta de qualidade inferior. Para obter o melhor desempenho possível, sempre que possível use junções entre tabelas base em vez de funções.  
  
 *select_stmt*  
 É a única instrução SELECT que define o valor de retorno de uma função com valor de tabela embutida.  
  
 ORDER (\<order_clause>) Especifica a ordem na qual os resultados são retornados da função com valor de tabela. Para obter mais informações, consulte a seção, "[Usando a ordem de classificação em função com valor de tabela CLR](#using-sort-order-in-clr-table-valued-functions)", mais adiante neste tópico.  
  
 EXTERNAL NAME \<method_specifier> *assembly_name*.*class_name*.*method_name* **Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Especifica o assembly e o método ao qual o nome da função criado deve referir-se.  
  
-   *assembly_name* – deve corresponder a um valor na coluna `name`   
    `SELECT * FROM sys.assemblies;`.  
    Esse é o nome usado na instrução `CREATE ASSEMBLY`.  
  
-   *class_name* – deve corresponder a um valor na coluna `assembly_name`  
    `SELECT * FROM sys.assembly_modules;`.  
    Muitas vezes o valor contém um ponto incorporado ou ponto. Nesses casos, a sintaxe Transact-SQL exige que o valor seja vinculado a um par de colchetes [] ou a um par de aspas duplas "".  
  
-   *method_name* – deve corresponder a um valor na coluna `method_name`   
    `SELECT * FROM sys.assembly_modules;`.  
    O método deve ser estático.  
  
 Um exemplo típico, para MyFood.DLL, onde todos os tipos estão no namespace MyFood, o valor `EXTERNAL NAME` poderia ser:   
`MyFood.[MyFood.MyClass].MyStaticMethod`  
  
> [!NOTE]  
>  Por padrão, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não pode executar código CLR. Você pode criar, modificar e remover objetos de banco de dados que referenciam módulos do Common Language Runtime; entretanto, não pode executar essas referências no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] até habilitar a [opção clr enabled](../../database-engine/configure-windows/clr-enabled-server-configuration-option.md). Para habilitar essa opção, use [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md).  
  
> [!NOTE]  
>  Essa opção não está disponível em um banco de dados independente.  
  
 *\<* table_type_definition*>* ( { \<column_definition> \<column_constraint>    | \<computed_column_definition> }    [ \<table_constraint> ] [ ,...*n* ] ) Define o tipo de dados da tabela para uma função [!INCLUDE[tsql](../../includes/tsql-md.md)]. A declaração da tabela inclui definições de coluna e restrições de coluna ou tabela. A tabela sempre é colocada no grupo de arquivos primário.  
  
 \< clr_table_type_definition >  ( { *column_name**data_type* } [ ,...*n* ] ) **Aplica-se ao**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] ([Versão prévia em algumas regiões](http://azure.microsoft.com/documentation/articles/sql-database-preview-whats-new/?WT.mc_id=TSQL_GetItTag)).|  
  
 Define os tipos de dados de tabela para uma função CLR. A declaração de tabela inclui somente nomes de colunas e tipos de dados. A tabela sempre é colocada no grupo de arquivos primário.  
  
 NULL|NOT NULL  
 Compatível apenas com funções escalares definidas pelo usuário compiladas nativamente. Para obter mais informações, consulte [Funções escalares definidas pelo usuário para OLTP in-memory](../../relational-databases/in-memory-oltp/scalar-user-defined-functions-for-in-memory-oltp.md).  
  
 NATIVE_COMPILATION  
 Indica se uma função definida pelo usuário é compilada nativamente. Esse argumento é obrigatório para funções escalares definidas pelo usuário compiladas nativamente.  
  
 BEGIN ATOMIC WITH  
 Compatível apenas com funções escalares definidas pelo usuário compiladas nativamente, sendo obrigatório. Para obter mais informações, veja [Blocos atômicos](../../relational-databases/in-memory-oltp/atomic-blocks-in-native-procedures.md).  
  
 SCHEMABINDING  
 O argumento SCHEMABINDING é obrigatório para funções escalares definidas pelo usuário compiladas nativamente.  
  
 EXECUTE AS  
 EXECUTE AS é exigida para as funções escalares definidas pelo usuário compiladas nativamente.  
  
 **\<function_option>::= e \<clr_function_option>::=** 
  
 Especifica que a função terá uma ou mais das opções a seguir.  
  
 ENCRYPTION  
 **Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Indica que o [!INCLUDE[ssDE](../../includes/ssde-md.md)] converterá o texto original da instrução CREATE FUNCTION em um formato ofuscado. A saída do ofuscamento não é diretamente visível em nenhuma exibição do catálogo. Os usuários que não tiverem nenhum acesso a tabelas do sistema ou arquivos de banco de dados não poderão recuperar o texto ofuscado. Entretanto, o texto estará disponível para usuários privilegiados que podem acessar as tabelas do sistema na [porta DAC](../../database-engine/configure-windows/diagnostic-connection-for-database-administrators.md) ou acessar diretamente os arquivos do banco de dados. Além disso, os usuários que podem anexar um depurador ao processo de servidor também podem recuperar o procedimento original da memória em tempo de execução. Para obter mais informações sobre como acessar metadados do sistema, consulte [Configuração de visibilidade de metadados](../../relational-databases/security/metadata-visibility-configuration.md).  
  
 O uso dessa opção impede que a função seja publicada como parte da replicação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Essa opção não pode ser especificada para funções CLR.  
  
 SCHEMABINDING  
 Especifica que a função está associada aos objetos de banco de dados referenciados por ela. Quando SCHEMABINDING for especificado, os objetos base não poderão ser modificadas de um modo que possa afetar a definição da função. A própria definição da função deve ser primeiro modificada ou descartada para remover as dependências no objeto a ser modificado.  
  
 A associação da função aos objetos referenciados por ela será removida somente quando ocorrer uma das ações a seguir: 
  
-   A função for descartada.  
  
-   A função for modificada com o uso da instrução ALTER sem a especificação da opção SCHEMABINDING.  
  
 Uma função poderá ser associada a esquemas apenas se as condições a seguir forem verdadeiras:  
  
-   A função é uma função [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
-   As exibições e funções definidas pelo usuário referenciadas pela função também são associadas a esquema.  
  
-   Os objetos referenciados pela função são referenciados com um nome de duas partes.  
  
-   A função e os objetos aos quais ela faz referência pertencem ao mesmo banco de dados.  
  
-   O usuário que executou a instrução CREATE FUNCTION tem permissão REFERENCES nos objetos do banco de dados referidos pela função.  
  
 RETURNS NULL ON NULL INPUT | **CALLED ON NULL INPUT**  
 Especifica o atributo **OnNULLCall** de uma função de valor escalar. Se não for especificado, CALLED ON NULL INPUT será implícito por padrão. Isso significa que o corpo da função será executado mesmo que NULL seja passado como um argumento.  
  
 Se RETURNS NULL ON NULL INPUT estiver especificado em uma função CLR, isso indicará que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] poderá retornar NULL quando qualquer um dos argumentos recebidos for NULL, sem realmente invocar o corpo da função. Se o método de uma função CLR especificado em \<method_specifier> já tiver um atributo personalizado que indica RETURNS NULL ON NULL INPUT, mas a instrução CREATE FUNCTION indicar CALLED ON NULL INPUT, a instrução CREATE FUNCTION terá precedência. O atributo **OnNULLCall** não pode ser especificado para funções com valor de tabela CLR. 
  
 Cláusula EXECUTE AS  
 Especifica o contexto de segurança sob o qual a função definida pelo usuário é executada. Portanto, é possível controlar a conta de usuário usada pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para validar permissões em quaisquer objetos do banco de dados referidos pela função.  
  
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
 Especifica o agrupamento da coluna. Se não for especificado, a coluna será atribuída ao agrupamento padrão do banco de dados. O nome do agrupamento pode ser um nome de agrupamento do Windows ou um nome de agrupamento SQL. Para obter uma lista e mais informações sobre agrupamentos, consulte [Nome de agrupamento do Windows &#40;Transact-SQL&#41;](../../t-sql/statements/windows-collation-name-transact-sql.md) e [Nome de agrupamento do SQL Server &#40;Transact-SQL&#41;](../../t-sql/statements/sql-server-collation-name-transact-sql.md).  
  
 A cláusula COLLATE pode ser usada para alterar os agrupamentos somente de colunas dos tipos de dados **char**, **varchar**, **nchar** e **nvarchar**.  
  
 COLLATE não pode ser especificado para funções CLR com valor de tabela.  
  
 ROWGUIDCOL  
 Indica que a nova coluna é uma de coluna de identificador globalmente exclusivo de linha. Somente uma coluna **uniqueidentifier** por tabela pode ser designada como a coluna ROWGUIDCOL. A propriedade ROWGUIDCOL pode ser atribuída somente a uma coluna **uniqueidentifier**.  
  
 A propriedade ROWGUIDCOL não impõe exclusividade dos valores armazenados na coluna. Também não gera automaticamente valores para novas linhas inseridas na tabela. Para gerar valores exclusivos para cada coluna, use a função NEWID em instruções INSERT. Um valor padrão pode ser especificado; entretanto, NEWID não pode ser especificado como o padrão.  
  
 IDENTITY  
 Indica que a nova coluna é uma coluna de identidade. Quando uma nova linha é adicionada à tabela, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornece um valor incremental exclusivo para a coluna. Geralmente, as colunas de identidade são usadas juntamente com restrições PRIMARY KEY para servir como o identificador exclusivo de linha da tabela. A propriedade IDENTITY pode ser atribuída às colunas **tinyint**, **smallint**, **int**, **bigint**, **decimal(p,0)** ou **numeric(p,0)**. Apenas uma coluna de identidade pode ser criada por tabela. Padrões associados e restrições DEFAULT não podem ser usados com uma coluna de identidade. Você deve especificar *seed* e *increment* ou nenhum dos dois. Se nenhum for especificado, o padrão será (1,1).  
  
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
  
 PAD_INDEX = { ON | **OFF** }  
 Especifica o preenchimento do índice. O padrão é OFF.  
  
 FILLFACTOR = *fillfactor*  
 Especifica uma porcentagem que indica quanto o [!INCLUDE[ssDE](../../includes/ssde-md.md)] deve preencher o nível folha de cada página de índice durante a criação ou alteração do índice. *fillfactor* deve ser um valor inteiro de 1 a 100. O padrão é 0.  
  
 IGNORE_DUP_KEY = { ON | **OFF** }  
 Especifica a resposta de erro quando uma operação de inserção tenta inserir valores da chave duplicada em um índice exclusivo. A opção IGNORE_DUP_KEY aplica-se apenas a operações de inserção depois que o índice é criado ou recriado. O padrão é OFF.  
  
 STATISTICS_NORECOMPUTE = { ON | **OFF** }  
 Especifica se as estatísticas de distribuição são recomputadas. O padrão é OFF.  
  
 ALLOW_ROW_LOCKS = { **ON** | OFF }  
 Especifica se bloqueios de linha são permitidos. O padrão é ON.  
  
 ALLOW_PAGE_LOCKS = { **ON** | OFF }  
 Especifica se bloqueios de página são permitidos. O padrão é ON.  
  
## <a name="best-practices"></a>Práticas recomendadas  
 Se uma função definida pelo usuário não for criada com a cláusula SCHEMABINDING, as alterações feitas nos objetos subjacentes poderão afetar a definição da função e produzir resultados inesperados quando ela for chamada. É recomendável que você implemente um dos seguintes métodos para garantir que a função não se torne desatualizada devido a alterações em seus objetos subjacentes:  
  
-   Especifique a cláusula WITH SCHEMABINDING quando estiver criando a função. Isso garante que os objetos referenciados na definição da função não possam ser modificados, a menos que a função também seja modificada.  
  
-   Execute o procedimento armazenado [sp_refreshsqlmodule](../../relational-databases/system-stored-procedures/sp-refreshsqlmodule-transact-sql.md) depois de modificar um objeto especificado na definição da função.  
  
## <a name="data-types"></a>Tipos de dados  
 Se forem especificados parâmetros em uma função CLR, eles deverão ser tipos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], conforme definido previamente para *scalar_parameter_data_type*. Para obter informações sobre como comparar tipos de dados do sistema [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] com tipos de dados de integração CLR ou tipos de dados Common Language Runtime [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)], consulte [Mapeando dados de parâmetro CLR](../../relational-databases/clr-integration-database-objects-types-net-framework/mapping-clr-parameter-data.md).  
  
 Para que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] referencie o método correto quando estiver sobrecarregado em uma classe, o método indicado em \<method_specifier> deve ter as seguintes características: 
  
-   Receber o mesmo número de parâmetros, conforme especificado em [ , ...*n* ].  
  
-   Receber todos os parâmetros por valor, não por referência.  
  
-   Use tipos de parâmetro que sejam compatíveis com os especificados na função [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Se o tipo de dados de retorno da função CLR especificar um tipo de tabela (RETURNS TABLE), o tipo de dados de retorno do método no \<method_specifier> deverá ser do tipo **IEnumerator** ou **IEnumerable** e pressupõe-se que a interface seja implementada pelo criador da função. Ao contrário de funções [!INCLUDE[tsql](../../includes/tsql-md.md)], as funções CLR não podem incluir restrições de PRIMARY KEY, UNIQUE ou CHECK em \<table_type_definition>. Os tipos de dados de colunas especificados em \<table_type_definition> devem corresponder aos tipos das colunas correspondentes do conjunto de resultados retornado pelo método no \<method_specifier> em tempo de execução. Essa verificação de tipo não é executada quando a função é criada. 
  
 Para obter mais informações sobre como programar funções CLR, consulte [Funções CLR definidas pelo usuário](../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-user-defined-functions.md).  
  
## <a name="general-remarks"></a>Comentários gerais  
 Funções com valor escalar podem ser invocadas quando expressões escalares são usadas. Isso inclui colunas computadas e definições de restrições CHECK. Funções de valor escalar também podem ser executadas com a instrução [EXECUTE](../../t-sql/language-elements/execute-transact-sql.md). Funções com valor escalar devem ser invocadas usando pelo menos o nome de duas partes da função. Para obter mais informações sobre nomes de várias partes, consulte [Convenções da sintaxe Transact-SQL &#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md). Funções com valor de tabela podem ser invocadas quando expressões de tabela são permitidas na cláusula FROM de instruções SELECT, INSERT, UPDATE ou DELETE. Para obter mais informações, consulte [Executar funções definidas pelo usuário](../../relational-databases/user-defined-functions/execute-user-defined-functions.md).  
  
## <a name="interoperability"></a>Interoperabilidade  
 As instruções a seguir são válidas em uma função:  
  
-   Instruções de atribuição.  
  
-   Instruções de controle de fluxo com exceção das instruções TRY...CATCH.  
  
-   Instruções DECLARE que definem variáveis de dados locais e cursores locais.  
  
-   Instruções SELECT que contêm listas de seleção com expressões que atribuem valores a variáveis locais.  
  
-   Operações de cursor que fazem referência a cursores locais que são declaradas, abertas, fechadas e desalocadas na função. Apenas instruções FETCH que atribuem valores a variáveis locais usando a cláusula INTO são permitidas. Instruções FETCH que retornam dados ao cliente não são permitidas.  
  
-   Instruções INSERT, UPDATE e DELETE que modificam variáveis de tabela locais.  
  
-   Instruções EXECUTE que chamam procedimentos armazenados estendidos.  
  
-   Para obter mais informações, consulte [Criar funções definidas pelo usuário &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/user-defined-functions/create-user-defined-functions-database-engine.md).  
  
### <a name="computed-column-interoperability"></a>Interoperabilidade de colunas computadas  
 As funções têm as seguintes propriedades. Os valores dessas propriedades determinam se as funções podem ser usadas em colunas computadas que podem ser persistidas ou indexadas.  
  
|Propriedade|Descrição|Observações|  
|--------------|-----------------|-----------|  
|**IsDeterministic**|A função é determinística ou não determinística.|O acesso a dados locais é permitido em funções determinísticas. Por exemplo, funções que sempre retornam o mesmo resultado quando são chamadas com o uso de um conjunto específico de valores de entrada e com o mesmo estado do banco de dados são rotuladas como determinísticas.|  
|**IsPrecise**|A função é precisa ou imprecisa.|As funções imprecisas contêm operações, como operações de ponto flutuante.|  
|**IsSystemVerified**|As propriedades de precisão e determinismo da função podem ser verificadas pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].||  
|**SystemDataAccess**|A função acessa dados do sistema (catálogos ou tabelas virtuais do sistema) na instância local do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].||  
|**UserDataAccess**|A função acessa dados de usuário na instância local do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|Inclui tabelas definidas pelo usuário e tabelas temporárias, mas não variáveis de tabela.|  
  
 As propriedades de precisão e determinismo de funções [!INCLUDE[tsql](../../includes/tsql-md.md)] são automaticamente determinadas pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O acesso a dados e as propriedades de determinismo de funções CLR podem ser especificadas pelo usuário. Para obter mais informações, consulte [Visão geral dos atributos personalizados da integração de CLR](http://msdn.microsoft.com/library/ecf5c097-0972-48e2-a9c0-b695b7dd2820).  
  
 Para exibir os valores atuais dessas propriedades, use [OBJECTPROPERTYEX](../../t-sql/functions/objectpropertyex-transact-sql.md).  
  
 As funções devem ser criadas com a associação de esquema para serem determinísticas.  
  
 Uma coluna computada que invoca uma função definida pelo usuário pode ser usada em um índice quando a função definida pelo usuário tem os seguintes valores de propriedades:  
  
-   **IsDeterministic** = true  
  
-   **IsSystemVerified** = true (a menos que a coluna computada seja persistida)  
  
-   **UserDataAccess** = false  
  
-   **SystemDataAccess** = false  
  
 Para obter mais informações, consulte [Indexes on Computed Columns](../../relational-databases/indexes/indexes-on-computed-columns.md).  
  
### <a name="calling-extended-stored-procedures-from-functions"></a>Chamando procedimentos armazenados estendidos de funções  
 O procedimento armazenado estendido, quando chamado de dentro de uma função, não pode retornar conjuntos de resultados ao cliente. Quaisquer APIs ODS que retornam conjuntos de resultados ao cliente retornarão FAIL. O procedimento armazenado estendido pode conectar-se novamente a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. No entanto, ele não deve tentar unir a mesma transação como a função que invocou o procedimento armazenado estendido.  
  
 Semelhante a invocações de um procedimento armazenado ou em lotes, o procedimento armazenado estendido será executado no contexto da conta de segurança do Windows sob a qual o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está em execução. O proprietário do procedimento armazenado deve considerar isso ao fornecer permissão EXECUTE para usuários no procedimento.  
  
## <a name="limitations-and-restrictions"></a>Limitações e restrições  
 Funções definidas pelo usuário não podem ser usadas para executar ações que modificam o estado do banco de dados.  
  
 As funções definidas pelo usuário não podem conter uma cláusula OUTPUT INTO que tenha uma tabela como seu destino.  
  
 As seguintes instruções do [!INCLUDE[ssSB](../../includes/sssb-md.md)] não podem ser incluídas na definição de uma função [!INCLUDE[tsql](../../includes/tsql-md.md)] definida pelo usuário:  
  
-   BEGIN DIALOG CONVERSATION  
  
-   END CONVERSATION  
  
-   GET CONVERSATION GROUP  
  
-   MOVE CONVERSATION  
  
-   RECEIVE  
  
-   SEND  
  
 Funções definidas pelo usuário podem ser aninhadas, isto é, uma função definida pelo usuário pode chamar outra. O nível de aninhamento é incrementado quando a execução da função é iniciada, e reduzido quando a execução da função chamada é concluída. Até 32 níveis de funções definidas pelo usuário podem ser aninhados. Se o máximo de níveis de aninhamento for excedido haverá falha em toda a cadeia de funções da chamada de aninhamento. Qualquer referência a um código gerenciado de uma função definida pelo usuário do [!INCLUDE[tsql](../../includes/tsql-md.md)] é contada como um nível em relação ao limite de 32 níveis de aninhamento. Os métodos invocados a partir do código gerenciado não são contados em relação a esse limite.  
  
### <a name="using-sort-order-in-clr-table-valued-functions"></a>Usando a ordem de classificação em funções CLR com valor de tabela  
 Ao usar a cláusula ORDER em funções CLR com valor de tabela, siga estas diretrizes:  
  
-   Você deve garantir que os resultados sejam sempre ordenados na ordem especificada. Se os resultados não estiverem na ordem especificada, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gerará uma mensagem de erro quando a consulta for executada.  
  
-   Se uma cláusula ORDER estiver especificada, a saída da função com valor de tabela deverá ser ordenada de acordo com o agrupamento da coluna (explícito ou implícito). Por exemplo, se o agrupamento da coluna for chinês (especificado no DDL para a função com valor de tabela ou obtido do agrupamento do banco de dados), os resultados retornados deverão ser ordenados de acordo com as regras de classificação do chinês.  
  
-   A cláusula ORDER, se especificada, é sempre verificada pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ao retornar resultados, quer ela seja usada ou não pelo processador de consultas para executar otimizações adicionais. Use a cláusula ORDER apenas se você souber que ela é útil para o processador de consultas.  
  
-   O processador de consultas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] beneficia-se automaticamente da cláusula ORDER nos seguintes casos:  
  
    -   Consultas de inserção em que a cláusula ORDER é compatível com um índice.  
  
    -   Cláusulas ORDER BY que são compatíveis com a cláusula ORDER.  
  
    -   Agregações, em que GROUP BY é compatível com a cláusula ORDER.  
  
    -   Agregações DISTINCT em que as colunas distintas são compatíveis com a cláusula ORDER.  
  
 A cláusula ORDER não garante resultados ordenados quando uma consulta SELECT é executada, a menos que ORDER BY também esteja especificado na consulta. Consulte [sys.function_order_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-function-order-columns-transact-sql.md) para obter informações sobre como consultar colunas incluídas na ordem de classificação nas funções com valor de tabela.  
  
## <a name="metadata"></a>Metadados  
 A tabela a seguir lista as exibições do catálogo do sistema que você pode usar para retornar metadados sobre funções definidas pelo usuário.  
  
|Exibição do sistema|Descrição|  
|-----------------|-----------------|  
|[sys.sql_modules](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)|Veja o exemplo E na seção Exemplos abaixo.|  
|[sys.assembly_modules](../../relational-databases/system-catalog-views/sys-assembly-modules-transact-sql.md)|Exibe informações sobre funções CLR definidas pelo usuário.|  
|[sys.parameters](../../relational-databases/system-catalog-views/sys-parameters-transact-sql.md)|Exibe informações sobre os parâmetros definidos em funções definidas pelo usuário.|  
|[sys.sql_expression_dependencies](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md)|Exibe os objetos subjacentes referenciados por uma função.|  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão CREATE FUNCTION no banco de dados e a permissão ALTER no esquema no qual a função está sendo criada. Se a função especificar um tipo definido pelo usuário, a permissão EXECUTE será exigida no tipo.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-using-a-scalar-valued-user-defined-function-that-calculates-the-iso-week"></a>A. Usando uma função definida pelo usuário com valor escalar que calcula a semana ISO  
 O exemplo a seguir cria a função definida pelo usuário `ISOweek`. Essa função usa um argumento de data e calcula o número da semana ISO. Para que essa função calcule corretamente, `SET DATEFIRST 1` deve ser invocado antes da função ser chamada.  
  
 O exemplo também mostra como usar a cláusula [EXECUTE AS](../../t-sql/statements/execute-as-clause-transact-sql.md) para especificar o contexto de segurança no qual um procedimento armazenado pode ser executado. No exemplo, a opção `CALLER` especifica que o procedimento será executado no contexto do usuário que o chama. As outras opções que podem ser especificadas são SELF, OWNER e *user_name*.  
  
 Esta é a chamada da função. Observe que `DATEFIRST` está definido como `1`.  
  
```sql
CREATE FUNCTION dbo.ISOweek (@DATE datetime)  
RETURNS int  
WITH EXECUTE AS CALLER  
AS  
BEGIN  
     DECLARE @ISOweek int;  
     SET @ISOweek= DATEPART(wk,@DATE)+1  
          -DATEPART(wk,CAST(DATEPART(yy,@DATE) as CHAR(4))+'0104');  
--Special cases: Jan 1-3 may belong to the previous year  
     IF (@ISOweek=0)   
          SET @ISOweek=dbo.ISOweek(CAST(DATEPART(yy,@DATE)-1   
               AS CHAR(4))+'12'+ CAST(24+DATEPART(DAY,@DATE) AS CHAR(2)))+1;  
--Special case: Dec 29-31 may belong to the next year  
     IF ((DATEPART(mm,@DATE)=12) AND   
          ((DATEPART(dd,@DATE)-DATEPART(dw,@DATE))>= 28))  
          SET @ISOweek=1;  
     RETURN(@ISOweek);  
END;  
GO  
SET DATEFIRST 1;  
SELECT dbo.ISOweek(CONVERT(DATETIME,'12/26/2004',101)) AS 'ISO Week';  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
``` 
ISO Week  
----------------  
52  
```  
  
### <a name="b-creating-an-inline-table-valued-function"></a>B. Criando uma função com valor de tabela embutida  
 O exemplo a seguir retorna uma função com valor de tabela embutida no banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]. Ela retorna três colunas `ProductID`, `Name` e a agregação dos totais acumulados no ano por loja como `YTD Total` para cada produto vendido para a loja.  
  
```sql  
CREATE FUNCTION Sales.ufn_SalesByStore (@storeid int)  
RETURNS TABLE  
AS  
RETURN   
(  
    SELECT P.ProductID, P.Name, SUM(SD.LineTotal) AS 'Total'  
    FROM Production.Product AS P   
    JOIN Sales.SalesOrderDetail AS SD ON SD.ProductID = P.ProductID  
    JOIN Sales.SalesOrderHeader AS SH ON SH.SalesOrderID = SD.SalesOrderID  
    JOIN Sales.Customer AS C ON SH.CustomerID = C.CustomerID  
    WHERE C.StoreID = @storeid  
    GROUP BY P.ProductID, P.Name  
);  
GO  
```

 Para invocar a função, execute esta consulta.    

```sql  
SELECT * FROM Sales.ufn_SalesByStore (602);  
```  
  
### <a name="c-creating-a-multi-statement-table-valued-function"></a>C. Criando uma função com valor de tabela de várias instruções  
 O exemplo a seguir cria a função com valor de tabela `fn_FindReports(InEmpID)` no banco de dados AdventureWorks2012. Quando fornecida com uma ID de funcionário válida, a função retorna uma tabela que corresponde a todos os funcionários subordinados ao funcionário direta ou indiretamente. A função usa uma CTE (expressão de tabela comum) recursiva para produzir a lista hierárquica de funcionários. Para obter mais informações sobre CTEs recursivas, consulte [WITH common_table_expression &#40;Transact-SQL&#41;](../../t-sql/queries/with-common-table-expression-transact-sql.md).  
  
```sql  
CREATE FUNCTION dbo.ufn_FindReports (@InEmpID INTEGER)  
RETURNS @retFindReports TABLE   
(  
    EmployeeID int primary key NOT NULL,  
    FirstName nvarchar(255) NOT NULL,  
    LastName nvarchar(255) NOT NULL,  
    JobTitle nvarchar(50) NOT NULL,  
    RecursionLevel int NOT NULL  
)  
--Returns a result set that lists all the employees who report to the   
--specific employee directly or indirectly.*/  
AS  
BEGIN  
WITH EMP_cte(EmployeeID, OrganizationNode, FirstName, LastName, JobTitle, RecursionLevel) -- CTE name and columns  
    AS (  
        -- Get the initial list of Employees for Manager n
        SELECT e.BusinessEntityID, e.OrganizationNode, p.FirstName, p.LastName, e.JobTitle, 0   
        FROM HumanResources.Employee e   
INNER JOIN Person.Person p   
ON p.BusinessEntityID = e.BusinessEntityID  
        WHERE e.BusinessEntityID = @InEmpID  
        UNION ALL  
        -- Join recursive member to anchor
        SELECT e.BusinessEntityID, e.OrganizationNode, p.FirstName, p.LastName, e.JobTitle, RecursionLevel + 1   
        FROM HumanResources.Employee e   
            INNER JOIN EMP_cte  
            ON e.OrganizationNode.GetAncestor(1) = EMP_cte.OrganizationNode  
INNER JOIN Person.Person p   
ON p.BusinessEntityID = e.BusinessEntityID  
        )  
-- copy the required columns to the result of the function   
   INSERT @retFindReports  
   SELECT EmployeeID, FirstName, LastName, JobTitle, RecursionLevel  
   FROM EMP_cte   
   RETURN  
END;  
GO  
-- Example invocation  
SELECT EmployeeID, FirstName, LastName, JobTitle, RecursionLevel  
FROM dbo.ufn_FindReports(1);   
  
GO  
```  
  
### <a name="d-creating-a-clr-function"></a>D. Criando uma função CLR  
 O exemplo cria a função CLR `len_s`. Antes que a função seja criada, o assembly `SurrogateStringFunction.dll` é registrado no banco de dados local.  
  
**Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
```sql  
DECLARE @SamplesPath nvarchar(1024);  
-- You may have to modify the value of this variable if you have  
-- installed the sample in a location other than the default location.  
SELECT @SamplesPath = REPLACE(physical_name, 'Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\DATA\master.mdf', 
                                              'Microsoft SQL Server\130\Samples\Engine\Programmability\CLR\')   
    FROM master.sys.database_files   
    WHERE name = 'master';  
  
CREATE ASSEMBLY [SurrogateStringFunction]  
FROM @SamplesPath + 'StringManipulate\CS\StringManipulate\bin\debug\SurrogateStringFunction.dll'  
WITH PERMISSION_SET = EXTERNAL_ACCESS;  
GO  
  
CREATE FUNCTION [dbo].[len_s] (@str nvarchar(4000))  
RETURNS bigint  
AS EXTERNAL NAME [SurrogateStringFunction].[Microsoft.Samples.SqlServer.SurrogateStringFunction].[LenS];  
GO  
```  
  
 Para obter um exemplo de como criar um função com valor de tabela CLR, consulte [Funções com valor de tabela CLR](../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-table-valued-functions.md).  
  
### <a name="e-displaying-the-definition-of-includetsqlincludestsql-mdmd-user-defined-functions"></a>E. Exibindo a definição de funções definidas pelo usuário [!INCLUDE[tsql](../../includes/tsql-md.md)]  
  
```sql  
SELECT definition, type   
FROM sys.sql_modules AS m  
JOIN sys.objects AS o ON m.object_id = o.object_id   
    AND type IN ('FN', 'IF', 'TF');  
GO  
```  
  
 A definição de funções criadas com a opção ENCRYPTION não pode ser exibida usando sys.sql_modules; no entanto, outras informações sobre as funções criptografadas são exibidas.  
  
## <a name="see-also"></a>Consulte Também  
 [ALTER FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-function-transact-sql.md)   
 [DROP FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/drop-function-transact-sql.md)   
 [OBJECTPROPERTYEX &#40;Transact-SQL&#41;](../../t-sql/functions/objectpropertyex-transact-sql.md)   
 [sys.sql_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)   
 [sys.assembly_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-assembly-modules-transact-sql.md)   
 [EXECUTE &#40;Transact-SQL&#41;](../../t-sql/language-elements/execute-transact-sql.md)   
 [Funções CLR definidas pelo usuário](../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-user-defined-functions.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [CREATE SECURITY POLICY &#40;Transact-SQL&#41;](../../t-sql/statements/create-security-policy-transact-sql.md)  
  
 

