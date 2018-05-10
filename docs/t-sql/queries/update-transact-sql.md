---
title: UPDATE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: t-sql|queries
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- UPDATE_TSQL
- UPDATE
dev_langs:
- TSQL
helpviewer_keywords:
- DML [SQL Server], UPDATE statement
- data updates [SQL Server], UPDATE statement
- updating data [SQL Server]
- TOP clause, UPDATE
- OUTPUT clause
- large value data types
- data manipulation language [SQL Server], UPDATE statement
- user-defined types [SQL Server], modifying
- INSTEAD OF triggers
- modifying data [SQL Server], UPDATE statement
- data modifications [SQL Server], UPDATE statement
- large data, modifying
- .WRITE clause
- table modifications [SQL Server], UPDATE statement
- UDTs [SQL Server], modifying
- UPDATE statement [SQL Server], about UPDATE statement
- LOB data [SQL Server], modifying
- modifying LOB data
- UPDATE statement [SQL Server]
- FROM clause, UPDATE statement
- WHERE clause, UPDATE statement
ms.assetid: 40e63302-0c68-4593-af3e-6d190181fee7
caps.latest.revision: 91
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: b89e99a4ddc1848193d20cf9f49e591b4360a767
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="update-transact-sql"></a>UPDATE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Altera dados existentes em uma tabela ou exibição no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Para obter exemplos, confira [Exemplos](#UpdateExamples).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```sql  
-- Syntax for SQL Server and Azure SQL Database  

[ WITH <common_table_expression> [...n] ]  
UPDATE   
    [ TOP ( expression ) [ PERCENT ] ]   
    { { table_alias | <object> | rowset_function_limited   
         [ WITH ( <Table_Hint_Limited> [ ...n ] ) ]  
      }  
      | @table_variable      
    }  
    SET  
        { column_name = { expression | DEFAULT | NULL }  
          | { udt_column_name.{ { property_name = expression  
                                | field_name = expression }  
                                | method_name ( argument [ ,...n ] )  
                              }  
          }  
          | column_name { .WRITE ( expression , @Offset , @Length ) }  
          | @variable = expression  
          | @variable = column = expression  
          | column_name { += | -= | *= | /= | %= | &= | ^= | |= } expression  
          | @variable { += | -= | *= | /= | %= | &= | ^= | |= } expression  
          | @variable = column { += | -= | *= | /= | %= | &= | ^= | |= } expression  
        } [ ,...n ]   
  
    [ <OUTPUT Clause> ]  
    [ FROM{ <table_source> } [ ,...n ] ]   
    [ WHERE { <search_condition>   
            | { [ CURRENT OF   
                  { { [ GLOBAL ] cursor_name }   
                      | cursor_variable_name   
                  }   
                ]  
              }  
            }   
    ]   
    [ OPTION ( <query_hint> [ ,...n ] ) ]  
[ ; ]  
  
<object> ::=  
{   
    [ server_name . database_name . schema_name .   
    | database_name .[ schema_name ] .   
    | schema_name .  
    ]  
    table_or_view_name}  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  

UPDATE [ database_name . [ schema_name ] . | schema_name . ] table_name   
SET { column_name = { expression | NULL } } [ ,...n ]  
[ FROM from_clause ]  
[ WHERE <search_condition> ]   
[ OPTION ( LABEL = label_name ) ]  
[;]  
```  
  
## <a name="arguments"></a>Argumentos  
 WITH \<common_table_expression>  
 Especifica a exibição ou o conjunto de resultados nomeado temporário, também conhecido como CTE (expressão de tabela comum), definido dentro do escopo da instrução UPDATE. O conjunto de resultados da CTE é derivado de uma consulta simples e é referido pela instrução UPDATE.  
  
 Expressões de tabela comuns também podem ser usadas com as instruções SELECT, INSERT, DELETE e CREATE VIEW. Para obter mais informações, confira [WITH common_table_expression &#40;Transact-SQL&#41;](../../t-sql/queries/with-common-table-expression-transact-sql.md).  
  
 TOP **(** *expression***)** [ PERCENT ]  
 Especifica o número ou o percentual de linhas atualizadas. *expression* pode ser um número ou uma porcentagem das linhas.  
  
 As linhas referenciadas na expressão TOP usada com INSERT, UPDATE ou DELETE não são organizadas em qualquer ordem.  
  
 Os parênteses delimitando a *expressão* em TOP são necessários em instruções INSERT, UPDATE e DELETE. Para obter mais informações, confira [TOP &#40;Transact-SQL&#41;](../../t-sql/queries/top-transact-sql.md).  
  
 *table_alias*  
 O alias especificado na cláusula FROM que representa a tabela ou exibição na qual as linhas devem ser atualizadas.  
  
 *server_name*  
 É o nome do servidor (usando um nome de servidor vinculado ou a função [OPENDATASOURCE](../../t-sql/functions/opendatasource-transact-sql.md) como o nome do servidor) no qual a tabela ou a exibição está localizada. Se *server_name* for especificado, *database_name* e *schema_name* serão necessários.  
  
 *database_name*  
 É o nome do banco de dados.  
  
 *schema_name*  
 É o nome do esquema ao qual a tabela ou exibição pertence.  
  
 *table_or view_name*  
 É o nome da tabela ou exibição na qual as linhas serão atualizadas. A exibição referenciada por *table_or_view_name* precisa ser atualizável e referenciar exatamente uma tabela base na cláusula FROM da exibição. Para obter mais informações sobre exibições atualizáveis, consulte [CREATE VIEW &#40;Transact-SQL&#41;](../../t-sql/statements/create-view-transact-sql.md).  
  
 *rowset_function_limited*  
 É a função [OPENQUERY](../../t-sql/functions/openquery-transact-sql.md) ou [OPENROWSET](../../t-sql/functions/openrowset-transact-sql.md), sujeita aos recursos do provedor.  
  
 WITH **(** \<Table_Hint_Limited> **)**  
 Especifica uma ou mais dicas de tabela permitidas para uma tabela de destino. A palavra-chave WITH e parênteses são necessários. NOLOCK e READUNCOMMITTED não são permitidos. Para obter informações sobre dicas de tabela, confira [Dicas de tabela &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-table.md).  
  
 @*table_variable*  
 Especifica uma variável [table](../../t-sql/data-types/table-transact-sql.md) como uma origem de tabela.  
  
 SET  
 Especifica a lista de colunas ou nomes de variáveis a serem atualizados.  
  
 *column_name*  
 É uma coluna que contém os dados a serem alterados. *column_name* precisa existir em *table_or view_name*. Colunas de identidade não podem ser atualizadas.  
  
 *expressão*  
 É uma variável, valor literal, expressão ou uma instrução de subseleção (incluída com parênteses) que retorna um único valor. O valor retornado pela *expressão* substituirá o valor existente em *column_name* ou em *@variable*.  
  
> [!NOTE]  
>  Ao referenciar os tipos de dados de caractere Unicode **nchar**, **nvarchar** e **ntext**, 'expression' deve ter a letra maiúscula 'N' como prefixo. Se N não for especificado, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] converte a cadeia na página de código correspondente ao agrupamento padrão do banco de dados ou coluna. Qualquer caractere não localizado nessa página de código será perdido.  
  
 DEFAULT  
 Especifica que o valor padrão definido para a coluna deve substituir o valor existente na coluna. Isso também poderá ser usado para alterar a coluna para NULL se ela não tiver nenhum padrão e estiver definida para permitir valores nulos.  
  
 { **+=** | **-=** | **\*=** | **/=** | **%=** | **&=** | **^=** | **|=** }  
 Operador de atribuição composto:  
 +=                       Adicionar e atribuir  
 -=                        Subtrair e atribuir  
 *=                        Multiplicar e atribuir  
 /=                         Dividir e atribuir  
 %=                       Módulo e atribuir  
 &=                        AND bit a bit e atribuir  
 ^=                       XOR bit a bit e atribuir  
 |=                         OR bit a bit e atribuir  
  
 *udt_column_name*  
 É uma coluna de tipo definido pelo usuário.  
  
 *property_name* | *field_name*  
 É uma propriedade pública ou membro de dados público de um tipo definido pelo usuário.  
  
 *method_name* **(** *argument* [ **,**... *n*] **)**  
 É um método modificador público não estático de *udt_column_name* que usa um ou mais argumentos.  
  
 **.** WRITE **(***expressão***,***@Offset***,***@Length***)**  
 Especifica que uma seção do valor de *column_name* deve ser modificada. A *expressão* substitui as unidades de *@Length* de *@Offset* do *column_name*. Somente colunas de **varchar(max)**, **nvarchar(max)** ou **varbinary(max)** podem ser especificadas com esta cláusula. *column_name* não pode ser NULL e não pode ser qualificado com um nome de tabela nem com um alias de tabela.  
  
 A *expressão* é o valor que é copiado para *column_name*. A *expressão* precisa ser avaliada ou ter a capacidade de ser convertida implicitamente no tipo *column_name*. Se a *expressão* for definida como NULL, *@Length* será ignorado e o valor em *column_name* será truncado no *@Offset* especificado.  
  
 *@Offset* é o ponto inicial no valor de *column_name* no qual a *expressão* é escrita. *@Offset* é uma posição ordinal com base em zero, é **bigint** e não pode ser um número negativo. Se *@Offset* for NULL, a operação de atualização acrescentará a *expressão* ao final do valor de *column_name* existente e *@Length* será ignorado. Se @Offset for maior que o comprimento do valor de *column_name*, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] retornará um erro. Se *@Offset* mais *@Length* exceder o final do valor subjacente na coluna, a exclusão ocorrerá até o último caractere do valor. Se *@Offset* mais LEN (*expressão*) for maior do que o tamanho subjacente declarado, ocorrerá um erro.  
  
 *@Length* é o comprimento da seção na coluna, começando em *@Offset*, que é substituído pela *expressão*. *@Length* é **bigint** e não pode ser um número negativo. Se *@Length* for NULL, a operação de atualização removerá todos os dados de *@Offset* até final do valor de *column_name*.  
  
 Para obter mais informações, consulte Comentários.  
  
 **@** *variable*  
 É uma variável declarada definida como o valor retornado pela *expressão*.  
  
 SET **@***variable* = *column* = *expression* define a variável com o mesmo valor que a coluna. Isso é diferente de SET **@***variable* = *column*, *column* = *expression*, que define a variável para o valor de pré-atualização da coluna.  
  
 \<OUTPUT_Clause>  
 Retorna dados atualizados ou expressões com base neles, como parte da operação UPDATE. A cláusula OUTPUT não tem suporte em nenhuma instrução DML destinada a exibições ou tabelas remotas. Para obter mais informações, confira [Cláusula OUTPUT &#40;Transact-SQL&#41;](../../t-sql/queries/output-clause-transact-sql.md).  
  
 FROM \<table_source>  
 Especifica que uma tabela, exibição ou origem de tabela derivada é usada para fornecer os critérios da operação de atualização. Para obter mais informações, consulte [FROM &#40;Transact-SQL&#41;](../../t-sql/queries/from-transact-sql.md).  
  
 Se o objeto que está sendo atualizado for o mesmo que o objeto na cláusula FROM e houver apenas uma referência ao objeto na cláusula FROM, um alias do objeto poder ser especificado ou não. Se o objeto que está sendo atualizado aparecer mais de uma vez na cláusula FROM, uma, e apenas uma, referência ao objeto não deve especificar o alias da tabela. Todas as outras referências ao objeto na cláusula FROM devem incluir um alias de objeto.  
  
 Uma exibição com um gatilho INSTEAD OF UPDATE não pode ser um destino de UPDATE com uma cláusula FROM.  
  
> [!NOTE]  
>  Qualquer chamada para OPENDATASOURCE, OPENQUERY ou OPENROWSET na cláusula FROM é avaliada separada e independentemente de qualquer chamada para essas funções usadas como o destino da atualização, mesmo se argumentos idênticos forem fornecidos às duas chamadas. Em particular, as condições de filtro ou junção aplicadas no resultado de uma dessas chamadas não têm efeito sobre os resultado da outra.  
  
 WHERE  
 Especifica os critérios que limitam as linhas que são atualizadas. Há duas formas de atualização com base na forma em que a clausula WHERE é usada:  
  
-   Atualizações pesquisadas especificam um critério de pesquisa para qualificar as linhas a serem excluídas.  
  
-   Atualizações posicionadas usam a cláusula CURRENT OF para especificar um cursor. A operação de atualização ocorre na posição atual do cursor.  
  
\<search_condition>  
 Especifica o critério a ser atendido para as linhas a serem atualizadas. O critério de pesquisa também pode ser o critério no qual uma junção é baseada. Não há nenhum limite para o número de predicados que podem ser incluídos em um critério de pesquisa. Para obter mais informações sobre predicados e condições de pesquisa, confira [Critério de pesquisa &#40;Transact-SQL&#41;](../../t-sql/queries/search-condition-transact-sql.md).  
  
CURRENT OF  
 Especifica que a atualização é executada na posição atual do cursor especificado.  
  
 Uma atualização posicionada usando uma cláusula WHERE CURRENT OF atualiza a única linha na posição atual do cursor. Isso pode ser mais preciso do que uma atualização pesquisada que usa uma cláusula WHERE \<search_condition> para qualificar as linhas a serem atualizadas. Uma atualização pesquisada modifica várias linhas quando o critério de pesquisa não identifica exclusivamente uma única linha.  
  
GLOBAL  
 Especifica que *cursor_name* se refere a um cursor global.  
  
*cursor_name*  
 É o nome do cursor aberto a partir do qual a busca deve ser feita. Se um cursor global e um cursor local com o nome *cursor_name* existirem, esse argumento fará referência ao cursor global se GLOBAL estiver especificado; caso contrário, fará referência ao cursor local. O cursor deve permitir atualizações.  
  
*cursor_variable_name*  
 É o nome de uma variável de cursor. *cursor_variable_name* precisa fazer referência a um cursor que permita atualizações.  
  
OPTION **(** \<query_hint> [ **,**... *n* ] **)**  
 Especifica que dicas de otimização são usadas para personalizar a maneira como o [!INCLUDE[ssDE](../../includes/ssde-md.md)] processa a instrução. Para obter mais informações, veja [Dicas de consulta &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-query.md).  
  
## <a name="best-practices"></a>Práticas recomendadas  
 Use a função @@ROWCOUNT para retornar o número de linhas inseridas no aplicativo cliente. Para obter mais informações, consulte [@@ROWCOUNT &#40;Transact-SQL&#41;](../../t-sql/functions/rowcount-transact-sql.md).  
  
 Nomes de variáveis podem ser usados em instruções UPDATE para mostrar os valores novos e antigos afetados, mas isso deve ser usado apenas quando a instrução UPDATE afeta um único registro. Se a instrução UPDATE afetar vários registros, para retornar os valores novos e antigos de cada registro, use a [cláusula OUTPUT](../../t-sql/queries/output-clause-transact-sql.md).  
  
 Tenha cuidado ao especificar a cláusula FROM para fornecer os critérios da operação de atualização. Os resultados de uma instrução UPDATE não serão definidos se a instrução incluir uma cláusula FROM que não esteja especificada de maneira que apenas um valor esteja disponível para cada ocorrência de coluna atualizada, ou seja, se a instrução UPDATE não for determinística. Por exemplo, na instrução UPDATE no script a seguir, as duas linhas em `Table1` atendem às qualificações da cláusula FROM na instrução UPDATE; mas não está definido qual linha da `Table1` é usada para atualizar a linha na `Table2.`  
  
```sql  
USE AdventureWorks2012;  
GO  
IF OBJECT_ID ('dbo.Table1', 'U') IS NOT NULL  
    DROP TABLE dbo.Table1;  
GO  
IF OBJECT_ID ('dbo.Table2', 'U') IS NOT NULL  
    DROP TABLE dbo.Table2;  
GO  
CREATE TABLE dbo.Table1   
    (ColA int NOT NULL, ColB decimal(10,3) NOT NULL);  
GO  
CREATE TABLE dbo.Table2   
    (ColA int PRIMARY KEY NOT NULL, ColB decimal(10,3) NOT NULL);  
GO  
INSERT INTO dbo.Table1 VALUES(1, 10.0), (1, 20.0);  
INSERT INTO dbo.Table2 VALUES(1, 0.0);  
GO  
UPDATE dbo.Table2   
SET dbo.Table2.ColB = dbo.Table2.ColB + dbo.Table1.ColB  
FROM dbo.Table2   
    INNER JOIN dbo.Table1   
    ON (dbo.Table2.ColA = dbo.Table1.ColA);  
GO  
SELECT ColA, ColB   
FROM dbo.Table2;  
```  
  
 O mesmo problema pode acontecer quando as cláusulas FROM e WHERE CURRENT OF forem combinadas. No exemplo a seguir, as duas linhas na `Table2` atendem às qualificações da cláusula `FROM` na instrução `UPDATE`. Não está definido qual linha na `Table2` será usada para atualizar a linha na `Table1`.  
  
```sql  
USE AdventureWorks2012;  
GO  
IF OBJECT_ID ('dbo.Table1', 'U') IS NOT NULL  
    DROP TABLE dbo.Table1;  
GO  
IF OBJECT_ID ('dbo.Table2', 'U') IS NOT NULL  
    DROP TABLE dbo.Table2;  
GO  
CREATE TABLE dbo.Table1  
    (c1 int PRIMARY KEY NOT NULL, c2 int NOT NULL);  
GO  
CREATE TABLE dbo.Table2  
    (d1 int PRIMARY KEY NOT NULL, d2 int NOT NULL);  
GO  
INSERT INTO dbo.Table1 VALUES (1, 10);  
INSERT INTO dbo.Table2 VALUES (1, 20), (2, 30);  
GO  
DECLARE abc CURSOR LOCAL FOR  
    SELECT c1, c2   
    FROM dbo.Table1;  
OPEN abc;  
FETCH abc;  
UPDATE dbo.Table1   
SET c2 = c2 + d2   
FROM dbo.Table2   
WHERE CURRENT OF abc;  
GO  
SELECT c1, c2 FROM dbo.Table1;  
GO  
```  
  
## <a name="compatibility-support"></a>Suporte de compatibilidade  
 O suporte ao uso de dicas de READUNCOMMITTED e NOLOCK na cláusula FROM que se aplicam à tabela de destino de uma instrução UPDATE ou DELETE será eliminado em uma versão futura do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Evite usar essas dicas nesse contexto em desenvolvimentos novos e planeje modificar aplicativos que as usam atualmente.  
  
## <a name="data-types"></a>Tipos de dados  
 Todas as colunas **char** e **nchar** são preenchidas à direita com o comprimento definido.  
  
 Se ANSI_PADDING estiver definido como OFF, todos os espaços à direita serão removidos dos dados inseridos nas colunas **varchar** e **nvarchar**, exceto em cadeias de caracteres que contenham apenas espaços. Essas cadeias de caracteres são truncadas para uma cadeia de caracteres vazia. Se ANSI_PADDING estiver definido como ON, serão inseridos espaços à direita. O driver ODBC do Microsoft SQL Server e o OLE DB Provider for SQL Server definem automaticamente ANSI_PADDING ON para cada conexão. Isso pode ser configurado em fontes de dados ODBC ou por meio da configuração de atributos ou propriedades de conexão. Para obter mais informações, veja [SET ANSI_PADDING &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-padding-transact-sql.md).  
  
### <a name="updating-text-ntext-and-image-columns"></a>Atualizando colunas text, ntext e image  
 Modificar uma coluna de **text**, **ntext** ou **image** com UPDATE inicializa a coluna, atribui um ponteiro de texto válido a ela e aloca pelo menos uma página de dados, a menos que a coluna esteja sendo atualizada com NULL.  
  
 Para substituir ou modificar blocos grandes de dados de **text**, **ntext** ou **image**, use [WRITETEXT](../../t-sql/queries/writetext-transact-sql.md) ou [UPDATETEXT](../../t-sql/queries/updatetext-transact-sql.md) em vez da instrução UPDATE.  
  
 Se a instrução UPDATE puder alterar mais de uma linha ao atualizar a chave de cluster e uma ou mais colunas de **text**, **ntext** ou **image**, a atualização parcial dessas colunas será executada como uma substituição completa dos valores.  
  
> [!IMPORTANT]  
>  Os tipos de dados **ntext**, **text** e **image** serão removidos em uma versão futura do [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Evite usar esses tipos de dados em novos trabalhos de desenvolvimento e planeje modificar os aplicativos que os utilizam atualmente. Em vez disso, use [nvarchar(max)](../../t-sql/data-types/nchar-and-nvarchar-transact-sql.md), [varchar(max)](../../t-sql/data-types/char-and-varchar-transact-sql.md)e [varbinary(max)](../../t-sql/data-types/binary-and-varbinary-transact-sql.md) .  
  
### <a name="updating-large-value-data-types"></a>Atualizando tipos de dados de valor grande  
 Use a cláusula **.** WRITE (*expression***,** *@Offset ***,***@Length*) para executar uma atualização parcial ou completa dos tipos de dados **varchar(max)**, **nvarchar(max)** e **varbinary(max)**. Por exemplo, talvez uma atualização parcial de uma coluna **varchar(max)** poderá excluir ou modificar somente os 200 primeiros caracteres da coluna, enquanto uma atualização completa excluirá ou modificará todos os dados na coluna. As atualizações de **.** WRITE que inserem ou acrescentam novos dados serão registradas em log minimamente se o modelo de recuperação do banco de dados estiver definido como bulk-logged ou simples. A criação mínima de log não é usada quando valores existentes são atualizados. Para obter mais informações, consulte [O log de transações &#40;SQL Server&#41;](../../relational-databases/logs/the-transaction-log-sql-server.md).  
  
 O [!INCLUDE[ssDE](../../includes/ssde-md.md)] converte uma atualização parcial em uma atualização completa quando a instrução UPDATE provoca uma destas ações:  
-   Altera uma coluna de chave da exibição ou tabela particionada.  
-   Modifica mais de uma linha e também atualiza a chave de um índice clusterizado não exclusivo para um valor não constante.  
  
Não é possível usar a cláusula **.** WRITE para atualizar uma coluna NULL nem para definir o valor de *column_name* como NULL.  
  
*@Offset* e *@Length* são especificados em bytes para os tipos de dados **varbinary** e **varchar** e em caracteres para o tipo de dados **nvarchar**. Os deslocamentos apropriados são computados para agrupamentos de DBCS (conjunto de caracteres de dois bytes).  
  
Para obter melhor desempenho, é recomendável que os dados sejam inseridos ou atualizados em tamanhos de blocos que sejam múltiplos de 8040 bytes.  
  
Se a coluna modificada pela cláusula **.** WRITE for referenciada em uma cláusula OUTPUT, o valor completo da coluna, na imagem anterior em **deleted.***column_name* ou na imagem posterior em **inserted.***column_name*, será retornado para a coluna especificada na variável de tabela. Veja o exemplo R a seguir.  
  
Para obter a mesma funcionalidade de **.** WRITE com outros tipos de dados de caractere ou binários, use [STUFF &#40;Transact-SQL&#41;](../../t-sql/functions/stuff-transact-sql.md).  
  
### <a name="updating-user-defined-type-columns"></a>Atualizando colunas de tipo definido pelo usuário  
 A atualização de valores em colunas de tipo definido pelo usuário pode ser realizada de uma das seguintes maneiras:  
  
-   Fornecendo um valor em um tipo de dados do sistema [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], contanto que o tipo definido pelo usuário ofereça suporte à conversão implícita ou explícita do referido tipo. O exemplo a seguir mostra como atualizar um valor em uma coluna de tipo definido pelo usuário `Point`, convertendo-o explicitamente de uma cadeia de caracteres:  
  
    ```sql  
    UPDATE Cities  
    SET Location = CONVERT(Point, '12.3:46.2')  
    WHERE Name = 'Anchorage';  
    ```  
  
-   Invocando um método, marcado como um modificador, do tipo definido pelo usuário, para executar a atualização. O exemplo a seguir invoca um método modificador de tipo `Point` denominado `SetXY`. Isso atualiza o estado da instância do tipo.  
  
    ```sql  
    UPDATE Cities  
    SET Location.SetXY(23.5, 23.5)  
    WHERE Name = 'Anchorage';  
    ```  
  
    > [!NOTE]  
    >  O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] retornará um erro se um método modificador for invocado com um valor nulo [!INCLUDE[tsql](../../includes/tsql-md.md)], ou se um novo valor produzido por um método modificador for nulo.  
  
-   Modificando o valor de uma propriedade registrada ou membro de dados público do tipo definido pelo usuário. A expressão que fornece o valor deve poder ser implicitamente convertida para o tipo da propriedade. O exemplo a seguir modifica o valor de propriedade `X` do tipo definido pelo usuário `Point`:  
  
    ```sql  
    UPDATE Cities  
    SET Location.X = 23.5  
    WHERE Name = 'Anchorage';  
    ```  
  
     Para modificar propriedades diferentes da mesma coluna do tipo definido pelo usuário, emita várias instruções UPDATE ou invoque um método modificador do tipo.  
  
### <a name="updating-filestream-data"></a>Atualizando dados de FILESTREAM  
 Você pode usar a instrução UPDATE para atualizar um campo FILESTREAM para um valor nulo, um valor vazio ou uma quantidade relativamente pequena de dados embutidos. No entanto, uma quantidade grande de dados é transmitida de maneira mais eficiente para um arquivo usando interfaces Win32. Ao atualizar um campo FILESTREAM, você modifica os dados BLOB subjacentes no sistema de arquivos. Quando um campo FILESTREAM é definido como NULL, os dados BLOB associados ao campo são excluídos. Não é possível usar .WRITE() para executar atualizações parciais em dados FILESTREAM. Para obter mais informações, veja [FILESTREAM &#40;SQL Server&#41;](../../relational-databases/blob/filestream-sql-server.md).  
  
## <a name="error-handling"></a>Tratamento de erros  
 Se uma atualização em uma linha violar uma restrição ou regra, violar a configuração NULL da coluna ou se o novo valor for um tipo de dados incompatível, a instrução será cancelada, um erro será retornado e nenhum registro será atualizado.  
  
 Quando uma instrução UPDATE encontra um erro aritmético (estouro, divisão por zero ou um erro de domínio) durante a avaliação da expressão, a atualização não é executada. O restante do lote não é executado e uma mensagem de erro é retornada.  
  
 Se uma atualização em uma ou mais colunas que participam de um índice clusterizado fizer com que o tamanho do índice clusterizado e a linha excedam 8.060 bytes, a atualização falhará e uma mensagem de erro será retornada.  
  
## <a name="interoperability"></a>Interoperabilidade  
 Instruções UPDATE são permitidas no corpo de funções definidas pelo usuário apenas se a tabela que está sendo modificada for uma variável de tabela.  
  
 Quando um gatilho INSTEAD OF é definido em ações UPDADE em uma tabela, o gatilho é executado em vez da instrução UPDATE. Versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oferecem suporte apenas a gatilhos AFTER definidos na UPDATE e em outras instruções de modificação de dados. A cláusula FROM não pode ser especificada em uma instrução UPDATE que faça referência, direta ou indiretamente, a uma exibição que tenha um gatilho INSTEAD OF definido. Para obter mais informações sobre gatilhos INSTEAD OF, confira [CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md).  
  
## <a name="limitations-and-restrictions"></a>Limitações e restrições  
 A cláusula FROM não pode ser especificada em uma instrução UPDATE que referencie, direta ou indiretamente, uma exibição que tenha um gatilho INSTEAD OF definido. Para obter mais informações sobre gatilhos INSTEAD OF, confira [CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md).  
  
 Quando uma CTE (expressão de tabela comum) for o destino de uma instrução UPDATE, todas as referências à CTE na instrução devem corresponder. Por exemplo, se for atribuído à CTE um alias na cláusula FROM, o alias deverá ser usado para todas as outras referências à CTE. São necessárias referências não ambíguas à CTE porque a CTE não tem ID de objeto, a qual o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa para reconhecer a relação implícita entre um objeto e seu alias. Sem essa relação, o plano de consulta pode gerar comportamento de junção inesperado e resultados de consulta não intencionais. Os exemplos a seguir demonstram métodos corretos e incorretos de especificação de uma CTE quando a CTE for o objeto de destino da operação de atualização.  
  
```sql  
USE tempdb;  
GO  
-- UPDATE statement with CTE references that are correctly matched.  
DECLARE @x TABLE (ID int, Value int);  
DECLARE @y TABLE (ID int, Value int);  
INSERT @x VALUES (1, 10), (2, 20);  
INSERT @y VALUES (1, 100),(2, 200);  
  
WITH cte AS (SELECT * FROM @x)  
UPDATE x -- cte is referenced by the alias.  
SET Value = y.Value  
FROM cte AS x  -- cte is assigned an alias.  
INNER JOIN @y AS y ON y.ID = x.ID;  
SELECT * FROM @x;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```  
 ID     Value  
 ------ -----  
 1      100  
 2      200  
 (2 row(s) affected)  
```  

Instrução UPDATE com referências à CTE (Expressão de Tabela Comum) correspondidas incorretamente.  
```sql  
USE tempdb;  
GO  
DECLARE @x TABLE (ID int, Value int);  
DECLARE @y TABLE (ID int, Value int);  
INSERT @x VALUES (1, 10), (2, 20);  
INSERT @y VALUES (1, 100),(2, 200);  
  
WITH cte AS (SELECT * FROM @x)  
UPDATE cte   -- cte is not referenced by the alias.  
SET Value = y.Value  
FROM cte AS x  -- cte is assigned an alias.  
INNER JOIN @y AS y ON y.ID = x.ID;   
SELECT * FROM @x;   
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
ID     Value  
------ -----  
1      100  
2      100  
(2 row(s) affected)  
```  

## <a name="locking-behavior"></a>Comportamento de bloqueio  
 Uma instrução UPDATE sempre adquire um bloqueio exclusivo (X) na tabela que modifica e mantém esse bloqueio até que a transação seja concluída. Com um bloqueio exclusivo, nenhuma outra transação pode modificar dados. Você pode especificar dicas de tabela para substituir esse comportamento padrão durante a instrução UPDATE especificando outro método de bloqueio; entretanto, é recomendável que as dicas só sejam usadas como último recurso por desenvolvedores experientes e administradores de bancos de dados. Para obter mais informações, consulte [Dicas de tabela &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-table.md).  
  
## <a name="logging-behavior"></a>Comportamento de log  
 A instrução UPDATE é registrada em log, no entanto, as atualizações parciais de tipos de dados de valor grande que usam a cláusula **.** WRITE são registradas minimamente. Para obter mais informações, consulte "Atualizando tipos de dados de valor grande" na seção anterior "Tipos de dados".  
  
## <a name="security"></a>Segurança  
  
### <a name="permissions"></a>Permissões  
 São necessárias permissões UPDATE na tabela de destino. As permissões SELECT também serão necessárias para a tabela que está sendo atualizada se a instrução UPDATE contiver uma cláusula WHERE ou se a *expression* na cláusula SET usar uma coluna na tabela.  
  
 As permissões UPDATE assumem como padrão os membros da função de servidor fixa **sysadmin**, das funções de banco de dados fixas **db_owner** e **db_datawriter** e o proprietário da tabela. Os membros das funções **sysadmin**, **db_owner** e **db_securityadmin** e o proprietário da tabela podem transferir permissões a outros usuários.  
  
##  <a name="UpdateExamples"></a> Exemplos  
  
|Categoria|Elementos de sintaxe em destaque|  
|--------------|------------------------------|  
|[Sintaxe básica](#BasicSyntax)|UPDATE|  
|[Limitando as linhas que são atualizadas](#LimitingValues)|WHERE • TOP • WITH expressão de tabela comum • WHERE CURRENT OF|  
|[Definindo valores de coluna](#ColumnValues)|valores computados • operadores compostos • valores padrão • subconsultas|  
|[Especificando objetos de destino que não sejam de tabelas padrão](#TargetObjects)|exibições • variáveis de tabela • aliases de tabela|  
|[Atualizando dados com base em dados de outras tabelas](#OtherTables)|FROM|  
|[Atualizando linhas em uma tabela remota](#RemoteTables)|servidor vinculado • OPENQUERY • OPENDATASOURCE|  
|[Atualizando tipos de dados de objeto grande](#LOBValues)|.WRITE • OPENROWSET|  
|[Atualizando tipos definidos pelo usuário](#UDTs)|tipos definidos pelo usuário|  
|[Substituindo o comportamento padrão do otimizador de consulta usando dicas](#TableHints)|dicas de tabela • dicas de consulta|  
|[Capturando os resultados da instrução UPDATE](#CaptureResults)|cláusula OUTPUT|  
|[Usando UPDATE em outras instruções](#Other)|Procedimentos armazenados • TRY…CATCH|  
  
###  <a name="BasicSyntax"></a> Sintaxe básica  
 Os exemplos nesta seção demonstram a funcionalidade básica da instrução UPDATE usando a sintaxe mínima necessária.  
  
#### <a name="a-using-a-simple-update-statement"></a>A. Usando uma instrução UPDATE simples  
 O exemplo a seguir atualiza uma única coluna de todas as linhas na tabela `Person.Address`.  
  
```sql  
USE AdventureWorks2012;  
GO  
UPDATE Person.Address  
SET ModifiedDate = GETDATE();  
```  
  
#### <a name="b-updating-multiple-columns"></a>B. Atualizando várias colunas  
 O exemplo a seguir atualiza os valores das colunas `Bonus`, `CommissionPct` e `SalesQuota` de todas as linhas da tabela `SalesPerson`.  
  
```sql  
USE AdventureWorks2012;  
GO  
UPDATE Sales.SalesPerson  
SET Bonus = 6000, CommissionPct = .10, SalesQuota = NULL;  
GO  
```  
  
###  <a name="LimitingValues"></a> Limitando as linhas que são atualizadas  
 Os exemplos desta seção demonstram as maneiras que podem ser usadas para limitar o número de linhas afetadas pela instrução UPDATE.  
  
#### <a name="c-using-the-where-clause"></a>C. Usando a cláusula WHERE  
 O exemplo a seguir usa a cláusula WHERE para especificar quais linhas devem ser atualizadas. A instrução atualiza o valor da coluna `Color` da tabela `Production.Product` para todas as linhas que têm um valor existente de 'Red' na coluna `Color` e têm um valor na coluna `Name` que é iniciado por 'Road-250.'  
  
```sql  
USE AdventureWorks2012;  
GO  
UPDATE Production.Product  
SET Color = N'Metallic Red'  
WHERE Name LIKE N'Road-250%' AND Color = N'Red';  
GO  
```  
  
#### <a name="d-using-the-top-clause"></a>D. Usando a cláusula TOP  
 Os exemplos a seguir usam a cláusula TOP para limitar o número de linhas que são modificadas em uma instrução UPDATE. Quando uma cláusula TOP (*n*) é usada com UPDATE, a operação de atualização é executada em uma seleção aleatória de um número '*n*' de linhas. O exemplo a seguir atualiza a coluna `VacationHours` em 25% para 10 linhas aleatórias na tabela `Employee`.  
  
```sql  
USE AdventureWorks2012;
GO
UPDATE TOP (10) HumanResources.Employee
SET VacationHours = VacationHours * 1.25 ;
GO  
```  
  
 Caso seja necessário usar a cláusula TOP para aplicar atualizações em uma ordem cronológica significativa, será necessário usar TOP junto com ORDER BY em uma instrução de subseleção. O exemplo a seguir atualiza as horas de férias dos 10 funcionários com as datas de contratação mais antigas.  
  
```sql  
UPDATE HumanResources.Employee  
SET VacationHours = VacationHours + 8  
FROM (SELECT TOP 10 BusinessEntityID FROM HumanResources.Employee  
     ORDER BY HireDate ASC) AS th  
WHERE HumanResources.Employee.BusinessEntityID = th.BusinessEntityID;  
GO  
```  
  
#### <a name="e-using-the-with-commontableexpression-clause"></a>E. Usando a cláusula WITH common_table_expression  
 O exemplo a seguir atualiza o valor `PerAssemnblyQty` para todas as partes e componentes que são usados direta ou indiretamente para criar o `ProductAssemblyID 800`. A expressão de tabela comum retorna uma lista hierárquica de partes que são usadas diretamente para compilar `ProductAssemblyID 800` e partes que são usadas para compilar esses componentes e assim por diante. Somente as linhas retornadas pela expressão de tabela comum são modificadas.  
  
```sql  
USE AdventureWorks2012;  
GO  
WITH Parts(AssemblyID, ComponentID, PerAssemblyQty, EndDate, ComponentLevel) AS  
(  
    SELECT b.ProductAssemblyID, b.ComponentID, b.PerAssemblyQty,  
        b.EndDate, 0 AS ComponentLevel  
    FROM Production.BillOfMaterials AS b  
    WHERE b.ProductAssemblyID = 800  
          AND b.EndDate IS NULL  
    UNION ALL  
    SELECT bom.ProductAssemblyID, bom.ComponentID, p.PerAssemblyQty,  
        bom.EndDate, ComponentLevel + 1  
    FROM Production.BillOfMaterials AS bom   
        INNER JOIN Parts AS p  
        ON bom.ProductAssemblyID = p.ComponentID  
        AND bom.EndDate IS NULL  
)  
UPDATE Production.BillOfMaterials  
SET PerAssemblyQty = c.PerAssemblyQty * 2  
FROM Production.BillOfMaterials AS c  
JOIN Parts AS d ON c.ProductAssemblyID = d.AssemblyID  
WHERE d.ComponentLevel = 0;  
```  
  
#### <a name="f-using-the-where-current-of-clause"></a>F. Usando a cláusula WHERE CURRENT OF  
 O exemplo a seguir usa a cláusula WHERE CURRENT OF para atualizar apenas a linha na qual o cursor está posicionado. Quando um cursor estiver baseado em uma junção, só o `table_name` especificado na instrução UPDATE é modificado. Outras tabelas que participam do cursor não são afetadas.  
  
```sql  
USE AdventureWorks2012;  
GO  
DECLARE complex_cursor CURSOR FOR  
    SELECT a.BusinessEntityID  
    FROM HumanResources.EmployeePayHistory AS a  
    WHERE RateChangeDate <>   
         (SELECT MAX(RateChangeDate)  
          FROM HumanResources.EmployeePayHistory AS b  
          WHERE a.BusinessEntityID = b.BusinessEntityID) ;  
OPEN complex_cursor;  
FETCH FROM complex_cursor;  
UPDATE HumanResources.EmployeePayHistory  
SET PayFrequency = 2   
WHERE CURRENT OF complex_cursor;  
CLOSE complex_cursor;  
DEALLOCATE complex_cursor;  
GO  
```  
  
###  <a name="ColumnValues"></a> Definindo valores de coluna  
 Os exemplos desta seção demonstram como atualizar colunas por meio de valores computados, subconsultas e valores DEFAULT.  
  
#### <a name="g-specifying-a-computed-value"></a>G. Especificando um valor computado  
 O exemplo a seguir usa valores computados em uma instrução UPDATE. O exemplo dobra o valor na coluna `ListPrice` de todas as linhas da tabela `Product`.  
  
```sql  
USE AdventureWorks2012 ;  
GO  
UPDATE Production.Product  
SET ListPrice = ListPrice * 2;  
GO  
```  
  
#### <a name="h-specifying-a-compound-operator"></a>H. Especificando um operador composto  
 O exemplo a seguir usa a variável `@NewPrice` para aumentar o preço de todas as bicicletas vermelhas obtendo o preço atual e adicionando 10.  
  
```sql  
USE AdventureWorks2012;  
GO  
DECLARE @NewPrice int = 10;  
UPDATE Production.Product  
SET ListPrice += @NewPrice  
WHERE Color = N'Red';  
GO  
```  
  
 O exemplo a seguir usa o operador composto + = para acrescentar o `' - tool malfunction'` de dados ao valor existente na coluna `Name` para linhas que têm um `ScrapReasonID` entre 10 e 12.  
  
```sql  
USE AdventureWorks2012;  
GO  
UPDATE Production.ScrapReason   
SET Name += ' - tool malfunction'  
WHERE ScrapReasonID BETWEEN 10 and 12;  
```  
  
#### <a name="i-specifying-a-subquery-in-the-set-clause"></a>I. Especificando uma subconsulta na cláusula SET  
 O exemplo a seguir usa uma subconsulta na cláusula SET para determinar o valor que é usado para atualizar a coluna. A subconsulta deve retornar apenas um valor escalar (ou seja, um único valor por linha). O exemplo modifica a coluna `SalesYTD` na tabela `SalesPerson` para refletir as vendas mais recentes registradas na tabela `SalesOrderHeader`. A subconsulta agrega as vendas de cada vendedor na instrução `UPDATE`.  
  
```sql  
USE AdventureWorks2012;  
GO  
UPDATE Sales.SalesPerson  
SET SalesYTD = SalesYTD +   
    (SELECT SUM(so.SubTotal)   
     FROM Sales.SalesOrderHeader AS so  
     WHERE so.OrderDate = (SELECT MAX(OrderDate)  
                           FROM Sales.SalesOrderHeader AS so2  
                           WHERE so2.SalesPersonID = so.SalesPersonID)  
     AND Sales.SalesPerson.BusinessEntityID = so.SalesPersonID  
     GROUP BY so.SalesPersonID);  
GO  
```  
  
#### <a name="j-updating-rows-using-default-values"></a>J. Atualizando linhas com valores DEFAULT  
 O exemplo a seguir define a coluna `CostRate` como seu valor padrão (0.00) para todas as linhas que têm um valor de `CostRate` maior que `20.00`.  
  
```sql  
USE AdventureWorks2012;  
GO  
UPDATE Production.Location  
SET CostRate = DEFAULT  
WHERE CostRate > 20.00;  
```  
  
###  <a name="TargetObjects"></a> Especificando objetos de destino diferentes de tabelas padrão  
 Os exemplos desta seção demonstram como atualizar linhas por meio da especificação de uma exibição, um alias de tabela ou uma variável de tabela.  
  
#### <a name="k-specifying-a-view-as-the-target-object"></a>K. Especificando uma exibição como objeto de destino  
 O exemplo a seguir atualiza linhas em uma tabela por meio da especificação de uma exibição como o objeto de destino. A definição da exibição faz referência a várias tabelas, no entanto, a instrução UPDATE têm êxito porque faz referência a várias colunas de apenas uma das tabelas subjacentes. A instrução UPDATE falhará se as colunas das duas tabelas forem especificadas. Para obter mais informações, confira [Modificar dados por meio de uma exibição](../../relational-databases/views/modify-data-through-a-view.md).  
  
```sql  
USE AdventureWorks2012;  
GO  
UPDATE Person.vStateProvinceCountryRegion  
SET CountryRegionName = 'United States of America'  
WHERE CountryRegionName = 'United States';  
```  
  
#### <a name="l-specifying-a-table-alias-as-the-target-object"></a>L. Especificando um alias de tabela como objeto de destino  
 O exemplo a seguir atualiza linhas da tabela `Production.ScrapReason`. O alias de tabela atribuído a `ScrapReason` na cláusula FROM é especificado como o objeto de destino na cláusula UPDATE.  
  
```sql  
USE AdventureWorks2012;  
GO  
UPDATE sr  
SET sr.Name += ' - tool malfunction'  
FROM Production.ScrapReason AS sr  
JOIN Production.WorkOrder AS wo   
     ON sr.ScrapReasonID = wo.ScrapReasonID  
     AND wo.ScrappedQty > 300;  
```  
  
#### <a name="m-specifying-a-table-variable-as-the-target-object"></a>M. Especificando uma variável de tabela como objeto de destino  
 O exemplo a seguir atualiza linhas em uma variável de tabela.  
  
```sql  
USE AdventureWorks2012;  
GO  
-- Create the table variable.  
DECLARE @MyTableVar table(  
    EmpID int NOT NULL,  
    NewVacationHours int,  
    ModifiedDate datetime);  
  
-- Populate the table variable with employee ID values from HumanResources.Employee.  
INSERT INTO @MyTableVar (EmpID)  
    SELECT BusinessEntityID FROM HumanResources.Employee;  
  
-- Update columns in the table variable.  
UPDATE @MyTableVar  
SET NewVacationHours = e.VacationHours + 20,  
    ModifiedDate = GETDATE()  
FROM HumanResources.Employee AS e   
WHERE e.BusinessEntityID = EmpID;  
  
-- Display the results of the UPDATE statement.  
SELECT EmpID, NewVacationHours, ModifiedDate FROM @MyTableVar  
ORDER BY EmpID;  
GO  
```  
  
###  <a name="OtherTables"></a> Atualizando dados com base em dados de outras tabelas  
 Os exemplos desta seção demonstram métodos para a atualização de linhas de uma tabela com base nas informações de outra tabela.  
  
#### <a name="n-using-the-update-statement-with-information-from-another-table"></a>N. Usando uma instrução UPDATE com informações de outra tabela  
 O exemplo a seguir modifica a coluna `SalesYTD` da tabela `SalesPerson` para refletir as vendas mais recentes registradas na tabela `SalesOrderHeader`.  
  
```sql  
USE AdventureWorks2012;  
GO  
UPDATE Sales.SalesPerson  
SET SalesYTD = SalesYTD + SubTotal  
FROM Sales.SalesPerson AS sp  
JOIN Sales.SalesOrderHeader AS so  
    ON sp.BusinessEntityID = so.SalesPersonID  
    AND so.OrderDate = (SELECT MAX(OrderDate)  
                        FROM Sales.SalesOrderHeader  
                        WHERE SalesPersonID = sp.BusinessEntityID);  
GO  
```  
  
 O exemplo anterior presume que seja registrada apenas uma venda para um vendedor especificado em uma determinada data e que as atualizações sejam atuais. Se puder ser registrada no mesmo dia mais de uma venda para um vendedor especificado, o exemplo mostrado não funcionará corretamente. O exemplo foi executado sem erros, mas cada valor de `SalesYTD` foi atualizado com apenas uma venda, independentemente de quantas vendas realmente ocorreram naquele dia. Isso ocorre porque uma única instrução UPDATE nunca atualiza a mesma linha duas vezes.  
  
 Em situações em que pode haver mais de uma venda no mesmo dia para um vendedor especificado, devem ser agregadas todas as vendas de cada vendedor na instrução `UPDATE`, como mostrado no seguinte exemplo:  
  
```sql  
USE AdventureWorks2012;  
GO  
UPDATE Sales.SalesPerson  
SET SalesYTD = SalesYTD +   
    (SELECT SUM(so.SubTotal)   
     FROM Sales.SalesOrderHeader AS so  
     WHERE so.OrderDate = (SELECT MAX(OrderDate)  
                           FROM Sales.SalesOrderHeader AS so2  
                           WHERE so2.SalesPersonID = so.SalesPersonID)  
     AND Sales.SalesPerson.BusinessEntityID = so.SalesPersonID  
     GROUP BY so.SalesPersonID);  
GO  
```  
  
###  <a name="RemoteTables"></a> Atualizando linhas em uma tabela remota  
 Os exemplos nesta seção demonstram como atualizar linhas em uma tabela de destino remota usando um [servidor vinculado](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md) ou uma [função de conjunto de linhas](../../t-sql/functions/rowset-functions-transact-sql.md) para referenciar a tabela remota.  
  
#### <a name="o-updating-data-in-a-remote-table-by-using-a-linked-server"></a>O. Atualizando dados em uma tabela remota por meio de um servidor vinculado  
 O exemplo a seguir atualiza uma tabela em um servidor remoto. O exemplo começa criando um link com a fonte de dados remota usando [sp_addlinkedserver](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md). O nome de servidor vinculado, `MyLinkServer`, é especificado então como parte do nome de objeto de quatro partes no formulário server.catalog.schema.object. Observe que você deve especificar um nome de servidor válido para `@datasrc`.  
  
```sql  
USE master;  
GO  
-- Create a link to the remote data source.   
-- Specify a valid server name for @datasrc as 'server_name' or 'server_nameinstance_name'.  
  
EXEC sp_addlinkedserver @server = N'MyLinkServer',  
    @srvproduct = N' ',  
    @provider = N'SQLNCLI10',   
    @datasrc = N'<server name>',  
    @catalog = N'AdventureWorks2012';  
GO  
USE AdventureWorks2012;  
GO  
-- Specify the remote data source using a four-part name   
-- in the form linked_server.catalog.schema.object.  
  
UPDATE MyLinkServer.AdventureWorks2012.HumanResources.Department  
SET GroupName = N'Public Relations'  
WHERE DepartmentID = 4;  
```  
  
#### <a name="p-updating-data-in-a-remote-table-by-using-the-openquery-function"></a>P. Atualizando dados em uma tabela remota por meio da função OPENQUERY  
 O exemplo a seguir atualiza uma linha em uma tabela remota especificando a função de conjunto de linhas [OPENQUERY](../../t-sql/functions/openquery-transact-sql.md). O nome de servidor vinculado criado no exemplo anterior é usado neste exemplo.  
  
```sql  
UPDATE OPENQUERY (MyLinkServer, 'SELECT GroupName FROM HumanResources.Department WHERE DepartmentID = 4')   
SET GroupName = 'Sales and Marketing';  
```  
  
#### <a name="q-updating-data-in-a-remote-table-by-using-the-opendatasource-function"></a>Q. Atualizando dados em uma tabela remota por meio da função OPENDATASOURCE  
 O exemplo a seguir insere uma linha em uma tabela remota especificando a função do conjunto de linhas [OPENDATASOURCE](../../t-sql/functions/opendatasource-transact-sql.md). Especifique um nome do servidor válido para a fonte de dados usando o formato *server_name* ou *server_name\instance_name*. Pode ser necessário configurar a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para Consultas Distribuídas Ad Hoc. Para obter mais informações, confira [Opção de configuração do servidor ad hoc distributed queries](../../database-engine/configure-windows/ad-hoc-distributed-queries-server-configuration-option.md).  
  
```sql  
UPDATE OPENQUERY (MyLinkServer, 'SELECT GroupName FROM HumanResources.Department WHERE DepartmentID = 4')   
SET GroupName = 'Sales and Marketing';  
```  
  
###  <a name="LOBValues"></a> Atualizando tipos de dados de objeto grande  
 Os exemplos desta seção demonstram métodos de atualização de valores em colunas que estão definidas com tipos de dados LOB (objetos grandes).  
  
#### <a name="r-using-update-with-write-to-modify-data-in-an-nvarcharmax-column"></a>R. Usando UPDATE com .WRITE para modificar dados em uma coluna nvarchar(max)  
 O exemplo a seguir usa a cláusula .WRITE para atualizar um valor parcial em `DocumentSummary`, uma coluna **nvarchar(max)** na tabela `Production.Document`. A palavra `components` é substituída pela palavra `features` especificando-se a palavra de substituição, o local de início (deslocamento) da palavra a ser substituída nos dados existentes e o número de caracteres a serem substituídos (comprimento). O exemplo também usa a cláusula OUTPUT para retornar as imagens anterior e posterior da coluna `DocumentSummary` para a variável de tabela `@MyTableVar`.  
  
```sql  
USE AdventureWorks2012;  
GO  
DECLARE @MyTableVar table (  
    SummaryBefore nvarchar(max),  
    SummaryAfter nvarchar(max));  
UPDATE Production.Document  
SET DocumentSummary .WRITE (N'features',28,10)  
OUTPUT deleted.DocumentSummary,   
       inserted.DocumentSummary   
    INTO @MyTableVar  
WHERE Title = N'Front Reflector Bracket Installation';  
SELECT SummaryBefore, SummaryAfter   
FROM @MyTableVar;  
GO  
```  
  
#### <a name="s-using-update-with-write-to-add-and-remove-data-in-an-nvarcharmax-column"></a>S. Usando UPDATE com .WRITE para adicionar e remover dados em uma coluna nvarchar(max)  
 Os exemplos a seguir adicionam e removem dados de uma coluna **nvarchar(max)** que tem um valor definido como NULL no momento. Como a cláusula .WRITE não pode ser usada para modificar uma coluna NULL, a coluna será populada com os dados temporários inicialmente. Em seguida, esses dados são substituídos pelos dados corretos por meio da cláusula .WRITE. Os exemplos adicionais acrescentam dados ao final do valor da coluna, removem (truncam) dados da coluna e, finalmente, removem dados parciais da coluna. As instruções SELECT exibem a modificação dos dados gerada em cada instrução UPDATE.  
  
```sql  
USE AdventureWorks2012;  
GO  
-- Replacing NULL value with temporary data.  
UPDATE Production.Document  
SET DocumentSummary = N'Replacing NULL value'  
WHERE Title = N'Crank Arm and Tire Maintenance';  
GO  
SELECT DocumentSummary   
FROM Production.Document  
WHERE Title = N'Crank Arm and Tire Maintenance';  
GO  
-- Replacing temporary data with the correct data. Setting @Length to NULL   
-- truncates all existing data from the @Offset position.  
UPDATE Production.Document  
SET DocumentSummary .WRITE(N'Carefully inspect and maintain the tires and crank arms.',0,NULL)  
WHERE Title = N'Crank Arm and Tire Maintenance';  
GO  
SELECT DocumentSummary   
FROM Production.Document  
WHERE Title = N'Crank Arm and Tire Maintenance';  
GO  
-- Appending additional data to the end of the column by setting   
-- @Offset to NULL.  
UPDATE Production.Document  
SET DocumentSummary .WRITE (N' Appending data to the end of the column.', NULL, 0)  
WHERE Title = N'Crank Arm and Tire Maintenance';  
GO  
SELECT DocumentSummary   
FROM Production.Document  
WHERE Title = N'Crank Arm and Tire Maintenance';  
GO  
-- Removing all data from @Offset to the end of the existing value by   
-- setting expression to NULL.   
UPDATE Production.Document  
SET DocumentSummary .WRITE (NULL, 56, 0)  
WHERE Title = N'Crank Arm and Tire Maintenance';  
GO  
SELECT DocumentSummary   
FROM Production.Document  
WHERE Title = N'Crank Arm and Tire Maintenance';  
GO  
-- Removing partial data beginning at position 9 and ending at   
-- position 21.  
UPDATE Production.Document  
SET DocumentSummary .WRITE ('',9, 12)  
WHERE Title = N'Crank Arm and Tire Maintenance';  
GO  
SELECT DocumentSummary   
FROM Production.Document  
WHERE Title = N'Crank Arm and Tire Maintenance';  
GO  
```  
  
#### <a name="t-using-update-with-openrowset-to-modify-a-varbinarymax-column"></a>T. Usando UPDATE com OPENROWSET para modificar uma coluna varbinary(max)  
 O exemplo a seguir substitui uma imagem existente armazenada em uma coluna **varbinary(max)** por uma nova imagem. A função [OPENROWSET](../../t-sql/functions/openrowset-transact-sql.md) é usada com a opção BULK para carregar a imagem na coluna. Este exemplo presume que existe um arquivo denominado `Tires.jpg` no caminho de arquivo especificado.  
  
```sql  
USE AdventureWorks2012;  
GO  
UPDATE Production.ProductPhoto  
SET ThumbNailPhoto = (  
    SELECT *  
    FROM OPENROWSET(BULK 'c:Tires.jpg', SINGLE_BLOB) AS x )  
WHERE ProductPhotoID = 1;  
GO  
```  
  
#### <a name="u-using-update-to-modify-filestream-data"></a>U. Usando UPDATE para modificar dados FILESTREAM  
 O exemplo a seguir usa a instrução UPDATE para modificar os dados no arquivo do sistema de arquivos. Esse método não é recomendado para streaming de grandes quantidades de dados para um arquivo. Use as interfaces do Win32 adequadas. O exemplo a seguir substitui qualquer texto no registro do arquivo pelo texto `Xray 1`. Para obter mais informações, veja [FILESTREAM &#40;SQL Server&#41;](../../relational-databases/blob/filestream-sql-server.md).  
  
```sql  
UPDATE Archive.dbo.Records  
SET [Chart] = CAST('Xray 1' as varbinary(max))  
WHERE [SerialNumber] = 2;  
```  
  
###  <a name="UDTs"></a> Atualizando tipos definidos pelo usuário  
 Os exemplos a seguir modificam valores em colunas de tipo de dados CLR UDT (definido pelo usuário). Três métodos são demonstrados. Para obter mais informações sobre colunas definidas pelo usuário, confira [Tipos CLR definidos pelo usuário](../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md).  
  
#### <a name="v-using-a-system-data-type"></a>V. Usando um tipo de dados do sistema  
 É possível atualizar um UDT fornecendo um valor em um tipo de dados do sistema [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], desde que o tipo definido pelo usuário ofereça suporte à conversão implícita ou explícita do referido tipo. O exemplo a seguir mostra como atualizar um valor em uma coluna de tipo definido pelo usuário `Point`, convertendo-o explicitamente de uma cadeia de caracteres:  
  
```sql  
UPDATE dbo.Cities  
SET Location = CONVERT(Point, '12.3:46.2')  
WHERE Name = 'Anchorage';  
```  
  
#### <a name="w-invoking-a-method"></a>W. Invocando um método  
 É possível atualizar um UDT com a invocação de um método, marcado como um modificador, do tipo definido pelo usuário, para executar a atualização. O exemplo a seguir invoca um método modificador de tipo `Point` denominado `SetXY`. Isso atualiza o estado da instância do tipo.  
  
```sql  
UPDATE dbo.Cities  
SET Location.SetXY(23.5, 23.5)  
WHERE Name = 'Anchorage';  
```  
  
#### <a name="x-modifying-the-value-of-a-property-or-data-member"></a>X. Modificando o valor de uma propriedade ou de um membro de dados  
 É possível atualizar um UDT com a modificação do valor de uma propriedade registrada ou membro de dados público do tipo definido pelo usuário. A expressão que fornece o valor deve poder ser implicitamente convertida para o tipo da propriedade. O exemplo a seguir modifica o valor de propriedade `X` do tipo definido pelo usuário `Point`:  
  
```sql  
UPDATE dbo.Cities  
SET Location.X = 23.5  
WHERE Name = 'Anchorage';  
```  
  
###  <a name="TableHints"></a> Substituindo o comportamento padrão do otimizador de consulta usando dicas  
 Os exemplos desta seção demonstram como usar dicas de tabela e de consulta para substituir temporariamente o comportamento padrão do otimizador de consultas durante o processamento da instrução UPDATE.  
  
> [!CAUTION]  
>  Como o otimizador de consulta do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] normalmente seleciona o melhor plano de execução para uma consulta, é recomendável que desenvolvedores e administradores de banco de dados experientes usem as dicas apenas como um último recurso.  
  
#### <a name="y-specifying-a-table-hint"></a>Y. Especificando uma dica de tabela  
 O exemplo a seguir especifica a [dica de tabela](../../t-sql/queries/hints-transact-sql-table.md) TABLOCK. Esta dica especifica que um bloqueio compartilhado é utilizado na tabela `Production.Product` e mantido até o término da instrução UPDATE.  
  
```sql  
USE AdventureWorks2012;  
GO  
UPDATE Production.Product  
WITH (TABLOCK)  
SET ListPrice = ListPrice * 1.10  
WHERE ProductNumber LIKE 'BK-%';  
GO  
```  
  
#### <a name="z-specifying-a-query-hint"></a>Z. Especificando uma dica de consulta  
 O exemplo a seguir especifica a [dica de consulta](../../t-sql/queries/hints-transact-sql-query.md)`OPTIMIZE FOR (@variable)` na instrução UPDATE. A dica instrui o otimizador de consultas a usar um valor específico para uma variável local quando a consulta é compilada e otimizada. O valor é usado somente durante a otimização da consulta e não durante sua execução.  
  
```sql  
USE AdventureWorks2012;  
GO  
CREATE PROCEDURE Production.uspProductUpdate  
@Product nvarchar(25)  
AS  
SET NOCOUNT ON;  
UPDATE Production.Product  
SET ListPrice = ListPrice * 1.10  
WHERE ProductNumber LIKE @Product  
OPTION (OPTIMIZE FOR (@Product = 'BK-%') );  
GO  
-- Execute the stored procedure   
EXEC Production.uspProductUpdate 'BK-%';  
```  
  
###  <a name="CaptureResults"></a> Capturando os resultados da instrução UPDATE  
 Os exemplos nesta seção demonstram como usar a [cláusula OUTPUT](../../t-sql/queries/output-clause-transact-sql.md) para retornar informações ou expressões baseadas em cada linha afetada por uma instrução UPDATE. Esses resultados podem ser retornados ao aplicativo de processamento para uso em mensagens de confirmação, arquivamentos e outros requisitos similares de aplicativo.  
  
#### <a name="aa-using-update-with-the-output-clause"></a>AA. Usando UPDATE com a cláusula OUTPUT  
 O exemplo a seguir atualiza a coluna `VacationHours` na tabela `Employee` em 25 por cento das primeiras 10 linhas e também define o valor na coluna `ModifiedDate` como a data atual. A cláusula `OUTPUT` retorna o valor de `VacationHours` existente antes da aplicação da instrução `UPDATE` na coluna `deleted.VacationHours` e o valor atualizado na coluna `inserted.VacationHours` para a variável de tabela `@MyTableVar`.  
  
 Seguem duas instruções `SELECT` que retornam os valores em `@MyTableVar` e os resultados da operação de atualização na tabela `Employee`. Para obter mais exemplos de uso da cláusula OUTPUT, confira [Cláusula OUTPUT &#40;Transact-SQL&#41;](../../t-sql/queries/output-clause-transact-sql.md).  
  
```sql  
USE AdventureWorks2012;  
GO  
DECLARE @MyTableVar table(  
    EmpID int NOT NULL,  
    OldVacationHours int,  
    NewVacationHours int,  
    ModifiedDate datetime);  
UPDATE TOP (10) HumanResources.Employee  
SET VacationHours = VacationHours * 1.25,  
    ModifiedDate = GETDATE()   
OUTPUT inserted.BusinessEntityID,  
       deleted.VacationHours,  
       inserted.VacationHours,  
       inserted.ModifiedDate  
INTO @MyTableVar;  
--Display the result set of the table variable.  
SELECT EmpID, OldVacationHours, NewVacationHours, ModifiedDate  
FROM @MyTableVar;  
GO  
--Display the result set of the table.  
SELECT TOP (10) BusinessEntityID, VacationHours, ModifiedDate  
FROM HumanResources.Employee;  
GO  
```  
  
###  <a name="Other"></a> Usando UPDATE em outras instruções  
 Os exemplos desta seção demonstram como usar o UPDATE em outras instruções.  
  
#### <a name="ab-using-update-in-a-stored-procedure"></a>AB. Usando UPDATE em um procedimento armazenado  
 O seguinte exemplo usa uma instrução UPDATE em um procedimento armazenado: o procedimento utiliza um parâmetro de entrada, `@NewHours`, e um parâmetro de saída, `@RowCount`. O valor do parâmetro `@NewHours` é usado na instrução UPDATE para atualizar a coluna `VacationHours` na tabela `HumanResources.Employee`. O parâmetro de saída `@RowCount` é usado para retornar o número de linhas afetadas para uma variável local. A expressão CASE é usada na cláusula SET para determinar condicionalmente o valor que é definido para `VacationHours`. Quando o funcionário é pago por hora (`SalariedFlag` = 0), `VacationHours` é definido como o número atual de horas mais o valor especificado em `@NewHours`; caso contrário, `VacationHours` é definido como o valor especificado em `@NewHours`.  
  
```sql  
USE AdventureWorks2012;  
GO  
CREATE PROCEDURE HumanResources.Update_VacationHours  
@NewHours smallint  
AS   
SET NOCOUNT ON;  
UPDATE HumanResources.Employee  
SET VacationHours =   
    ( CASE  
         WHEN SalariedFlag = 0 THEN VacationHours + @NewHours  
         ELSE @NewHours  
       END  
    )  
WHERE CurrentFlag = 1;  
GO  
  
EXEC HumanResources.Update_VacationHours 40;  
```  
  
#### <a name="ac-using-update-in-a-trycatch-block"></a>AC. Usando UPDATE em um bloco TRY…CATCH  
 O exemplo a seguir usa uma instrução UPDATE em um bloco TRY...CATCH para tratar os erros de execução que podem ocorrer durante a operação de atualização.  
  
```sql  
USE AdventureWorks2012;  
GO  
BEGIN TRANSACTION;  
  
BEGIN TRY  
    -- Intentionally generate a constraint violation error.  
    UPDATE HumanResources.Department  
    SET Name = N'MyNewName'  
    WHERE DepartmentID BETWEEN 1 AND 2;  
END TRY  
BEGIN CATCH  
    SELECT   
         ERROR_NUMBER() AS ErrorNumber  
        ,ERROR_SEVERITY() AS ErrorSeverity  
        ,ERROR_STATE() AS ErrorState  
        ,ERROR_PROCEDURE() AS ErrorProcedure  
        ,ERROR_LINE() AS ErrorLine  
        ,ERROR_MESSAGE() AS ErrorMessage;  
  
    IF @@TRANCOUNT > 0  
        ROLLBACK TRANSACTION;  
END CATCH;  
  
IF @@TRANCOUNT > 0  
    COMMIT TRANSACTION;  
GO  
```  
  
## <a name="examples-includesssdwincludessssdw-mdmd-and-includesspdwincludessspdw-mdmd"></a>Exemplos: [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="ad-using-a-simple-update-statement"></a>AD. Usando uma instrução UPDATE simples  
 Os exemplos a seguir mostram como todas as linhas podem ser afetadas quando uma cláusula WHERE não é usada para especificar as linhas a serem atualizadas.  
  
 Este exemplo atualiza os valores nas colunas `EndDate` e `CurrentFlag` para todas as linhas na tabela `DimEmployee`.  
  
```sql  
-- Uses AdventureWorks  
  
UPDATE DimEmployee  
SET EndDate = '2010-12-31', CurrentFlag='False';  
```  
  
 Também é possível usar valores computados em uma instrução UPDATE. O exemplo a seguir dobra o valor na coluna `ListPrice` de todas as linhas da tabela`Product`.  
  
```sql  
-- Uses AdventureWorks  
  
UPDATE DimEmployee  
SET BaseRate = BaseRate * 2;  
```  
  
### <a name="ae-using-the-update-statement-with-a-where-clause"></a>AE. Usando a instrução UPDATE com uma cláusula WHERE  
 O exemplo a seguir usa a cláusula WHERE para especificar quais linhas devem ser atualizadas.  
  
```sql  
-- Uses AdventureWorks  
  
UPDATE DimEmployee  
SET FirstName = 'Gail'  
WHERE EmployeeKey = 500;  
```  
  
### <a name="af-using-the-update-statement-with-label"></a>AF. Usando a instrução UPDATE com rótulo  
 O exemplo a seguir mostra o uso de um LABEL para a instrução UPDATE.  
  
```sql  
-- Uses AdventureWorks  
  
UPDATE DimProduct  
SET ProductSubcategoryKey = 2   
WHERE ProductKey = 313  
OPTION (LABEL = N'label1');  
```  
  
### <a name="ag-using-the-update-statement-with-information-from-another-table"></a>AG. Usando uma instrução UPDATE com informações de outra tabela  
 Este exemplo cria uma tabela para armazenar o total de vendas por ano. Ele atualiza o total de vendas do ano de 2004, executando uma instrução SELECT na tabela FactInternetSales.  
  
```sql  
-- Uses AdventureWorks  
  
CREATE TABLE YearlyTotalSales (  
    YearlySalesAmount money NOT NULL,  
    Year smallint NOT NULL )  
WITH ( DISTRIBUTION = REPLICATE );  
  
INSERT INTO YearlyTotalSales VALUES (0, 2004);  
INSERT INTO YearlyTotalSales VALUES (0, 2005);  
INSERT INTO YearlyTotalSales VALUES (0, 2006);  
  
UPDATE YearlyTotalSales  
SET YearlySalesAmount=  
(SELECT SUM(SalesAmount) FROM FactInternetSales WHERE OrderDateKey >=20040000 AND OrderDateKey < 20050000)  
WHERE Year=2004;  
  
SELECT * FROM YearlyTotalSales;   
```  

### <a name="ah-ansi-join-replacement-for-update-statements"></a>AH. Substituição de junção ANSI para instruções de atualização
É possível que você tenha uma atualização complexa que una mais de duas tabelas usando a sintaxe de junção ANSI para executar UPDATE ou DELETE.  

Imagine que você precisasse atualizar esta tabela:  

```sql
CREATE TABLE [dbo].[AnnualCategorySales]
(   [EnglishProductCategoryName]    NVARCHAR(50)    NOT NULL
,   [CalendarYear]                  SMALLINT        NOT NULL
,   [TotalSalesAmount]              MONEY           NOT NULL
)
WITH
(
    DISTRIBUTION = ROUND_ROBIN
)
;  
```

A consulta original seria semelhante a esta:  

```
UPDATE  acs
SET     [TotalSalesAmount] = [fis].[TotalSalesAmount]
FROM    [dbo].[AnnualCategorySales]     AS acs
JOIN    (
        SELECT  [EnglishProductCategoryName]
        ,       [CalendarYear]
        ,       SUM([SalesAmount])              AS [TotalSalesAmount]
        FROM    [dbo].[FactInternetSales]       AS s
        JOIN    [dbo].[DimDate]                 AS d    ON s.[OrderDateKey]             = d.[DateKey]
        JOIN    [dbo].[DimProduct]              AS p    ON s.[ProductKey]               = p.[ProductKey]
        JOIN    [dbo].[DimProductSubCategory]   AS u    ON p.[ProductSubcategoryKey]    = u.[ProductSubcategoryKey]
        JOIN    [dbo].[DimProductCategory]      AS c    ON u.[ProductCategoryKey]       = c.[ProductCategoryKey]
        WHERE   [CalendarYear] = 2004
        GROUP BY
                [EnglishProductCategoryName]
        ,       [CalendarYear]
        ) AS fis
ON  [acs].[EnglishProductCategoryName]  = [fis].[EnglishProductCategoryName]
AND [acs].[CalendarYear]                = [fis].[CalendarYear]
;  
```

Como o [!INCLUDE[ssSDW_md](../../includes/sssdw-md.md)] não é compatível com junções ANSI na cláusula FROM de uma instrução UPDATE, não é possível copiar este código sem alterá-lo um pouco.  

É possível usar uma combinação de um CTAS e uma junção implícita para substituir este código:  

```sql
-- Create an interim table
CREATE TABLE CTAS_acs
WITH (DISTRIBUTION = ROUND_ROBIN)
AS
SELECT  ISNULL(CAST([EnglishProductCategoryName] AS NVARCHAR(50)),0)    AS [EnglishProductCategoryName]
,       ISNULL(CAST([CalendarYear] AS SMALLINT),0)                      AS [CalendarYear]
,       ISNULL(CAST(SUM([SalesAmount]) AS MONEY),0)                     AS [TotalSalesAmount]
FROM    [dbo].[FactInternetSales]       AS s
JOIN    [dbo].[DimDate]                 AS d    ON s.[OrderDateKey]             = d.[DateKey]
JOIN    [dbo].[DimProduct]              AS p    ON s.[ProductKey]               = p.[ProductKey]
JOIN    [dbo].[DimProductSubCategory]   AS u    ON p.[ProductSubcategoryKey]    = u.[ProductSubcategoryKey]
JOIN    [dbo].[DimProductCategory]      AS c    ON u.[ProductCategoryKey]       = c.[ProductCategoryKey]
WHERE   [CalendarYear] = 2004
GROUP BY
        [EnglishProductCategoryName]
,       [CalendarYear]
;

-- Use an implicit join to perform the update
UPDATE  AnnualCategorySales
SET     AnnualCategorySales.TotalSalesAmount = CTAS_ACS.TotalSalesAmount
FROM    CTAS_acs
WHERE   CTAS_acs.[EnglishProductCategoryName] = AnnualCategorySales.[EnglishProductCategoryName]
AND     CTAS_acs.[CalendarYear]               = AnnualCategorySales.[CalendarYear]
;

--Drop the interim table
DROP TABLE CTAS_acs
;
```
  
## <a name="see-also"></a>Consulte Também  
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)   
 [Cursores &#40;Transact-SQL&#41;](../../t-sql/language-elements/cursors-transact-sql.md)   
 [DELETE &#40;Transact-SQL&#41;](../../t-sql/statements/delete-transact-sql.md)   
 [INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)   
 [Funções de texto e imagem &#40;Transact-SQL&#41;](http://msdn.microsoft.com/library/b9c70488-1bf5-4068-a003-e548ccbc5199)   
 [WITH common_table_expression &#40;Transact-SQL&#41;](../../t-sql/queries/with-common-table-expression-transact-sql.md)   
 [FILESTREAM &#40;SQL Server&#41;](../../relational-databases/blob/filestream-sql-server.md)  
  
  
