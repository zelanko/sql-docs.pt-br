---
title: Recuperar dados por um DataReader
description: Saiba como recuperar dados usando um DataReader no ADO.NET com este exemplo de código. O DataReader fornece um fluxo de dados sem buffer.
ms.date: 11/30/2020
dev_langs:
- csharp
ms.assetid: 97afc121-fb8b-465b-bab3-6d844420badb
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-chmalh
ms.openlocfilehash: e7a618ef92a9f4a4cc969112886a4246ad25adc6
ms.sourcegitcommit: 866554663ca3191748b6e4eb4d8d82fa58c4e426
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/16/2020
ms.locfileid: "97559198"
---
# <a name="retrieve-data-by-a-datareader"></a>Recuperar dados por um DataReader

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

Para recuperar dados usando um **DataReader**, crie uma instância do objeto **Command** e, em seguida, crie um **DataReader** chamando **Command.ExecuteReader** a fim de recuperar linhas de uma fonte de dados. O **DataReader** fornece um fluxo de dados não armazenado em buffer que permite que a lógica procedural processe resultados com eficiência por meio de uma fonte de dados em sequência.

> [!NOTE]
> O **DataReader** é uma boa opção ao recuperar grandes quantidades de dados porque os dados não são armazenados em cache na memória.

O exemplo a seguir ilustra o uso de um **DataReader**, em que `reader` representa um DataReader válido e `command` representa um objeto Command válido.  

```csharp
reader = command.ExecuteReader();  
```

Use o método **DataReader.Read** para obter uma linha dos resultados da consulta. É possível acessar cada coluna da linha retornada passando o nome ou o número ordinal da coluna para o **DataReader**. No entanto, para oferecer o melhor desempenho, o **DataReader** fornece uma série de métodos que permitem que você acesse valores de coluna nos tipos de dados nativos delas (**GetDateTime**, **GetDouble**, **GetGuid**, **GetInt32** e assim por diante). Para obter uma lista dos métodos acessadores tipados para **DataReaders** específicos de provedor de dados, confira <xref:Microsoft.Data.SqlClient.SqlDataReader>. Usar os métodos acessadores tipados quando você já conhece o tipo de dados subjacente, reduz a quantidade de conversão de tipos necessária ao recuperar o valor da coluna.  

O exemplo a seguir faz a iteração por meio de um objeto **DataReader** e retorna duas colunas de cada linha.  

[!code-csharp[DataWorks SqlClient.HasRows#1](~/../sqlclient/doc/samples/SqlDataReader_HasRows.cs#1)]

## <a name="closing-the-datareader"></a>Fechando o DataReader  

Sempre chame o método **Close** quando terminar de usar o objeto **DataReader**.

> [!NOTE]
> Se o **Command** contiver parâmetros de saída ou valores de retorno, esses valores não serão disponibilizados até que o **DataReader** seja fechado.  

> [!IMPORTANT]
> Enquanto um **DataReader** estiver aberto, a **Connection** estará sendo usada exclusivamente por esse **DataReader**. Você não poderá executar nenhum comando usando a **Connection**, incluindo criar um outro **DataReader**, até o **DataReader** original esteja fechado.  

> [!NOTE]
> Não chame **Close** nem **Dispose** em um **Connection**, um **DataReader** ou qualquer outro objeto gerenciado no método **Finalize** da classe. Em um finalizador, libere somente recursos não gerenciados que sua classe possui diretamente. Se a classe não tiver nenhum recurso não gerenciado, não inclua um método **Finalize** na definição de classe. Para obter mais informações, confira [Coleta de lixo](/dotnet/standard/garbage-collection/index).
 
## <a name="retrieve-multiple-result-sets-using-nextresult"></a>Recuperar vários conjuntos de resultados usando o NextResult

Se o **DataReader** retornar vários conjuntos de resultados, chame o método **NextResult** para percorrer os conjuntos de resultados em sequência. O exemplo a seguir mostra <xref:Microsoft.Data.SqlClient.SqlDataReader> processando os resultados de duas instruções SELECT usando o método <xref:Microsoft.Data.SqlClient.SqlCommand.ExecuteReader%2A>.  

[!code-csharp[DataWorks SqlClient.NextResult#1](~/../sqlclient/doc/samples/SqlDataReader_NextResult.cs#1)]

## <a name="get-schema-information-from-the-datareader"></a>Obtendo informações de esquema por meio do DataReader  

Enquanto o **DataReader** estiver aberto, você poderá recuperar informações de esquema sobre o conjunto de resultados atual usando o método **GetSchemaTable**. O **GetSchemaTable** retorna um objeto <xref:System.Data.DataTable> preenchido com linhas e colunas que contêm informações de esquema do conjunto de resultados atual. O **DataTable** contém uma linha para cada coluna do conjunto de resultados. Cada coluna da tabela do esquema é mapeada para uma propriedade da coluna retornada nas linhas do conjunto de resultados, onde **ColumnName** é o nome da propriedade e o valor da coluna é o valor da propriedade. O exemplo a seguir gravará as informações de esquema para o **DataReader**.  

[!code-csharp[DataWorks SqlClient.GetSchemaTable#1](~/../sqlclient/doc/samples/SqlDataReader_GetSchemaTable.cs#1)]

## <a name="see-also"></a>Confira também

- [DataAdapters e DataReaders](dataadapters-datareaders.md)
- [Comandos e parâmetros](commands-parameters.md)
- [Microsoft ADO.NET for SQL Server](microsoft-ado-net-sql-server.md)
