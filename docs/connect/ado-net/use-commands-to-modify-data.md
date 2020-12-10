---
title: Usar comandos para modificar dados
description: Descreve como usar um provedor de dados para executar procedimentos armazenados ou instruções DDL (linguagem de definição de dados).
ms.date: 11/25/2020
ms.assetid: f4160389-b9ff-4b74-b655-437c76dcd586
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-chmalh
ms.openlocfilehash: 98127e41b5b07c38030ef27214c9c92bf7c4b4be
ms.sourcegitcommit: c127c0752e84cccd38a7e23ac74c0362a40f952e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/07/2020
ms.locfileid: "96761474"
---
# <a name="using-commands-to-modify-data"></a>Usar comandos para modificar dados

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

Com o Provedor de Dados do Microsoft SqlClient para SQL Server, você pode executar procedimentos armazenados ou instruções de linguagem de definição de dados (por exemplo, CREATE TABLE e ALTER COLUMN) para executar manipulação de esquema em um banco de dados ou catálogo. Esses comandos não retornam linhas como uma consulta e, portanto, o objeto <xref:Microsoft.Data.SqlClient.SqlCommand> fornece um <xref:Microsoft.Data.SqlClient.SqlCommand.ExecuteNonQuery%2A> para processá-los.

Além de usar **ExecuteNonQuery** para modificar o esquema, você também pode usar esse método para processar instruções SQL que modificam dados, mas que não retornam linhas, como INSERT, UPDATE e DELETE.

Embora as linhas não sejam retornadas pelo método **ExecuteNonQuery**, os parâmetros de entrada e saída e os valores de retorno podem ser passados e retornados por meio da coleção de **Parâmetros** do objeto **Command**.

## <a name="in-this-section"></a>Nesta seção

[Atualizar dados em uma fonte de dados](update-data-inside-data-source.md)  
Descreve como executar comandos ou procedimentos armazenados que modificam dados em um banco de dados.

[Executar de operações de catálogo](perform-catalog-operations.md)  
Descreve como executar comandos que modificam o esquema de banco de dados.

## <a name="see-also"></a>Confira também

- [Recuperar e modificar dados no ADO.NET](retrieving-modifying-data.md)
- [Comandos e parâmetros](commands-parameters.md)
- [Microsoft ADO.NET for SQL Server](microsoft-ado-net-sql-server.md)
