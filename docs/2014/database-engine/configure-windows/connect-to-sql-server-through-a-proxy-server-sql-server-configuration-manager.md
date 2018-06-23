---
title: Conecte-se ao SQL Server por meio de um servidor Proxy (SQL Server Configuration Manager) | Microsoft Docs
ms.custom: ''
ms.date: 06/22/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Remote WinSock
- RWS
- LATs
- proxy servers [SQL Server]
- connections [SQL Server], proxy server
- Microsoft Proxy Server [SQL Server]
- local address tables [SQL Server]
ms.assetid: 39714de0-2a1f-4179-9091-5c3fa4612545
caps.latest.revision: 20
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 1eb07c9e7b17caa4498ab8ddbc70388ae8a8cebc
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36122905"
---
# <a name="connect-to-sql-server-through-a-proxy-server-sql-server-configuration-manager"></a>Conectar-se ao SQL Server com um servidor proxy (SQL Server Configuration Manager)
  Este tópico descreve como conectar-se ao SQL Server por meio de um servidor proxy no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o SQL Server Configuration Manager. Para escutar Remote WinSock (RWS) remotamente, defina a tabela de endereço local (LAT) para o servidor proxy, para que o endereço do nó de escuta fique fora do intervalo de entradas de LAT.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Configuration Manager  
  
#### <a name="to-enable-connections-to-sql-server-through-microsoft-proxy-server"></a>Habilitar conexões com o SQL Server usando o Microsoft Proxy Server  
  
1.  Siga as etapas em [Configurar um servidor para escutar em uma porta TCP específica &#40;SQL Server Configuration Manager&#41;](configure-a-server-to-listen-on-a-specific-tcp-port.md) para determinar quais portas TCP/IP são usadas pelo [!INCLUDE[ssDE](../../includes/ssde-md.md)] ou para configurar o [!INCLUDE[ssDE](../../includes/ssde-md.md)] para usar uma porta desejada.  
  
2.  No servidor proxy, defina a tabela de endereço local (LAT) para o servidor proxy, para que o endereço do nó de escuta fique fora do intervalo de entradas de LAT. Para obter mais informações, consulte a documentação do servidor proxy.  
  
  