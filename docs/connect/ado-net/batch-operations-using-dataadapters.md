---
title: Operações em lote usando DataAdapters
description: Descreve o aprimoramento do desempenho do aplicativo, reduzindo o número de viagens de ida e volta para o SQL Server ao aplicar atualizações do DataSet.
ms.date: 11/30/2020
dev_langs:
- csharp
ms.assetid: e72ed5af-b24f-486c-8429-c8fd2208f844
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-chmalh
ms.openlocfilehash: 1b720dff0678c68396fe7d8cf1f60f3ade70dd9d
ms.sourcegitcommit: c127c0752e84cccd38a7e23ac74c0362a40f952e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/07/2020
ms.locfileid: "96772179"
---
# <a name="batch-operations-using-dataadapters"></a>Operações em lote usando DataAdapters

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

O suporte a lotes no ADO.NET permite que um <xref:System.Data.Common.DataAdapter> agrupe operações INSERT, UPDATE e DELETE de um <xref:System.Data.DataSet> ou <xref:System.Data.DataTable> para o servidor, em vez de enviar uma operação de cada vez. A redução no número de viagens de ida e volta para o servidor costuma resultar em ganhos significativos de desempenho. A atualização do lote é compatível com o provedor de dados do Microsoft SqlClient para SQL Server (<xref:Microsoft.Data.SqlClient>).

Ao atualizar um banco de dados com alterações de um <xref:System.Data.DataSet> em versões anteriores do ADO.NET, o método `Update` de um `DataAdapter` executava atualizações no banco de dados em uma linha por vez. Ao iterar pelas linhas no <xref:System.Data.DataTable> especificado, ele revisava cada <xref:System.Data.DataRow> para verificar se ocorreram modificações. Se a linha tivesse sido alterada, ele chamava o `UpdateCommand`, `InsertCommand` ou `DeleteCommand` apropriado, dependendo do valor da propriedade <xref:System.Data.DataRow.RowState%2A> para essa linha. Cada atualização de linha envolvia uma viagem de ida e volta da rede ao banco de dados.

No Provedor de Dados do Microsoft SqlClient para SQL Server, o <xref:Microsoft.Data.SqlClient.SqlDataAdapter> expõe uma propriedade <xref:Microsoft.Data.SqlClient.SqlDataAdapter.UpdateBatchSize%2A>. Definir o `UpdateBatchSize` com um valor inteiro positivo causa o envio de atualizações do banco de dados como lotes de tamanho especificado. Por exemplo, a definição do `UpdateBatchSize` como 10 agrupará 10 instruções separadas e as submeterá como um único lote. Definir o `UpdateBatchSize` como 0 fará com que o <xref:Microsoft.Data.SqlClient.SqlDataAdapter> use o maior tamanho de lotes que o servidor possa manipular. Defini-lo como 1 desabilitará atualizações em lotes, pois as linhas são enviadas uma de cada vez.

> [!NOTE]
> Executar um lote extremamente grande pode diminuir o desempenho. Portanto, você deve testar para verificar qual é a melhor configuração de tamanho de lote antes de implementar seu aplicativo.

## <a name="use-the-updatebatchsize-property"></a>Usar a propriedade UpdateBatchSize

Quando atualizações em lotes são habilitadas, o valor da propriedade <xref:System.Data.IDbCommand.UpdatedRowSource%2A> de `UpdateCommand`, de `InsertCommand` e de `DeleteCommand` do DataAdapter deve ser definido como <xref:System.Data.UpdateRowSource.None> ou <xref:System.Data.UpdateRowSource.OutputParameters>. Ao executar uma atualização em lotes, o valor da propriedade <xref:System.Data.IDbCommand.UpdatedRowSource%2A> do comando de <xref:System.Data.UpdateRowSource.FirstReturnedRecord> ou de <xref:System.Data.UpdateRowSource.Both> é inválido.
  
O procedimento a seguir demonstra o uso da propriedade `UpdateBatchSize`. O procedimento tem dois argumentos, um objeto <xref:System.Data.DataSet> com colunas que representam os campos **ProductCategoryID** e **Name** na tabela **Production.ProductCategory** e um inteiro que representa o tamanho do lote (o número de linhas no lote). O código cria um novo objeto <xref:Microsoft.Data.SqlClient.SqlDataAdapter>, definindo suas propriedades <xref:Microsoft.Data.SqlClient.SqlDataAdapter.UpdateCommand%2A>, <xref:Microsoft.Data.SqlClient.SqlDataAdapter.InsertCommand%2A> e <xref:Microsoft.Data.SqlClient.SqlDataAdapter.DeleteCommand%2A>. O código pressupõe que o objeto <xref:System.Data.DataSet> alterou linhas. Ele define a propriedade `UpdateBatchSize` e executa a atualização.

[!code-csharp[SqlDataAdapter_Batch#1](~/../sqlclient/doc/samples/SqlDataAdapter_Batch.cs#1)]

## <a name="handle-batch-update-related-events-and-errors"></a>Gerenciar eventos e erros relacionados à atualização em lote

O **DataAdapter** tem dois eventos relacionados à atualização: **RowUpdating** e **RowUpdated**. Para obter mais informações, confira [Gerenciar eventos do DataAdapter](handle-dataadapter-events.md).

### <a name="event-behavior-changes-with-batch-updates"></a>Alterações de comportamento de evento com atualizações em lote

Quando o processamento em lotes está habilitado, várias linhas são atualizadas em uma única operação de banco de dados. Portanto, somente um evento `RowUpdated` ocorre para cada lote, enquanto o evento `RowUpdating` ocorre para cada linha processada. Quando o processamento em lotes está desabilitado, os dois eventos são disparados com interpolação um a um, onde um evento `RowUpdating` e um evento `RowUpdated` são disparados para uma linha e, depois, um evento `RowUpdating` e um evento `RowUpdated` são disparados para a próxima linha, até que todas as linhas sejam processadas.

### <a name="access-updated-rows"></a>Acessar linhas atualizadas

Quando o processamento em lotes está desabilitado, a linha que está sendo atualizada pode ser acessada usando a propriedade <xref:System.Data.Common.RowUpdatedEventArgs.Row%2A> da classe <xref:System.Data.Common.RowUpdatedEventArgs>.

Quando o processamento em lotes está habilitado, um único evento `RowUpdated` é gerado para várias linhas. Portanto, o valor da propriedade `Row` para cada linha é nulo. Os eventos `RowUpdating` ainda são gerados para cada linha. O método <xref:System.Data.Common.RowUpdatedEventArgs.CopyToRows%2A> da classe <xref:System.Data.Common.RowUpdatedEventArgs> permite que você acesse as linhas processadas copiando referências às linhas em uma matriz. Se nenhuma linha está sendo processada, `CopyToRows` gera <xref:System.ArgumentNullException>. Use a propriedade <xref:System.Data.Common.RowUpdatedEventArgs.RowCount%2A> para retornar o número de linhas processadas antes de chamar o método <xref:System.Data.Common.RowUpdatedEventArgs.CopyToRows%2A>.

### <a name="handle-data-errors"></a>Gerenciar erros de dados

A execução em lotes tem o mesmo efeito que a execução de cada instrução individual. As instruções são executadas na ordem em que elas foram adicionados ao lote. O tratamento de erros no modo em lotes é o mesmo de quando esse modo está desabilitado. Cada linha é processada separadamente. Somente linhas que foram processadas com êxito no banco de dados serão atualizadas na <xref:System.Data.DataRow> correspondente dentro da <xref:System.Data.DataTable>.

> [!NOTE]
> O Provedor de Dados do Microsoft SqlClient para SQL Server e o servidor de banco de dados de back-end determinam quais constructos SQL são compatíveis com a execução em lote. Uma exceção pode ser gerada quando uma instrução sem suporte é enviada para execução.

## <a name="see-also"></a>Confira também

- [DataAdapters e DataReaders](dataadapters-datareaders.md)
- [Atualizar fontes de dados com DataAdapters](update-data-sources-with-dataadapters.md)
- [Manipular eventos de DataAdapter](handle-dataadapter-events.md)
- [Microsoft ADO.NET for SQL Server](microsoft-ado-net-sql-server.md)
