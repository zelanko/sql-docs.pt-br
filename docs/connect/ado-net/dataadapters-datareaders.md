---
title: DataAdapters e DataReaders
description: Saiba mais sobre o Provedor de Dados do Microsoft SqlClient para SQL Server DataReader, que recupera dados de um banco de dados, e sobre o DataAdapter, que recupera dados de uma fonte de dados e preenche um DataSet.
ms.date: 11/30/2020
ms.assetid: cc952ca2-ec19-46ab-9189-15174b52cb74
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-chmalh
ms.openlocfilehash: e71f6218c9fecd956a7c287581caa72a1a787462
ms.sourcegitcommit: c127c0752e84cccd38a7e23ac74c0362a40f952e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/07/2020
ms.locfileid: "96772158"
---
# <a name="dataadapters-and-datareaders"></a>DataAdapters e DataReaders

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

Você pode usar o Provedor de Dados do Microsoft SqlClient para SQL Server **DataReader** a fim de recuperar um fluxo de dados somente leitura e somente encaminhamento de um banco de dados. Os resultados são retornados conforme a consulta é executada e são armazenados no buffer da rede no cliente até que você os solicite usando o método **Read** do **DataReader**. O uso do **DataReader** pode aumentar o desempenho do aplicativo recuperando dados assim que estejam disponíveis e (por padrão) armazenando apenas uma linha de cada vez na memória e reduzindo a sobrecarga do sistema.

Um <xref:System.Data.Common.DataAdapter> é usado para recuperar dados de uma fonte de dados e para popular tabelas em um <xref:System.Data.DataSet>. O `DataAdapter` também resolve as alterações feitas no `DataSet` de volta para a fonte de dados. `DataAdapter` usa o objeto `Connection` da Provedor de Dados do Microsoft SqlClient para SQL Server a fim de se conectar a uma fonte de dados e usa objetos `Command` para recuperar dados e resolver alterações na fonte de dados.

O .NET tem um <xref:System.Data.Common.DbDataReader> e um objeto <xref:System.Data.Common.DbDataAdapter>: o Provedor de Dados do Microsoft SqlClient para SQL Server inclui um objeto <xref:Microsoft.Data.SqlClient.SqlDataReader> e um <xref:Microsoft.Data.SqlClient.SqlDataAdapter>.

## <a name="in-this-section"></a>Nesta seção

[Recuperar dados por um DataReader](retrieve-data-by-datareader.md)  
Descreve o objeto **DataReader** do ADO.NET e como usá-lo para retornar um fluxo de resultados de uma fonte de dados.

[Preencher um DataSet de um DataAdapter](populate-dataset-from-dataadapter.md)  
Descreve como preencher um `DataSet` com tabelas, colunas, e linhas usando um `DataAdapter`.

[Parâmetros de DataAdapter](dataadapter-parameters.md)  
Descreve como usar parâmetros com as propriedades de comando de um `DataAdapter` incluindo como mapear o conteúdo de uma coluna em um `DataSet` para um parâmetro de comando.

[Adicionar restrições existentes a um DataSet](add-existing-constraints-to-dataset.md)  
Descreve como adicionar as restrições existentes a um `DataSet`.

[Mapeamentos de DataAdapter, DataTable e DataColumn](dataadapter-datatable-datacolumn-mappings.md)  
Descreve como configurar `DataTableMappings` e `ColumnMappings` para um `DataAdapter`.

[Paginação por meio de um resultado de consulta](paging-through-query-result.md)  
Fornece um exemplo de como exibir os resultados de uma consulta como páginas de dados.

[Atualizar fontes de dados com DataAdapters](update-data-sources-with-dataadapters.md)  
Descreve como usar um `DataAdapter` para resolver alterações em um `DataSet` de volta para o banco de dados.

[Manipular eventos de DataAdapter](handle-dataadapter-events.md)  
Descreve os eventos do `DataAdapter` e como usá-los.

[Operações em lote usando DataAdapters](batch-operations-using-dataadapters.md)  
Descreve como melhorar o desempenho do aplicativo reduzindo o número de viagens de ida e volta ao SQL Server para aplicar atualizações do `DataSet`.

## <a name="see-also"></a>Confira também

- [Conectar-se a fontes de dados](connecting-to-data-source.md)
- [Comandos e parâmetros](commands-parameters.md)
- [Microsoft ADO.NET for SQL Server](microsoft-ado-net-sql-server.md)
