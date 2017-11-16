---
title: Contadores de desempenho de XTP do SQL Server (OLTP in-memory) | Microsoft Docs
ms.custom: 
ms.date: 04/06/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: fe3cbaf4-65f4-44c5-acc6-7b735cda0c5d
caps.latest.revision: "17"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 0aeab35f0f8814aa3bd9d7dc51821017cf67d966
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="sql-server-xtp-in-memory-oltp-performance-counters"></a>Contadores de desempenho de XTP (OLTP na memória) do SQL Server
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornece objetos e contadores que podem ser usados pelo Monitor de Desempenho para monitorar a atividade OLTP in-memory. Os objetos e contadores são compartilhados entre todas as instâncias de determinada versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no computador, a partir do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)].  
  
 No passado, os nomes de objeto e de contador começavam com *XTP*, como em **Cursores XTP**. Agora, a partir do [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], os nomes são parecidos com o seguinte padrão:  
  
-   **SQL Server** *\<versão>* **Cursores XTP**  
  
 Para *\<version>* o valor é algo como 2016.  
  
##  <a name="SQLServerPOs"></a> Objetos de desempenho XTP do SQL Server  
 A tabela a seguir descreve os objetos de desempenho do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
|Objeto de desempenho|Descrição|  
|------------------------|-----------------|  
|[Cursores de XTP do SQL Server](../../relational-databases/performance-monitor/sql-server-xtp-cursors.md)|O objeto de desempenho Cursores de XTP do SQL Server contém os contadores relacionados aos cursores do mecanismo de XTP interno OLTP in-memory. Os cursores são os blocos de construção de baixo nível que o mecanismo OLTP In-Memory usa para processar consultas [!INCLUDE[tsql](../../includes/tsql-md.md)] . Como tal, você normalmente não tem controle direto sobre eles.|  
|[Bancos de dados XTP do SQL Server](../../relational-databases/performance-monitor/sql-server-xtp-databases.md)|O objeto de desempenho Bancos de dados XTP do SQL Server fornece contadores específicos do banco de dados OLTP in-memory.|  
|[Coleta de Lixo de XTP do SQL Server](../../relational-databases/performance-monitor/sql-server-xtp-garbage-collection.md)|O objeto de desempenho Coleta de Lixo de XTP do SQL Server contém os contadores relacionados ao coletor de lixo do mecanismo OLTP in-memory.|  
|[Administrador de E/S XTP do SQL Server 2016](../../relational-databases/performance-monitor/sql-server-xtp-io-governor.md)|O objeto de desempenho Administrador de E/S XTP do SQL Server contém contadores relacionados ao Administrador da Taxa de E/S do OLTP in-memory.|
|[Processador Fantasma de XTP do SQL Server](../../relational-databases/performance-monitor/sql-server-xtp-phantom-processor.md)|O objeto de desempenho Processador Fantasma de XTP do SQL Server contém os contadores relacionados ao subsistema de processamento fantasma do mecanismo OLTP in-memory. Esse componente é responsável por detectar as linhas fantasmas nas transações que são executadas no nível de isolamento SERIALIZABLE.|  
|[Armazenamento XTP do SQL Server](../../relational-databases/performance-monitor/sql-server-xtp-storage.md)|O objeto de desempenho Armazenamento XTP do SQL Server contém contadores relacionados ao armazenamento OLTP in-memory do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|[Log de transações XTP do SQL Server](../../relational-databases/performance-monitor/sql-server-xtp-transaction-log.md)|O objeto de desempenho do Log de Transações XTP do SQL Server contém contadores relacionados ao log de transações do OLTP in-memory no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|[Transações XTP do SQL Server](../../relational-databases/performance-monitor/sql-server-xtp-transactions.md)|O objeto de desempenho do Log Transações XTP do SQL Server contém contadores relacionados às transações do mecanismo do OLTP in-memory no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
  
  
