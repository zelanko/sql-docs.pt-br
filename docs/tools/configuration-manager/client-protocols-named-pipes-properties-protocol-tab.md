---
title: "Protocolos de Cliente – Propriedades de Pipes Nomeados (guia Protocolo) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "pipes [SQL Server], conectando-se a"
  - "Pipes nomeados [SQL Server], pipe padrão"
  - "protocolos de cliente [SQL Server]"
ms.assetid: 30fbae62-2f2e-4d36-9c6e-3444fff68781
caps.latest.revision: 23
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 23
---
# Protocolos de Cliente – Propriedades de Pipes Nomeados (guia Protocolo)
  No [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager, use a guia **Protocolo** na caixa de diálogo **Propriedades de Pipes Nomeados** para exibir ou modificar a descrição do pipe padrão. Para se conectar a um pipe diferente, digite o pipe na caixa **Pipe Padrão** . Para obter mais informações sobre cadeias de conexão, consulte [Creating a Valid Connection String Using Named Pipes](../Topic/Creating%20a%20Valid%20Connection%20String%20Using%20Named%20Pipes.md).  
  
## Opções  
 **Pipe Padrão**  
 Especifica o pipe padrão que a biblioteca de rede Pipes Nomeados usará para tentar se conectar à instância de destino do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Por padrão, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] escuta em: `\\.\pipe\sql\query`  
  
 Para se conectar ao pipe padrão, digite `sql\query`  
  
 **Ativado**  
 Os valores possíveis são **Sim** e **Não**.  
  
## Consulte também  
 [Escolhendo um protocolo de rede](../Topic/Choosing%20a%20Network%20Protocol.md)  
  
  