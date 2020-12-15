---
title: Manipular eventos de DataAdapter
description: Descreve os eventos do DataAdapter e como usá-los.
ms.date: 11/30/2020
dev_langs:
- csharp
ms.assetid: 11515b25-ee49-4b1d-9294-a142147c1ec5
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-chmalh
ms.openlocfilehash: 003a8e77ad80f83c210ffb565ce4fac5c93c2166
ms.sourcegitcommit: c127c0752e84cccd38a7e23ac74c0362a40f952e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/07/2020
ms.locfileid: "96772155"
---
# <a name="handle-dataadapter-events"></a>Manipular eventos de DataAdapter

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

O provedor de dados do Microsoft SqlClient para SQL Server <xref:Microsoft.Data.SqlClient.SqlDataAdapter> expõe três eventos que você pode usar para responder a alterações feitas nos dados na fonte de dados. A tabela a seguir mostra os `DataAdapter` eventos.

|Evento|Descrição|  
|-----------|-----------------|  
|`RowUpdating`|Uma operação UPDATE, INSER ou DELETE em uma linha (por meio da chamada a um dos métodos `Update`) está prestes a começar.|  
|`RowUpdated`|Uma operação UPDATE, INSER ou DELETE em uma linha (por meio da chamada a um dos métodos `Update`) está concluída.|  
|`FillError`|Ocorreu um erro durante uma operação `Fill`.|  

## <a name="rowupdating-and-rowupdated-events"></a>Eventos RowUpdating e RowUpdated

`RowUpdating` é gerado antes que qualquer atualização em uma linha de <xref:System.Data.DataSet> tenha sido processada na fonte de dados. `RowUpdated` é gerado depois que qualquer atualização em uma linha de `DataSet` tenha sido processada na fonte de dados. Como resultado, você pode usar `RowUpdating` para modificar o comportamento da atualização antes que ela ocorra, para fornecer tratamento adicional quando ocorre uma atualização, para manter uma referência a uma linha atualizada, para cancelar a atualização atual e agendá-la para que um processo em lote seja processado posteriormente e assim por diante. `RowUpdated` é útil para responder a erros e exceções que ocorrem durante a atualização. Você pode adicionar **informações de erro** ao `DataSet`, bem como **tentar novamente a lógica** e assim por diante.

Os argumentos <xref:System.Data.Common.RowUpdatingEventArgs> e <xref:System.Data.Common.RowUpdatedEventArgs> passados para os eventos `RowUpdating` e `RowUpdated` incluem o seguinte: uma propriedade `Command` que faz referência ao objeto `Command` que está sendo usado para executar a atualização; uma propriedade `Row` que faz referência ao objeto `DataRow` que contém as informações atualizadas; uma propriedade `StatementType` para qual tipo de atualização está sendo executada; a `TableMapping`, se aplicável; e a `Status` da operação.

Você pode usar a propriedade `Status` para determinar se ocorreu um erro durante a operação e, se desejar, para controlar as ações sobre as linhas atuais e resultantes. Quando o evento ocorre, a propriedade `Status` é igual a `Continue` ou `ErrorsOccurred`. A tabela a seguir mostra os valores para os quais você pode definir a propriedade `Status` para controlar as ações posteriores durante a atualização.

|Status|Descrição|  
|------------|-----------------|  
|`Continue`|Continue com a operação de atualização.|  
|`ErrorsOccurred`|Anule a operação de atualização e lance uma exceção.|  
|`SkipCurrentRow`|Ignore a linha atual e continue com a operação de atualização.|  
|`SkipAllRemainingRows`|Anule a operação de atualização, mas não lance uma exceção.|  

Definir a propriedade `Status` como `ErrorsOccurred` faz com que uma exceção seja lançada. Você pode controlar qual exceção é lançada definindo a propriedade `Errors` como a exceção desejada. O uso de um dos outros valores para `Status` impede que uma exceção seja gerada.

Você também pode usar a propriedade `ContinueUpdateOnError` para gerenciar os erros das linhas atualizadas. Se `DataAdapter.ContinueUpdateOnError` for `true`, quando a atualização de uma linha resultar no lançamento de uma exceção, o texto da exceção será colocado nas informações de `RowError` da linha específica e o processamento continuará sem lançar uma exceção. Isso permite que você responda aos erros quando a `Update` for concluída, ao contrário do evento `RowUpdated`, que lhe permite responder aos erros no momento em que eles são encontrados.

O exemplo de código a seguir mostra como adicionar e remover manipuladores de eventos. O manipulador de eventos `RowUpdating` grava um log com todos os registros excluídos com um carimbo de data/hora. O manipulador de eventos `RowUpdated` adiciona informações de erro à propriedade `RowError` da linha em `DataSet`, suprime a exceção e continua o processamento (espelhando o comportamento de `ContinueUpdateOnError` = `true`).

[!code-csharp[SqlDataAdapter_Events#1](~/../sqlclient/doc/samples/SqlDataAdapter_Events.cs#1)]

## <a name="fillerror-event"></a>Evento FillError

`DataAdapter` emite o evento `FillError` quando ocorre um erro durante uma operação `Fill`. Esse tipo de erro geralmente ocorre quando os dados da linha que está sendo adicionados não podem ser convertidos em um tipo .NET sem alguma perda de precisão.

Se ocorrer um erro durante uma operação `Fill`, a linha atual não será adicionada à `DataTable`. O evento `FillError` permite que você resolva o erro e adicione a linha ou ignore a linha excluída e continue com a operação `Fill`.

O <xref:System.Data.FillErrorEventArgs> passado para o evento `FillError` pode conter várias propriedades que lhe permitem responder aos erros e resolvê-los. A tabela a seguir mostra as propriedades do objeto `FillErrorEventArgs`.

|Propriedade|Descrição|  
|--------------|-----------------|  
|`Errors`|O `Exception` que ocorreu.|  
|`DataTable`|O objeto `DataTable` que estava sendo preenchido quando o erro ocorreu.|  
|`Values`|A matriz de objetos que contém os valores da linha que estava sendo adicionada quando o erro ocorreu. As referências ordinais da matriz `Values` correspondem às referências ordinais das colunas da linha que está sendo adicionada. Por exemplo, `Values[0]` é o valor que estava sendo adicionado como a primeira coluna da linha.|  
|`Continue`|Permite que você escolha se deseja ou não lançar uma exceção. Definir a propriedade `Continue` como `false` interromperá a operação `Fill` atual e lançará uma exceção. A configuração de `Continue` como `true` permite continuar com a operação `Fill` apesar do erro.|  

O exemplo de código a seguir adiciona um manipulador de eventos para o evento `FillError` de `DataAdapter`. No código do evento `FillError`, o exemplo determina se há o potencial para perda de precisão, fornecendo a oportunidade de responder à exceção.

[!code-csharp[SqlDataAdapter_Events#2](~/../sqlclient/doc/samples/SqlDataAdapter_Events.cs#2)]

## <a name="see-also"></a>Confira também

- [DataAdapters e DataReaders](dataadapters-datareaders.md)
- [Eventos](/dotnet/standard/events/index.md)
- [Microsoft ADO.NET for SQL Server](microsoft-ado-net-sql-server.md)
