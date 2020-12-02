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
ms.openlocfilehash: ab6edc2a7090de85e970445cdb2b86d6ed5cb8f2
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96126341"
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
