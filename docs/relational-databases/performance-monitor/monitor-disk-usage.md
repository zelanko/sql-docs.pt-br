---
title: "Monitorar o uso do disco | Microsoft Docs"
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
  - "monitoramento do banco de dados [SQL Server], uso do disco"
  - "discos [SQL Server]"
  - "monitorando o desempenho [SQL Server], uso do disco"
  - "desempenho do sistema [SQL Server], uso do disco"
  - "monitoramento [SQL Server], atividade do disco"
  - "paginação excessiva [SQL Server]"
  - "ajustando bancos de dados [SQL Server], uso do disco"
  - "E/S [SQL Server], monitorando"
  - "discos [SQL Server], monitorando a atividade"
  - "isolando atividade de disco [o SQL Server]"
  - "desempenho do banco de dados [SQL Server], uso do disco"
  - "monitorando o desempenho do servidor [SQL Server], uso do disco"
ms.assetid: 1525449c-ea7d-4222-b294-1ba1fe99c9ac
caps.latest.revision: 23
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 23
---
# Monitorar o uso do disco
  O Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa chamadas de E/S (entrada/saída) do sistema operacional Microsoft Windows para executar operações de leitura e gravação no seu disco. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gerencia quando e como a E/S de disco é executada, mas o sistema operacional Windows executa as operações de E/S subjacentes. O subsistema de E/S compreende o barramento do sistema, as placas do controlador de disco, os discos, as unidades de fita, a unidade de CD-ROM e vários outros dispositivos de E/S. E/S no disco é, muitas vezes, a causa de afunilamentos em um sistema.  
  
 Monitorar a atividade de disco envolve duas áreas de foco:  
  
-   Monitorar E/S no disco e detectar paginação excessiva  
  
-   Isolar a atividade de disco criada pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
 Para obter mais informações, consulte [Monitorando o uso do disco](http://social.technet.microsoft.com/wiki/contents/articles/monitoring-disk-usage.aspx)  
  
  