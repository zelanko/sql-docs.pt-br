---
title: Pool de conexões
description: Saiba mais sobre pool de conexões, uma técnica de otimização que o ADO.NET usa para minimizar o custo da abertura de conexões com fontes de dados.
ms.date: 11/13/2020
ms.assetid: 955c057f-aea8-4ba8-aa6d-e3dfa18ba8d5
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-chmalh
ms.openlocfilehash: 41b139d2f22a9cb3137879d96224b02eafc24bab
ms.sourcegitcommit: c127c0752e84cccd38a7e23ac74c0362a40f952e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/07/2020
ms.locfileid: "96761494"
---
# <a name="connection-pooling"></a>Pool de conexões

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

A conexão a uma fonte de dados pode ser um processo demorado. Para minimizar o custo da abertura de conexões, o ADO.NET usa uma técnica de otimização chamada *pool de conexões*, que minimiza o custo de abrir e fechar conexões repetidamente.

## <a name="in-this-section"></a>Nesta seção  

[Pool de conexões do SQL Server (ADO.NET)](sql-server-connection-pooling.md)  
Fornece uma visão geral do pool de conexões e descreve como o pool funciona no SQL Server.

## <a name="see-also"></a>Confira também

- [Recuperando e modificando dados no ADO.NET](retrieving-modifying-data.md)
- [Microsoft ADO.NET for SQL Server](microsoft-ado-net-sql-server.md)
