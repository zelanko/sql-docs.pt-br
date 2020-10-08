---
title: Parâmetros com valor de tabela
description: Descreve como trabalhar com parâmetros com valor de tabela, apresentados no SQL Server 2008.
ms.date: 08/15/2019
dev_langs:
- csharp
ms.assetid: 370c16d5-db7b-43e3-945b-ccaab35b739b
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-kaywon
ms.openlocfilehash: 02b05f65928aad5f0022d31e00847baeeb42e75c
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/05/2020
ms.locfileid: "91725547"
---
# <a name="table-valued-parameters"></a>Parâmetros com valor de tabela

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

Os parâmetros com valor de tabela fornecem uma maneira fácil de realizar marshaling em várias linhas de dados de um aplicativo cliente do SQL Server sem exigir várias viagens de ida e volta ou uma lógica especial do lado do servidor para processar os dados. Você pode usar parâmetros com valor de tabela para encapsular linhas de dados em um aplicativo cliente e enviar os dados para o servidor em um único comando parametrizado. As linhas de dados de entrada são armazenadas em uma variável de tabela, as quais você poderá operar usando o Transact-SQL.  
  
Os valores de coluna em parâmetros com valor de tabela podem ser acessados usando instruções SELECT padrão do Transact-SQL. Os parâmetros com valor de tabela são fortemente tipados e a estrutura deles é validada automaticamente. O tamanho dos parâmetros com valor de tabela é limitado somente pela memória do servidor.  
  
> [!NOTE]
>  Não é possível retornar dados em um parâmetro com valor de tabela. Os parâmetros com valor de tabela são somente entrada; não há suporte para a palavra-chave OUTPUT.  
  
Para obter mais informações sobre os parâmetros com valor de tabela, confira os recursos a seguir.  
  
|Recurso|DESCRIÇÃO|  
|--------------|-----------------|  
|[Parâmetros de valores de tabela (Mecanismo de Banco de Dados)](/previous-versions/sql/sql-server-2008/bb510489(v=sql.100)) nos Manuais Online do SQL Server|Descreve como criar e usar parâmetros com valor de tabela.|  
|[Tipos de tabela definidos pelo usuário](/previous-versions/sql/sql-server-2008/bb522526(v=sql.100)) nos Manuais Online do SQL Server|Descreve os tipos de tabela definidos pelo usuário usados para declarar parâmetros com valor de tabela.|  
  
## <a name="passing-multiple-rows-in-previous-versions-of-sql-server"></a>Como passar várias linhas nas versões anteriores do SQL Server  
Antes de os parâmetros de valores de tabela serem introduzidos no SQL Server 2008, as opções para passar várias linhas de dados para um procedimento armazenado ou um comando SQL parametrizado eram limitadas. Um desenvolvedor pode escolher entre as seguintes opções para passar várias linhas para o servidor:  
  
- Usar uma série de parâmetros individuais para representar os valores em várias colunas e linhas de dados. A quantidade de dados que pode ser passada usando esse método é limitada pelo número de parâmetros permitidos. Os procedimentos do SQL Server podem ter, no máximo, 2100 parâmetros. A lógica do lado do servidor é necessária para montar esses valores individuais em uma variável de tabela ou uma tabela temporária para processamento.  
  
- Agrupe múltiplos valores de dados em cadeias de caracteres delimitadas ou em documentos XML e, em seguida, passe esses valores de texto para um procedimento ou uma instrução. Isso requer que o procedimento ou a instrução inclua a lógica necessária para validar as estruturas de dados e desagrupar os valores.  
  
- Criar uma série de instruções SQL individuais para modificações de dados que afetam várias linhas, como aquelas criadas ao chamar o método `Update` de um <xref:Microsoft.Data.SqlClient.SqlDataAdapter>. As alterações podem ser enviadas ao servidor individualmente ou em lotes em grupos. No entanto, mesmo quando enviados em lotes que contêm várias instruções, cada instrução é executada separadamente no servidor.  
  
- Usar o programa utilitário `bcp` ou o objeto <xref:Microsoft.Data.SqlClient.SqlBulkCopy> para carregar várias linhas de dados em uma tabela. Embora essa técnica seja muito eficiente, ela não dá suporte ao processamento do lado do servidor, a menos que os dados sejam carregados em uma tabela temporária ou variável de tabela.  
  
## <a name="creating-table-valued-parameter-types"></a>Como criar tipos de parâmetro com valor de tabela  
Os parâmetros com valor de tabela são baseados em estruturas de tabela fortemente tipadas e definidas usando as instruções CREATE TYPE do Transact-SQL. Você precisa criar um tipo de tabela e definir a estrutura no SQL Server antes de poder usar parâmetros de valores de tabela em seus aplicativos cliente. Para obter mais informações sobre como criar tipos de tabela, confira [Tipos de tabela definidos pelo usuário](/previous-versions/sql/sql-server-2008/bb522526(v=sql.100)) nos Manuais Online do SQL Server.  
  
A seguinte instrução cria um tipo de tabela chamado CategoryTableType que é composto pelas colunas CategoryID e CategoryName:  
  
```sql
CREATE TYPE dbo.CategoryTableType AS TABLE  
    ( CategoryID int, CategoryName nvarchar(50) )  
```  
  
Depois de criar um tipo de tabela é possível declarar os parâmetros com valor de tabela baseados nesse tipo. O fragmento do Transact-SQL a seguir demonstra como declarar um parâmetro com valor de tabela em uma definição de procedimento armazenado. Observe que a palavra-chave READONLY é necessária para declarar um parâmetro com valor de tabela.  
  
```sql
CREATE PROCEDURE usp_UpdateCategories   
    (@tvpNewCategories dbo.CategoryTableType READONLY)  
```  
  
## <a name="modifying-data-with-table-valued-parameters-transact-sql"></a>Como modificar dados com parâmetros com valor de tabela (Transact-SQL)  
Os parâmetros com valor de tabela podem ser usados em modificações de dados baseadas em conjunto que afetam várias linhas executando uma instrução. Por exemplo, você pode selecionar todas as linhas em um parâmetro com valor de tabela e inseri-las em uma tabela de banco de dados ou pode criar uma declaração de atualização unindo um parâmetro com valor de tabela à tabela que você deseja atualizar.  
  
A instrução UPDATE do Transact-SQL a seguir demonstra como usar um parâmetro com valor de tabela unindo-o à tabela Categorias. Ao usar um parâmetro com valor de tabela com JOIN em uma cláusula FROM, você também deverá usar o alias, conforme mostrado aqui, em que o parâmetro com valor de tabela tem um alias como "ec":  
  
```sql
UPDATE dbo.Categories  
    SET Categories.CategoryName = ec.CategoryName  
    FROM dbo.Categories INNER JOIN @tvpEditedCategories AS ec  
    ON dbo.Categories.CategoryID = ec.CategoryID;  
```  
  
Este exemplo do Transact-SQL demonstra como selecionar linhas de um parâmetro com valor de tabela para executar um INSERT em uma operação baseada em conjunto.  
  
```sql
INSERT INTO dbo.Categories (CategoryID, CategoryName)  
    SELECT nc.CategoryID, nc.CategoryName FROM @tvpNewCategories AS nc;  
```  
  
## <a name="limitations-of-table-valued-parameters"></a>Limitações de parâmetros com valor de tabela  
Há várias limitações para parâmetros com valor de tabela:  
  
- Você não pode passar parâmetros de valores de tabela para [Funções CLR definidas pelo usuário](../../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-user-defined-functions.md).  
  
- Os parâmetros com valor de tabela podem ser indexados somente para dar suporte às restrições UNIQUE ou PRIMARY KEY. O SQL Server não mantém estatísticas de parâmetros com valor de tabela.  
  
- Os parâmetros com valor de tabela são somente leitura no código Transact-SQL. Não é possível atualizar os valores da coluna nas linhas de um parâmetro com valor de tabela nem inserir ou excluir linhas. Para modificar os dados que são passados para um procedimento armazenado ou para uma instrução parametrizada no parâmetro com valor de tabela, será necessário inserir os dados em uma tabela temporária ou em uma variável de tabela.  
  
- Não é possível usar as instruções ALTER TABLE para modificar o design dos parâmetros com valor de tabela.  
  
## <a name="configuring-a-sqlparameter-example"></a>Como configurar um exemplo de SqlParameter  
O <xref:Microsoft.Data.SqlClient> é compatível com o preenchimento dos parâmetros com valor de tabela dos objetos <xref:System.Data.DataTable>, <xref:System.Data.Common.DbDataReader> ou <xref:System.Collections.Generic.IEnumerable%601> \ <xref:Microsoft.Data.SqlClient.Server.SqlDataRecord>. É necessário especificar um nome de tipo para o parâmetro com valor de tabela usando a propriedade <xref:Microsoft.Data.SqlClient.SqlParameter.TypeName%2A> de um <xref:Microsoft.Data.SqlClient.SqlParameter>. O `TypeName` deve corresponder ao nome de um tipo compatível criado anteriormente no servidor. O fragmento de código a seguir demonstra como configurar o <xref:Microsoft.Data.SqlClient.SqlParameter> para inserir dados.  
 
No exemplo a seguir, o nome da variável `addedCategories` contém um <xref:System.Data.DataTable>. Para ver como a variável é preenchida, confira os exemplos na próxima seção, [Como passar um parâmetro com valor de tabela para um procedimento armazenado](#passing).

```csharp  
// Configure the command and parameter.  
SqlCommand insertCommand = new SqlCommand(sqlInsert, connection);  
SqlParameter tvpParam = insertCommand.Parameters.AddWithValue("@tvpNewCategories", addedCategories);  
tvpParam.SqlDbType = SqlDbType.Structured;  
tvpParam.TypeName = "dbo.CategoryTableType";  
```   
  
Também é possível usar qualquer objeto derivado de <xref:System.Data.Common.DbDataReader> para transmitir linhas de dados a um parâmetro com valor de tabela, conforme mostrado neste fragmento:  
  
```csharp  
// Configure the SqlCommand and table-valued parameter.  
SqlCommand insertCommand = new SqlCommand("usp_InsertCategories", connection);  
insertCommand.CommandType = CommandType.StoredProcedure;  
SqlParameter tvpParam = insertCommand.Parameters.AddWithValue("@tvpNewCategories", dataReader);  
tvpParam.SqlDbType = SqlDbType.Structured;  
```  
  
## <a name="passing-a-table-valued-parameter-to-a-stored-procedure"></a><a name="passing"></a> Passando um parâmetro com valor de tabela para um procedimento armazenado  
Este exemplo demonstra como passar dados de parâmetro com valor de tabela para um procedimento armazenado. O código extrai linhas adicionadas em um novo <xref:System.Data.DataTable> usando o método <xref:System.Data.DataTable.GetChanges%2A>. Em seguida, o código define um <xref:Microsoft.Data.SqlClient.SqlCommand>, configurando a propriedade <xref:Microsoft.Data.SqlClient.SqlCommand.CommandType%2A> como <xref:System.Data.CommandType.StoredProcedure>. O <xref:Microsoft.Data.SqlClient.SqlParameter> é preenchido usando o método <xref:Microsoft.Data.SqlClient.SqlParameterCollection.AddWithValue%2A> e o <xref:Microsoft.Data.SqlClient.SqlParameter.SqlDbType%2A> é definido como `Structured`. Em seguida, o <xref:Microsoft.Data.SqlClient.SqlCommand> é executado usando o método <xref:Microsoft.Data.SqlClient.SqlCommand.ExecuteNonQuery%2A>.  
  
```csharp  
// Assumes connection is an open SqlConnection object.  
using (connection)  
{  
  // Create a DataTable with the modified rows.  
  DataTable addedCategories = CategoriesDataTable.GetChanges(DataRowState.Added);  

  // Configure the SqlCommand and SqlParameter.  
  SqlCommand insertCommand = new SqlCommand("usp_InsertCategories", connection);  
  insertCommand.CommandType = CommandType.StoredProcedure;  
  SqlParameter tvpParam = insertCommand.Parameters.AddWithValue("@tvpNewCategories", addedCategories);  
  tvpParam.SqlDbType = SqlDbType.Structured;  

  // Execute the command.  
  insertCommand.ExecuteNonQuery();  
}  
```  
  
### <a name="passing-a-table-valued-parameter-to-a-parameterized-sql-statement"></a>Como passar um parâmetro com valor de tabela para uma instrução SQL parametrizada  
 O exemplo a seguir demonstra como inserir dados na tabela dbo.Categories usando uma instrução INSERT com uma consulta aninhada SELECT que tem um parâmetro com valor de tabela como fonte de dados. Ao passar um parâmetro com valor de tabela para uma instrução SQL parametrizada, será necessário especificar um nome de tipo para ele usando a nova propriedade <xref:Microsoft.Data.SqlClient.SqlParameter.TypeName%2A> de um <xref:Microsoft.Data.SqlClient.SqlParameter>. Esse `TypeName` deve corresponder ao nome de um tipo compatível criado anteriormente no servidor. O código nesse exemplo usa a propriedade `TypeName` para fazer referência à estrutura de tipo definida em dbo.CategoryTableType.  
  
> [!NOTE]
>  Caso forneça um valor para uma coluna de identidade em um parâmetro com valor de tabela, você deverá emitir a instrução SET IDENTITY_INSERT para a sessão.  
  
```csharp  
// Assumes connection is an open SqlConnection.  
using (connection)  
{  
  // Create a DataTable with the modified rows.  
  DataTable addedCategories = CategoriesDataTable.GetChanges(DataRowState.Added);  

  // Define the INSERT-SELECT statement.  
  string sqlInsert =   
      "INSERT INTO dbo.Categories (CategoryID, CategoryName)"  
      + " SELECT nc.CategoryID, nc.CategoryName"  
      + " FROM @tvpNewCategories AS nc;"  

  // Configure the command and parameter.  
  SqlCommand insertCommand = new SqlCommand(sqlInsert, connection);  
  SqlParameter tvpParam = insertCommand.Parameters.AddWithValue("@tvpNewCategories", addedCategories);  
  tvpParam.SqlDbType = SqlDbType.Structured;  
  tvpParam.TypeName = "dbo.CategoryTableType";  

  // Execute the command.  
  insertCommand.ExecuteNonQuery();  
}  
```  
  
## <a name="streaming-rows-with-a-datareader"></a>Como transmitir linhas com um DataReader  
Também é possível usar qualquer objeto derivado de <xref:System.Data.Common.DbDataReader> para transmitir linhas de dados a um parâmetro com valor de tabela. O fragmento de código a seguir demonstra como recuperar dados de um Oracle Database usando um <xref:System.Data.OracleClient.OracleCommand> e um <xref:System.Data.OracleClient.OracleDataReader>. Em seguida, o código configura um <xref:Microsoft.Data.SqlClient.SqlCommand> para invocar um procedimento armazenado com um parâmetro de entrada. A propriedade <xref:Microsoft.Data.SqlClient.SqlParameter.SqlDbType%2A> do <xref:Microsoft.Data.SqlClient.SqlParameter> é definida como `Structured`. O <xref:Microsoft.Data.SqlClient.SqlParameterCollection.AddWithValue%2A> passa o conjunto de resultados do `OracleDataReader` para o procedimento armazenado como um parâmetro com valor de tabela.  
  
```csharp  
// Assumes connection is an open SqlConnection.  
// Retrieve data from Oracle.  
OracleCommand selectCommand = new OracleCommand(  
   "Select CategoryID, CategoryName FROM Categories;",  
   oracleConnection);  
OracleDataReader oracleReader = selectCommand.ExecuteReader(  
   CommandBehavior.CloseConnection);  
  
 // Configure the SqlCommand and table-valued parameter.  
 SqlCommand insertCommand = new SqlCommand(  
   "usp_InsertCategories", connection);  
 insertCommand.CommandType = CommandType.StoredProcedure;  
 SqlParameter tvpParam =  
    insertCommand.Parameters.AddWithValue(  
    "@tvpNewCategories", oracleReader);  
 tvpParam.SqlDbType = SqlDbType.Structured;  
  
 // Execute the command.  
 insertCommand.ExecuteNonQuery();  
```  
  
## <a name="next-steps"></a>Próximas etapas
- [Operações de dados do SQL Server no ADO.NET](sql-server-data-operations.md)