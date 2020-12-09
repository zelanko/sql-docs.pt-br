---
title: Executar de operações de catálogo
description: Descreve como executar comandos que modificam o esquema de banco de dados.
ms.date: 11/25/2020
dev_langs:
- csharp
ms.assetid: e60f542f-6271-495b-a9e4-48553481c2a3
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-chmalh
ms.openlocfilehash: 85e68bd77b11fd70e4071d7ae67ebf26c643b540
ms.sourcegitcommit: debaff72dbfae91b303f0acd42dd6d99e03135a2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/01/2020
ms.locfileid: "96428170"
---
# <a name="performing-catalog-operations"></a>Executar de operações de catálogo

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

Para executar um comando a fim de modificar um banco de dados ou catálogo, como a instrução CREATE TABLE ou CREATE PROCEDURE, crie um objeto **Command** usando as instruções SQL apropriadas e um objeto **Connection**. Execute o comando com o método <xref:Microsoft.Data.SqlClient.SqlCommand.ExecuteNonQuery%2A> do objeto <xref:Microsoft.Data.SqlClient.SqlCommand>.

## <a name="example"></a>Exemplo

O exemplo de código a seguir cria um procedimento armazenado em um banco de dados do Microsoft SQL Server.

[!code-csharp[DataWorks SqlCommand.ExecuteNonQuery#3](~/../sqlclient/doc/samples/SqlCommand_ExecuteNonQuery_SP_DML.cs#3)]

## <a name="see-also"></a>Confira também

- [Usar comandos para modificar dados](use-commands-to-modify-data.md)
- [Comandos e parâmetros](commands-parameters.md)
