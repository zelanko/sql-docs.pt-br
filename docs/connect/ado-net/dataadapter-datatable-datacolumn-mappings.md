---
title: Mapeamentos de DataAdapter, DataTable e DataColumn
description: Descreve como configurar DataTableMappings e ColumnMappings para um DataAdapter.
ms.date: 11/30/2020
dev_langs:
- csharp
ms.assetid: d023260a-a66a-4c39-b8f4-090cd130e730
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-chmalh
ms.openlocfilehash: e8b2f84fbbf888fc67cdb8f945d7f0c887c14eaa
ms.sourcegitcommit: c127c0752e84cccd38a7e23ac74c0362a40f952e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/07/2020
ms.locfileid: "96772166"
---
# <a name="dataadapter-datatable-and-datacolumn-mappings"></a>Mapeamentos de DataAdapter, DataTable e DataColumn

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

Um <xref:Microsoft.Data.SqlClient.SqlDataAdapter> contém uma coleção de zero ou mais objetos <xref:System.Data.Common.DataTableMapping> na propriedade <xref:System.Data.Common.DataAdapter.TableMappings%2A>. Um **DataTableMapping** fornece um mapeamento mestre entre os dados retornados de uma consulta em uma fonte de dados e um <xref:System.Data.DataTable>. O nome do **DataTableMapping** pode ser passado no lugar do nome do **DataTable** para o método <xref:System.Data.Common.DbDataAdapter.Fill%2A> do **DataAdapter**. O exemplo a seguir cria um **DataTableMapping** denominado **AuthorsMapping** para a tabela **Authors**.

```csharp
workAdapter.TableMappings.Add("AuthorsMapping", "Authors");
```

Um **DataTableMapping** permite que você use nomes de colunas em um **DataTable** que sejam diferentes daqueles do banco de dados. O **DataAdapter** usa o mapeamento para corresponder as colunas quando a tabela é atualizada.

> [!NOTE]
> Se você não especificar um **TableName** ou um nome de **DataTableMapping** ao chamar o método **Fill** ou **Update** do **DataAdapter**, o **DataAdapter** vai procurar o **DataTableMapping** denominado "Table". O **TableName** do **DataTable** será "Table" se aquele **DataTableMapping** não existir. Você pode especificar um **DataTableMapping** padrão criando um **DataTableMapping** com o nome de "Table".

O exemplo de código a seguir cria um **DataTableMapping** (do namespace <xref:System.Data.Common>) e o transforma no mapeamento padrão para o **DataAdapter** especificado, nomeando-o como "Table". Em seguida, o exemplo mapeia as colunas da primeira tabela no resultado da consulta (a tabela **Customers** do banco de dados **Northwind**) para um conjunto de nomes mais amigáveis na tabela **Northwind Customers** no <xref:System.Data.DataSet>. Para colunas que não são mapeadas, o nome da coluna na fonte de dados é usado.

[!code-csharp[SqlDataAdapter_TableMappings#1](~/../sqlclient/doc/samples/SqlDataAdapter_TableMappings.cs#1)]

Em situações mais avançadas, você pode decidir que deseja que o mesmo **DataAdapter** dê suporte ao carregamento de diferentes tabelas com diferentes mapeamentos. Para fazer isso, adicione outros objetos **DataTableMapping**.

Quando o método **Fill** recebe uma instância de **DataSet** e um nome de **DataTableMapping**, se existir um mapeamento com esse nome, ele será usado. Caso contrário, um **DataTable** com esse nome será usado.

Os exemplos a seguir criam um **DataTableMapping** com um nome de **Customers** e um nome de **DataTable** de **BizTalkSchema**. Em seguida, o exemplo mapeia as linhas retornadas pela instrução SELECT ao **DataTable** do **BizTalkSchema**.

[!code-csharp[SqlDataAdapter_TableMappings#2](~/../sqlclient/doc/samples/SqlDataAdapter_TableMappings.cs#2)]

> [!NOTE]
> Se um nome de coluna de origem não for fornecido para um mapeamento de coluna, os nomes padrão serão gerados automaticamente. O mapeamento de coluna recebe um nome padrão incremental de **SourceColumn** *N*, começando com **SourceColumn1** se nenhuma coluna de origem for fornecida para o mapeamento de coluna.

> [!NOTE]
> Se um nome de tabela de origem não for fornecido para um mapeamento de tabela, os nomes padrão serão gerados automaticamente. O mapeamento de tabela recebe um nome padrão incremental de **SourceTable** *N*, começando com **SourceTable1** se nenhum nome de tabela de origem for fornecido ao mapeamento de tabela.

> [!NOTE]
> É recomendável evitar a convenção de nomenclatura de **SourceColumn** *N* para um mapeamento de coluna ou **SourceTable** *N* para um mapeamento de tabela, porque o nome que você fornece pode entrar em conflito com um nome padrão de mapeamento de coluna existente no **ColumnMappingCollection** ou um nome de mapeamento de tabela existente no **DataTableMappingCollection**. Se o nome fornecido já existir, será gerada uma exceção.

## <a name="handle-multiple-result-sets"></a>Gerenciar vários conjuntos de resultados

Se o comando **SelectCommand** retornar várias tabelas, o **Fill** vai gerar automaticamente nomes de tabelas com valores incrementais para as tabelas do **DataSet**, começando com o nome da tabela especificado e continuando no formato **TableName** *N*, começando com **TableName1**. Você pode usar mapeamentos de tabela para mapear o nome de tabela gerado automaticamente para um nome que você deseja especificado para a tabela no **DataSet**. Por exemplo, para um **SelectCommand** que retorne duas tabelas, **Customers** e **Orders**, emita a seguinte chamada para **Fill**.

```csharp
adapter.Fill(customersDataSet, "Customers");
```

Duas tabelas são criadas no **DataSet**: **Customers** e **Customers1**. Você pode usar mapeamentos de tabela para que a segunda tabela seja denominada **Orders** em vez de **Customers1**. Para fazer isso, mapeie a tabela de origem de **Customers1** para a tabela do **DataSet** **Orders**, conforme mostrado no exemplo a seguir.

[!code-csharp[SqlDataAdapter_TableMappings#3](~/../sqlclient/doc/samples/SqlDataAdapter_TableMappings.cs#3)]

## <a name="see-also"></a>Confira também

- [DataAdapters e DataReaders](dataadapters-datareaders.md)
- [Recuperar e modificar dados no ADO.NET](retrieving-modifying-data.md)
- [Microsoft ADO.NET for SQL Server](microsoft-ado-net-sql-server.md)
