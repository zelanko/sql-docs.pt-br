---
title: INSERT (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/10/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- INSERT_TSQL
- INSERT
dev_langs:
- TSQL
helpviewer_keywords:
- inserting multiple rows
- user-defined types [SQL Server], inserting values
- DML [SQL Server], INSERT statement
- bulk load [SQL Server]
- row additions [SQL Server], INSERT statement
- inserting rows
- table value constructor [SQL Server]
- adding data
- INSERT statement [SQL Server], about INSERT statement
- INSERT statement [SQL Server]
- UDTs [SQL Server], inserting values
- adding rows
- INSERT INTO statement
- data manipulation language [SQL Server], INSERT statement
- inserting data
ms.assetid: 1054c76e-0fd5-4131-8c07-a6c5d024af50
caps.latest.revision: 136
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: ef8387c2bbbc109ad7ec325e4faf632a983d96c9
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="insert-transact-sql"></a>INSERT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Adiciona uma ou mais linhas a uma tabela ou exibição no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter exemplos, consulte [exemplos](#InsertExamples).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
-- Syntax for SQL Server and Azure SQL Database  

[ WITH <common_table_expression> [ ,...n ] ]  
INSERT   
{  
        [ TOP ( expression ) [ PERCENT ] ]   
        [ INTO ]   
        { <object> | rowset_function_limited   
          [ WITH ( <Table_Hint_Limited> [ ...n ] ) ]  
        }  
    {  
        [ ( column_list ) ]   
        [ <OUTPUT Clause> ]  
        { VALUES ( { DEFAULT | NULL | expression } [ ,...n ] ) [ ,...n     ]   
        | derived_table   
        | execute_statement  
        | <dml_table_source>  
        | DEFAULT VALUES   
        }  
    }  
}  
[;]  
  
<object> ::=  
{   
    [ server_name . database_name . schema_name .   
      | database_name .[ schema_name ] .   
      | schema_name .   
    ]  
  table_or_view_name  
}  
  
<dml_table_source> ::=  
    SELECT <select_list>  
    FROM ( <dml_statement_with_output_clause> )   
      [AS] table_alias [ ( column_alias [ ,...n ] ) ]  
    [ WHERE <search_condition> ]  
        [ OPTION ( <query_hint> [ ,...n ] ) ]  
```  
  
```  
-- External tool only syntax  

INSERT   
{  
    [BULK]  
    [ database_name . [ schema_name ] . | schema_name . ]  
    [ table_name | view_name ]  
    ( <column_definition> )  
    [ WITH (  
        [ [ , ] CHECK_CONSTRAINTS ]  
        [ [ , ] FIRE_TRIGGERS ]  
        [ [ , ] KEEP_NULLS ]  
        [ [ , ] KILOBYTES_PER_BATCH = kilobytes_per_batch ]  
        [ [ , ] ROWS_PER_BATCH = rows_per_batch ]  
        [ [ , ] ORDER ( { column [ ASC | DESC ] } [ ,...n ] ) ]  
        [ [ , ] TABLOCK ]  
    ) ]  
}  
  
[; ] <column_definition> ::=  
 column_name <data_type>  
    [ COLLATE collation_name ]  
    [ NULL | NOT NULL ]  
  
<data type> ::=   
[ type_schema_name . ] type_name   
    [ ( precision [ , scale ] | max ]  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  

INSERT INTO [ database_name . [ schema_name ] . | schema_name . ] table_name   
    [ ( column_name [ ,...n ] ) ]  
    {   
      VALUES ( { NULL | expression } )  
      | SELECT <select_criteria>  
    }  
    [ OPTION ( <query_option> [ ,...n ] ) ]  
[;]  
```  
  
## <a name="arguments"></a>Argumentos  
 COM \<common_table_expression >  
 Especifica o conjunto de resultados nomeado temporário, também conhecido como expressão de tabela comum, definido dentro do escopo da instrução INSERT. O conjunto de resultados é derivado de uma instrução SELECT. Para obter mais informações, consulte [com common_table_expression &#40; Transact-SQL &#41; ](../../t-sql/queries/with-common-table-expression-transact-sql.md).  
  
 Parte superior (*expressão*) [%]  
 Especifica o número ou a porcentagem de linhas aleatórias que serão inseridas. *expression* pode ser um número ou uma porcentagem das linhas. Para obter mais informações, consulte [TOP &#40; Transact-SQL &#41; ](../../t-sql/queries/top-transact-sql.md).  
  
 INTO  
 É uma palavra-chave opcional que pode ser usada entre INSERT e a tabela de destino.  
  
 *server_name*  
 **Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 É o nome do servidor vinculado no qual a tabela ou exibição especificada está localizada. *server_name* pode ser especificado como um [servidor vinculado](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md) nome, ou usando o [OPENDATASOURCE](../../t-sql/functions/opendatasource-transact-sql.md) função.  
  
 Quando *nome_do_servidor* é especificado como um servidor vinculado, *database_name* e *schema_name* são necessários. Quando *nome_do_servidor* é especificado com OPENDATASOURCE, *database_name* e *schema_name* não podem ser aplicadas a todas as fontes de dados e está sujeita aos recursos do OLE DB provedor que acessa o objeto remoto.  
  
 *database_name*  
 **Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 É o nome do banco de dados.  
  
 *schema_name*  
 É o nome do esquema ao qual a tabela ou exibição pertence.  
  
 *view_name table_or*  
 É o nome da tabela ou exibição que irá receber os dados.  
  
 Um [tabela](../../t-sql/data-types/table-transact-sql.md) variável, dentro de seu escopo, pode ser usada como uma origem de tabela em uma instrução INSERT.  
  
 A exibição referenciada por *table_or_view_name* deve ser atualizável e fazer referência exatamente uma tabela base na cláusula FROM da exibição. Por exemplo, um INSERT em uma exibição de várias tabelas deve usar um *column_list* que faça referência apenas a colunas de uma tabela base. Para obter mais informações sobre exibições atualizáveis, consulte [CREATE VIEW &#40; Transact-SQL &#41; ](../../t-sql/statements/create-view-transact-sql.md).  
  
 *rowset_function_limited*  
 **Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 É o [OPENQUERY](../../t-sql/functions/openquery-transact-sql.md) ou [OPENROWSET](../../t-sql/functions/openrowset-transact-sql.md) função. O uso dessas funções está sujeito aos recursos do provedor OLE DB que acessa o objeto remoto.  
  
 COM ( \<dica_de_tabela_limitada > [... *n* ] )  
 Especifica uma ou mais dicas de tabela permitidas para uma tabela de destino. A palavra-chave WITH e parênteses são necessários.  
  
 READPAST, NOLOCK e READUNCOMMITTED não são permitidos. Para obter mais informações sobre dicas de tabela, consulte [dicas de tabela &#40; Transact-SQL &#41; ](../../t-sql/queries/hints-transact-sql-table.md).  
  
> [!IMPORTANT]  
>  A capacidade de especificar as dicas HOLDLOCK, SERIALIZABLE, READCOMMITTED, REPEATABLEREAD ou UPDLOCK em tabelas que são destinos de instruções INSERT será removida em uma versão futura do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Essas dicas não afetam o desempenho de instruções INSERT. Evite usá-las em novos projetos de desenvolvimento e planeje modificar os aplicativos que as utilizam atualmente.  
  
 Especificar a dica TABLOCK em uma tabela que é o destino de uma instrução INSERT tem o mesmo efeito de especificar a dica TABLOCKX. Um bloqueio exclusivo é obtido na tabela.  
  
 (*column_list*)  
 É uma lista de uma ou mais colunas onde os dados devem ser inseridos. *column_list* devem ser colocados entre parênteses e delimitado por vírgulas.  
  
 Se uma coluna não está em *column_list*, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] deve ser capaz de fornecer um valor com base na definição de coluna; caso contrário, a linha não pode ser carregada. O [!INCLUDE[ssDE](../../includes/ssde-md.md)] fornecerá um valor automaticamente para a coluna, se a coluna:  
  
-   Tiver uma propriedade IDENTITY. O próximo valor de identidade incremental for usado.  
  
-   Tiver um padrão. O valor padrão da coluna for usado.  
  
-   Tem um **timestamp** tipo de dados. O valor do carimbo de data/hora atual for usado.  
  
-   Permite valor nulo. Um valor nulo for usado.  
  
-   For uma coluna computada. O valor calculado for usado.  
  
*column_list* deve ser usado quando valores explícitos são inseridos em uma coluna de identidade, e a opção SET IDENTITY_INSERT deve estar ON para a tabela.  
  
Cláusula OUTPUT  
 Retorna linhas inseridas como parte da operação de inserção. Os resultados podem ser retornados ao aplicativo de processamento ou inseridos em uma tabela ou variável de tabela para processamento futuro.  
  
 O [cláusula OUTPUT](../../t-sql/queries/output-clause-transact-sql.md) não é suportada em instruções DML que fazem referência a exibições particionadas locais, exibições particionadas distribuídas ou tabelas remotas, ou instruções INSERT que contêm um *execute_statement*. Não há suporte para a cláusula OUTPUT INTO em instruções INSERT que contêm um \<dml_table_source > cláusula. 
  
 VALUES  
 Apresenta a(s) lista(s) de valores de dados a serem inseridos. Deve haver um valor de dados para cada coluna na *column_list*, se especificado, ou na tabela. A lista de valores deve ser colocada entre parênteses.  
  
 Se os valores na lista de valores não estiverem na mesma ordem que as colunas na tabela ou não tem um valor para cada coluna na tabela, *column_list* deve ser usado para especificar explicitamente a coluna que armazena cada valor de entrada.  
  
 É possível usar o construtor de linhas do [!INCLUDE[tsql](../../includes/tsql-md.md)] (também chamado construtor de valor de tabela) para especificar várias linhas em uma única instrução INSERT. O construtor de linhas consiste em uma única cláusula VALUES com várias listas de valores entre parênteses e separados por uma vírgula. Para obter mais informações, consulte [construtor de valor de tabela &#40; Transact-SQL &#41; ](../../t-sql/queries/table-value-constructor-transact-sql.md).  
  
 DEFAULT  
 Força o [!INCLUDE[ssDE](../../includes/ssde-md.md)] a carregar o valor padrão definido para uma coluna. Se não existir um padrão para a coluna e a coluna aceitar valores nulos, NULL será inserido. Para uma coluna definida com o **timestamp** tipo de dados, o próximo valor de carimbo de hora é inserido. DEFAULT não é válido para uma coluna de identidade.  
  
 *expressão*  
 É uma constante, uma variável ou uma expressão. A expressão não pode conter uma instrução EXECUTE.  
  
 Ao fazer referência a tipos de dados de caractere Unicode **nchar**, **nvarchar**, e **ntext**, '*expressão*' devem ser prefixados com o Letra maiuscula ' n '. Se N não for especificado, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] converte a cadeia na página de código correspondente ao agrupamento padrão do banco de dados ou coluna. Qualquer caractere não localizado nessa página de código será perdido.  
  
 *derived_table*  
 É qualquer instrução SELECT válida que retorne linhas de dados a serem carregadas na tabela. A instrução SELECT não pode conter uma CTE (expressão de tabela comum).  
  
 *execute_statement*  
 É qualquer instrução EXECUTE que retorne dados com instruções SELECT ou READTEXT. Para obter mais informações, veja [EXECUTE &#40;Transact-SQL&#41;](../../t-sql/language-elements/execute-transact-sql.md).  
  
 As opções de RESULT SETS da instrução EXECUTE não podem ser especificadas em uma instrução INSERT...EXEC.  
  
 Se *execute_statement* é usado com INSERT, cada conjunto de resultados deve ser compatível com as colunas na tabela ou no *column_list*.  
  
 *execute_statement* pode ser usado para executar procedimentos armazenados no mesmo servidor ou um servidor remoto. O procedimento no servidor remoto é executado e os conjuntos de resultados são retornados ao servidor local e carregados na tabela no servidor local. Em uma transação distribuída, *execute_statement* não pode ser emitida em um servidor vinculado de loopback quando a conexão tem vários conjuntos de resultados ativos (MARS) habilitados.  
  
 Se *execute_statement* retorna dados com a instrução READTEXT, cada instrução READTEXT poderá retornar um máximo de 1 MB (1024 KB) de dados. *execute_statement* também pode ser usado com procedimentos estendidos. *execute_statement* insere os dados retornados pelo thread principal do procedimento estendido; no entanto, a saída de threads diferentes do thread principal não são inseridos.  
  
 Você não pode especificar um parâmetro avaliado por tabela como o destino de uma instrução INSERT EXEC; porém, ele pode ser especificado como uma origem na cadeia de caracteres INSERT EXEC ou procedimento armazenado. Para obter mais informações, veja [Usar parâmetros com valor de tabela &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/tables/use-table-valued-parameters-database-engine.md).  
  
 \<dml_table_source >  
 Especifica que as linhas inseridas na tabela de destino são as retornadas pela cláusula OUTPUT de uma instrução INSERT, UPDATE, DELETE ou MERGE, opcionalmente filtradas por uma cláusula WHERE. Se \<dml_table_source > for especificado, o destino da instrução INSERT externa deve atender aos seguintes restrições: 
  
-   Deve ser uma tabela base, não uma exibição.  
  
-   Não pode ser uma tabela remota.  
  
-   Não pode ter gatilhos definidos.  
  
-   Não pode participar de relações de chave primária/chave estrangeira.  
  
-   Não pode participar de replicação de mesclagem ou de assinaturas atualizáveis para replicação transacional.  
  
 O nível de compatibilidade do banco de dados deve ser definido como 100 ou superior. Para obter mais informações, consulte [cláusula OUTPUT &#40; Transact-SQL &#41; ](../../t-sql/queries/output-clause-transact-sql.md).  
  
 \<select_list >  
 É uma lista separada por vírgulas que especifica quais colunas retornadas pela cláusula OUTPUT devem ser inseridas. As colunas na \<select_list > devem ser compatíveis com as colunas nas quais os valores serão inseridos. \<select_list > não pode fazer referência a funções de agregação ou a TEXTPTR. 
  
> [!NOTE]  
>  Todas as variáveis listadas na lista de seleção se referir aos seus valores originais, independentemente de quaisquer alterações feitas a eles no \<dml_statement_with_output_clause >.  
  
 \<dml_statement_with_output_clause >  
 É uma instrução INSERT, UPDATE, DELETE ou MERGE válida que retorna linhas afetadas em uma cláusula OUTPUT. A instrução não pode conter uma cláusula WITH nem pode ter como destino tabelas remotas ou exibições particionadas. Se UPDATE ou DELETE for especificada, ela não poderá ser uma instrução UPDATE ou DELETE baseada em cursor. Linhas de origem não podem ser referenciadas como instruções DML aninhadas.  
  
 ONDE \<search_condition >  
 É qualquer cláusula WHERE que contenha um válido \<search_condition > que filtra as linhas retornadas pela \<dml_statement_with_output_clause >. Para obter mais informações, consulte [critério de pesquisa &#40; Transact-SQL &#41; ](../../t-sql/queries/search-condition-transact-sql.md). Quando usado neste contexto, \<search_condition > não pode conter subconsultas, funções escalares definidas pelo usuário que executam o acesso a dados, funções de agregação, TEXTPTR ou predicados de pesquisa de texto completo. 
  
 DEFAULT VALUES  
 **Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Força a nova linha a conter os valores padrão definidos para cada coluna.  
  
 BULK  
**Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Usado por ferramentas externas para carregar um fluxo de dados binários. Essa opção não se destina para uso com ferramentas como [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], SQLCMD, OSQL ou acesso a dados interfaces de programação de aplicativo, como [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client.  
  
 FIRE_TRIGGERS  
 **Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Especifica que qualquer gatilho de inserção definido na tabela de destino seja executado durante a operação de carregamento de fluxo de dados binários. Para obter mais informações, veja [BULK INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md).  
  
 CHECK_CONSTRAINTS  
 **Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Especifica que todas as restrições na tabela ou exibição de destino devem ser verificadas durante a operação de carregamento de fluxo de dados binários. Para obter mais informações, veja [BULK INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md).  
  
 KEEPNULLS  
 **Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Especifica que as colunas vazias devem reter um valor nulo durante a operação de carregamento de fluxo de dados binários. Para obter mais informações, veja [Manter valores nulos ou usar os valores padrão durante a importação em massa &#40;SQL Server&#41;](../../relational-databases/import-export/keep-nulls-or-use-default-values-during-bulk-import-sql-server.md).  
  
 KILOBYTES_PER_BATCH = kilobytes_per_batch  
 Especifica o número aproximado de kilobytes (KB) de dados por lote como *kilobytes_per_batch*. Para obter mais informações, veja [BULK INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md).  
  
 ROWS_PER_BATCH =*rows_per_batch*  
 **Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Indica o número aproximado de linhas de dados no fluxo de dados binários. Para obter mais informações, veja [BULK INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md).  
  
>  [!NOTE]
>  Um erro de sintaxe é gerado se uma lista de colunas não for fornecida.  

## <a name="remarks"></a>Comentários  
Para obter informações específicas para inserir dados em tabelas de gráfico SQL, consulte [INSERT (gráfico de SQL)](../../t-sql/statements/insert-sql-graph.md). 

## <a name="best-practices"></a>Práticas recomendadas  
 Use o @@ROWCOUNT inseridos de função para retornar o número de linhas para o aplicativo cliente. Para obter mais informações, consulte [@@ROWCOUNT &#40; Transact-SQL &#41; ](../../t-sql/functions/rowcount-transact-sql.md).  
  
### <a name="best-practices-for-bulk-importing-data"></a>Práticas recomendadas para importar dados em massa  
  
#### <a name="using-insert-intoselect-to-bulk-import-data-with-minimal-logging"></a>Usando INSERT INTO…SELECT em importação de dados em massa com log mínimo  
 Você pode usar `INSERT INTO <target_table> SELECT <columns> FROM <source_table>` para transferir com eficiência um grande número de linhas de uma tabela, como uma tabela de preparo para outra tabela com log mínimo. O log mínimo pode melhorar o desempenho da instrução e reduzir a possibilidade de a operação preencher o espaço de log disponível durante a transação.  
  
 O log mínimo dessa instrução possui os seguintes requisitos:  
  
-   O modelo de recuperação do banco de dados é definido como simples ou bulk-logged.  
  
-   A tabela de destino é um heap vazio ou não vazio.  
  
-   A tabela de destino não é usada na replicação.  
  
-   A dica TABLOCK é especificada para a tabela de destino.  
  
As linhas inseridas em um heap como o resultado de uma ação de inserção em uma instrução MERGE também podem ser minimamente registradas.  
  
 Diferentemente da instrução BULK INSERT, que possui um bloqueio de atualização em massa menos restritivo, INSERT INTO.SELECT com a dica TABLOCK possui um bloqueio exclusivo (X) na tabela. Isso significa que você não pode inserir linhas usando operações de inserção paralelas.  
  
#### <a name="using-openrowset-and-bulk-to-bulk-import-data"></a>Usando OPENROWSET e BULK para importação de dados em massa  
 A função OPENROWSET pode aceitar as seguintes dicas de tabela, que fornecem otimizações de carregamento em massa com a instrução INSERT:  
  
-   A dica TABLOCK pode minimizar o número de registros de log para a operação de inserção. O modelo de recuperação do banco de dados deve ser definido como simples ou bulk-logged e a tabela de destino não pode ser usada na replicação. Para obter mais informações, consulte [pré-requisitos para log mínimo em importação em massa](../../relational-databases/import-export/prerequisites-for-minimal-logging-in-bulk-import.md).  
  
-   A dica IGNORE_CONSTRAINTS pode desabilitar temporariamente a verificação de restrição FOREIGN KEY e CHECK.  
  
-   A dica IGNORE_TRIGGERS pode desabilitar temporariamente a execução de gatilhos.  
  
-   A dica KEEPDEFAULTS permite a inserção de um valor padrão da coluna de tabela, se houver algum, em vez de NULL, se o registro de dados não tiver um valor para a coluna.  
  
-   A dica KEEPIDENTITY permite que os valores de identidade no arquivo de dados importado sejam usados para a coluna de identidade na tabela de destino.  
  
Essas otimizações são semelhantes àquelas disponíveis com o comando BULK INSERT. Para obter mais informações, consulte [Dicas de tabela &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-table.md).  
  
## <a name="data-types"></a>Tipos de dados  
 Quando você inserir linhas, considere o comportamento do seguinte tipo de dados:  
  
-   Se um valor está sendo carregado em colunas com um **char**, **varchar**, ou **varbinary** tipo de dados, o preenchimento ou truncamento de à direita de espaços em branco (espaços para  **char** e **varchar**, zeros para **varbinary**) é determinado pela configuração de SET ANSI_PADDING definida para a coluna quando a tabela foi criada. Para obter mais informações, veja [SET ANSI_PADDING &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-padding-transact-sql.md).  
  
     A tabela a seguir mostra a operação padrão de SET ANSI_PADDING OFF.  
  
    |Tipo de dados|Operação padrão|  
    |---------------|-----------------------|  
    |**char**|Valor de preenchimento com espaços para a largura definida da coluna.|  
    |**varchar**|Remove espaços à direita do último caractere não-espaço ou do caractere de espaço único para cadeias de caracteres compostas apenas de espaços.|  
    |**varbinary**|Remova zeros à direita.|  
  
-   Se uma cadeia de caracteres vazia (' ') é carregado em uma coluna com um **varchar** ou **texto** tipo de dados, a operação padrão será carregar uma cadeia de caracteres de comprimento zero.  
  
-   Inserindo um valor nulo em uma **texto** ou **imagem** coluna não cria um ponteiro de texto válido, nem pré-aloca uma página de texto de 8 KB.  
  
-   Colunas criadas com o **uniqueidentifier** repositório do tipo de dados especialmente formatados valores binários de 16 bytes. Ao contrário de com colunas de identidade, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] não gera automaticamente valores para colunas com o **uniqueidentifier** tipo de dados. Durante uma operação de inserção, as variáveis com dados de um tipo de **uniqueidentifier** e constantes no formulário de cadeia de caracteres *xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx* (36 caracteres, inclusive hífens, onde *x* é um dígito hexadecimal no intervalo 0-9 ou a f) podem ser usados para **uniqueidentifier** colunas. Por exemplo, 6F9619FF-8B86-D011-B42D-00C04FC964FF é um valor válido para uma **uniqueidentifier** variável ou coluna. Use o [NEWID ()](../../t-sql/functions/newid-transact-sql.md) função para obter uma ID globalmente exclusiva (GUID).  
  
### <a name="inserting-values-into-user-defined-type-columns"></a>Inserindo valores em colunas de tipo definido pelo usuário  
 É possível inserir valores em colunas de tipo definido pelo usuário das seguintes maneiras:  
  
-   Fornecendo um valor do tipo definido pelo usuário.  
  
-   Fornecendo um valor em um tipo de dados do sistema [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], contanto que o tipo definido pelo usuário ofereça suporte à conversão implícita ou explícita do referido tipo. O exemplo a seguir mostra como inserir um valor em uma coluna de tipo definido pelo usuário `Point`, convertendo explicitamente de uma cadeia de caracteres.  
  
    ```  
    INSERT INTO Cities (Location)  
    VALUES ( CONVERT(Point, '12.3:46.2') );  
    ```  
  
     Um valor binário também pode ser fornecido sem executar conversão explícita, porque todos os tipos definidos pelo usuário podem ser implicitamente convertidos de binário.  
  
-   Chamando uma função definida pelo usuário que retorna um valor do tipo definido pelo usuário. O exemplo a seguir usa uma função definida pelo usuário `CreateNewPoint()` para criar um novo valor de tipo definido pelo usuário `Point` e inserir o valor na tabela `Cities`.  
  
    ```  
    INSERT INTO Cities (Location)  
    VALUES ( dbo.CreateNewPoint(x, y) );  
    ```  
  
## <a name="error-handling"></a>Tratamento de erros  
 Você pode implementar a manipulação de erros para a instrução INSERT especificando essa instrução em uma construção TRY.CATCH.  
  
 Se uma instrução INSERT violar uma restrição ou regra ou se ela tiver um valor incompatível com o tipo de dados da coluna, a instrução falhará e uma mensagem de erro será retornada.  
  
 Se INSERT estiver carregando várias linhas com SELECT ou EXECUTE, qualquer violação de uma regra ou restrição que ocorra nos valores que estão sendo carregados faz com que a instrução seja interrompida e nenhuma linha seja carregada.  
  
 Quando uma instrução INSERT encontra um erro aritmético (estouro, divisão por zero ou um erro de domínio) que ocorre durante a avaliação da expressão, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] trata esses erros como se a opção SET ARITHABORT estivesse definida como ON. O lote é interrompido e uma mensagem de erro é retornada. Durante a avaliação da expressão, quando SET ARITHABORT e SET ANSI_WARNINGS estão definidas como OFF, se uma instrução INSERT, DELETE ou UPDATE encontrar um erro aritmético, de estouro, de divisão por zero ou um erro de domínio, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] irá inserir ou atualizar um valor NULL. Se a coluna de destino não for anulável, a ação de inserção ou atualização falhará e o usuário receberá uma mensagem de erro.  
  
## <a name="interoperability"></a>Interoperabilidade  
 Quando um gatilho INSTEAD OF é definido em ações INSERT em uma tabela ou exibição, o gatilho é executado em vez da instrução INSERT. Para obter mais informações sobre gatilhos INSTEAD of, consulte [CREATE TRIGGER &#40; Transact-SQL &#41; ](../../t-sql/statements/create-trigger-transact-sql.md).  
  
## <a name="limitations-and-restrictions"></a>Limitações e restrições  
 Quando você insere valores em tabelas remotas e nem todos os valores de todas as colunas são especificados, é necessário identificar as colunas para as quais os valores devem ser inseridos.  
  
 Quando TOP é usado com INSERT, as linhas referenciadas não são organizadas em nenhuma ordem e a cláusula ORDER BY não pode ser especificada diretamente nessas instruções. Se você precisar usar TOP para inserir linhas em uma ordem cronológica significativa, deverá usar TOP junto com uma cláusula ORDER BY especificada em uma instrução de subseleção. Consulte a seção Exemplos a seguir neste tópico.
 
SELECIONAM inserir as consultas que usam com ORDER BY para preencher as garantias de linhas como valores de identidade são computados, mas não a ordem na qual as linhas são inseridas.    
  
## <a name="logging-behavior"></a>Comportamento de log  
 A instrução INSERT é sempre totalmente registrada exceto ao usar a função OPENROWSET com a palavra-chave em MASSA ou ao usar `INSERT INTO <target_table> SELECT <columns> FROM <source_table>`. Essas operações podem ser registradas minimamente. Para obter mais informações, consulte a seção "Práticas recomendadas para o carregamento de dados em massa" anteriormente neste tópico.  
  
## <a name="security"></a>Segurança  
 Durante uma conexão de servidor vinculado, o servidor de envio fornece um nome de logon e uma senha para conexão com o servidor de recebimento em seu nome. Para essa conexão funcione, você deve criar um mapeamento de logon entre os servidores vinculados usando [sp_addlinkedsrvlogin](../../relational-databases/system-stored-procedures/sp-addlinkedsrvlogin-transact-sql.md).  
  
 Quando você usar OPENROWSET(BULK…), é importante entender como o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] manipula a representação. Para obter mais informações, consulte "Considerações sobre segurança" no [importação em massa dados usando BULK INSERT ou OPENROWSET &#40; BULK... &#41; &#40; SQL Server &#41; ](../../relational-databases/import-export/import-bulk-data-by-using-bulk-insert-or-openrowset-bulk-sql-server.md).  
  
### <a name="permissions"></a>Permissões  
 A permissão INSERT é necessária na tabela de destino.  
  
 Inserir as permissões padrão para membros do **sysadmin** função de servidor fixa, o **db_owner** e **db_datawriter** fixo de funções de banco de dados e o proprietário da tabela. Membros de **sysadmin**, **db_owner**e o **db_securityadmin** funções e o proprietário da tabela podem transferir permissões a outros usuários.  
  
 Para executar INSERT com a opção BULK da função OPENROWSET, você deve ser um membro do **sysadmin** função fixa de servidor ou o **bulkadmin** função de servidor fixa.  
  
##  <a name="InsertExamples"></a> Exemplos  
  
|Categoria|Elementos de sintaxe em destaque|  
|--------------|------------------------------|  
|[Sintaxe básica](#BasicSyntax)|INSERT • construtor de valor de tabela|  
|[Manipulando valores de coluna](#ColumnValues)|IDENTITY • NEWID • valores padrão • Tipos definidos pelo usuário|  
|[Inserindo dados de outras tabelas](#OtherTables)|INSERT…SELECT • INSERT…EXECUTE • expressão de tabela comum WITH • TOP • OFFSET FETCH|  
|[Especificando objetos de destino que não sejam de tabelas padrão](#TargetObjects)|Exibições • variáveis de tabela|  
|[Inserindo linhas em uma tabela remota](#RemoteTables)|Servidor vinculado • Função de conjunto de linhas OPENQUERY • Função de conjunto de linhas OPENDATASOURCE|  
|[Carregando dados de tabelas ou arquivos de dados em massa](#BulkLoad)|INSERT…SELECT • Função OPENROWSET|  
|[Substituindo o comportamento padrão do otimizador de consulta usando dicas](#TableHints)|Dicas de tabela|  
|[Capturando os resultados da instrução INSERT](#CaptureResults)|cláusula OUTPUT|  
  
###  <a name="BasicSyntax"></a>Sintaxe básica  
 Os exemplos nesta seção demonstram a funcionalidade básica da instrução INSERT usando a sintaxe mínima necessária.  
  
#### <a name="a-inserting-a-single-row-of-data"></a>A. Inserindo uma única linha de dados  
 O exemplo a seguir insere uma linha na tabela `Production.UnitMeasure` do banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]. As colunas nesta tabela são `UnitMeasureCode`, `Name` e `ModifiedDate`. Como os valores para todas as colunas são fornecidos e listados na mesma ordem que as colunas na tabela, os nomes de coluna não precisa ser especificado na lista de colunas*.*  
  
```  
INSERT INTO Production.UnitMeasure  
VALUES (N'FT', N'Feet', '20080414');  
```  
  
#### <a name="b-inserting-multiple-rows-of-data"></a>B. Inserindo várias linhas de dados  
 O exemplo a seguir usa o [construtor de valor de tabela](../../t-sql/queries/table-value-constructor-transact-sql.md) para inserir três linhas no `Production.UnitMeasure` tabela o [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] banco de dados em uma única instrução INSERT. Como os valores de todas as colunas são fornecidos e listados na mesma ordem que as colunas da tabela, os nomes das colunas não precisam ser especificados na lista de colunas.  
  
```  
INSERT INTO Production.UnitMeasure  
VALUES (N'FT2', N'Square Feet ', '20080923'), (N'Y', N'Yards', '20080923')
    , (N'Y3', N'Cubic Yards', '20080923');  
```  
  
#### <a name="c-inserting-data-that-is-not-in-the-same-order-as-the-table-columns"></a>C. Inserindo dados que não estão na mesma ordem que as colunas da tabela  
 O exemplo a seguir usa uma lista de colunas para especificar explicitamente os valores inseridos em cada coluna. A ordem das colunas no `Production.UnitMeasure` tabela o [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] banco de dados é `UnitMeasureCode`, `Name`, `ModifiedDate`; no entanto, as colunas não são listadas na ordem em *column_list*.  
  
```  
INSERT INTO Production.UnitMeasure (Name, UnitMeasureCode,  
    ModifiedDate)  
VALUES (N'Square Yards', N'Y2', GETDATE());  
```  
  
###  <a name="ColumnValues"></a>Manipulando valores de coluna  
 Os exemplos nesta seção demonstram métodos de inserção de valores em colunas que são definidas com uma propriedade de identidade, o valor padrão, ou são definidas com tipos de dados, como **uniqueidentifer** ou colunas do tipo definido pelo usuário.  
  
#### <a name="d-inserting-data-into-a-table-with-columns-that-have-default-values"></a>D. Inserindo dados em uma tabela com colunas que têm valores padrão  
 O exemplo a seguir mostra como inserir linhas em uma tabela com colunas que geram automaticamente um valor ou têm um valor padrão. `Column_1` é uma coluna computada que gera automaticamente um valor concatenando uma cadeia de caracteres com o valor inserido em `column_2`. `Column_2` é definido com uma restrição padrão. Se um valor não for especificado para essa coluna, o valor padrão será usado. `Column_3`é definido com o **rowversion** tipo de dados, que gera automaticamente um número binário incremental exclusivo. `Column_4` não gera um valor automaticamente. Quando um valor para esta coluna não é especificado, NULL é inserido. As instruções INSERT inserem linhas que contêm valores para algumas das colunas, mas não todas. Na última instrução INSERT, nenhuma coluna é especificada e somente os valores padrão são inseridos com o uso da cláusula DEFAULT VALUES.  
  
```  
CREATE TABLE dbo.T1   
(  
    column_1 AS 'Computed column ' + column_2,   
    column_2 varchar(30)   
        CONSTRAINT default_name DEFAULT ('my column default'),  
    column_3 rowversion,  
    column_4 varchar(40) NULL  
);  
GO  
INSERT INTO dbo.T1 (column_4)   
    VALUES ('Explicit value');  
INSERT INTO dbo.T1 (column_2, column_4)   
    VALUES ('Explicit value', 'Explicit value');  
INSERT INTO dbo.T1 (column_2)   
    VALUES ('Explicit value');  
INSERT INTO T1 DEFAULT VALUES;   
GO  
SELECT column_1, column_2, column_3, column_4  
FROM dbo.T1;  
GO  
```  
  
#### <a name="e-inserting-data-into-a-table-with-an-identity-column"></a>E. Inserindo dados em uma tabela com uma coluna de identidade  
 O exemplo a seguir mostra métodos diferentes para inserção de dados em uma coluna de identidade. As primeiras duas instruções INSERT permitem identificar valores de identidade a serem gerados para as novas linhas. A terceira instrução INSERT substitui a propriedade IDENTITY da coluna com a instrução SET IDENTITY_INSERT e insere um valor explícito na coluna de identidade.  
  
```  
CREATE TABLE dbo.T1 ( column_1 int IDENTITY, column_2 VARCHAR(30));  
GO  
INSERT T1 VALUES ('Row #1');  
INSERT T1 (column_2) VALUES ('Row #2');  
GO  
SET IDENTITY_INSERT T1 ON;  
GO  
INSERT INTO T1 (column_1,column_2)   
    VALUES (-99, 'Explicit identity value');  
GO  
SELECT column_1, column_2  
FROM T1;  
GO  
```  
  
#### <a name="f-inserting-data-into-a-uniqueidentifier-column-by-using-newid"></a>F. Inserindo dados em uma coluna uniqueidentifier usando NEWID()  
 O exemplo a seguir usa o [NEWID](../../t-sql/functions/newid-transact-sql.md)função () para obter um GUID para `column_2`. Ao contrário de colunas de identidade, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] não gera automaticamente valores para colunas com o [uniqueidentifier](../../t-sql/data-types/uniqueidentifier-transact-sql.md) tipo de dados, conforme mostrado pela segunda `INSERT` instrução.  
  
```  
CREATE TABLE dbo.T1   
(  
    column_1 int IDENTITY,   
    column_2 uniqueidentifier,  
);  
GO  
INSERT INTO dbo.T1 (column_2)   
    VALUES (NEWID());  
INSERT INTO T1 DEFAULT VALUES;   
GO  
SELECT column_1, column_2  
FROM dbo.T1;  
  
```  
  
#### <a name="g-inserting-data-into-user-defined-type-columns"></a>G. Inserindo dados em colunas de tipo definido pelo usuário  
 As instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] a seguir inserem três linhas na coluna `PointValue` da tabela `Points`. Essa coluna usa um [tipo CLR definido pelo usuário](../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md) (UDT). O tipo de dados `Point` consiste em valores inteiros de X e Y que são expostos como propriedades do UDT. Você deve usar a função CAST ou CONVERT para converter os valores X e Y delimitados por vírgulas no tipo `Point`. As duas primeiras instruções usam a função CONVERT para converter um valor de cadeia de caracteres para o `Point` tipo e a terceira instrução usa a função CAST. Para obter mais informações, consulte [manipulando dados de UDT](../../relational-databases/clr-integration-database-objects-user-defined-types/working-with-user-defined-types-manipulating-udt-data.md).  
  
```  
INSERT INTO dbo.Points (PointValue) VALUES (CONVERT(Point, '3,4'));  
INSERT INTO dbo.Points (PointValue) VALUES (CONVERT(Point, '1,5'));  
INSERT INTO dbo.Points (PointValue) VALUES (CAST ('1,99' AS Point));  
```  
  
###  <a name="OtherTables"></a>Inserindo dados de outras tabelas  
 Os exemplos nesta seção demonstram métodos para a inserção de linhas de uma tabela em outra tabela.  
  
#### <a name="h-using-the-select-and-execute-options-to-insert-data-from-other-tables"></a>H. Usando as opções SELECT e EXECUTE para inserir dados de outras tabelas  
 O exemplo a seguir mostra como inserir dados de uma tabela em outra tabela usando INSERT...SELECT ou INSERT...EXECUTE. Cada um é baseado em uma instrução SELECT de várias tabelas que inclui uma expressão e um valor literal na lista de colunas.  
  
 A primeira instrução INSERT usa uma instrução SELECT para derivar os dados das tabelas de origem (`Employee`, `SalesPerson`, e `Person`) no [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] banco de dados e armazenar o conjunto de resultados no `EmployeeSales` tabela. A segunda instrução INSERT usa a cláusula EXECUTE para chamar um procedimento armazenado que contém a instrução SELECT, e a terceira INSERT usa a cláusula EXECUTE para referenciar a instrução SELECT como uma cadeia literal.  
  
```  
CREATE TABLE dbo.EmployeeSales  
( DataSource   varchar(20) NOT NULL,  
  BusinessEntityID   varchar(11) NOT NULL,  
  LastName     varchar(40) NOT NULL,  
  SalesDollars money NOT NULL  
);  
GO  
CREATE PROCEDURE dbo.uspGetEmployeeSales   
AS   
    SET NOCOUNT ON;  
    SELECT 'PROCEDURE', sp.BusinessEntityID, c.LastName,   
        sp.SalesYTD   
    FROM Sales.SalesPerson AS sp    
    INNER JOIN Person.Person AS c  
        ON sp.BusinessEntityID = c.BusinessEntityID  
    WHERE sp.BusinessEntityID LIKE '2%'  
    ORDER BY sp.BusinessEntityID, c.LastName;  
GO  
--INSERT...SELECT example  
INSERT INTO dbo.EmployeeSales  
    SELECT 'SELECT', sp.BusinessEntityID, c.LastName, sp.SalesYTD   
    FROM Sales.SalesPerson AS sp  
    INNER JOIN Person.Person AS c  
        ON sp.BusinessEntityID = c.BusinessEntityID  
    WHERE sp.BusinessEntityID LIKE '2%'  
    ORDER BY sp.BusinessEntityID, c.LastName;  
GO  
--INSERT...EXECUTE procedure example  
INSERT INTO dbo.EmployeeSales   
EXECUTE dbo.uspGetEmployeeSales;  
GO  
--INSERT...EXECUTE('string') example  
INSERT INTO dbo.EmployeeSales   
EXECUTE   
('  
SELECT ''EXEC STRING'', sp.BusinessEntityID, c.LastName,   
    sp.SalesYTD   
    FROM Sales.SalesPerson AS sp   
    INNER JOIN Person.Person AS c  
        ON sp.BusinessEntityID = c.BusinessEntityID  
    WHERE sp.BusinessEntityID LIKE ''2%''  
    ORDER BY sp.BusinessEntityID, c.LastName  
');  
GO  
--Show results.  
SELECT DataSource,BusinessEntityID,LastName,SalesDollars  
FROM dbo.EmployeeSales;  
```  
  
#### <a name="i-using-with-common-table-expression-to-define-the-data-inserted"></a>I. Usando a expressão de tabela comum WITH para definir os dados inseridos  
 O exemplo a seguir cria a tabela `NewEmployee` no banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]. Uma expressão de tabela comum (`EmployeeTemp`) define as linhas de uma ou mais tabelas a serem inseridas na tabela `NewEmployee`. A instrução INSERT faz referência às colunas na expressão de tabela comum.  
  
```  
CREATE TABLE HumanResources.NewEmployee  
(  
    EmployeeID int NOT NULL,  
    LastName nvarchar(50) NOT NULL,  
    FirstName nvarchar(50) NOT NULL,  
    PhoneNumber Phone NULL,  
    AddressLine1 nvarchar(60) NOT NULL,  
    City nvarchar(30) NOT NULL,  
    State nchar(3) NOT NULL,   
    PostalCode nvarchar(15) NOT NULL,  
    CurrentFlag Flag  
);  
GO  
WITH EmployeeTemp (EmpID, LastName, FirstName, Phone,   
                   Address, City, StateProvince,   
                   PostalCode, CurrentFlag)  
AS (SELECT   
       e.BusinessEntityID, c.LastName, c.FirstName, pp.PhoneNumber,  
       a.AddressLine1, a.City, sp.StateProvinceCode,   
       a.PostalCode, e.CurrentFlag  
    FROM HumanResources.Employee e  
        INNER JOIN Person.BusinessEntityAddress AS bea  
        ON e.BusinessEntityID = bea.BusinessEntityID  
        INNER JOIN Person.Address AS a  
        ON bea.AddressID = a.AddressID  
        INNER JOIN Person.PersonPhone AS pp  
        ON e.BusinessEntityID = pp.BusinessEntityID  
        INNER JOIN Person.StateProvince AS sp  
        ON a.StateProvinceID = sp.StateProvinceID  
        INNER JOIN Person.Person as c  
        ON e.BusinessEntityID = c.BusinessEntityID  
    )  
INSERT INTO HumanResources.NewEmployee   
    SELECT EmpID, LastName, FirstName, Phone,   
           Address, City, StateProvince, PostalCode, CurrentFlag  
    FROM EmployeeTemp;  
GO  
```  
  
#### <a name="j-using-top-to-limit-the-data-inserted-from-the-source-table"></a>J. Usando TOP para limitar os dados inseridos na tabela de origem  
 O exemplo a seguir cria a tabela `EmployeeSales` e insere o nome e os dados de vendas acumuladas no ano dos cinco funcionários principais aleatórios da tabela `HumanResources.Employee` no banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]. A instrução INSERT escolhe quaisquer cinco linhas retornadas pela instrução `SELECT`. A cláusula OUTPUT exibe as linhas inseridas na tabela `EmployeeSales`. Observe que a cláusula ORDER BY na instrução SELECT não é usada para determinar os cinco funcionários principais.  
  
```  
CREATE TABLE dbo.EmployeeSales  
( EmployeeID   nvarchar(11) NOT NULL,  
  LastName     nvarchar(20) NOT NULL,  
  FirstName    nvarchar(20) NOT NULL,  
  YearlySales  money NOT NULL  
 );  
GO  
INSERT TOP(5)INTO dbo.EmployeeSales  
    OUTPUT inserted.EmployeeID, inserted.FirstName, 
        inserted.LastName, inserted.YearlySales  
    SELECT sp.BusinessEntityID, c.LastName, c.FirstName, sp.SalesYTD   
    FROM Sales.SalesPerson AS sp  
    INNER JOIN Person.Person AS c  
        ON sp.BusinessEntityID = c.BusinessEntityID  
    WHERE sp.SalesYTD > 250000.00  
    ORDER BY sp.SalesYTD DESC;  
```  
  
 Se você precisar usar TOP para inserir linhas em uma ordem cronológica significativa, deverá usar TOP com ORDER BY em uma instrução de subseleção, conforme mostrado no exemplo a seguir. A cláusula OUTPUT exibe as linhas inseridas na tabela `EmployeeSales`. Observe que os cinco funcionários principais agora são inseridos com base nos resultados da cláusula ORDER BY em vez de linhas aleatórias.  
  
```  
INSERT INTO dbo.EmployeeSales  
    OUTPUT inserted.EmployeeID, inserted.FirstName, 
        inserted.LastName, inserted.YearlySales  
    SELECT TOP (5) sp.BusinessEntityID, c.LastName, c.FirstName, sp.SalesYTD   
    FROM Sales.SalesPerson AS sp  
    INNER JOIN Person.Person AS c  
        ON sp.BusinessEntityID = c.BusinessEntityID  
    WHERE sp.SalesYTD > 250000.00  
    ORDER BY sp.SalesYTD DESC;  
```  
  
###  <a name="TargetObjects"></a>Especificando objetos de destino que não sejam de tabelas padrão  
 Os exemplos desta seção demonstram como inserir linhas com a especificação de uma exibição ou variável de tabela.  
  
#### <a name="k-inserting-data-by-specifying-a-view"></a>K. Inserindo dados especificando uma exibição  
 O exemplo a seguir especifica um nome de exibição como objeto de destino. No entanto, a nova linha é inserida na tabela básica subjacente. A ordem dos valores na instrução `INSERT` deve corresponder à ordem das colunas da exibição. Para obter mais informações, consulte [modificar dados por meio de um modo de exibição](../../relational-databases/views/modify-data-through-a-view.md).  
  
```  
CREATE TABLE T1 ( column_1 int, column_2 varchar(30));  
GO  
CREATE VIEW V1 AS   
SELECT column_2, column_1   
FROM T1;  
GO  
INSERT INTO V1   
    VALUES ('Row 1',1);  
GO  
SELECT column_1, column_2   
FROM T1;  
GO  
SELECT column_1, column_2  
FROM V1;  
GO  
```  
  
#### <a name="l-inserting-data-into-a-table-variable"></a>L. Inserindo dados em uma variável de tabela  
 O exemplo a seguir especifica uma variável de tabela como o objeto de destino no banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)].  
  
```  
-- Create the table variable.  
DECLARE @MyTableVar table(  
    LocationID int NOT NULL,  
    CostRate smallmoney NOT NULL,  
    NewCostRate AS CostRate * 1.5,  
    ModifiedDate datetime);  
  
-- Insert values into the table variable.  
INSERT INTO @MyTableVar (LocationID, CostRate, ModifiedDate)  
    SELECT LocationID, CostRate, GETDATE() 
    FROM Production.Location  
    WHERE CostRate > 0;  
  
-- View the table variable result set.  
SELECT * FROM @MyTableVar;  
GO  
```  
  
###  <a name="RemoteTables"></a>Inserindo linhas em uma tabela remota  
 Os exemplos nesta seção demonstram como inserir linhas em uma tabela de destino remoto usando um [servidor vinculado](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md) ou um [função de conjunto de linhas](../../t-sql/functions/rowset-functions-transact-sql.md) para referenciar a tabela remota.  
  
#### <a name="m-inserting-data-into-a-remote-table-by-using-a-linked-server"></a>M. Inserindo dados em uma tabela remota usando um servidor vinculado  
 O exemplo a seguir insere linhas em uma tabela remota. O exemplo começa criando um link para a fonte de dados remota usando [sp_addlinkedserver](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md). O nome do servidor vinculado, `MyLinkServer`, é especificado como parte do nome do objeto de quatro partes no formulário *Object*.  
  
**Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
```  
USE master;  
GO  
-- Create a link to the remote data source.   
-- Specify a valid server name for @datasrc as 'server_name' 
-- or 'server_nameinstance_name'.  
  
EXEC sp_addlinkedserver @server = N'MyLinkServer',  
    @srvproduct = N' ',  
    @provider = N'SQLNCLI',   
    @datasrc = N'server_name',  
    @catalog = N'AdventureWorks2012';  
GO  
```  
  
```  
-- Specify the remote data source in the FROM clause using a four-part name   
-- in the form linked_server.catalog.schema.object.  
  
INSERT INTO MyLinkServer.AdventureWorks2012.HumanResources.Department (Name, GroupName)  
VALUES (N'Public Relations', N'Executive General and Administration');  
GO  
```  
  
#### <a name="n-inserting-data-into-a-remote-table-by-using-the-openquery-function"></a>N. Inserindo dados em uma tabela remota usando a função OPENQUERY  
 O exemplo a seguir insere uma linha em uma tabela remota especificando a [OPENQUERY](../../t-sql/functions/openquery-transact-sql.md) função de conjunto de linhas. O nome de servidor vinculado criado no exemplo anterior é usado neste exemplo.  
  
**Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
```  
INSERT OPENQUERY (MyLinkServer, 
    'SELECT Name, GroupName 
     FROM AdventureWorks2012.HumanResources.Department')  
VALUES ('Environmental Impact', 'Engineering');  
GO  
```  
  
#### <a name="o-inserting-data-into-a-remote-table-by-using-the-opendatasource-function"></a>O. Inserindo dados em uma tabela remota usando a função OPENDATASOURCE  
 O exemplo a seguir insere uma linha em uma tabela remota especificando a [OPENDATASOURCE](../../t-sql/functions/opendatasource-transact-sql.md) função de conjunto de linhas. Especifique um nome de servidor válido para a fonte de dados usando o formato *nome_do_servidor* ou *server_name\instance_name*.  
  
**Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
```  
-- Use the OPENDATASOURCE function to specify the remote data source.  
-- Specify a valid server name for Data Source using the format 
-- server_name or server_nameinstance_name.  
  
INSERT INTO OPENDATASOURCE('SQLNCLI',  
    'Data Source= <server_name>; Integrated Security=SSPI')  
    .AdventureWorks2012.HumanResources.Department (Name, GroupName)  
    VALUES (N'Standards and Methods', 'Quality Assurance');  
GO  
```  
  
#### <a name="p-inserting-into-an-external-table-created-using-polybase"></a>P. Inserindo em uma tabela externa criada usando o PolyBase  
 Exporte dados do SQL Server para o Hadoop ou armazenamento do Azure. Primeiro, crie uma tabela externa que aponta para o diretório ou arquivo de destino. Em seguida, use INSERT INTO para exportar dados de uma tabela do SQL Server local para uma fonte de dados externa. A instrução INSERT INTO cria o arquivo ou o diretório de destino se eles não existirem, e os resultados da instrução SELECT são exportados para o local especificado no formato de arquivo especificado.  Para obter mais informações, consulte [Introdução ao PolyBase](../../relational-databases/polybase/get-started-with-polybase.md).  
  
**Aplica-se a**: [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
```  
-- Create an external table.   
CREATE EXTERNAL TABLE [dbo].[FastCustomers2009] (  
        [FirstName] char(25) NOT NULL,   
        [LastName] char(25) NOT NULL,   
        [YearlyIncome] float NULL,   
        [MaritalStatus] char(1) NOT NULL  
)  
WITH (  
        LOCATION='/old_data/2009/customerdata.tbl',  
        DATA_SOURCE = HadoopHDP2,  
        FILE_FORMAT = TextFileFormat,  
        REJECT_TYPE = VALUE,  
        REJECT_VALUE = 0  
);  
  
-- Export data: Move old data to Hadoop while keeping 
-- it query-able via external table.  

INSERT INTO dbo.FastCustomer2009  
SELECT T.* FROM Insured_Customers T1 JOIN CarSensor_Data T2  
ON (T1.CustomerKey = T2.CustomerKey)  
WHERE T2.YearMeasured = 2009 and T2.Speed > 40;  
```  
  
###  <a name="BulkLoad"></a>Carregando dados de tabelas ou arquivos de dados em massa  
 Os exemplos nesta seção demonstram dois métodos para carregar dados em massa em uma tabela usando a instrução INSERT.  
  
#### <a name="q-inserting-data-into-a-heap-with-minimal-logging"></a>Q. Inserindo dados em um heap com registro em log mínimo  
 O exemplo a seguir cria uma nova tabela (um heap) e insere dados de outra tabela nela usando o registro em log mínimo. O exemplo pressupõe que o modelo de recuperação do banco de dados `AdventureWorks2012` esteja definido como FULL. Para assegurar um registro em log mínimo, o modelo de recuperação do banco de dados `AdventureWorks2012` é definido como BULK_LOGGED antes da inserção das linhas e redefinido como FULL após a instrução INSERT INTO...SELECT. Além disso, a dica TABLOCK é especificada para o tabela de destino `Sales.SalesHistory`. Isso garante que a instrução use espaço mínimo no log de transação e seja executada de forma eficaz.  
  
```  
-- Create the target heap.  
CREATE TABLE Sales.SalesHistory(  
    SalesOrderID int NOT NULL,  
    SalesOrderDetailID int NOT NULL,  
    CarrierTrackingNumber nvarchar(25) NULL,  
    OrderQty smallint NOT NULL,  
    ProductID int NOT NULL,  
    SpecialOfferID int NOT NULL,  
    UnitPrice money NOT NULL,  
    UnitPriceDiscount money NOT NULL,  
    LineTotal money NOT NULL,  
    rowguid uniqueidentifier ROWGUIDCOL  NOT NULL,  
    ModifiedDate datetime NOT NULL );  
GO  
-- Temporarily set the recovery model to BULK_LOGGED.  
ALTER DATABASE AdventureWorks2012  
SET RECOVERY BULK_LOGGED;  
GO  
-- Transfer data from Sales.SalesOrderDetail to Sales.SalesHistory  
INSERT INTO Sales.SalesHistory WITH (TABLOCK)  
    (SalesOrderID,   
     SalesOrderDetailID,  
     CarrierTrackingNumber,   
     OrderQty,   
     ProductID,   
     SpecialOfferID,   
     UnitPrice,   
     UnitPriceDiscount,  
     LineTotal,   
     rowguid,   
     ModifiedDate)  
SELECT * FROM Sales.SalesOrderDetail;  
GO  
-- Reset the recovery model.  
ALTER DATABASE AdventureWorks2012  
SET RECOVERY FULL;  
GO  
```  
  
#### <a name="r-using-the-openrowset-function-with-bulk-to-bulk-load-data-into-a-table"></a>R. Usando uma função OPENROWSET com BULK para carregar dados em massa em uma tabela  
 O exemplo a seguir insere linhas de um arquivo de dados em uma tabela especificando a função OPENROWSET. A dica de tabela IGNORE_TRIGGERS é especificada para otimização de desempenho. Para obter mais exemplos, consulte [importação em massa dados usando BULK INSERT ou OPENROWSET &#40; BULK... &#41; &#40; SQL Server &#41; ](../../relational-databases/import-export/import-bulk-data-by-using-bulk-insert-or-openrowset-bulk-sql-server.md).  
  
**Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
```  
INSERT INTO HumanResources.Department WITH (IGNORE_TRIGGERS) (Name, GroupName)  
SELECT b.Name, b.GroupName   
FROM OPENROWSET (  
    BULK 'C:SQLFilesDepartmentData.txt',  
    FORMATFILE = 'C:SQLFilesBulkloadFormatFile.xml',  
    ROWS_PER_BATCH = 15000)AS b ;  
```  
  
###  <a name="TableHints"></a>Substituindo o comportamento padrão do otimizador de consulta usando dicas  
 Os exemplos nesta seção demonstram como usar [dicas de tabela](../../t-sql/queries/hints-transact-sql-table.md) para substituir temporariamente o comportamento padrão do otimizador de consulta ao processar a instrução INSERT.  
  
> [!CAUTION]  
>  Como o otimizador de consulta do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] normalmente seleciona o melhor plano de execução para uma consulta, é recomendável que desenvolvedores e administradores de banco de dados experientes usem as dicas apenas como um último recurso.  
  
#### <a name="s-using-the-tablock-hint-to-specify-a-locking-method"></a>S. Usando a dica TABLOCK para especificar um método de bloqueio  
 O exemplo a seguir especifica que um bloqueio exclusivo (X) é executado na tabela Production.Location e é mantido até o fim da instrução INSERT.  
  
**Aplica-se a**: [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)].  
  
```  
INSERT INTO Production.Location WITH (XLOCK)  
(Name, CostRate, Availability)  
VALUES ( N'Final Inventory', 15.00, 80.00);  
```  
  
###  <a name="CaptureResults"></a>Capturando os resultados da instrução INSERT  
 Os exemplos nesta seção demonstram como usar o [cláusula OUTPUT](../../t-sql/queries/output-clause-transact-sql.md) para retornar informações ou expressões baseadas em, cada linha afetada por uma instrução INSERT. Esses resultados podem ser retornados ao aplicativo de processamento para uso em mensagens de confirmação, arquivamentos e outros requisitos similares de aplicativo.  
  
#### <a name="t-using-output-with-an-insert-statement"></a>T. Usando OUTPUT com uma instrução INSERT  
 O exemplo a seguir insere uma linha na tabela `ScrapReason` e usa a cláusula `OUTPUT` para retornar os resultados da instrução para a variável de tabela `@MyTableVar`. Como a coluna `ScrapReasonID` está definida com uma propriedade `IDENTITY`, não é especificado um valor na instrução `INSERT` para essa coluna. No entanto, observe que o valor gerado pelo [!INCLUDE[ssDE](../../includes/ssde-md.md)] para a coluna é retornado na cláusula `OUTPUT` na coluna `INSERTED.ScrapReasonID`.  
  
```  
DECLARE @MyTableVar table( NewScrapReasonID smallint,  
                           Name varchar(50),  
                           ModifiedDate datetime);  
INSERT Production.ScrapReason  
    OUTPUT INSERTED.ScrapReasonID, INSERTED.Name, INSERTED.ModifiedDate  
        INTO @MyTableVar  
VALUES (N'Operator error', GETDATE());  
  
--Display the result set of the table variable.  
SELECT NewScrapReasonID, Name, ModifiedDate FROM @MyTableVar;  
--Display the result set of the table.  
SELECT ScrapReasonID, Name, ModifiedDate   
FROM Production.ScrapReason;  
```  
  
#### <a name="u-using-output-with-identity-and-computed-columns"></a>U. Usando OUTPUT com colunas de identidade e colunas computadas  
 O exemplo a seguir cria a tabela `EmployeeSales` e, em seguida, insere várias linhas nela por meio de uma instrução INSERT com uma instrução SELECT para recuperar dados das tabelas de origem. A tabela `EmployeeSales` contém uma coluna de identidade (`EmployeeID`) e uma coluna computada (`ProjectedSales`). Como esses valores são gerados pelo [!INCLUDE[ssDE](../../includes/ssde-md.md)] durante a operação de inserção, nenhuma dessas colunas pode ser definida em `@MyTableVar`.  
  
```  
CREATE TABLE dbo.EmployeeSales  
( EmployeeID   int IDENTITY (1,5)NOT NULL,  
  LastName     nvarchar(20) NOT NULL,  
  FirstName    nvarchar(20) NOT NULL,  
  CurrentSales money NOT NULL,  
  ProjectedSales AS CurrentSales * 1.10   
);  
GO  
DECLARE @MyTableVar table(  
  LastName     nvarchar(20) NOT NULL,  
  FirstName    nvarchar(20) NOT NULL,  
  CurrentSales money NOT NULL  
  );  
  
INSERT INTO dbo.EmployeeSales (LastName, FirstName, CurrentSales)  
  OUTPUT INSERTED.LastName,   
         INSERTED.FirstName,   
         INSERTED.CurrentSales  
  INTO @MyTableVar  
    SELECT c.LastName, c.FirstName, sp.SalesYTD  
    FROM Sales.SalesPerson AS sp  
    INNER JOIN Person.Person AS c  
        ON sp.BusinessEntityID = c.BusinessEntityID  
    WHERE sp.BusinessEntityID LIKE '2%'  
    ORDER BY c.LastName, c.FirstName;  
  
SELECT LastName, FirstName, CurrentSales  
FROM @MyTableVar;  
GO  
SELECT EmployeeID, LastName, FirstName, CurrentSales, ProjectedSales  
FROM dbo.EmployeeSales;  
```  
  
#### <a name="v-inserting-data-returned-from-an-output-clause"></a>V. Inserindo dados retornados de uma cláusula OUTPUT  
 O exemplo a seguir captura dados retornados pela cláusula OUTPUT de uma instrução MERGE e insere esses dados em outra tabela. A instrução MERGE atualiza diariamente a coluna `Quantity` da tabela `ProductInventory`, com base em pedidos processados na tabela `SalesOrderDetail` do banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]. Ela também exclui linhas de produtos cujos inventários chegaram a 0. O exemplo captura as linhas excluídas e as insere em outra tabela, `ZeroInventory`, que rastreia produtos sem-estoque.  
  
```  
--Create ZeroInventory table.  
CREATE TABLE Production.ZeroInventory (DeletedProductID int, RemovedOnDate DateTime);  
GO  
  
INSERT INTO Production.ZeroInventory (DeletedProductID, RemovedOnDate)  
SELECT ProductID, GETDATE()  
FROM  
(   MERGE Production.ProductInventory AS pi  
    USING (SELECT ProductID, SUM(OrderQty) FROM Sales.SalesOrderDetail AS sod  
           JOIN Sales.SalesOrderHeader AS soh  
           ON sod.SalesOrderID = soh.SalesOrderID  
           AND soh.OrderDate = '20070401'  
           GROUP BY ProductID) AS src (ProductID, OrderQty)  
    ON (pi.ProductID = src.ProductID)  
    WHEN MATCHED AND pi.Quantity - src.OrderQty <= 0  
        THEN DELETE  
    WHEN MATCHED  
        THEN UPDATE SET pi.Quantity = pi.Quantity - src.OrderQty  
    OUTPUT $action, deleted.ProductID) AS Changes (Action, ProductID)  
WHERE Action = 'DELETE';  
IF @@ROWCOUNT = 0  
PRINT 'Warning: No rows were inserted';  
GO  
SELECT DeletedProductID, RemovedOnDate FROM Production.ZeroInventory;  
```  

#### <a name="w-inserting-data-using-the-select-option"></a>W. Inserindo dados usando a opção selecionar  
 O exemplo a seguir mostra como inserir várias linhas de dados usando uma instrução INSERT com uma opção de seleção. A primeira `INSERT` instrução usa um `SELECT` instrução diretamente para recuperar dados da tabela de origem, e, em seguida armazenar o resultado definido no `EmployeeTitles` tabela.  
  
```  
CREATE TABLE EmployeeTitles  
( EmployeeKey   INT NOT NULL,  
  LastName     varchar(40) NOT NULL,  
  Title      varchar(50) NOT NULL  
);  
INSERT INTO EmployeeTitles  
    SELECT EmployeeKey, LastName, Title   
    FROM ssawPDW.dbo.DimEmployee  
    WHERE EndDate IS NULL;  
```  
  
#### <a name="x-specifying-a-label-with-the-insert-statement"></a>X. Especificando um rótulo com a instrução INSERT  
 O exemplo a seguir mostra o uso de um rótulo com uma instrução INSERT.  
  
```  
-- Uses AdventureWorks  
  
INSERT INTO DimCurrency   
VALUES (500, N'C1', N'Currency1')  
OPTION ( LABEL = N'label1' );  
```  
  
#### <a name="y-using-a-label-and-a-query-hint-with-the-insert-statement"></a>Y. Usando um rótulo e dica de consulta com a instrução INSERT  
 Esta consulta mostra a sintaxe básica para usar um rótulo e dica de junção de consulta com a instrução INSERT. Depois que a consulta é enviada para o nó de controle, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], em execução em nós de computação, serão aplicadas a estratégia de junção de hash ao gerar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] plano de consulta. Para obter mais informações sobre dicas de junção e como usar a cláusula OPTION, consulte [opção (SQL Server PDW)](http://msdn.microsoft.com/en-us/72bbce98-305b-42fa-a19f-d89620621ecc).  
  
```  
-- Uses AdventureWorks  
  
INSERT INTO DimCustomer (CustomerKey, CustomerAlternateKey, 
    FirstName, MiddleName, LastName )   
SELECT ProspectiveBuyerKey, ProspectAlternateKey, 
    FirstName, MiddleName, LastName  
FROM ProspectiveBuyer p JOIN DimGeography g ON p.PostalCode = g.PostalCode  
WHERE g.CountryRegionCode = 'FR'  
OPTION ( LABEL = 'Add French Prospects', HASH JOIN);  
```  
  
## <a name="see-also"></a>Consulte também  
 [BULK INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md)   
 [DELETE &#40;Transact-SQL&#41;](../../t-sql/statements/delete-transact-sql.md)   
 [EXECUTE &#40;Transact-SQL&#41;](../../t-sql/language-elements/execute-transact-sql.md)   
 [FROM &#40;Transact-SQL&#41;](../../t-sql/queries/from-transact-sql.md)   
 [IDENTITY &#40;Propriedade&#41; &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql-identity-property.md)   
 [NEWID &#40; Transact-SQL &#41;](../../t-sql/functions/newid-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [UPDATE &#40;Transact-SQL&#41;](../../t-sql/queries/update-transact-sql.md)   
 [Mesclar &#40; Transact-SQL &#41;](../../t-sql/statements/merge-transact-sql.md)   
 [Cláusula OUTPUT &#40; Transact-SQL &#41;](../../t-sql/queries/output-clause-transact-sql.md)   
 [Usar as tabelas inseridas e excluídas](../../relational-databases/triggers/use-the-inserted-and-deleted-tables.md)  
  
  




