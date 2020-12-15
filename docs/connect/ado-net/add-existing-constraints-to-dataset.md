---
title: Adicionar restrições existentes a um DataSet
description: Descreve como adicionar restrições existentes a um DataSet.
ms.date: 11/30/2020
dev_langs:
- csharp
ms.assetid: 307d2809-208b-4cf8-b6a9-5d16f15fc16c
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-chmalh
ms.openlocfilehash: 9471f62c36604cb01ea78f558ac3bfbcb7f4bc01
ms.sourcegitcommit: c127c0752e84cccd38a7e23ac74c0362a40f952e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/07/2020
ms.locfileid: "96772181"
---
# <a name="add-existing-constraints-to-a-dataset"></a>Adicionar restrições existentes a um DataSet

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

O método <xref:System.Data.Common.DbDataAdapter.Fill%2A> de <xref:Microsoft.Data.SqlClient.SqlDataAdapter> preenche um <xref:System.Data.DataSet> somente com colunas e linhas da tabela de uma fonte de dados; embora as restrições normalmente sejam definidas pela fonte de dados, o método **Fill** não adiciona essas informações de esquema ao **DataSet** por padrão.

Para preencher um **DataSet** com as informações de restrição de chave primária existentes de uma fonte de dados, você pode chamar o método <xref:System.Data.Common.DbDataAdapter.FillSchema%2A> do **DataAdapter** ou definir a propriedade <xref:System.Data.Common.DataAdapter.MissingSchemaAction%2A> do **DataAdapter** como **AddWithKey** antes de chamar o método **Fill**. Isso fará com que as restrições de chave primária do **DataSet** reflitam as restrições da fonte de dados.

> [!NOTE]
> As informações de restrição de chave estrangeira não estão incluídas e devem ser criadas explicitamente.

A adição de informações de esquema a um **DataSet** antes de preenchê-lo com os dados desejados faz com que as restrições de chave primária sejam incluídas com os objetos <xref:System.Data.DataTable> no **DataSet**. Como resultado, quando as chamadas adicionais para preencher o **DataSet** são feitas, as informações da coluna de chave primária são usadas para fazer a correspondência de novas linhas da fonte de dados com as linhas atuais de cada **DataTable**, e os dados atuais das tabelas são substituídos pelos dados da fonte de dados. Sem as informações do esquema, as novas linhas da fonte de dados são acrescentadas ao **DataSet**, resultando em linhas duplicadas.

> [!NOTE]
> Se uma coluna em uma fonte de dados for identificada como de incrementação automática, o método <xref:System.Data.Common.DbDataAdapter.FillSchema%2A> ou o método <xref:System.Data.Common.DbDataAdapter.Fill%2A> com uma <xref:System.Data.Common.DataAdapter.MissingSchemaAction%2A> de **AddWithKey**, criará uma **DataColumn** com uma propriedade **AutoIncrement** definida como `true`. No entanto, você precisará definir os valores de **AutoIncrementStep** e **AutoIncrementSeed** por conta própria.

> [!NOTE]
> O uso do **FillSchema** ou a definição do **MissingSchemaAction** como **AddWithKey** requer processamento extra na fonte de dados para determinar as informações da coluna de chave primária. Esse processamento adicional pode prejudicar o desempenho. Se você souber as informações de chave primária em tempo de design, recomendamos especificar explicitamente a coluna (ou colunas) de chave primária, a fim de alcançar um desempenho ideal.

O seguinte exemplo de código mostra como adicionar informações de esquema a um **DataSet** usando <xref:System.Data.Common.DbDataAdapter.FillSchema%2A>:

[!code-csharp[SqlDataAdapter_FillDataSet#1](~/../sqlclient/doc/samples/SqlDataAdapter_FillDataSet.cs#1)]

O seguinte exemplo de código mostra como adicionar informações de esquema a um **DataSet** usando a propriedade <xref:System.Data.Common.DataAdapter.MissingSchemaAction%2A> e o método <xref:System.Data.Common.DbDataAdapter.Fill%2A>:

[!code-csharp[SqlDataAdapter_FillDataSet#2](~/../sqlclient/doc/samples/SqlDataAdapter_FillDataSet.cs#2)]

## <a name="handling-multiple-result-sets"></a>Manipulando vários conjuntos de resultados

Se o **DataAdapter** atender a vários conjuntos de resultados retornados de <xref:Microsoft.Data.SqlClient.SqlDataAdapter.SelectCommand%2A>, ele criará várias tabelas no **DataSet**. As tabelas receberão um nome padrão incremental partindo do zero correspondente a **Tabela** *N*, começando apenas com **Tabela** em vez de "Table0". As tabelas receberão um nome incremental partindo do zero correspondente a **TableName** *N*, começando com **TableName** em vez de "TableName0" se um nome de tabela for passado como argumento para o método <xref:System.Data.Common.DbDataAdapter.FillSchema%2A>.

## <a name="see-also"></a>Confira também

- [DataAdapters e DataReaders](dataadapters-datareaders.md)
- [Recuperar e modificar dados no ADO.NET](retrieving-modifying-data.md)
- [Microsoft ADO.NET for SQL Server](microsoft-ado-net-sql-server.md)
