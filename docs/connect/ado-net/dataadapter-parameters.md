---
title: Parâmetros de DataAdapter
description: Saiba mais sobre as propriedades do DbDataAdapter que retornam dados de uma fonte de dados e gerenciam as alterações da fonte de dados.
ms.date: 11/30/2020
dev_langs:
- csharp
ms.assetid: f21e6aba-b76d-46ad-a83e-2ad8e0af1e12
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-chmalh
ms.openlocfilehash: d72660a55fa047864148c90ae4087782302adc22
ms.sourcegitcommit: c127c0752e84cccd38a7e23ac74c0362a40f952e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/07/2020
ms.locfileid: "96772156"
---
# <a name="dataadapter-parameters"></a>Parâmetros de DataAdapter

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

O <xref:System.Data.Common.DbDataAdapter> tem quatro propriedades que são usadas para recuperar dados da fonte de dados e atualizá-los nela: a propriedade <xref:System.Data.Common.DbDataAdapter.SelectCommand%2A> retorna dados da fonte de dados; e as propriedades <xref:System.Data.Common.DbDataAdapter.InsertCommand%2A>, <xref:System.Data.Common.DbDataAdapter.UpdateCommand%2A> e <xref:System.Data.Common.DbDataAdapter.DeleteCommand%2A> são usadas para gerenciar alterações na fonte de dados.

> [!NOTE]
> A propriedade `SelectCommand` deve ser definida antes que você chame o método `Fill` do `DataAdapter`. A propriedade `InsertCommand`, `UpdateCommand` ou `DeleteCommand` deve ser definida antes que o método `Update` do `DataAdapter` seja chamado, dependendo de quais alterações foram feitas nos dados da <xref:System.Data.DataTable>. Por exemplo, se as linhas tiverem sido adicionadas, o `InsertCommand` deve ser definido antes de chamar `Update`. Quando `Update` estiver processando uma linha inserida, atualizada ou excluída, o `DataAdapter` usará a respectiva propriedade `Command` para processar a ação. As informações atuais sobre a linha modificada são passadas para o objeto `Command` através da coleção `Parameters`.

Ao atualizar uma linha da fonte de dados, você chama a instrução UPDATE, que usa um identificador exclusivo para identificar a linha da tabela a ser atualizada. O identificador exclusivo é geralmente o valor de um campo de chave primária. A instrução UPDATE usa os parâmetros que contêm o identificador exclusivo e as colunas e os valores a serem atualizados, conforme mostrado na declaração Transact-SQL a seguir.

```sql
UPDATE Customers SET CompanyName = @CompanyName
  WHERE CustomerID = @CustomerID  
```  

> [!NOTE]
> A sintaxe para espaços reservados de parâmetro depende da fonte de dados. Este exemplo mostra os espaços reservados de uma fonte de dados do SQL Server.

Neste exemplo, o campo `CompanyName` é atualizado com o valor do parâmetro `@CompanyName` na linha em que `CustomerID` é igual ao valor do parâmetro `@CustomerID`. Os parâmetros recuperam informações da linha modificada usando a propriedade <xref:Microsoft.Data.SqlClient.SqlParameter.SourceColumn%2A> do objeto <xref:Microsoft.Data.SqlClient.SqlParameter>. Estes são os parâmetros da instrução UPDATE de exemplo anterior. O código assume que a variável `adapter` representa um objeto <xref:Microsoft.Data.SqlClient.SqlDataAdapter> válido.

[!code-csharp[Classic WebData SqlDataAdapter.SqlDataAdapter#2](~/../sqlclient/doc/samples/SqlDataAdapter_SqlDataAdapter.cs#2)]

O método `Add` da coleção `Parameters` adota o nome do parâmetro, o tipo de dados, o tamanho (se aplicável ao tipo) e o nome da <xref:System.Data.Common.DbParameter.SourceColumn%2A> da `DataTable`. Observe que <xref:System.Data.Common.DbParameter.SourceVersion%2A> do parâmetro `@CustomerID` é definido como `Original`. Isso garante que a linha existente na fonte de dados será atualizada se o valor da(s) coluna(s) de identificação tiverem sido alteradas na <xref:System.Data.DataRow> modificada. Nesse caso, o valor de linha `Original` corresponderia ao valor atual na fonte de dados, e o valor de linha `Current` conteria o valor atualizado. A `SourceVersion` do parâmetro `@CompanyName` não está definida e usa o padrão, o valor de linha `Current`.

> [!NOTE]
> Para ambas as operações `Fill` dos métodos `DataAdapter` e `Get` do `DataReader`, o tipo .NET é inferido do tipo retornado do Provedor de Dados Microsoft SqlClient para SQL Server. Os tipos .NET inferidos e os métodos acessadores para tipos de dados do Microsoft SQL Server são descritos nos [Mapeamentos do Tipo de Dados do ADO.NET](data-type-mappings-ado-net.md).

## <a name="parametersourcecolumn-parametersourceversion"></a>Parameter.SourceColumn, Parameter.SourceVersion

A `SourceColumn` e a `SourceVersion` podem ser passadas como argumentos para o construtor `Parameter` ou definidas como propriedades de um `Parameter` existente. A `SourceColumn` é o nome da <xref:System.Data.DataColumn> da <xref:System.Data.DataRow>, em que o valor do `Parameter` será recuperado. A `SourceVersion` especifica a versão da `DataRow` que o `DataAdapter` usa para recuperar o valor.

A tabela a seguir mostra os valores de enumeração <xref:System.Data.DataRowVersion> disponíveis para uso com a `SourceVersion`.

|Enumeração DataRowVersion|Descrição|  
|--------------------------------|-----------------|  
|`Current`|O parâmetro usa o valor atual da coluna. Este é o padrão.|  
|`Default`|O parâmetro usa o `DefaultValue` da coluna.|  
|`Original`|O parâmetro usa o valor original da coluna.|  
|`Proposed`|O parâmetro usa um valor proposto.|  

O exemplo de código `SqlClient` na seção a seguir define um parâmetro para um <xref:System.Data.Common.DbDataAdapter.UpdateCommand%2A> em que a coluna `CustomerID` é usada como `SourceColumn` de dois parâmetros: `@CustomerID` (`SET CustomerID = @CustomerID`) e `@OldCustomerID` (`WHERE CustomerID = @OldCustomerID`). O parâmetro `@CustomerID` é usado para atualizar a coluna **CustomerID** com o valor atual em `DataRow`. Como resultado, a `SourceColumn` `CustomerID` com uma `SourceVersion` de `Current` é usada. O parâmetro `@OldCustomerID` é usado para identificar a linha atual na fonte de dados. Como o valor de coluna correspondente é encontrado na versão `Original` da linha, a mesma `SourceColumn` (`CustomerID`) com uma `SourceVersion` de `Original` é usada.

## <a name="work-with-sqlclient-parameters"></a>Trabalhar com parâmetros do SqlClient

O exemplo a seguir demonstra como criar um <xref:Microsoft.Data.SqlClient.SqlDataAdapter> e definir <xref:System.Data.Common.DataAdapter.MissingSchemaAction%2A> para <xref:System.Data.MissingSchemaAction.AddWithKey> a fim de recuperar informações adicionais do esquema no banco de dados. O conjunto de propriedades <xref:Microsoft.Data.SqlClient.SqlDataAdapter.SelectCommand%2A>, <xref:Microsoft.Data.SqlClient.SqlDataAdapter.InsertCommand%2A>, <xref:Microsoft.Data.SqlClient.SqlDataAdapter.UpdateCommand%2A> e <xref:Microsoft.Data.SqlClient.SqlDataAdapter.DeleteCommand%2A> e os objetos <xref:Microsoft.Data.SqlClient.SqlParameter> correspondentes adicionados à coleção <xref:Microsoft.Data.SqlClient.SqlCommand.Parameters%2A>. O método retorna um objeto `SqlDataAdapter`.

[!code-csharp[Classic WebData SqlDataAdapter.SqlDataAdapter#1](~/../sqlclient/doc/samples/SqlDataAdapter_SqlDataAdapter.cs#1)]

## <a name="see-also"></a>Confira também

- [DataAdapters e DataReaders](dataadapters-datareaders.md)
- [Comandos e parâmetros](commands-parameters.md)
- [Atualizar fontes de dados com DataAdapters](update-data-sources-with-dataadapters.md)
- [Mapeamentos de tipo de dados no ADO.NET](data-type-mappings-ado-net.md)
- [Microsoft ADO.NET for SQL Server](microsoft-ado-net-sql-server.md)
