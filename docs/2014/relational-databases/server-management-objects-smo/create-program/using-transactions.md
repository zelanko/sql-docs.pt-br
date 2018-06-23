---
title: Usando transações | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server Management Objects, transactions
- transactions [SMO]
- SMO [SQL Server], transactions
ms.assetid: 399aded8-bee3-4cfb-a671-1877c7d0de9f
caps.latest.revision: 36
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 2c132ac199fb6af9e0349c463d5b30954acbf8bd
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36118614"
---
# <a name="using-transactions"></a>Usando transações
  No SMO ([!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Management Objects), o processamento de transações é feito por meio da conexão com a instância de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] usando o objeto <xref:Microsoft.SqlServer.Management.Common.ServerConnection>. O <xref:Microsoft.SqlServer.Management.Common.ServerConnection> o objeto é referenciado pelo <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> propriedade o <xref:Microsoft.SqlServer.Management.Smo.Server> objeto quando a conexão é estabelecida. Métodos como <xref:Microsoft.SqlServer.Management.Common.DataTransferProgressEventType.StartTransaction>, <xref:Microsoft.SqlServer.Management.Common.ServerConnection.RollBackTransaction%2A>e <xref:Microsoft.SqlServer.Management.Common.ServerConnection.CommitTransaction%2A> pertencem à propriedade de objeto <xref:Microsoft.SqlServer.Management.Smo.Server.ConnectionContext%2A>.  
  
## <a name="see-also"></a>Consulte também  
 [Criando programas SMO](creating-smo-programs.md)  
  
  