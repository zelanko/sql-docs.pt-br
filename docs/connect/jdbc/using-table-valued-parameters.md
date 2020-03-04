---
title: Como usar parâmetros com valor de tabela | Microsoft Docs
ms.custom: ''
ms.date: 11/19/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 3af61054-a886-4e1a-ad85-93f87c6d3584
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1dfa8438e7afb1763129748368a7f6e08fa892c3
ms.sourcegitcommit: 844793cd1c058e6bba136f050734e7dc62024a82
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/25/2020
ms.locfileid: "77575338"
---
# <a name="using-table-valued-parameters"></a>Como usar parâmetros com valor de tabela

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Os parâmetros com valor de tabela fornecem uma maneira fácil de realizar marshaling em várias linhas de dados de um aplicativo cliente do SQL Server sem exigir várias viagens de ida e volta ou uma lógica especial do lado do servidor para processar os dados. Você pode usar parâmetros com valor de tabela para encapsular linhas de dados em um aplicativo cliente e enviar os dados para o servidor em um único comando parametrizado. As linhas de dados de entrada são armazenadas em uma variável de tabela, as quais você poderá operar usando o Transact-SQL.  
  
Os valores de coluna em parâmetros com valor de tabela podem ser acessados usando instruções SELECT padrão do Transact-SQL. Os parâmetros com valor de tabela são fortemente tipados e a estrutura deles é validada automaticamente. O tamanho dos parâmetros com valor de tabela é limitado somente pela memória do servidor.  
  
> [!NOTE]  
> O suporte para parâmetros com valor de tabela está disponível do Microsoft JDBC Driver 6.0 para SQL Server em diante.
>
> Não é possível retornar dados em um parâmetro com valor de tabela. Os parâmetros com valor de tabela são somente entrada; não há suporte para a palavra-chave OUTPUT.  
  
 Para obter mais informações sobre os parâmetros com valor de tabela, confira os recursos a seguir.  
  
| Recurso                                                                                                             | Descrição                                                                         |
| -------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------- |
| [Parâmetros de valores de tabela (Mecanismo de Banco de Dados)](https://go.microsoft.com/fwlink/?LinkId=98363) nos Manuais Online do SQL Server | Descreve como criar e usar parâmetros com valor de tabela                             |
| [Tipos de tabela definidos pelo usuário](https://go.microsoft.com/fwlink/?LinkId=98364) nos Manuais Online do SQL Server                  | Descreve os tipos de tabela definidos pelo usuário usados para declarar parâmetros com valor de tabela |
| A seção [Mecanismo de Banco de Dados do Microsoft SQL Server](https://go.microsoft.com/fwlink/?LinkId=120507) do CodePlex        | Contém exemplos que demonstram como usar recursos e funcionalidade do SQL Server  |
  
## <a name="passing-multiple-rows-in-previous-versions-of-sql-server"></a>Como passar várias linhas nas versões anteriores do SQL Server  

Antes de os parâmetros de valores de tabela serem introduzidos no SQL Server 2008, as opções para passar várias linhas de dados para um procedimento armazenado ou um comando SQL parametrizado eram limitadas. Um desenvolvedor pode escolher entre as seguintes opções para passar várias linhas para o servidor:  
  
- Usar uma série de parâmetros individuais para representar os valores em várias colunas e linhas de dados. A quantidade de dados que pode ser passada usando esse método é limitada pelo número de parâmetros permitidos. Os procedimentos do SQL Server podem ter, no máximo, 2100 parâmetros. A lógica do lado do servidor é necessária para montar esses valores individuais em uma variável de tabela ou uma tabela temporária para processamento.  
  
- Agrupe múltiplos valores de dados em cadeias de caracteres delimitadas ou em documentos XML e, em seguida, passe esses valores de texto para um procedimento ou uma instrução. Isso requer que o procedimento ou a instrução inclua a lógica necessária para validar as estruturas de dados e desagrupar os valores.  
  
- Crie uma série de instruções SQL individuais para modificações de dados que afetam várias linhas. As alterações podem ser enviadas ao servidor individualmente ou em lotes em grupos. No entanto, mesmo quando enviados em lotes que contêm várias instruções, cada instrução é executada separadamente no servidor.  
  
- Use o programa utilitário bcp ou [SQLServerBulkCopy](../../connect/jdbc/using-bulk-copy-with-the-jdbc-driver.md) para carregar várias linhas de dados em uma tabela. Embora essa técnica seja muito eficiente, ela não dá suporte ao processamento do lado do servidor, a menos que os dados sejam carregados em uma tabela temporária ou variável de tabela.
  
## <a name="creating-table-valued-parameter-types"></a>Como criar tipos de parâmetro com valor de tabela  

Os parâmetros com valor de tabela se baseiam em estruturas de tabela fortemente tipadas que são definidas usando instruções Transact-SQL `CREATE TYPE`. Você precisa criar um tipo de tabela e definir a estrutura no SQL Server antes de poder usar parâmetros de valores de tabela em seus aplicativos cliente. Para obter mais informações sobre como criar tipos de tabela, confira [Tipos de tabela definidos pelo usuário](https://go.microsoft.com/fwlink/?LinkID=98364) nos Manuais Online do SQL Server.  

```sql
CREATE TYPE dbo.CategoryTableType AS TABLE  
    ( CategoryID int, CategoryName nvarchar(50) )  
```

Depois de criar um tipo de tabela, você pode declarar parâmetros com valor de tabela com base nesse tipo. O fragmento do Transact-SQL a seguir demonstra como declarar um parâmetro com valor de tabela em uma definição de procedimento armazenado. Observe que a palavra-chave `READONLY` é necessária para declarar um parâmetro com valor de tabela.  

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
  
- Você não pode passar parâmetros de valores de tabela para funções definidas pelo usuário.  
  
- Os parâmetros com valor de tabela podem ser indexados somente para dar suporte às restrições UNIQUE ou PRIMARY KEY. O SQL Server não mantém estatísticas de parâmetros com valor de tabela.  
  
- Os parâmetros com valor de tabela são somente leitura no código Transact-SQL. Não é possível atualizar os valores da coluna nas linhas de um parâmetro com valor de tabela nem inserir ou excluir linhas. Para modificar os dados que são passados para um procedimento armazenado ou para uma instrução parametrizada no parâmetro com valor de tabela, será necessário inserir os dados em uma tabela temporária ou em uma variável de tabela.  
  
- Não é possível usar as instruções ALTER TABLE para modificar o design dos parâmetros com valor de tabela.

- Você pode transmitir objetos grandes em um parâmetro com valor de tabela.  
  
## <a name="configuring-a-table-valued-parameter"></a>Configurando um parâmetro com valor de tabela

Do Microsoft JDBC Driver 6.0 para SQL Server em diante, há suporte para parâmetros com valor de tabela com uma instrução parametrizada ou um procedimento armazenado com parâmetros. Os parâmetros com valor de tabela podem ser preenchidos de um SQLServerDataTable, de um ResultSet ou de uma implementação fornecida pelo usuário da interface ISQLServerDataRecord. Ao configurar um parâmetro com valor de tabela para uma consulta preparada, você deve especificar um nome de tipo que deve corresponder ao nome de um tipo compatível criado anteriormente no servidor.  
  
Os dois fragmentos de código a seguir demonstram como configurar um parâmetro com valor de tabela com um SQLServerPreparedStatement e com um SQLServerCallableStatement para inserir dados. Aqui, sourceTVPObject pode ser um SQLServerDataTable, um ResultSet ou um objeto ISQLServerDataRecord. Os exemplos presumem que a conexão é um objeto de conexão ativo.  

```java
// Using table-valued parameter with a SQLServerPreparedStatement.  
SQLServerPreparedStatement pStmt =
    (SQLServerPreparedStatement) connection.prepareStatement("INSERT INTO dbo.Categories SELECT * FROM ?");  
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
> Confira a seção **API de parâmetro com valor de tabela para o JDBC Driver** abaixo para obter uma lista completa de APIs disponíveis para configurar o parâmetro com valor de tabela.  
  
## <a name="passing-a-table-valued-parameter-as-a-sqlserverdatatable-object"></a>Passando um parâmetro com valor de tabela como um objeto SQLServerDataTable  

Do Microsoft JDBC Driver 6.0 para SQL Server em diante, a classe SQLServerDataTable representa uma tabela na memória de dados relacionais. Este exemplo demonstra como construir um parâmetro com valor de tabela com base em dados na memória usando o objeto SQLServerDataTable. Primeiramente, o código cria um objeto SQLServerDataTable, define seu esquema e preenche a tabela usando dados. Em seguida, o código configura um SQLServerPreparedStatement que passa essa tabela de dados como um parâmetro com valor de tabela para o SQL Server.  

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
> Confira a seção **API de parâmetro com valor de tabela para o JDBC Driver** abaixo para obter uma lista completa de APIs disponíveis para configurar o parâmetro com valor de tabela.  
  
## <a name="passing-a-table-valued-parameter-as-a-resultset-object"></a>Passando um parâmetro com valor de tabela como um objeto ResultSet  

Este exemplo demonstra como transmitir linhas de dados de um ResultSet para um parâmetro com valor de tabela. Primeiramente, o código recupera os dados de uma tabela de origem em um objeto SQLServerDataTable, define seu esquema e preenche a tabela usando dados. Em seguida, o código configura um SQLServerPreparedStatement que passa essa tabela de dados como um parâmetro com valor de tabela para o SQL Server.  

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
> Confira a seção **API de parâmetro com valor de tabela para o JDBC Driver** abaixo para obter uma lista completa de APIs disponíveis para configurar o parâmetro com valor de tabela.  

## <a name="passing-a-table-valued-parameter-as-an-isqlserverdatarecord-object"></a>Passando um parâmetro com valor de tabela como um objeto ISQLServerDataRecord  

Do Microsoft JDBC Driver 6.0 para SQL Server em diante, um ISQLServerDataRecord com nova interface está disponível para streaming de dados (dependendo de como o usuário fornece a implementação) usando um parâmetro com valor de tabela. O exemplo a seguir demonstra como implementar a interface do ISQLServerDataRecord e como passá-la como um parâmetro com valor de tabela. Para simplificar, o exemplo a seguir passa apenas uma linha com valores codificados para o parâmetro com valor de tabela. O ideal é que o usuário Implemente essa interface para transmitir linhas de qualquer fonte, por exemplo, de arquivos de texto.  

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
> Confira a seção **API de parâmetro com valor de tabela para o JDBC Driver** abaixo para obter uma lista completa de APIs disponíveis para configurar o parâmetro com valor de tabela.

## <a name="table-valued-parameter-api-for-the-jdbc-driver"></a>API de parâmetro com valor de tabela para o driver JDBC

### <a name="sqlservermetadata"></a>SQLServerMetaData

Essa classe representa os metadados de uma coluna. Ele é usado na interface do ISQLServerDataRecord para passar os metadados da coluna para o parâmetro com valor de tabela. Os métodos nessa classe são:  

| Nome                                                                                                                                                                             | Descrição                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| public SQLServerMetaData(String columnName, int sqlType, int precision, int scale, boolean useServerDefault, boolean isUniqueKey, SQLServerSortOrder sortOrder, int sortOrdinal) | Inicializa uma nova instância de SQLServerMetaData com o nome da coluna, tipo SQL, precisão, escala e padrão do servidor especificados. Essa forma do construtor dá suporte a parâmetros com valor de tabela, permitindo que você especifique se a coluna é exclusiva no parâmetro com valor de tabela, a ordem de classificação da coluna e o ordinal da coluna de classificação. <br/><br/>useServerDefault – especifica se essa coluna deve usar o valor de servidor padrão; o valor padrão é false.<br>isUniqueKey – indica se a coluna no parâmetro com valor de tabela é exclusiva; O valor padrão é false.<br>sortOrder – indica a ordem de classificação de uma coluna; o valor padrão é SQLServerSortOrder.Unspecified.<br>sortOrdinal – especifica o ordinal da coluna de classificação; sortOrdinal começa em 0; O valor padrão é-1. |
| public SQLServerMetaData( String columnName, int sqlType)                                                                                                                        | Inicializa uma nova instância de SQLServerMetaData usando o nome da coluna e o tipo SQL.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| public SQLServerMetaData( String columnName, int sqlType, int length)                                                                                                                        | Inicializa uma nova instância de SQLServerMetaData usando o nome da coluna, o tipo SQL e o tamanho (para dados de cadeia de caracteres). O tamanho é usado para diferenciar cadeias de caracteres grandes de cadeias de caracteres com menos de 4000 caracteres. Introduzido na versão 7.2 do driver JDBC.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| public SQLServerMetaData( String columnName, int sqlType, int precision, int scale)                                                                                              | Inicializa uma nova instância de SQLServerMetaData usando o nome da coluna, o tipo SQL, a precisão e a escala.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| Public SQLServerMetaData(SQLServerMetaData sqlServerMetaData)                                                                                                                    | Inicializa uma nova instância de SQLServerMetaData de outro objeto SQLServerMetaData.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| public String getColumName()                                                                                                                                                     | Recupera o nome da coluna.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| public int getSqlType()                                                                                                                                                          | Recupera o tipo SQL do Java.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| public int getPrecision()                                                                                                                                                        | Recupera a precisão do tipo passado para a coluna.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| public int getScale()                                                                                                                                                            | Recupera a escala do tipo passado para a coluna.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| public SQLServerSortOrder getSortOrder()                                                                                                                                         | Recupera a ordem de classificação.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| public int getSortOrdinal()                                                                                                                                                      | Recupera o ordinal de classificação.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| public boolean isUniqueKey()                                                                                                                                                     | Retorna se a coluna é exclusiva.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| public boolean useServerDefault()                                                                                                                                                | Retorna se a coluna usa o valor de servidor padrão.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
  
### <a name="sqlserversortorder"></a>SQLServerSortOrder

Uma enumeração que define a ordem de classificação. Os valores possíveis são Ascending, Descending e Unspecified.
  
### <a name="sqlserverdatatable"></a>SQLServerDataTable

Essa classe representa uma tabela de dados na memória a ser usada com parâmetros com valor de tabela. Os métodos nessa classe são:  

| Nome                                                          | Descrição                                          |
| ------------------------------------------------------------- | ---------------------------------------------------- |
| Public SQLServerDataTable()                                   | Inicializa uma nova instância de SQLServerDataTable.    |
| public Iterator<Entry\<Integer, Object[]>> getIterator()      | Recupera um iterador nas linhas da tabela de dados. |
| public void addColumnMetadata(String columnName, int sqlType) | Adiciona metadados para a coluna especificada.              |
| public void addColumnMetadata(SQLServerDataColumn column)     | Adiciona metadados para a coluna especificada.              |
| public void addRow(Object... values)                          | Adiciona uma linha de dados à tabela de dados.              |
| public Map\<Integer, SQLServerDataColumn> getColumnMetadata() | Recupera os metadados de coluna desta tabela de dados.       |
| public void clear()                                           | Limpa esta tabela de dados.                              |

### <a name="sqlserverdatacolumn"></a>SQLServerDataColumn

Essa classe representa uma coluna da tabela de dados na memória representada por SQLServerDataTable. Os métodos nessa classe são:  

| Nome                                                       | Descrição                                                                      |
| ---------------------------------------------------------- | -------------------------------------------------------------------------------- |
| public SQLServerDataColumn(String columnName, int sqlType) | Inicializa uma nova instância de SQLServerDataColumn com o nome da coluna e o tipo. |
| public String getColumnName()                              | Recupera o nome da coluna.                                                       |
| public int getColumnType()                                 | Recupera o tipo de coluna.                                                       |

### <a name="isqlserverdatarecord"></a>ISQLServerDataRecord

Essa classe representa uma interface que os usuários podem implementar para transmitir dados a um parâmetro com valor de tabela. Os métodos nesta interface são:  
  
| Nome                                                    | Descrição                                                                                             |
| ------------------------------------------------------- | ------------------------------------------------------------------------------------------------------- |
| public SQLServerMetaData getColumnMetaData(int column); | Recupera os metadados de coluna do índice de coluna fornecido.                                               |
| public int getColumnCount();                            | Recupera o número total de colunas.                                                                  |
| public Object[] getRowData();                           | Recupera os dados para a linha atual como uma matriz de Objetos.                                          |
| public boolean next();                                  | Avança para a próxima linha. Retornará True se a movimentação for bem-sucedida e houver uma próxima linha; caso contrário, false. |

### <a name="sqlserverpreparedstatement"></a>SQLServerPreparedStatement

Os métodos a seguir foram adicionados a essa classe para dar suporte à passagem de parâmetros com valor de tabela.  

| Nome                                                                                                    | Descrição                                                                                                                                                                                                                                                                                                |
| ------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| public final void setStructured(int parameterIndex, String tvpName, SQLServerDataTable tvpDataTable)    | Popula um parâmetro com valor de tabela com uma tabela de dados. parameterIndex é o índice de parâmetro, tvpName é o nome do parâmetro com valor de tabela e tvpDataTable é o objeto de tabela de dados de origem.                                                                                                          |
| public final void setStructured(int parameterIndex, String tvpName, ResultSet tvpResultSet)             | Popula um parâmetro com valor de tabela com um ResultSet recuperado de outra tabela. parameterIndex é o índice de parâmetro, tvpName é o nome do parâmetro com valor de tabela e tvpResultSet é o objeto de conjunto de resultados de origem.                                                                               |
| public final void setStructured(int parameterIndex, String tvpName, ISQLServerDataRecord tvpDataRecord) | Popula um parâmetro com valor de tabela com um objeto ISQLServerDataRecord. ISQLServerDataRecord é usado para transmitir dados e o usuário decide como usá-lo. parameterIndex é o índice de parâmetro, tvpName é o nome do parâmetro com valor de tabela e tvpDataRecord é um objeto ISQLServerDataRecord. |
  
### <a name="sqlservercallablestatement"></a>SQLServerCallableStatement

Os métodos a seguir foram adicionados a essa classe para dar suporte à passagem de parâmetros com valor de tabela.  
  
| Nome                                                                                                        | Descrição                                                                                                                                                                                                                                                                                                                      |
| ----------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| public final void setStructured(String paratemeterName, String tvpName, SQLServerDataTable tvpDataTable)    | Popula um parâmetro com valor de tabela passado para um procedimento armazenado com uma tabela de dados. paratemeterName é o nome do parâmetro, tvpName é o nome do tipo TVP e tvpDataTable é o objeto da tabela de dados.                                                                                                                 |
| public final void setStructured(String paratemeterName, String tvpName, ResultSet tvpResultSet)             | Popula um parâmetro com valor de tabela passado para um procedimento armazenado com um ResultSet recuperado de outra tabela. paratemeterName é o nome do parâmetro, tvpName é o nome do tipo TVP e tvpResultSet é o objeto de conjunto de resultados de origem.                                                                              |
| public final void setStructured(String paratemeterName, String tvpName, ISQLServerDataRecord tvpDataRecord) | Popula um parâmetro com valor de tabela passado para um procedimento armazenado com um objeto ISQLServerDataRecord. ISQLServerDataRecord é usado para transmitir dados e o usuário decide como usá-lo. paratemeterName é o nome do parâmetro, tvpName é o nome do tipo TVP e tvpDataRecord é um objeto ISQLServerDataRecord. |

## <a name="see-also"></a>Confira também

[Visão geral do JDBC Driver](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
