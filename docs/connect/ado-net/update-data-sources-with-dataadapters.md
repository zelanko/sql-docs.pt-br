---
title: Atualizar fontes de dados com DataAdapters
description: Saiba como o método Atualizar do DataAdapter resolve as alterações de um DataSet de volta para a fonte de dados em aplicativos ADO.NET.
ms.date: 11/30/2020
dev_langs:
- csharp
ms.assetid: d1bd9a8c-0e29-40e3-bda8-d89176b72fb1
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-chmalh
ms.openlocfilehash: 0be62b3c2a63f7b25889e25f88969aa5aaa9b50e
ms.sourcegitcommit: c127c0752e84cccd38a7e23ac74c0362a40f952e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/07/2020
ms.locfileid: "96772159"
---
# <a name="update-data-sources-with-dataadapters"></a>Atualizar fontes de dados com DataAdapters

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

O método `Update` do <xref:System.Data.Common.DataAdapter> é chamado para resolver alterações de um <xref:System.Data.DataSet> de volta para a fonte de dados. O método `Update`, como o método de `Fill`, utiliza como argumentos uma instância do `DataSet` e um objeto <xref:System.Data.DataTable> opcional ou um nome de `DataTable`. A instância do `DataSet` é o `DataSet` que contém as alterações que foram feitas, e o `DataTable` identifica a tabela da qual recuperar as alterações. Se nenhum `DataTable` for especificado, o primeiro `DataTable` no `DataSet` será usado.

Quando você chama o método `Update`, o `DataAdapter` analisa as alterações que foram feitas e executa o comando apropriado (INSERT, UPDATE ou DELETE). Quando o `DataAdapter` encontra uma alteração em um <xref:System.Data.DataRow>, ele usa <xref:Microsoft.Data.SqlClient.SqlDataAdapter.InsertCommand%2A>, <xref:Microsoft.Data.SqlClient.SqlDataAdapter.UpdateCommand%2A> ou <xref:Microsoft.Data.SqlClient.SqlDataAdapter.DeleteCommand%2A> para processar a alteração.

Essas propriedades permitem maximizar o desempenho do aplicativo ADO.NET, especificando a sintaxe do comando em tempo de design e, sempre que possível, por meio do uso de procedimentos armazenados. Você deve definir explicitamente os comandos antes de chamar `Update`. Se `Update` for chamado e o comando apropriado não existir para uma atualização específica (por exemplo, nenhum `DeleteCommand` para linhas excluídas), será gerada uma exceção.

> [!IMPORTANT]
> Se você estiver usando procedimentos armazenados do SQL Server para editar ou excluir dados usando um `DataAdapter`, jamais utilize `SET NOCOUNT ON` na definição do procedimento armazenado. Isso faz com que a contagem retornada de linhas afetadas seja zero, o que o `DataAdapter` interpreta como um conflito de simultaneidade. Nesse caso, será gerada uma <xref:System.Data.DBConcurrencyException>.

Os parâmetros do comando podem ser usados para especificar valores de entrada e saída para uma instrução SQL ou procedimento armazenado para cada linha modificada em um `DataSet`. Para obter mais informações, confira [Parâmetros do DataAdapter](dataadapter-parameters.md).

> [!NOTE]
> É importante compreender a diferença entre excluir uma linha em um <xref:System.Data.DataTable> e remover a linha. Quando você chama o método `Remove` ou `RemoveAt`, a linha é removida imediatamente. As linhas correspondentes da fonte de dados de back-end **não serão afetadas** se você passar `DataTable` ou `DataSet` para `DataAdapter` e chamar `Update`. Quando você usa o método `Delete`, a linha permanece no `DataTable` e é marcada para exclusão. Se você passar `DataTable` ou `DataSet` para `DataAdapter` e chamar `Update`, a linha correspondente da fonte de dados de back-end **será excluída**.

Se seu `DataTable` mapear para ou for gerado a partir de uma única tabela do banco de dados, você poderá aproveitar o objeto <xref:System.Data.Common.DbCommandBuilder> para gerar automaticamente os objetos `DeleteCommand`, `InsertCommand` e `UpdateCommand` para o `DataAdapter`. Para obter mais informações, confira [Gerar comandos com CommandBuilders](generate-commands-with-commandbuilders.md).

## <a name="use-updatedrowsource-to-map-values-to-a-dataset"></a>Usar o UpdatedRowSource a fim de mapear valores para um DataSet

Você pode controlar como os valores retornados da fonte de dados são mapeados de volta para `DataTable` após uma chamada ao método <xref:System.Data.Common.DbDataAdapter.Update%2A> de `DataAdapter`, usando a propriedade <xref:Microsoft.Data.SqlClient.SqlCommand.UpdatedRowSource%2A> de um objeto <xref:Microsoft.Data.SqlClient.SqlCommand>. Definindo a propriedade `UpdatedRowSource` para um dos valores de enumeração de <xref:System.Data.UpdateRowSource>, você pode controlar se os parâmetros de saída retornados pelos comandos de `DataAdapter` serão ignorados ou aplicados à linha alterada no `DataSet`. Você também pode especificar se a primeira linha retornada (se existir) é aplicada à linha alterada no `DataTable`.

A tabela a seguir descreve os diferentes valores da enumeração de `UpdateRowSource` e como eles afetam o comportamento de um comando usado com o `DataAdapter`.

|Enumeração de UpdatedRowSource|Descrição|
|----------------------------------|-----------------|
|<xref:System.Data.UpdateRowSource.Both>|Os parâmetros de saída e a primeira linha de um conjunto de resultados retornado podem ser mapeados para a linha alterada no `DataSet`.|
|<xref:System.Data.UpdateRowSource.FirstReturnedRecord>|Somente os dados da primeira linha de um conjunto de resultados retornado podem ser mapeados para a linha alterada no `DataSet`.|
|<xref:System.Data.UpdateRowSource.None>|Todos os parâmetros de saída ou linhas de um conjunto de resultados retornado são ignorados.|
|<xref:System.Data.UpdateRowSource.OutputParameters>|Somente os parâmetros de saída podem ser mapeados para a linha alterada no `DataSet`.|

O método `Update` resolve as alterações de volta para a fonte de dados. No entanto, outros clientes podem ter modificado dados na fonte de dados desde a última vez que você preencheu o `DataSet`. Para atualizar seu `DataSet` com dados atuais, use o método `DataAdapter` e o método `Fill`. As novas linhas serão adicionadas à tabela, e informações atualizadas serão incorporadas às linhas existentes.

O método `Fill` determina se uma nova linha será adicionada ou se uma linha existente será atualizada examinando os valores de chave primária das linhas no `DataSet` e as linhas retornadas pelo `SelectCommand`. Se o método `Fill` encontrar um valor de chave primária para uma linha no `DataSet` que corresponda a um valor de chave primária de uma linha nos resultados retornados pelo `SelectCommand`, ele atualizará a linha existente com as informações da linha retornadas pelo `SelectCommand` e definirá o <xref:System.Data.DataRow.RowState%2A> da linha existente como `Unchanged`. Se uma linha retornada pelo `SelectCommand` tiver um valor de chave primária que não corresponda a alguns dos valores de chave primária das linhas do `DataSet`, o método `Fill` adicionará uma nova linha com um `RowState` de `Unchanged`.

> [!NOTE]
> Se `SelectCommand` retornar os resultados de um **OUTER JOIN**, `DataAdapter` não definirá um valor `PrimaryKey` para o `DataTable` resultante. Você deve definir o `PrimaryKey` você mesmo para garantir que as linhas duplicadas sejam resolvidas corretamente.

Para gerenciar exceções que possam ocorrer ao chamar o método `Update`, você pode usar o evento `RowUpdated` para responder a erros na atualização da linha conforme ocorrerem (confira [Gerenciar eventos do DataAdapter](handle-dataadapter-events.md)) ou você pode definir <xref:System.Data.Common.DataAdapter.ContinueUpdateOnError%2A> como `true` antes de chamar `Update` e responder às informações de erro armazenadas na propriedade `RowError` de uma linha específica quando a atualização for concluída.

> [!NOTE]
> Chamar `AcceptChanges` em `DataSet`, `DataTable` ou `DataRow` fará com que todos os valores `Original` de `DataRow` sejam substituídos pelos valores `Current` de `DataRow`. Se os valores dos campos que identificam a linha como exclusiva foram modificados, depois de chamar `AcceptChanges` os valores `Original` não corresponderão mais aos valores na fonte de dados. `AcceptChanges` é chamado automaticamente para cada linha durante uma chamada ao método `Update` de `DataAdapter`. Você pode preservar os valores originais durante uma chamada para o método Update definindo primeiro a propriedade `AcceptChangesDuringUpdate` do `DataAdapter` como false, ou criando um manipulador de eventos para o evento `RowUpdated` e definindo o <xref:System.Data.Common.RowUpdatedEventArgs.Status%2A> como <xref:System.Data.UpdateStatus.SkipCurrentRow>. Para obter mais informações, confira [Gerenciar eventos do DataAdapter](handle-dataadapter-events.md).

Os exemplos a seguir demonstram como executar atualizações em linhas modificadas definindo explicitamente `UpdateCommand` de `DataAdapter` e chamando o método `Update`.

> [!NOTE]
> O parâmetro especificado em `WHERE clause` de `UPDATE statement` é definido para usar o valor `Original` de `SourceColumn`. Isso é importante, porque o valor `Current` pode ter sido modificado e não corresponder ao valor na fonte de dados. O valor `Original` é o valor que foi usado para popular o `DataTable` da fonte de dados.

[!code-csharp[SqlDataAdapter_Update#1](~/../sqlclient/doc/samples/SqlDataAdapter_Update.cs#1)]

## <a name="autoincrement-columns"></a>Colunas AutoIncrement

Se as tabelas de sua fonte de dados possuírem colunas de incremento automático, você poderá preencher as colunas em seu `DataSet` retornando o valor de incremento automático como um parâmetro de saída de um procedimento armazenado e mapeando esse valor para uma coluna em uma tabela, retornando o valor de incremento automático na primeira linha de um conjunto de resultados retornado por um procedimento armazenado ou instrução SQL ou usando o evento `RowUpdated` do `DataAdapter` para executar uma instrução SELECT adicional.

## <a name="ordering-of-inserts-updates-and-deletes"></a>Ordenação de inserções, atualizações e exclusões

Em muitas circunstâncias, a ordem em que as alterações feitas no `DataSet` são enviadas para a fonte de dados é importante. Por exemplo, se um valor de chave primária de uma linha existente for atualizado, e uma nova linha for adicionada com o novo valor de chave primária como uma chave estrangeira, é importante processar a atualização antes da inserção.

Você pode usar o método `Select` do `DataTable` para retornar uma matriz de `DataRow` que referencie somente linhas com um `RowState` específico. Você pode passar a matriz de `DataRow` retornada para o método `Update` do `DataAdapter` para processar as linhas modificadas. Especificando um subconjunto de linhas a serem atualizadas, você pode controlar a ordem na qual as inserções, atualizações e exclusões são processadas.

## <a name="example"></a>Exemplo

Por exemplo, o código a seguir garante que as linhas excluídas da tabela sejam processadas primeiro, em seguida as linhas atualizadas e depois as linhas inseridas.

[!code-csharp[SqlDataAdapter_Update#2](~/../sqlclient/doc/samples/SqlDataAdapter_Update.cs#2)]

## <a name="use-a-dataadapter-to-retrieve-and-update-data"></a>Usar um DataAdapter para recuperar e atualizar os dados

Você pode usar um DataAdapter para recuperar e atualizar os dados.

- O exemplo usa `DataAdapter.AcceptChangesDuringFill` para clonar os dados no banco de dado. Se a propriedade for definida como **false**, **AcceptChanges** não será chamado ao preencher a tabela e as linhas adicionadas recentemente serão tratadas como linhas inseridas. Portanto, o exemplo usa essas linhas para inserir novas linhas no banco de dados.

- Os exemplos usam `DataAdapter.TableMappings` para definir o mapeamento entre a tabela de origem e a DataTable.

- O exemplo usa `DataAdapter.FillLoadOption` para determinar como o adaptador preenche a **DataTable** por meio do **DbDataReader**. Ao criar uma DataTable, você só pode gravar os dados do banco de dado na versão atual ou na versão original, definindo a propriedade como o **LoadOption.Upsert** ou **LoadOption.PreserveChanges**.

- O exemplo também atualizará a tabela usando `DbDataAdapter.UpdateBatchSize` para executar operações em lote.

Antes de compilar e executar o exemplo, você precisará criar o banco de dados de exemplo:

```sql
USE [master]
GO

CREATE DATABASE [MySchool]

GO

USE [MySchool]
GO

SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[Course]([CourseID] [nvarchar](10) NOT NULL,
[Year] [smallint] NOT NULL,
[Title] [nvarchar](100) NOT NULL,
[Credits] [int] NOT NULL,
[DepartmentID] [int] NOT NULL,
 CONSTRAINT [PK_Course] PRIMARY KEY CLUSTERED
(
[CourseID] ASC,
[Year] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON) ON [PRIMARY]) ON [PRIMARY]

GO

SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[Department]([DepartmentID] [int] IDENTITY(1,1) NOT NULL,
[Name] [nvarchar](50) NOT NULL,
[Budget] [money] NOT NULL,
[StartDate] [datetime] NOT NULL,
[Administrator] [int] NULL,
 CONSTRAINT [PK_Department] PRIMARY KEY CLUSTERED
(
[DepartmentID] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON) ON [PRIMARY]) ON [PRIMARY]

GO

INSERT [dbo].[Course] ([CourseID], [Year], [Title], [Credits], [DepartmentID]) VALUES (N'C1045', 2012, N'Calculus', 4, 7)
INSERT [dbo].[Course] ([CourseID], [Year], [Title], [Credits], [DepartmentID]) VALUES (N'C1061', 2012, N'Physics', 4, 1)
INSERT [dbo].[Course] ([CourseID], [Year], [Title], [Credits], [DepartmentID]) VALUES (N'C2021', 2012, N'Composition', 3, 2)
INSERT [dbo].[Course] ([CourseID], [Year], [Title], [Credits], [DepartmentID]) VALUES (N'C2042', 2012, N'Literature', 4, 2)

SET IDENTITY_INSERT [dbo].[Department] ON

INSERT [dbo].[Department] ([DepartmentID], [Name], [Budget], [StartDate], [Administrator]) VALUES (1, N'Engineering', 350000.0000, CAST(0x0000999C00000000 AS DateTime), 2)
INSERT [dbo].[Department] ([DepartmentID], [Name], [Budget], [StartDate], [Administrator]) VALUES (2, N'English', 120000.0000, CAST(0x0000999C00000000 AS DateTime), 6)
INSERT [dbo].[Department] ([DepartmentID], [Name], [Budget], [StartDate], [Administrator]) VALUES (4, N'Economics', 200000.0000, CAST(0x0000999C00000000 AS DateTime), 4)
INSERT [dbo].[Department] ([DepartmentID], [Name], [Budget], [StartDate], [Administrator]) VALUES (7, N'Mathematics', 250024.0000, CAST(0x0000999C00000000 AS DateTime), 3)
SET IDENTITY_INSERT [dbo].[Department] OFF

ALTER TABLE [dbo].[Course]  WITH CHECK ADD  CONSTRAINT [FK_Course_Department] FOREIGN KEY([DepartmentID])
REFERENCES [dbo].[Department] ([DepartmentID])
GO
ALTER TABLE [dbo].[Course] CHECK CONSTRAINT [FK_Course_Department]
GO
```

[!code-csharp[SqlDataAdapter_Properties#1](~/../sqlclient/doc/samples/SqlDataAdapter_Properties.cs#1)]

## <a name="see-also"></a>Confira também

- [DataAdapters e DataReaders](dataadapters-datareaders.md)
- [Microsoft ADO.NET for SQL Server](microsoft-ado-net-sql-server.md)
