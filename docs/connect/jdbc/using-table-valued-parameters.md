---
title: Usando parâmetros com valor de tabela | Microsoft Docs
ms.custom: ''
ms.date: 07/11/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 3af61054-a886-4e1a-ad85-93f87c6d3584
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e3b6790bce4cc3eb84ec707b56e909876606fa02
ms.sourcegitcommit: 63b4f62c13ccdc2c097570fe8ed07263b4dc4df0
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 11/13/2018
ms.locfileid: "51603526"
---
# <a name="using-table-valued-parameters"></a>Como usar parâmetros com valor de tabela

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Os parâmetros com valor de tabela fornecem uma maneira fácil de realizar marshaling em várias linhas de dados de um aplicativo cliente do SQL Server sem exigir várias viagens de ida e volta ou uma lógica especial do lado do servidor para processar os dados. Você pode usar parâmetros com valor de tabela para encapsular linhas de dados em um aplicativo cliente e enviar os dados para o servidor em um único comando parametrizado. As linhas de dados de entrada são armazenadas em uma variável de tabela que pode ser operada usando o Transact-SQL.  
  
Valores de coluna em parâmetros com valor de tabela podem ser acessados usando instruções Transact-SQL SELECT padrão. Parâmetros com valor de tabela são fortemente tipados e sua estrutura é validada automaticamente. O tamanho dos parâmetros com valor de tabela é limitado apenas pela memória de servidor.  
  
> [!NOTE]  
> Suporte para parâmetros com valor de tabela está disponível começando com o Microsoft JDBC Driver 6.0 para SQL Server.
>
> Você não pode retornar dados em um parâmetro com valor de tabela. Parâmetros com valor de tabela são somente entrada; Não há suporte para a palavra-chave OUTPUT.  
  
 Para obter mais informações sobre parâmetros com valor de tabela, consulte os seguintes recursos.  
  
| Recurso                                                                                                             | Descrição                                                                         |
| -------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------- |
| [Parâmetros com valor de tabela (mecanismo de banco de dados)](https://go.microsoft.com/fwlink/?LinkId=98363) nos Manuais Online do SQL Server | Descreve como criar e usar parâmetros com valor de tabela                             |
| [Tipos de tabela definidos pelo usuário](https://go.microsoft.com/fwlink/?LinkId=98364) nos Manuais Online do SQL Server                  | Descreve os tipos de tabela definido pelo usuário que são usados para declarar parâmetros com valor de tabela |
| O [mecanismo de banco de dados do Microsoft SQL Server](https://go.microsoft.com/fwlink/?LinkId=120507) seção do CodePlex        | Contém exemplos que demonstram como usar a funcionalidade e recursos do SQL Server  |
  
## <a name="passing-multiple-rows-in-previous-versions-of-sql-server"></a>Passando várias linhas em versões anteriores do SQL Server  

Antes de parâmetros com valor de tabela foram introduzidos no SQL Server 2008, as opções para passar várias linhas de dados para um procedimento armazenado ou um comando SQL parametrizado eram limitadas. Um desenvolvedor poderia escolher as seguintes opções para passar várias linhas para o servidor:  
  
- Use uma série de parâmetros individuais para representar os valores em várias colunas e linhas de dados. A quantidade de dados que podem ser passados usando esse método é limitada pelo número de parâmetros permitidos. Procedimentos do SQL Server podem ter, no máximo, 2100 parâmetros. Lógica do lado do servidor é necessária para reunir esses valores individuais em uma variável de tabela ou uma tabela temporária para processamento.  
  
- Empacotar vários valores de dados em cadeias de caracteres delimitadas ou documentos XML e, em seguida, passar esses valores de texto para uma instrução ou procedimento. Isso requer o procedimento ou a instrução para incluir a lógica necessária para validar as estruturas de dados e desempacotar os valores.  
  
- Crie uma série de instruções SQL individuais para modificações de dados que afetam várias linhas. As alterações podem ser enviadas para o servidor individualmente ou reunidas em grupos. No entanto, mesmo quando enviadas em lotes que contêm várias instruções, cada instrução é executada separadamente no servidor.  
  
- Use o programa de utilitário bcp ou o [SQLServerBulkCopy](https://msdn.microsoft.com/library/system.data.sqlclient.sqlbulkcopy(v=vs.110).aspx) objeto para carregar várias linhas de dados em uma tabela. Embora essa técnica é muito eficiente, ele não oferece suporte a servidor de processamento, a menos que os dados são carregados em uma tabela temporária ou variável de tabela.  
  
## <a name="creating-table-valued-parameter-types"></a>Criando tipos de parâmetro com valor de tabela  

Parâmetros com valor de tabela são baseados nas estruturas de tabela fortemente tipadas que são definidas usando o Transact-SQL `CREATE TYPE` instruções. Você precisa criar um tipo de tabela e definir a estrutura no SQL Server antes de poder usar parâmetros com valor de tabela em seus aplicativos cliente. Para obter mais informações sobre como criar tipos de tabela, consulte [tipos de tabela definidos pelo usuário](https://go.microsoft.com/fwlink/?LinkID=98364) nos Manuais Online do SQL Server.  

```sql
CREATE TYPE dbo.CategoryTableType AS TABLE  
    ( CategoryID int, CategoryName nvarchar(50) )  
```

Depois de criar um tipo de tabela, você pode declarar parâmetros com valor de tabela com base nesse tipo. O fragmento de Transact-SQL a seguir demonstra como declarar um parâmetro com valor de tabela em uma definição de procedimento armazenado. Observe que o `READONLY` palavra-chave é necessária para declarar um parâmetro com valor de tabela.  

```sql
CREATE PROCEDURE usp_UpdateCategories
    (@tvpNewCategories dbo.CategoryTableType READONLY)  
```

## <a name="modifying-data-with-table-valued-parameters-transact-sql"></a>Modificando dados com parâmetros com valor de tabela (Transact-SQL)  

Parâmetros com valor de tabela podem ser usados em modificações de dados baseada em conjunto que afetam várias linhas executando uma única instrução. Por exemplo, você pode selecionar todas as linhas em um parâmetro com valor de tabela e inseri-los em uma tabela de banco de dados, ou você pode criar uma instrução de atualização unindo um parâmetro com valor de tabela para a tabela que você deseja atualizar.  
  
A instrução UPDATE Transact-SQL a seguir demonstra como usar um parâmetro com valor de tabela unindo-à tabela Categories. Quando você usa um parâmetro com valor de tabela com uma junção em uma cláusula FROM, você deve também alias, conforme mostrado aqui, onde o parâmetro com valor de tabela é um alias como "ec":  

```sql
UPDATE dbo.Categories  
    SET Categories.CategoryName = ec.CategoryName  
    FROM dbo.Categories INNER JOIN @tvpEditedCategories AS ec  
    ON dbo.Categories.CategoryID = ec.CategoryID;  
```

Este exemplo de Transact-SQL demonstra como selecionar linhas de um parâmetro com valor de tabela para realizar um INSERT em uma única operação baseada em conjunto.

```sql
INSERT INTO dbo.Categories (CategoryID, CategoryName)  
    SELECT nc.CategoryID, nc.CategoryName FROM @tvpNewCategories AS nc;  
```

## <a name="limitations-of-table-valued-parameters"></a>Limitações de parâmetros com valor de tabela

Existem várias limitações para parâmetros com valor de tabela:  
  
- Você não pode passar parâmetros com valor de tabela para funções definidas pelo usuário.  
  
- Parâmetros com valor de tabela só podem ser indexados para dar suporte a restrições UNIQUE ou PRIMARY KEY. O SQL Server não mantém estatísticas de parâmetros com valor de tabela.  
  
- Parâmetros com valor de tabela são somente leitura no código Transact-SQL. Você não pode atualizar os valores de coluna nas linhas de um parâmetro com valor de tabela e você não pode inserir ou excluir linhas. Para modificar os dados que são passados para um procedimento armazenado ou instrução parametrizada no parâmetro com valor de tabela, você deve inserir os dados em uma tabela temporária ou em uma variável de tabela.  
  
- É possível usar instruções ALTER TABLE para modificar o design de parâmetros com valor de tabela.

- Você pode transmitir objetos grandes em um parâmetro com valor de tabela.  
  
## <a name="configuring-a-table-valued-parameter"></a>Configuração de um parâmetro com valor de tabela

Começando com o Microsoft JDBC Driver 6.0 para SQL Server, os parâmetros com valor de tabela têm suporte com uma instrução parametrizada ou um procedimento armazenado parametrizado. Parâmetros com valor de tabela podem ser preenchidos a partir de um SQLServerDataTable, de um conjunto de resultados ou de um usuário fornecidos a implementação da interface ISQLServerDataRecord. Ao definir um parâmetro com valor de tabela para uma consulta preparada, você deve especificar um nome de tipo que deve corresponder ao nome de um tipo compatível criado anteriormente no servidor.  
  
Os fragmentos de código a seguir demonstram como configurar um parâmetro com valor de tabela com um SQLServerPreparedStatement e SQLServerCallableStatement uma para inserir dados. Aqui, sourceTVPObject pode ser um SQLServerDataTable, ou um conjunto de resultados ou um objeto ISQLServerDataRecord. Os exemplos pressupõem que a conexão é um objeto de Conexão ativado.  

```java
// Using table-valued parameter with a SQLServerPreparedStatement.  
SQLServerPreparedStatement pStmt =
    (SQLServerPreparedStatement) connection.prepareStatement(“INSERT INTO dbo.Categories SELECT * FROM ?”);  
pStmt.setStructured(1, "dbo.CategoryTableType", sourceTVPObject);  
pStmt.execute();  
```

```java
// Using table-valued parameter with a SQLServerCallableStatement.  
SQLServerCallableStatement pStmt =
    (SQLServerCallableStatement) connection.prepareCall("exec usp_InsertCategories ?");
pStmt.setStructured(1, "dbo.CategoryTableType", sourceTVPObject);;  
pStmt.execute();  
```

> [!NOTE]  
> Consulte a seção **API de parâmetro com valor de tabela para o Driver JDBC** abaixo para obter uma lista completa das APIs disponíveis para definir o parâmetro com valor de tabela.  
  
## <a name="passing-a-table-valued-parameter-as-a-sqlserverdatatable-object"></a>Passando um parâmetro com valor de tabela como um objeto de SQLServerDataTable  

Começando com o Microsoft JDBC Driver 6.0 para SQL Server, a classe SQLServerDataTable representa uma tabela na memória de dados relacionais. Este exemplo demonstra como construir um parâmetro com valor de tabela de dados na memória usando o objeto SQLServerDataTable. O código primeiro cria um objeto de SQLServerDataTable, define seu esquema e preenche a tabela com dados. O código, em seguida, configura uma SQLServerPreparedStatement que passa essa tabela de dados como um parâmetro com valor de tabela para o SQL Server.  

```java
/* Assumes connection is an active Connection object. */

// Create an in-memory data table.  
SQLServerDataTable sourceDataTable = new SQLServerDataTable();
  
// Define metadata for the data table.  
sourceDataTable.addColumnMetadata("CategoryID" ,java.sql.Types.INTEGER);
sourceDataTable.addColumnMetadata("CategoryName" ,java.sql.Types.NVARCHAR);
  
// Populate the data table.  
sourceDataTable.addRow(1, "CategoryNameValue1");
sourceDataTable.addRow(2, "CategoryNameValue2");
  
// Pass the data table as a table-valued parameter using a prepared statement.  
SQLServerPreparedStatement pStmt =
        (SQLServerPreparedStatement) connection.prepareStatement(  
            "INSERT INTO dbo.Categories SELECT * FROM ?;");  
pStmt.setStructured(1, "dbo.CategoryTableType", sourceDataTable);  
pStmt.execute();  
```

> [!NOTE]  
> Consulte a seção **API de parâmetro com valor de tabela para o Driver JDBC** abaixo para obter uma lista completa das APIs disponíveis para definir o parâmetro com valor de tabela.  
  
## <a name="passing-a-table-valued-parameter-as-a-resultset-object"></a>Passando um parâmetro com valor de tabela como um objeto de conjunto de resultados  

Este exemplo demonstra como transmitir as linhas de dados de um conjunto de resultados para um parâmetro com valor de tabela. O código recupera primeiro os dados de uma tabela de origem em um cria um objeto de SQLServerDataTable, define seu esquema e preenche a tabela com dados. O código, em seguida, configura uma SQLServerPreparedStatement que passa essa tabela de dados como um parâmetro com valor de tabela para o SQL Server.  

```java
/* Assumes connection is an active Connection object. */

// Create the source ResultSet object. Here SourceCategories is a table defined with the same schema as Categories table.
ResultSet sourceResultSet = connection.createStatement().executeQuery("SELECT * FROM SourceCategories");  

// Pass the source result set as a table-valued parameter using a prepared statement.  
SQLServerPreparedStatement pStmt =
        (SQLServerPreparedStatement) connection.prepareStatement(  
                "INSERT INTO dbo.Categories SELECT * FROM ?;");  
pStmt.setStructured(1, "dbo.CategoryTableType", sourceResultSet);  
pStmt.execute();  
```

> [!NOTE]  
> Consulte a seção **API de parâmetro com valor de tabela para o Driver JDBC** abaixo para obter uma lista completa das APIs disponíveis para definir o parâmetro com valor de tabela.  

## <a name="passing-a-table-valued-parameter-as-an-isqlserverdatarecord-object"></a>Passando um parâmetro com valor de tabela como um objeto ISQLServerDataRecord  

Começando com o Microsoft JDBC Driver 6.0 para SQL Server, uma nova interface ISQLServerDataRecord está disponível para streaming de dados (dependendo de como o usuário fornece a implementação para ele) usando um parâmetro com valor de tabela. O exemplo a seguir demonstra como implementar a interface ISQLServerDataRecord e como passá-lo como um parâmetro com valor de tabela. Para simplificar, o exemplo a seguir passa apenas uma linha com valores embutidos em código para o parâmetro com valor de tabela. O ideal é que o usuário poderia implementar essa interface para transmitir as linhas de qualquer origem, por exemplo, de arquivos de texto.  

```java
class MyRecords implements ISQLServerDataRecord  
{  
    int currentRow = 0;  
    Object[] row = new Object[2];  
  
    MyRecords(){  
        // Constructor. This implementation has just one row.
        row[0] = new Integer(1);  
        row[1] = "categoryName1";  
    }  
  
    public int getColumnCount(){  
        // Return the total number of columns, for this example it is 2.  
        return 2;  
    }  
  
    public SQLServerMetaData getColumnMetaData(int columnIndex) {  
        // Return the column metadata.  
        if (1 == columnIndex)  
            return new SQLServerMetaData("CategoryID", java.sql.Types.INTEGER);  
        else  
            return new SQLServerMetaData("CategoryName", java.sql.Types.NVARCHAR);  
    }  
  
    public Object[] getRowData(){  
        // Return the columns in the current row as an array of objects. This implementation has just one row.  
        return row;
    }  
  
    public boolean next(){  
        // Move to the next row. This implementation has just one row, after processing the first row, return false.  
        currentRow++;  
        if (1 == currentRow)  
            return true;  
        else  
            return false;  
    }
}

// Following code demonstrates how to pass MyRecords object as a table-valued parameter.  
MyRecords sourceRecords = new MyRecords();  
SQLServerPreparedStatement pStmt =
        (SQLServerPreparedStatement) connection.prepareStatement(  
                "INSERT INTO dbo.Categories SELECT * FROM ?;");  
pStmt.setStructured(1, "dbo.CategoryTableType", sourceRecords);  
pStmt.execute();  
```

> [!NOTE]  
> Consulte a seção **API de parâmetro com valor de tabela para o Driver JDBC** abaixo para obter uma lista completa das APIs disponíveis para definir o parâmetro com valor de tabela.

## <a name="table-valued-parameter-api-for-the-jdbc-driver"></a>API de parâmetro com valor de tabela para o JDBC Driver

### <a name="sqlservermetadata"></a>SQLServerMetaData

Essa classe representa os metadados para uma coluna. Ele é usado na interface do ISQLServerDataRecord para passar os metadados da coluna para o parâmetro com valor de tabela. Os métodos nessa classe são:  

| Nome                                                                                                                                                                             | Descrição                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| SQLServerMetaData pública (columnName de cadeia de caracteres, sqlType int, int precisão, escala de int, boolean useServerDefault, isUniqueKey booliano, SQLServerSortOrder sortOrder, sortOrdinal int) | Inicializa uma nova instância da SQLServerMetaData com o nome de coluna especificado, o tipo de sql, a precisão, a escala e o servidor padrão. Este formulário do construtor dá suporte a parâmetros com valor de tabela, permitindo que você especifique se a coluna é exclusiva no parâmetro com valor de tabela, a ordem de classificação para a coluna e o ordinal da coluna de classificação. <br/><br/>useServerDefault - Especifica se essa coluna deve usar o valor padrão do servidor; Valor padrão é false.<br>isUniqueKey - indica se a coluna no parâmetro com valor de tabela é exclusiva; Valor padrão é false.<br>sortOrder - indica a ordem de classificação para uma coluna; Valor padrão é SQLServerSortOrder.Unspecified.<br>sortOrdinal - Especifica o ordinal da coluna de classificação; sortOrdinal começa em 0; Valor padrão é -1. |
| SQLServerMetaData pública (columnName de cadeia de caracteres, sqlType int)                                                                                                                        | Inicializa uma nova instância da SQLServerMetaData usando o nome da coluna e o tipo de sql.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| SQLServerMetaData pública (columnName de cadeia de caracteres, sqlType int, int precisão, escala de int)                                                                                              | Inicializa uma nova instância da SQLServerMetaData usando o nome da coluna, tipo de sql, precisão e escala.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| SQLServerMetaData pública (SQLServerMetaData sqlServerMetaData)                                                                                                                    | Inicializa uma nova instância da SQLServerMetaData de outro objeto SQLServerMetaData.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| público getColumName() de cadeia de caracteres                                                                                                                                                     | Recupera o nome da coluna.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| int público getSqlType()                                                                                                                                                          | Recupera o tipo do sql java.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| int público getPrecision()                                                                                                                                                        | Recupera a precisão do tipo passado para a coluna.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| int público getScale()                                                                                                                                                            | Recupera a escala do tipo passado para a coluna.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| getSortOrder() de SQLServerSortOrder pública                                                                                                                                         | Recupera a ordem de classificação.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| int público getSortOrdinal()                                                                                                                                                      | Recupera o ordinal de classificação.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| público isUniqueKey() booliano                                                                                                                                                     | Retorna se a coluna é exclusiva.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| público useServerDefault() booliano                                                                                                                                                | Retorna se a coluna usa o valor padrão do servidor.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
  
### <a name="sqlserversortorder"></a>SQLServerSortOrder

Uma enumeração que define a ordem de classificação. Os valores possíveis são crescente, decrescente e não especificado.
  
### <a name="sqlserverdatatable"></a>SQLServerDataTable

Essa classe representa uma tabela de dados na memória a ser usado com parâmetros com valor de tabela. Os métodos nessa classe são:  

| Nome                                                          | Descrição                                          |
| ------------------------------------------------------------- | ---------------------------------------------------- |
| SQLServerDataTable() pública                                   | Inicializa uma nova instância da SQLServerDataTable.    |
| Iteradores públicos < entrada\<inteiro, Object [] >> getIterator()      | Recupera um iterador nas linhas da tabela de dados. |
| público addColumnMetadata void (columnName de cadeia de caracteres, sqlType int) | Adiciona metadados da coluna especificada.              |
| addColumnMetadata public void (SQLServerDataColumn coluna)     | Adiciona metadados da coluna especificada.              |
| público addRow void (valores de objetos...)                          | Adiciona uma linha de dados à tabela de dados.              |
| Mapa público\<Integer, SQLServerDataColumn > getColumnMetadata() | Recupera metadados de coluna dessa tabela de dados.       |
| Clear () void pública                                           | Limpa a tabela de dados.                              |

### <a name="sqlserverdatacolumn"></a>SQLServerDataColumn

Essa classe representa uma coluna da tabela de dados na memória representada por SQLServerDataTable. Os métodos nessa classe são:  

| Nome                                                       | Descrição                                                                      |
| ---------------------------------------------------------- | -------------------------------------------------------------------------------- |
| SQLServerDataColumn pública (columnName de cadeia de caracteres, sqlType int) | Inicializa uma nova instância da SQLServerDataColumn com o nome da coluna e tipo. |
| público getColumnName() de cadeia de caracteres                              | Recupera o nome da coluna.                                                       |
| int público getColumnType()                                 | Recupera o tipo de coluna.                                                       |

### <a name="isqlserverdatarecord"></a>ISQLServerDataRecord

Essa classe representa uma interface que os usuários podem implementar para transmitir dados para um parâmetro com valor de tabela. Os métodos nessa interface são:  
  
| Nome                                                    | Descrição                                                                                             |
| ------------------------------------------------------- | ------------------------------------------------------------------------------------------------------- |
| público SQLServerMetaData getColumnMetaData (coluna int); | Recupera os metadados de coluna de índice de coluna especificado.                                               |
| getColumnCount() int público;                            | Recupera o número total de colunas.                                                                  |
| getRowData() de [] de objeto público;                           | Recupera os dados para a linha atual como uma matriz de Objetos.                                          |
| público booliano Next ();                                  | Move para a próxima linha. Retornará True se a movimentação for bem-sucedida e não há uma linha seguinte, false caso contrário. |

### <a name="sqlserverpreparedstatement"></a>SQLServerPreparedStatement

Os métodos a seguir foram adicionados a essa classe para dar suporte à passagem de parâmetros com valor de tabela.  

| Nome                                                                                                    | Descrição                                                                                                                                                                                                                                                                                                |
| ------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| público setStructured void final (parameterIndex int, cadeia de caracteres tvpName, SQLServerDataTable tvpDataTable)    | Popula um parâmetro com valor de tabela com uma tabela de dados. parameterIndex é o índice do parâmetro, tvpName é o nome do parâmetro com valor de tabela e tvpDataTable é o objeto de tabela de dados de origem.                                                                                                          |
| público setStructured void final (parameterIndex int, cadeia de caracteres tvpName, tvpResultSet do conjunto de resultados)             | Popula um parâmetro com valor de tabela com um conjunto de resultados recuperado da tabela de outro. parameterIndex é o índice do parâmetro, tvpName é o nome do parâmetro com valor de tabela e tvpResultSet é o objeto de conjunto de resultados de origem.                                                                               |
| público setStructured void final (parameterIndex int, cadeia de caracteres tvpName, ISQLServerDataRecord tvpDataRecord) | Popula um parâmetro com valor de tabela com um objeto ISQLServerDataRecord. ISQLServerDataRecord é usado para transmissão de dados e o usuário decide como usá-lo. parameterIndex é o índice do parâmetro, tvpName é o nome do parâmetro com valor de tabela e tvpDataRecord é um objeto ISQLServerDataRecord. |
  
### <a name="sqlservercallablestatement"></a>SQLServerCallableStatement

Os métodos a seguir foram adicionados a essa classe para dar suporte à passagem de parâmetros com valor de tabela.  
  
| Nome                                                                                                        | Descrição                                                                                                                                                                                                                                                                                                                      |
| ----------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| público setStructured void final (paratemeterName de cadeia de caracteres, cadeia de caracteres tvpName, SQLServerDataTable tvpDataTable)    | Popula um parâmetro com valor de tabela passado para um procedimento armazenado com uma tabela de dados. paratemeterName é o nome do parâmetro, tvpName é o nome do tipo TVP e tvpDataTable é o objeto de tabela de dados.                                                                                                                 |
| público setStructured void final (paratemeterName de cadeia de caracteres, cadeia de caracteres tvpName, tvpResultSet do conjunto de resultados)             | Popula um parâmetro com valor de tabela passado para um procedimento armazenado com um conjunto de resultados recuperado de outra tabela. paratemeterName é o nome do parâmetro, tvpName é o nome do tipo TVP e tvpResultSet é o objeto de conjunto de resultados de origem.                                                                              |
| público setStructured void final (paratemeterName de cadeia de caracteres, cadeia de caracteres tvpName, ISQLServerDataRecord tvpDataRecord) | Popula um parâmetro com valor de tabela passado para um procedimento armazenado com um objeto ISQLServerDataRecord. ISQLServerDataRecord é usado para transmissão de dados e o usuário decide como usá-lo. paratemeterName é o nome do parâmetro, tvpName é o nome do tipo TVP e tvpDataRecord é um objeto ISQLServerDataRecord. |

## <a name="see-also"></a>Consulte Também

[Visão geral do JDBC Driver](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
