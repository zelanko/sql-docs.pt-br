---
title: Paginação por meio de um resultado de consulta
description: Fornece um exemplo de como exibir os resultados de uma consulta como páginas de dados.
ms.date: 11/30/2020
dev_langs:
- csharp
ms.assetid: fa360c46-e5f8-411e-a711-46997771133d
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-chmalh
ms.openlocfilehash: 2de305e1069964f2d1a67b7f201578c7448d3e09
ms.sourcegitcommit: c127c0752e84cccd38a7e23ac74c0362a40f952e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/07/2020
ms.locfileid: "96772154"
---
# <a name="paging-through-a-query-result"></a>Paginação por meio de um resultado de consulta

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

A paginação por meio de um resultado de consulta é o processo de retornar os resultados de uma consulta em subconjuntos menores de dados ou páginas. Essa é uma prática comum a fim de exibir os resultados para um usuário em partes pequenas e fáceis de gerenciar.

<xref:Microsoft.Data.SqlClient.SqlDataAdapter> fornece um recurso que permite retornar apenas uma página de dados, por meio de sobrecargas do método <xref:System.Data.Common.DbDataAdapter.Fill%2A>. No entanto, essa pode não ser a melhor opção para paginar grandes resultados de consulta porque, embora o **DataAdapter** preencha o <xref:System.Data.DataTable> de destino ou o <xref:System.Data.DataSet> apenas com os registros solicitados, ainda serão usados os recursos para retornar a consulta inteira.

Para retornar uma página de dados de uma fonte de dados sem usar os recursos para retornar a consulta inteira, especifique critérios adicionais na consulta que reduzam as linhas retornadas para apenas aquelas necessárias.

Para usar o método <xref:System.Data.Common.DbDataAdapter.Fill%2A> a fim de retornar uma página de dados, especifique um parâmetro **startRecord** (que corresponderá ao primeiro registro da página de dados) e um parâmetro **maxRecords** (que corresponderá ao número de registros na página de dados).

## <a name="example"></a>Exemplo

O exemplo de código a seguir mostra como usar o método <xref:System.Data.Common.DbDataAdapter.Fill%2A> para retornar a primeira página de um resultado de consulta cujo tamanho da página corresponde a cinco registros.

[!code-csharp[SqlDataAdapter_Paging#1](~/../sqlclient/doc/samples/SqlDataAdapter_Paging.cs#1)]

No exemplo anterior, o **DataSet** é preenchido apenas com cinco registros, mas a tabela **Orders** inteira é retornada. Para preencher o **DataSet** com aqueles mesmos cinco registros, mas retornando apenas eles, use as cláusulas `TOP` e `WHERE` na instrução SQL, como mostrado no exemplo de código a seguir.

[!code-csharp[SqlDataAdapter_Paging#2](~/../sqlclient/doc/samples/SqlDataAdapter_Paging.cs#2)]

> [!NOTE]
> Ao paginar os resultados da consulta dessa forma, você deve preservar o `unique identifier` que ordena as linhas, a fim de passar a ID exclusiva para o comando e retornar a próxima página de registros, conforme mostrado no exemplo de código a seguir.

[!code-csharp[SqlDataAdapter_Paging#4](~/../sqlclient/doc/samples/SqlDataAdapter_Paging.cs#4)]

Para retornar o `next page of records` usando a sobrecarga do método **Fill** que usa os parâmetros **startRecord** e **maxRecords**, incremente o índice de registro atual com o tamanho da página e preencha a tabela.

> [!NOTE]
> Lembre-se de que o servidor de banco de dados retorna todos os resultados da consulta, muito embora apenas uma página de registros seja adicionada ao **DataSet**.

No exemplo de código a seguir, as linhas da tabela são limpas antes de serem preenchidas com a próxima página de dados. Talvez você queira preservar um determinado número de linhas retornadas em um cache local a fim de reduzir os acessos ao servidor de banco de dados.

[!code-csharp[SqlDataAdapter_Paging#3](~/../sqlclient/doc/samples/SqlDataAdapter_Paging.cs#3)]

Para retornar a próxima página de registros sem que o servidor de banco de dados precise retornar a consulta inteira, especifique critérios restritivos na instrução SELECT. Como o exemplo anterior preservava o último registro retornado, você pode usá-lo na cláusula WHERE a fim de especificar um ponto de partida para a consulta, conforme mostrado no exemplo de código a seguir.

[!code-csharp[SqlDataAdapter_Paging#5](~/../sqlclient/doc/samples/SqlDataAdapter_Paging.cs#5)]

## <a name="see-also"></a>Confira também

- [DataAdapters e DataReaders](dataadapters-datareaders.md)
- [Microsoft ADO.NET for SQL Server](microsoft-ado-net-sql-server.md)
