---
title: Preencher um DataSet de um DataAdapter
description: Saiba como preencher um DataSet de um DataAdapter no ADO.NET, que fornece um modelo de programação relacional consistente, independente da fonte de dados.
ms.date: 11/30/2020
dev_langs:
- csharp
ms.assetid: 3fa0ac7d-e266-4954-bfac-3fbe2f913153
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-chmalh
ms.openlocfilehash: c632d83b092f5f68ce5bbca32d4315821252603c
ms.sourcegitcommit: c127c0752e84cccd38a7e23ac74c0362a40f952e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/07/2020
ms.locfileid: "96772160"
---
# <a name="populate-a-dataset-from-a-dataadapter"></a>Preencher um DataSet de um DataAdapter

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

O <xref:System.Data.DataSet> do ADO.NET é uma representação de dados residentes na memória que fornece um modelo de programação relacional consistente, independente da fonte de dados. O `DataSet` representa um conjunto completo de dados, que inclui tabelas, restrições e relações entre as tabelas. Como `DataSet` é independente da fonte de dados, um `DataSet` pode incluir o local de dados para o aplicativo, e os dados de várias fontes de dados. A interação com fontes de dados existente é controlada com o `DataAdapter`.

A propriedade `SelectCommand` do `DataAdapter` é um objeto `Command` que recupera dados da fonte de dados. As propriedades `InsertCommand`, `UpdateCommand`, e `DeleteCommand` do `DataAdapter` são objetos `Command` que gerenciam as atualizações aos dados na fonte de dados de acordo com as alterações feitas aos dados no `DataSet`. Essas propriedades são abordadas com mais detalhes em [Atualizar fontes de dados com os DataAdapters](update-data-sources-with-dataadapters.md).

O método `Fill` do `DataAdapter` é usado para preencher um `DataSet` com os resultados do `SelectCommand` do `DataAdapter`. `Fill` utiliza como seus argumentos um `DataSet` a ser preenchido, e um objeto `DataTable`, ou nome do `DataTable` a ser preenchido com as linhas retornadas do `SelectCommand`.

> [!NOTE]
> Usar o `DataAdapter` para recuperar todas as tabelas leva tempo, especialmente se há várias linhas na tabela. Isso ocorre porque acessar o banco de dados, localizar e processar os dados e, em seguida, transferir os dados para o cliente é demorado. Receber todas as tabelas para o cliente também bloqueia todas as linhas no servidor. Para melhorar o desempenho, você pode usar a cláusula `WHERE` para reduzir bastante o número de linhas retornadas para o cliente. Você também pode reduzir a quantidade de dados retornados para o cliente somente listando explicitamente as colunas necessárias na instrução `SELECT`. Outra boa solução alternativa é recuperar as linhas em lotes (como várias centenas de linhas de cada vez) e recuperar somente o próximo lote quando o cliente tiver terminado o lote atual.

O método `Fill` usa o objeto `DataReader` implicitamente para retornar os nomes de coluna e os tipos que são usados para criar as tabelas no `DataSet`, e os dados para preencher as linhas das tabelas no `DataSet`. As tabelas e as colunas são criadas somente se já não existirem; caso contrário, `Fill` usará o esquema existente do `DataSet`. Os tipos de coluna são criados como tipos do .NET Framework, de acordo com as tabelas dos [Mapeamentos de Tipos de Dados do ADO.NET](data-type-mappings-ado-net.md). As chaves primárias não são criadas, a menos que elas existam na fonte de dados e `DataAdapter` **.** `MissingSchemaAction` está definido como `MissingSchemaAction` **.** `AddWithKey`. Se `Fill` descobrir que uma chave primária existe para uma tabela, ele substituirá os dados no `DataSet` pelos dados da fonte de dados para as linhas onde os valores de coluna de chave primária coincidirem com os da linha retornada da fonte de dados. Se nenhuma chave primária tiver sido encontrada, os dados serão adicionados às tabelas no `DataSet`. `Fill` usa qualquer mapeamento que possa existir ao preencher `DataSet` (confira os [Mapeamentos de DataAdapter, DataTable e DataColumn](dataadapter-datatable-datacolumn-mappings.md)).

> [!NOTE]
> Se o `SelectCommand` retornar os resultados de um OUTER JOIN, o `DataAdapter` não definirá um valor de `PrimaryKey` para o`DataTable` resultante. Você deve definir o `PrimaryKey` você mesmo para garantir que as linhas duplicadas sejam resolvidas corretamente.

O exemplo de código a seguir cria uma instância de um <xref:Microsoft.Data.SqlClient.SqlDataAdapter> que usa um <xref:Microsoft.Data.SqlClient.SqlConnection> para o banco de dados `Northwind` do Microsoft SQL Server e preenche uma <xref:System.Data.DataTable> em um `DataSet` com a lista de clientes. A instrução SQL e os argumentos <xref:Microsoft.Data.SqlClient.SqlConnection> passados para o construtor de <xref:Microsoft.Data.SqlClient.SqlDataAdapter> são usados para criar a propriedade de <xref:Microsoft.Data.SqlClient.SqlDataAdapter.SelectCommand%2A> de <xref:Microsoft.Data.SqlClient.SqlDataAdapter>.

## <a name="example"></a>Exemplo

[!code-csharp[SqlDataAdapter_FillDataSet#1](~/../sqlclient/doc/samples/SqlDataAdapter_FillDataSet.cs#1)]

> [!NOTE]
> O código mostrado neste exemplo não abre e não fecha explicitamente a `Connection`. O método `Fill` abre implicitamente a `Connection` que o `DataAdapter` estiver usando se descobrir que a conexão ainda não está aberta. Se `Fill` tiver aberto a conexão, ele também fechará a conexão quando `Fill` terminar. Isso pode simplificar o seu código quando você manipula uma única operação como `Fill` ou `Update`. No entanto, se você estiver executando várias operações que exigem uma conexão aberta, poderá melhorar o desempenho do seu aplicativo explicitamente chamando o método `Open` da `Connection`, executando operações na fonte de dados e, em seguida, chamando o método `Close` da `Connection`. Você deve tentar manter abertas as conexões para a fonte de dados o mais rapidamente possível para liberar recursos para o uso por outros aplicativos cliente.

## <a name="multiple-result-sets"></a>Vários conjuntos de resultados

Se o `DataAdapter` encontrar vários conjuntos de resultados, criará várias tabelas no `DataSet`. As tabelas recebem um nome padrão incremental correspondente a Table *N*, começando com "Table" para o primeiro item (Table0). Se um nome de tabela for passado como argumento para o método `Fill`, as tabelas receberão um nome padrão incremental correspondente a TableName *N*, começando com "TableName" para o primeiro item (TableName0).  
  
## <a name="populating-a-dataset-from-multiple-dataadapters"></a>Preenchendo um DataSet por meio de vários DataAdapters  

 Vários objetos `DataAdapter` podem ser usados com `DataSet`. Cada `DataAdapter` pode ser usado para preencher um ou mais objetos `DataTable` e resolver atualizações de volta para a fonte de dados relevante. Os objetos `DataRelation` e `Constraint` podem ser adicionados ao `DataSet` localmente, o que permite relacionar dados de fontes de dados não semelhantes. Por exemplo, um `DataSet` pode conter dados de um banco de dados Microsoft SQL Server, um banco de dados IBM DB2 exposto por meio do OLE DB e uma fonte de dados que transmite XML. Um ou mais objetos `DataAdapter` podem administrar a comunicação para cada fonte de dados.  
  
### <a name="example"></a>Exemplo  

 O exemplo de código a seguir preenche uma lista de clientes do banco de dados `Northwind` no Microsoft SQL Server, e uma lista de pedidos do banco de dados `Northwind` armazenado no Microsoft Access 2000. As tabelas preenchidas estão relacionadas com um `DataRelation`, e a lista de clientes é exibida com os pedidos para aquele cliente.

[!code-csharp[SqlDataAdapter_FillDataSet#2](~/../sqlclient/doc/samples/SqlDataAdapter_FillDataSet.cs#2)]

## <a name="sql-server-decimal-type"></a>Tipo decimal do SQL Server

Por padrão, `DataSet` armazena dados usando os tipos de dados do .NET. Para a maioria dos aplicativos, eles fornecem uma representação conveniente de informações da fonte de dados. No entanto, essa representação pode causar um problema quando o tipo de dados na fonte de dados é um decimal ou um tipo de dados numérico do SQL Server. O tipo de dados `decimal` do .NET permite um máximo de 28 dígitos significativos, ao passo que o tipo de dados `decimal` do SQL Server permite 38 dígitos significativos. Se o `SqlDataAdapter` determina durante uma operação de `Fill` que a precisão de um campo do SQL Server `decimal` é maior que 28 caracteres, a linha atual não será adicionada ao `DataTable`. Em vez disso, o evento de `FillError` ocorre, o que permite determinar se uma perda de precisão ocorrerá e responder corretamente. Para obter mais informações sobre o evento `FillError`, confira [Gerenciar eventos do DataAdapter](handle-dataadapter-events.md). Para obter o valor `decimal` do SQL Server, você também poderá usar um objeto <xref:Microsoft.Data.SqlClient.SqlDataReader> e chamar o método <xref:Microsoft.Data.SqlClient.SqlDataReader.GetSqlDecimal%2A>.

O ADO.NET também inclui suporte aprimorado para <xref:System.Data.SqlTypes> em `DataSet`. Para obter mais informações, confira [SqlTypes e o DataSet](./sql/sqltypes-dataset.md).

## <a name="see-also"></a>Confira também

- [DataAdapters e DataReaders](dataadapters-datareaders.md)
- [Mapeamentos de tipo de dados no ADO.NET](data-type-mappings-ado-net.md)
- [MARS (conjunto de resultados ativos múltiplos)](./sql/multiple-active-result-sets-mars.md)
- [Microsoft ADO.NET for SQL Server](microsoft-ado-net-sql-server.md)
