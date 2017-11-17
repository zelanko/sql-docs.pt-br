---
title: EXECUTE (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/07/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- EXEC
- EXECUTE_TSQL
- EXECUTE
- EXEC_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- remote stored procedures [SQL Server]
- command strings [SQL Server]
- extended stored procedures [SQL Server], executing
- stored procedures [SQL Server], executing
- Transact-SQL statements, executing
- strings [SQL Server], executing
- statements [SQL Server], executing
- context switching [SQL Server], execution context
- user-defined functions [SQL Server], executing
- character strings [SQL Server], executing
- switching execution context
- EXECUTE statement
ms.assetid: bc806b71-cc55-470a-913e-c5f761d5c4b7
caps.latest.revision: 104
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: aecf422ca2289b2a417147eb402921bb8530d969
ms.openlocfilehash: 67a2880a573a1b0ff0f1e9a56216ebe8c60ddaf5
ms.contentlocale: pt-br
ms.lasthandoff: 10/24/2017

---
# <a name="execute-transact-sql"></a>EXECUTE-o Transact-SQL
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Executa uma cadeia de caracteres de comando ou de cadeia de caracteres dentro de um [!INCLUDE[tsql](../../includes/tsql-md.md)] lote ou um dos seguintes módulos: sistema armazenados procedimento, o procedimento armazenado definido pelo usuário, o procedimento armazenado CLR, função definida pelo usuário de valor escalar ou procedimento armazenado estendido. A instrução EXECUTE pode ser usada para enviar comandos de passagem aos servidores vinculados. Além disso, o contexto no qual uma cadeia de caracteres ou comando é executado pode ser definido explicitamente. É possível definir metadados para o conjunto de resultados usando as opções do WITH RESULT SETS.
  
> [!IMPORTANT]  
>  Antes de chamar EXECUTE com uma cadeia de caracteres, valide a cadeia de caracteres. Nunca execute um comando construído por uma entrada de usuário que não foi validada.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
-- Syntax for SQL Server  
  
Execute a stored procedure or function  
[ { EXEC | EXECUTE } ]  
    {   
      [ @return_status = ]  
      { module_name [ ;number ] | @module_name_var }   
        [ [ @parameter = ] { value   
                           | @variable [ OUTPUT ]   
                           | [ DEFAULT ]   
                           }  
        ]  
      [ ,...n ]  
      [ WITH <execute_option> [ ,...n ] ]  
    }  
[;]  
  
Execute a character string  
{ EXEC | EXECUTE }   
    ( { @string_variable | [ N ]'tsql_string' } [ + ...n ] )  
    [ AS { LOGIN | USER } = ' name ' ]  
[;]  
  
Execute a pass-through command against a linked server  
{ EXEC | EXECUTE }  
    ( { @string_variable | [ N ] 'command_string [ ? ]' } [ + ...n ]  
        [ { , { value | @variable [ OUTPUT ] } } [ ...n ] ]  
    )   
    [ AS { LOGIN | USER } = ' name ' ]  
    [ AT linked_server_name ]  
[;]  
  
<execute_option>::=  
{  
        RECOMPILE   
    | { RESULT SETS UNDEFINED }   
    | { RESULT SETS NONE }   
    | { RESULT SETS ( <result_sets_definition> [,...n ] ) }  
}   
  
<result_sets_definition> ::=   
{  
    (  
         { column_name   
           data_type   
         [ COLLATE collation_name ]   
         [ NULL | NOT NULL ] }  
         [,...n ]  
    )  
    | AS OBJECT   
        [ db_name . [ schema_name ] . | schema_name . ]   
        {table_name | view_name | table_valued_function_name }  
    | AS TYPE [ schema_name.]table_type_name  
    | AS FOR XML   
}  
```  
  
```  
-- In-Memory OLTP   

Execute a natively compiled, scalar user-defined function  
[ { EXEC | EXECUTE } ]   
    {   
      [ @return_status = ]   
      { module_name | @module_name_var }   
        [ [ @parameter = ] { value   
                           | @variable   
                           | [ DEFAULT ]   
                           }  
        ]   
      [ ,...n ]   
      [ WITH <execute_option> [ ,...n ] ]   
    }  
<execute_option>::=  
{  
    | { RESULT SETS UNDEFINED }   
    | { RESULT SETS NONE }   
    | { RESULT SETS ( <result_sets_definition> [,...n ] ) }  
}  
```  
  
```  
-- Syntax for Azure SQL Database   
  
Execute a stored procedure or function  
[ { EXEC | EXECUTE } ]  
    {   
      [ @return_status = ]  
      { module_name  | @module_name_var }   
        [ [ @parameter = ] { value   
                           | @variable [ OUTPUT ]   
                           | [ DEFAULT ]   
                           }  
        ]  
      [ ,...n ]  
      [ WITH RECOMPILE ]  
    }  
[;]  
  
Execute a character string  
{ EXEC | EXECUTE }   
    ( { @string_variable | [ N ]'tsql_string' } [ + ...n ] )  
    [ AS {  USER } = ' name ' ]  
[;]  
  
<execute_option>::=  
{  
        RECOMPILE   
    | { RESULT SETS UNDEFINED }   
    | { RESULT SETS NONE }   
    | { RESULT SETS ( <result_sets_definition> [,...n ] ) }  
}   
  
<result_sets_definition> ::=   
{  
    (  
         { column_name   
           data_type   
         [ COLLATE collation_name ]   
         [ NULL | NOT NULL ] }  
         [,...n ]  
    )  
    | AS OBJECT   
        [ db_name . [ schema_name ] . | schema_name . ]   
        {table_name | view_name | table_valued_function_name }  
    | AS TYPE [ schema_name.]table_type_name  
    | AS FOR XML  
  
```  
  
```tsql  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  

-- Execute a stored procedure  
[ { EXEC | EXECUTE } ]  
    procedure_name   
        [ { value | @variable [ OUT | OUTPUT ] } ] [ ,...n ] }  
[;]  
  
-- Execute a SQL string  
{ EXEC | EXECUTE }  
    ( { @string_variable | [ N ] 'tsql_string' } [ +...n ] )  
[;]  
```  
  
## <a name="arguments"></a>Argumentos  
 @*return_status*  
 É uma variável de inteiro opcional que armazena o status de retorno de um módulo. Essa variável deve ser declarada no lote, procedimento armazenado ou função para ser usada antes em uma instrução EXECUTE.  
  
 Quando usado para invocar uma função valor escalar definida pelo usuário, o @*return_status* variável pode ser de qualquer tipo de dados escalares.  
  
 *nome_de_módulo*  
 É o nome totalmente qualificado do procedimento armazenado ou do valor escalar da função a ser chamada, definida pelo usuário. Nomes de módulo devem estar em conformidade com as regras de [identificadores](../../relational-databases/databases/database-identifiers.md). Os nomes de procedimentos armazenados estendidos sempre têm diferenciação entre maiúsculas e minúsculas, independentemente do agrupamento do servidor.  
  
 Um módulo que tenha sido criado em outro banco de dados poderá ser executado se o usuário que estiver executando o módulo for o proprietário ou se tiver permissão apropriada para executá-lo no referido banco de dados. Um módulo poderá ser executado em outro servidor que executa [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se o usuário que estiver executando o módulo tiver a permissão apropriada para usar esse servidor (acesso remoto) e executar o módulo no referido banco de dados. Se você especificar um nome de servidor mas não especificar um nome de banco de dados, o [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] procurará o módulo no banco de dados padrão do usuário.  
  
 ; *número*  
**Aplica-se a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] por meio de[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
 É um inteiro opcional usado para agrupar procedimentos do mesmo nome. Esse parâmetro não é usado para procedimentos armazenados estendidos.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
 Para obter mais informações sobre grupos de procedimentos, consulte [CREATE PROCEDURE &#40; Transact-SQL &#41; ](../../t-sql/statements/create-procedure-transact-sql.md).  
  
 @*module_name_var*  
 É o nome de uma variável localmente definida que representa um nome de módulo.  
  
 Isso pode ser uma variável que contém o nome de uma função definida pelo usuário escalares.  
  
 @*parâmetro*  
 É o parâmetro para *nome_de_módulo*, conforme definido no módulo. Os nomes de parâmetro devem ser precedidos pelo sinal de arroba (@). Quando usado com o @*parameter_name*=*valor* formulário, os nomes de parâmetro e constantes não precisam ser fornecidos na ordem em que eles são definidos no módulo. No entanto, se a @*parameter_name*=*valor* formulário é usado para qualquer parâmetro, ele deve ser usado para todos os parâmetros subsequentes.  
  
 Por padrão, os parâmetros são anuláveis.  
  
 *value*  
 É o valor do parâmetro a ser informado ao módulo ou comando de passagem. Se não forem especificados nomes de parâmetro, os valores de parâmetro deverão ser fornecidos na ordem definida no módulo.  
  
 Na execução dos comandos de passagem em servidores vinculados, a ordem dos valores de parâmetro dependerá do provedor OLE DB do servidor vinculado. A maioria dos provedores OLE DB associa valores para os parâmetros da esquerda para a direita.  
  
 Se o valor de um parâmetro for o nome de um objeto, cadeia de caracteres ou qualificado por um nome de esquema ou nome de banco de dados, o nome todo deverá ficar dentro de aspas simples. Se o valor de um parâmetro for uma palavra-chave, a palavra-chave deverá ficar dentro de aspas duplas.  
  
 Se um padrão estiver definido no módulo, um usuário poderá executar o módulo sem especificar um parâmetro.  
  
 O padrão também pode ser NULL. Geralmente, a definição de módulo especificará a ação a ser tomada se um valor de parâmetro for NULL.  
  
 @*variável*  
 É a variável que armazena um parâmetro ou um parâmetro de retorno.  
  
 OUTPUT  
 Especifica que o módulo ou a cadeia de caracteres de comando deve retornar um parâmetro. O parâmetro correspondente no módulo ou na cadeia de caracteres de comando também deve ter sido criado com o uso da palavra-chave OUTPUT. Use essa palavra-chave quando você usar variáveis de cursor como parâmetros.  
  
 Se *valor* é definido como OUTPUT de um módulo executado em um servidor vinculado, qualquer alteração correspondente*parâmetro* executada pelo OLE DB provider será copiada novamente para a variável no final das execução do módulo.  
  
 Se os parâmetros de saída estão sendo usados e a intenção é usar os valores de retorno em outras instruções no módulo ou lote de chamada, o valor do parâmetro deve ser passado como uma variável, como*parâmetro* = @*variável* . Não é possível executar um módulo especificando OUTPUT para um parâmetro que não esteja definido como OUTPUT no módulo. Não é possível passar constantes ao módulo usando OUTPUT; o parâmetro de retorno requer um nome de variável. O tipo de dados da variável deve ser declarado e ter um valor atribuído antes da execução do procedimento.  
  
 Quando EXECUTE é usado em um procedimento armazenado remoto ou para executar um comando de passagem em um servidor vinculado, os parâmetros OUTPUT não podem ser nenhum dos tipos de dados LOB (objeto grande).  
  
 Os parâmetros de retorno podem ser de qualquer tipo de dados, exceto os tipos de dados LOB.  
  
 DEFAULT  
 Fornece o valor padrão do parâmetro como definido no módulo. Quando o módulo esperar um valor para um parâmetro que não tem um padrão definido e houver um parâmetro ausente ou a palavra-chave DEFAULT estiver especificada, ocorrerá um erro.  
  
 @*string_variable*  
 É o nome de uma variável local. @*string_variable* pode ser qualquer **char**, **varchar**, **nchar**, ou **nvarchar** tipo de dados. Isso inclui o **(max)** tipos de dados.  
  
 [N] '*tsql_string*'  
 É uma cadeia de caracteres constante. *tsql_string* pode ser qualquer **nvarchar** ou **varchar** tipo de dados. Se N for incluído, a cadeia de caracteres será interpretada como **nvarchar** tipo de dados.  
  
 AS \<context_specification >  
 Especifica o contexto no qual a instrução é executada.  
  
 Logon  
**Aplica-se a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] por meio de[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
 Especifica que o contexto para ser representado é um logon. O escopo de personificação é o servidor.  
  
 Usuário  
 Especifica que o contexto a ser representado é um usuário no banco de dados atual. O escopo de representação é restrito ao banco de dados atual. Uma opção de contexto para um usuário de banco de dados não herda as permissões em nível de servidor desse usuário.  
  
> [!IMPORTANT]  
>  Enquanto a opção de contexto para o usuário do banco de dados estiver ativa, qualquer tentativa de acessar os recursos fora do banco de dados causará a falha da instrução. Isso inclui usar *banco de dados* instruções, consultas distribuídas e consultas que fazem referência a outro banco de dados usando identificadores em três ou quatro partes.  
  
 '*nome*'  
 É um usuário ou nome de logon válido. *nome* deve ser um membro da função de servidor fixa sysadmin ou existir como uma entidade no [database_principals](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md) ou [sys. server_principals](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md), respectivamente.  
  
 *nome* não pode ser uma conta interna, como NT AUTHORITY\LocalService, NT AUTHORITY\NetworkService ou NT authority\localsystem.  
  
 Para obter mais informações, consulte [especificando um nome de logon ou usuário](#_user) mais adiante neste tópico.  
  
 [N] '*command_string*'  
 É uma cadeia de caracteres constante que contém o comando a ser passado ao servidor vinculado. Se N for incluído, a cadeia de caracteres será interpretada como **nvarchar** tipo de dados.  
  
 [?]  
 Indica parâmetros para os quais os valores são fornecidos no \<arg-list > de comandos de passagem que são usados em um EXEC('...', \<arg-list>) em \<linkedsrv > instrução.  
  
 EM *linked_server_name*  
**Aplica-se a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] por meio de[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
 Especifica que *command_string* é executada em *linked_server_name* e resultados, se houver, são retornados ao cliente. *linked_server_name* devem se referir a uma definição de servidor vinculado existente no servidor local. Servidores vinculados são definidos usando [sp_addlinkedserver](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md).  
  
 COM \<execute_option >  
 Opções de execução possíveis. As opções de RESULT SETS não podem ser especificadas em uma instrução INSERT.EXEC.  
  
|Termo|Definição|  
|----------|----------------|  
|RECOMPILE|Força a compilação, a utilização e o descarte de um novo plano após a execução do módulo. Se houver um plano de consulta existente para o módulo, esse plano permanecerá no cache.<br /><br /> Use essa opção se o parâmetro sendo fornecido for atípico ou se os dados tiverem sido alterados significativamente. Ela não é usada para procedimentos armazenados estendidos. É aconselhável usar essa opção se realmente for necessário porque ela é expansiva.<br /><br /> **Observação:** não é possível usar WITH RECOMPILE ao chamar um procedimento armazenado que usa a sintaxe OPENDATASOURCE. A opção WITH RECOMPILE será ignorada quando um nome de objeto de quatro partes for especificado.<br /><br /> **Observação:** RECOMPILE não é suportado com funções escalares definidas pelo usuário. Se você precisar recompilar, use [sp_recompile &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/sp-recompile-transact-sql.md).|  
|**CONJUNTOS DE RESULTADOS INDEFINIDOS**|**Aplica-se a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] por meio de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].<br /><br /> Esta opção não fornece nenhuma garantia de quais resultados, se houver, serão retornados. Além disso, não é fornecida nenhuma definição. A instrução é executada sem erro se algum resultado for retornado ou se nenhum resultado for retornado. RESULT SETS UNDEFINED será o comportamento padrão se não for fornecido result_sets_option.<br /><br /> Para interpretada funções escalares definidas pelo usuário e compiladas nativamente funções escalares definidas pelo usuário, essa opção não está operacional porque as funções não retornam um conjunto de resultados.|  
|RESULT SETS NONE|**Aplica-se a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] por meio de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].<br /><br /> Garante que a instrução execute não retornará nenhum resultado. Se algum resultado for retornado, o lote será anulado.<br /><br /> Para interpretada funções escalares definidas pelo usuário e compiladas nativamente funções escalares definidas pelo usuário, essa opção não está operacional porque as funções não retornam um conjunto de resultados.|  
|*\<result_sets_definition >*|**Aplica-se a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] por meio de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].<br /><br /> Fornece uma garantia de que o resultado voltará como especificado em result_sets_definition. Para instruções que retornam vários conjuntos de resultados, forneça várias *result_sets_definition* seções. Inclua cada *result_sets_definition* entre parênteses, separados por vírgulas. Para obter mais informações, consulte \<result_sets_definition > mais adiante neste tópico.<br /><br /> Essa opção sempre resulta em um erro para funções escalares definidas pelo usuário porque as funções não retornam um conjunto de resultados.|
  
\<result_sets_definition > **aplica-se a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] por meio de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)],[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]
  
 Descreve os conjuntos de resultados retornados pelas instruções executadas. As cláusulas de result_sets_definition têm o seguinte significado  
  
|Termo|Definição|  
|----------|----------------|  
|{<br /><br /> column_name<br /><br /> data_type<br /><br /> [ COLLATE collation_name]<br /><br /> [NULL &#124; NÃO NULO]<br /><br /> }|Consulte a tabela a seguir.|  
|db_name|O nome do banco de dados que contém a tabela, a exibição ou a função com valor de tabela.|  
|schema_name|O nome do esquema proprietário da tabela, da exibição ou da função com valor de tabela.|  
|table_name &#124; view_name &#124; table_valued_function_name|Especifica que as colunas retornadas serão as especificadas na tabela, exibição ou função com valor de tabela nomeada. Não há suporte para variáveis de tabela, tabelas temporárias e sinônimos na sintaxe de objetos do AS.|  
|AS TYPE [schema_name.]table_type_name|Especifica que as colunas retornadas serão as especificadas no tipo de tabela.|  
|AS FOR XML|Especifica que os resultados XML da instrução ou procedimento armazenado chamado pela instrução EXECUTE serão convertidos no formato como se fossem gerados por uma instrução SELECT … FOR XML … . Toda a formatação das políticas do tipo na instrução original é removida, e os resultados são retornados como se nenhuma política do tipo fosse especificada. AS FOR XML não converte em XML os resultados de tabela não XML da instrução executada ou do procedimento armazenado.|  
  
|Termo|Definição|  
|----------|----------------|  
|column_name|Os nomes de cada coluna. Se o número de colunas for diferente do conjunto de resultados, ocorrerá um erro e o lote será anulado. Se o nome de uma coluna for diferente do conjunto de resultados, o nome de coluna retornado será definido como o nome definido.|  
|data_type|Os tipos de dados de cada coluna. Se os tipos de dados forem diferentes, será executada uma conversão implícita para o tipo de dados definido. Se a conversão falhar, o lote será anulado|  
|COLLATE collation_name|O agrupamento de cada coluna. Se houver uma incompatibilidade de agrupamento, será tentado um agrupamento implícito. Se isso falhar, o lote será anulado.|  
|NULL &#124; NÃO NULO|A nulidade de cada coluna. Se a nulidade definida for NOT NULL e os dados retornados contiver NULLs, ocorrerá um erro e o lote será anulado. Se não especificado, o valor padrão se conforma à configuração das opções do ANSI_NULL_DFLT_ON e ANSI_NULL_DFLT_OFF.|  
  
 O conjunto de resultados real retornado durante execução pode diferir do resultado definido usando a cláusula WITH RESULT SETS de uma das seguintes maneiras: número de conjuntos de resultados, número de colunas, nome de coluna, nulidade e tipo de dados. Se o número de conjuntos de resultados for diferente, ocorrerá um erro e o lote será anulado.  
  
## <a name="remarks"></a>Comentários  
 Os parâmetros podem ser fornecidos usando *valor* ou usando*parameter_name*=*valor.* . Um parâmetro não faz parte de uma transação; portanto, se um parâmetro for alterado em uma transação que for posteriormente revertida, o parâmetro não será revertido para seu valor anterior. O valor retornado ao chamador será sempre o valor no momento do retorno do módulo.  
  
 O aninhamento ocorre quando um módulo chama outro ou executa código gerenciado, fazendo referência a um módulo CLR (Common Language Runtime) a um tipo definido pelo usuário ou agregação. O nível de aninhamento é aumentado quando o módulo chamado ou a referência de código gerenciado inicia a execução e diminuído quando ela termina. Exceder o máximo de 32 níveis de aninhamento faz com que toda a cadeia de chamada falhe. O nível de aninhamento atual é armazenado no @@NESTLEVEL função do sistema.  
  
 Como os procedimentos armazenados remotos e estendidos não estão no escopo de uma transação (a menos que emitidos em uma instrução BEGIN DISTRIBUTED TRANSACTION ou quando usados com várias opções de configuração), os comandos executados por meio de chamadas a eles não poderão ser revertidos. Para obter mais informações, consulte [procedimentos armazenados do sistema &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md) e [iniciar transação DISTRIBUÍDA &#40; Transact-SQL &#41; ](../../t-sql/language-elements/begin-distributed-transaction-transact-sql.md).  
  
 Ao utilizar variáveis de cursor, se você executar um procedimento que passe em uma variável de cursor com um cursor alocado a ele, ocorrerá um erro.  
  
 Não é necessário especificar a palavra-chave EXECUTE durante a execução de módulos se a instrução for a primeira em um lote.  
  
 Para obter informações adicionais específicas de procedimentos armazenados CLR, consulte Procedimentos armazenados CLR.  
  
## <a name="using-execute-with-stored-procedures"></a>Usando EXECUTE com procedimentos armazenados  
 Não será preciso especificar a palavra-chave EXECUTE durante a execução de procedimentos armazenados quando a instrução for a primeira em um lote.  
  
 Procedimentos armazenados do sistema [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] iniciam com os caracteres sp_. Eles são armazenados fisicamente no [banco de dados do recurso](../../relational-databases/databases/resource-database.md), mas aparecem logicamente no esquema sys de cada sistema e banco de dados definido pelo usuário. Quando você executa um procedimento armazenado de sistema, em um lote ou dentro de um módulo, como a função ou o procedimento armazenado definido pelo usuário, recomendamos qualificar o nome do procedimento armazenado com o nome do esquema sys.  
  
 Os procedimentos armazenados estendidos de sistema [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] iniciam com os caracteres xp_ e estão contidos no esquema dbo do banco de dados mestre. Quando você executa um procedimento armazenado estendido de sistema, em um lote ou dentro de um módulo, como a função ou o procedimento armazenado definido pelo usuário, recomendamos qualificar o nome do procedimento armazenado com master.dbo.  
  
 Quando você executa um procedimento definido pelo usuário, em um lote ou dentro de um módulo, como a função ou o procedimento armazenado definido pelo usuário, recomendamos qualificar o nome do procedimento armazenado com um nome de esquema. Não recomendamos nomear um procedimento armazenado definido pelo usuário com o mesmo nome de uma procedimento armazenado no sistema. Para obter mais informações sobre a execução de procedimentos armazenados, consulte [executar um procedimento armazenado](../../relational-databases/stored-procedures/execute-a-stored-procedure.md).  
  
## <a name="using-execute-with-a-character-string"></a>Usando EXECUTE com uma cadeia de caracteres  
 Em versões anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], as cadeias de caracteres estão limitadas a 8.000 bytes. Isso requer a concatenação de cadeias de caracteres grandes para execução dinâmica. Em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o **varchar (max)** e **nvarchar (max)** tipos de dados podem ser especificados que permitem de cadeias de caracteres a ser até 2 gigabytes de dados.  
  
 As alterações no contexto de banco de dados duram apenas até o fim da instrução EXECUTE. Por exemplo, depois que `EXEC` na instrução seguinte é executado, o contexto de banco de dados se torna o mestre.  
  
```tsql  
USE master; EXEC ('USE AdventureWorks2012; SELECT BusinessEntityID, JobTitle FROM HumanResources.Employee;');  
```  
  
## <a name="context-switching"></a>Alternância de contexto  
 Você pode usar a cláusula `AS { LOGIN | USER } = ' name '` para alternar o contexto de execução de uma instrução dinâmica. Quando a alternância de contexto for especificada como `EXECUTE ('string') AS <context_specification>`, a duração dessa alternância estará limitada ao escopo da consulta sendo executada.  
  
###  <a name="_user"></a>Especificando um nome de logon ou usuário  
 O nome de logon ou de usuário especificado em `AS { LOGIN | USER } = ' name '` deve existir como principal em sys.database_principals ou sys.server_principals, respectivamente, ou a instrução falhará. Além disso, as permissões IMPERSONATE devem ser concedidas na entidade de segurança. A menos que o chamador seja o proprietário do banco de dados ou membro da função de servidor fixa sysadmin, o principal deverá existir quando o usuário estiver acessando o banco de dados ou a instância de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] por meio de uma associação de grupo do Windows. Por exemplo, considere as seguintes condições:  
  
-   O grupo CompanyDomain\SQLUsers tem acesso ao banco de dados de vendas.  
  
-   CompanyDomain\SqlUser1 é membro de SQLUsers e, por isso, tem acesso implícito ao banco de dados de vendas.  
  
 Embora CompanyDomain\SqlUser1 tenha acesso ao banco de dados por meio de associação no SQLUsers grupo, a instrução `EXECUTE @string_variable AS USER = 'CompanyDomain\SqlUser1'` falhará porque `CompanyDomain\SqlUser1` não existe como uma entidade de segurança no banco de dados.  
  
### <a name="best-practices"></a>Práticas recomendadas  
 Especifique um logon ou um usuário que tenha os privilégios mínimos necessários para executar as operações definidas na instrução ou módulo. Por exemplo, não especifique um nome de logon que tenha permissões em nível de servidor se apenas as permissões em nível de banco de dados forem necessárias; ou não especifique uma conta de proprietário de banco de dados, a menos que essas permissões sejam solicitadas.  
  
## <a name="permissions"></a>Permissões  
 Não são solicitadas permissões para executar a instrução EXECUTE. Porém, são solicitadas permissões nos protegíveis mencionados na cadeia de caracteres EXECUTE. Por exemplo, se a cadeia de caracteres tiver uma instrução INSERT, o chamador da instrução EXECUTE deverá ter a permissão INSERT na tabela de destino. As permissões são verificadas quando a instrução EXECUTE for encontrada, mesmo se ela estiver incluída em um módulo.  
  
 As permissões EXECUTE de um padrão de módulo para o proprietário do módulo, que pode transferi-las a outros usuários. Quando um módulo que executa uma cadeia de caracteres é executado, as permissões são verificadas no contexto do usuário que executa o módulo e não no contexto do usuário que o criou. Entretanto, se o mesmo usuário for proprietário do módulo chamador e do módulo sendo chamado, a verificação da permissão EXECUTE não será feita para o segundo módulo.  
  
 Se o módulo acessar outros objetos de banco de dados, a execução ocorrerá quando a permissão EXECUTE estiver no módulo e uma das seguintes condições for verdadeira:  
  
-   O módulo está marcado como EXECUTE AS USER ou SELF, e o seu proprietário tem as permissões correspondentes no objeto mencionado. Para obter mais informações sobre representação dentro de um módulo, consulte [cláusula EXECUTE AS &#40; Transact-SQL &#41; ](../../t-sql/statements/execute-as-clause-transact-sql.md).  
  
-   O módulo está marcado como EXECUTE AS CALLER e você tem as permissões correspondentes no objeto.  
  
-   O módulo está marcado como EXECUTE AS *user_name*, e *user_name* tem as permissões correspondentes no objeto.  
  
### <a name="context-switching-permissions"></a>Permissões de alternância de contexto  
 Para especificar EXECUTE AS em um logon, o chamador precisa ter permissões IMPERSONATE no nome de logon especificado. Para especificar EXECUTE AS em um usuário de banco de dados, o chamador precisa ter permissões IMPERSONATE no nome de usuário especificado. Quando nenhum contexto de execução é especificado ou EXECUTE AS CALLER é especificado, as permissões de IMPERSONATE não são solicitadas.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-using-execute-to-pass-a-single-parameter"></a>A. Usando EXECUTE para passar um único parâmetro  
 O procedimento armazenado `uspGetEmployeeManagers` no banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] espera um parâmetro (`@EmployeeID`). Os exemplos seguintes executam o `uspGetEmployeeManagers` procedimento com armazenado `Employee ID 6` como seu valor de parâmetro.  
  
```  
EXEC dbo.uspGetEmployeeManagers 6;  
GO  
```  
  
 A variável pode ser nomeada explicitamente na execução:  
  
```  
EXEC dbo.uspGetEmployeeManagers @EmployeeID = 6;  
GO  
```  
  
 Se esta é a primeira instrução em um lote ou uma **osql** ou **sqlcmd** script, EXEC não é necessário.  
  
```  
dbo.uspGetEmployeeManagers 6;  
GO  
--Or  
dbo.uspGetEmployeeManagers @EmployeeID = 6;  
GO  
```  
  
### <a name="b-using-multiple-parameters"></a>B. Usando vários parâmetros  
 O exemplo a seguir executa o procedimento armazenado `spGetWhereUsedProductID` no banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]. Ele passa dois parâmetros: o primeiro é uma identificação de produto (`819`) e o segundo `@CheckDate,` é um valor `datetime`.  
  
```  
DECLARE @CheckDate datetime;  
SET @CheckDate = GETDATE();  
EXEC dbo.uspGetWhereUsedProductID 819, @CheckDate;  
GO  
```  
  
### <a name="c-using-execute-tsqlstring-with-a-variable"></a>C. Usando EXECUTE 'tsql_string' com uma variável  
 O exemplo seguinte mostra como `EXECUTE` controla dinamicamente as cadeias de caracteres criadas que contêm variáveis. Esse exemplo cria o cursor `tables_cursor` para manter uma lista de todas as tabelas definidas pelo usuário no banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] e, depois, usa essa lista para criar novamente todos os índices nas tabelas.  
  
```  
DECLARE tables_cursor CURSOR  
   FOR  
   SELECT s.name, t.name   
   FROM sys.objects AS t  
   JOIN sys.schemas AS s ON s.schema_id = t.schema_id  
   WHERE t.type = 'U';  
OPEN tables_cursor;  
DECLARE @schemaname sysname;  
DECLARE @tablename sysname;  
FETCH NEXT FROM tables_cursor INTO @schemaname, @tablename;  
WHILE (@@FETCH_STATUS <> -1)  
BEGIN;  
   EXECUTE ('ALTER INDEX ALL ON ' + @schemaname + '.' + @tablename + ' REBUILD;');  
   FETCH NEXT FROM tables_cursor INTO @schemaname, @tablename;  
END;  
PRINT 'The indexes on all tables have been rebuilt.';  
CLOSE tables_cursor;  
DEALLOCATE tables_cursor;  
GO  
  
```  
  
### <a name="d-using-execute-with-a-remote-stored-procedure"></a>D. Usando EXECUTE com um procedimento armazenado remoto  
 O exemplo a seguir executa o procedimento `uspGetEmployeeManagers` armazenado no servidor remoto `SQLSERVER1` e armazena o status de retorno que indica o êxito ou a falha em `@retstat`.  
  
**Aplica-se a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] por meio de[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
```  
DECLARE @retstat int;  
EXECUTE @retstat = SQLSERVER1.AdventureWorks2012.dbo.uspGetEmployeeManagers @BusinessEntityID = 6;  
```  
  
### <a name="e-using-execute-with-a-stored-procedure-variable"></a>E. Usando EXECUTE com uma variável de procedimento armazenado  
 O exemplo seguinte cria uma variável que representa um nome de procedimento armazenado.  
  
```tsql  
DECLARE @proc_name varchar(30);  
SET @proc_name = 'sys.sp_who';  
EXEC @proc_name;  
  
```  
  
### <a name="f-using-execute-with-default"></a>F. Usando EXECUTE com DEFAULT  
 O exemplo seguinte cria um procedimento armazenado com valores padrão para o primeiro e terceiro parâmetros. Quando o procedimento é executado, esses padrões serão inseridos para o primeiro e terceiro parâmetros quando nenhum valor for informado na chamada ou quando o padrão for especificado. Observe os vários modos que a palavra-chave `DEFAULT` pode ser usada.  
  
```  
IF OBJECT_ID(N'dbo.ProcTestDefaults', N'P')IS NOT NULL  
   DROP PROCEDURE dbo.ProcTestDefaults;  
GO  
-- Create the stored procedure.  
CREATE PROCEDURE dbo.ProcTestDefaults (  
@p1 smallint = 42,   
@p2 char(1),   
@p3 varchar(8) = 'CAR')  
AS   
   SET NOCOUNT ON;  
   SELECT @p1, @p2, @p3  
;  
GO  
  
```  
  
 O procedimento armazenado `Proc_Test_Defaults` pode ser executado em muitas combinações.  
  
```  
-- Specifying a value only for one parameter (@p2).  
EXECUTE dbo.ProcTestDefaults @p2 = 'A';  
-- Specifying a value for the first two parameters.  
EXECUTE dbo.ProcTestDefaults 68, 'B';  
-- Specifying a value for all three parameters.  
EXECUTE dbo.ProcTestDefaults 68, 'C', 'House';  
-- Using the DEFAULT keyword for the first parameter.  
EXECUTE dbo.ProcTestDefaults @p1 = DEFAULT, @p2 = 'D';  
-- Specifying the parameters in an order different from the order defined in the procedure.  
EXECUTE dbo.ProcTestDefaults DEFAULT, @p3 = 'Local', @p2 = 'E';  
-- Using the DEFAULT keyword for the first and third parameters.  
EXECUTE dbo.ProcTestDefaults DEFAULT, 'H', DEFAULT;  
EXECUTE dbo.ProcTestDefaults DEFAULT, 'I', @p3 = DEFAULT;  
  
```  
  
### <a name="g-using-execute-with-at-linkedservername"></a>G. Usando EXECUTE com AT linked_server_name  
 O exemplo seguinte envia uma cadeia de caracteres de comando a um servidor remoto. Ele cria um servidor vinculado `SeattleSales` que aponta para outra instância de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e executa uma instrução DDL (`CREATE TABLE`) nesse servidor vinculado.  
  
**Aplica-se a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] por meio de[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
```  
EXEC sp_addlinkedserver 'SeattleSales', 'SQL Server'  
GO  
EXECUTE ( 'CREATE TABLE AdventureWorks2012.dbo.SalesTbl   
(SalesID int, SalesName varchar(10)) ; ' ) AT SeattleSales;  
GO  
```  
  
### <a name="h-using-execute-with-recompile"></a>H. Usando EXECUTE WITH RECOMPILE  
 O exemplo a seguir executa o `Proc_Test_Defaults` procedimento armazenado e força um novo plano de consulta a ser compilado, usados e descartadas após a execução do módulo.  
  
```  
EXECUTE dbo.Proc_Test_Defaults @p2 = 'A' WITH RECOMPILE;  
GO  
```  
  
### <a name="i-using-execute-with-a-user-defined-function"></a>I. Usando EXECUTE com uma função definida pelo usuário  
 O exemplo a seguir executa a função escalar definida pelo usuário `ufnGetSalesOrderStatusText` no banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]. É utilizada a variável `@returnstatus` para armazenar o valor retornado pela função. A função espera um parâmetro de entrada, `@Status`. Isso é definido como um **tinyint** tipo de dados.  
  
```  
DECLARE @returnstatus nvarchar(15);  
SET @returnstatus = NULL;  
EXEC @returnstatus = dbo.ufnGetSalesOrderStatusText @Status = 2;  
PRINT @returnstatus;  
GO  
```  
  
### <a name="j-using-execute-to-query-an-oracle-database-on-a-linked-server"></a>J. Usando EXECUTE para consultar um banco de dados Oracle em um servidor vinculado  
 O exemplo a seguir executa várias instruções `SELECT` no servidor remoto Oracle. O exemplo começa adicionando o servidor Oracle como um servidor vinculado e criando o logon de servidor vinculado.  
  
**Aplica-se a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] por meio de[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
```  
-- Setup the linked server.  
EXEC sp_addlinkedserver    
        @server='ORACLE',  
        @srvproduct='Oracle',  
        @provider='OraOLEDB.Oracle',   
        @datasrc='ORACLE10';  
  
EXEC sp_addlinkedsrvlogin   
    @rmtsrvname='ORACLE',  
    @useself='false',   
    @locallogin=null,   
    @rmtuser='scott',   
    @rmtpassword='tiger';  
  
EXEC sp_serveroption 'ORACLE', 'rpc out', true;  
GO  
  
-- Execute several statements on the linked Oracle server.  
EXEC ( 'SELECT * FROM scott.emp') AT ORACLE;  
GO  
EXEC ( 'SELECT * FROM scott.emp WHERE MGR = ?', 7902) AT ORACLE;  
GO  
DECLARE @v INT;   
SET @v = 7902;  
EXEC ( 'SELECT * FROM scott.emp WHERE MGR = ?', @v) AT ORACLE;  
GO   
```  
  
### <a name="k-using-execute-as-user-to-switch-context-to-another-user"></a>K. Usando EXECUTE AS USER para alternar o contexto para outro usuário  
 O exemplo a seguir executa uma cadeia de caracteres [!INCLUDE[tsql](../../includes/tsql-md.md)] que cria uma tabela e especifica a cláusula `AS USER` para alternar o contexto de execução da instrução do chamador para `User1`. O [!INCLUDE[ssDE](../../includes/ssde-md.md)] verificará as permissões de `User1` quando a instrução for executada. `User1` deve existir como um usuário no banco de dados e deve ter permissão para criar tabelas no esquema `Sales`, caso contrário, haverá falha na instrução.  
  
```  
EXECUTE ('CREATE TABLE Sales.SalesTable (SalesID int, SalesName varchar(10));')  
AS USER = 'User1';  
GO  
```  
  
### <a name="l-using-a-parameter-with-execute-and-at-linkedservername"></a>L. Usando um parâmetro com EXECUTE e AT linked_server_name  
 O exemplo a seguir envia uma cadeia de caracteres de comando a um servidor remoto usando um ponto de interrogação (`?`) como espaço reservado de um parâmetro. O exemplo cria um servidor vinculado `SeattleSales` que aponta para outra instância de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e executa uma instrução `SELECT` nesse servidor vinculado. A instrução `SELECT` usa o ponto de interrogação como um espaço reservado para o parâmetro `ProductID` (`952`), fornecido após a instrução.  
  
**Aplica-se a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] por meio de[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
```  
-- Setup the linked server.  
EXEC sp_addlinkedserver 'SeattleSales', 'SQL Server'  
GO  
-- Execute the SELECT statement.  
EXECUTE ('SELECT ProductID, Name   
    FROM AdventureWorks2012.Production.Product  
    WHERE ProductID = ? ', 952) AT SeattleSales;  
GO  
```  
  
### <a name="m-using-execute-to-redefine-a-single-result-set"></a>M. Usando EXECUTE para redefinir um único conjunto de resultados  
 Alguns dos exemplos anteriores executaram `EXEC dbo.uspGetEmployeeManagers 6;` que retornou 7 colunas. O exemplo a seguir demonstra o uso da sintaxe `WITH RESULT SET` para alterar os nomes e tipos de dados do conjunto de resultados retornado.  
  
**Aplica-se a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] por meio de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)],[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]
  
```  
EXEC uspGetEmployeeManagers 16  
WITH RESULT SETS  
(   
   ([Reporting Level] int NOT NULL,  
    [ID of Employee] int NOT NULL,  
    [Employee First Name] nvarchar(50) NOT NULL,  
    [Employee Last Name] nvarchar(50) NOT NULL,  
    [Employee ID of Manager] nvarchar(max) NOT NULL,  
    [Manager First Name] nvarchar(50) NOT NULL,  
    [Manager Last Name] nvarchar(50) NOT NULL )  
);  
  
```  
  
### <a name="n-using-execute-to-redefine-a-two-result-sets"></a>N. Usando EXECUTE para redefinir dois conjuntos de resultados  
 Ao executar uma instrução que retorna mais de um conjunto de resultados, defina cada conjunto de resultados esperado. O exemplo a seguir em [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] cria um procedimento armazenado que retorna dois conjuntos de resultados. Em seguida, o procedimento é executado usando o **com conjuntos de resultados** cláusula e especificando os dois resultados conjunto de definições.  
  
**Aplica-se a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] por meio de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)],[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]
  
```  
--Create the procedure  
CREATE PROC Production.ProductList @ProdName nvarchar(50)  
AS  
-- First result set  
SELECT ProductID, Name, ListPrice  
    FROM Production.Product  
    WHERE Name LIKE @ProdName;  
-- Second result set   
SELECT Name, COUNT(S.ProductID) AS NumberOfOrders  
    FROM Production.Product AS P  
    JOIN Sales.SalesOrderDetail AS S  
        ON P.ProductID  = S.ProductID   
    WHERE Name LIKE @ProdName  
    GROUP BY Name;  
GO  
  
-- Execute the procedure   
EXEC Production.ProductList '%tire%'  
WITH RESULT SETS   
(  
    (ProductID int,   -- first result set definition starts here  
    Name Name,  
    ListPrice money)  
    ,                 -- comma separates result set definitions  
    (Name Name,       -- second result set definition starts here  
    NumberOfOrders int)  
);  
  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Exemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="example-o-basic-procedure-execution"></a>Exemplo O: execução de procedimento básico  
 Executar um procedimento armazenado:  
  
```  
EXEC proc1;  
```  
  
 Chamando um procedimento armazenado com nome determinado em tempo de execução:  
  
```  
EXEC ('EXEC ' + @var);  
```  
  
 Chamar um procedimento armazenado de dentro de um procedimento armazenado:  
  
```  
CREATE sp_first AS EXEC sp_second; EXEC sp_third;  
```  
  
### <a name="example-p-executing-strings"></a>Exemplo p: cadeias de caracteres de execução  
 Executando uma cadeia de caracteres SQL:  
  
```  
EXEC ('SELECT * FROM sys.types');  
```  
  
 Executando uma cadeia de caracteres aninhada:  
  
```  
EXEC ('EXEC (''SELECT * FROM sys.types'')');  
```  
  
 Execução de uma variável de cadeia de caracteres:  
  
```  
DECLARE @stringVar nvarchar(100);  
SET @stringVar = N'SELECT name FROM' + ' sys.sql_logins';  
EXEC (@stringVar);  
```  
  
### <a name="example-q-procedures-with-parameters"></a>Exemplo p: procedimentos com parâmetros  
 O exemplo a seguir cria um procedimento com parâmetros e demonstra 3 maneiras de executar o procedimento:  
  
```  
-- Uses AdventureWorks  
  
CREATE PROC ProcWithParameters  
    @name nvarchar(50),  
@color nvarchar (15)  
AS   
SELECT ProductKey, EnglishProductName, Color FROM [dbo].[DimProduct]  
WHERE EnglishProductName LIKE @name  
AND Color = @color;  
GO  
  
-- Executing using positional parameters  
EXEC ProcWithParameters N'%arm%', N'Black';  
-- Executing using named parameters in order  
EXEC ProcWithParameters @name = N'%arm%', @color = N'Black';  
-- Executing using named parameters out of order  
EXEC ProcWithParameters @color = N'Black', @name = N'%arm%';  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [@@NESTLEVEL &#40;Transact-SQL&#41;](../../t-sql/functions/nestlevel-transact-sql.md)   
 [DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)   
 [Cláusula EXECUTE AS &#40;Transact-SQL&#41;](../../t-sql/statements/execute-as-clause-transact-sql.md)   
 [Utilitário osql](../../tools/osql-utility.md)   
 [Entidades &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [REVERTER &#40; Transact-SQL &#41;](../../t-sql/statements/revert-transact-sql.md)   
 [sp_addlinkedserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)   
 [Utilitário sqlcmd](../../tools/sqlcmd-utility.md)   
 [SUSER_NAME &#40; Transact-SQL &#41;](../../t-sql/functions/suser-name-transact-sql.md)   
 [sys.database_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)   
 [sys.server_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)   
 [User_name &#40; Transact-SQL &#41;](../../t-sql/functions/user-name-transact-sql.md)   
 [OPENDATASOURCE &#40;Transact-SQL&#41;](../../t-sql/functions/opendatasource-transact-sql.md)   
 [Funções escalares definidas pelo usuário para OLTP in-memory](../../relational-databases/in-memory-oltp/scalar-user-defined-functions-for-in-memory-oltp.md)  
  
  

