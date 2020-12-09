---
title: Conectar-se a fonte de dados
description: Saiba mais sobre os objetos Connection, usados para se conectar a fontes de dados no ADO.NET. O objeto Connection que você escolhe depende do tipo de fonte de dados.
ms.date: 11/13/2020
ms.assetid: 9abc3f92-1be3-4e1a-b360-762dc689650e
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-chmalh
ms.openlocfilehash: 26554deb5d8a3786efd1bd869a2692d368132531
ms.sourcegitcommit: debaff72dbfae91b303f0acd42dd6d99e03135a2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/01/2020
ms.locfileid: "96419807"
---
# <a name="connecting-to-a-data-source-in-adonet"></a>Conectar-se a uma fonte de dados no ADO.NET

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

No Provedor de Dados Microsoft SqlClient, você usa um objeto **Connection** para se conectar a uma fonte de dados específica fornecendo as informações de autenticação necessárias em uma cadeia de conexão. O objeto **Connection** que você usa depende do tipo de fonte de dados.

O Provedor de Dados Microsoft SqlClient para SQL Server inclui um tipo de <xref:Microsoft.Data.SqlClient.SqlConnection> que é derivado de uma classe <xref:System.Data.Common.DbConnection>.

## <a name="in-this-section"></a>Nesta seção  

[Estabelecer a conexão](establishing-connection.md)\
Descreve como usar um objeto **Connection** para estabelecer uma conexão com uma fonte de dados.

[Eventos de conexão](connection-events.md)\
Descreve como usar um evento **InfoMessage** para recuperar mensagens informativas de uma fonte de dados.

## <a name="see-also"></a>Confira também

- [Cadeias de conexão](connection-strings.md)
- [Pool de conexões](connection-pooling.md)
