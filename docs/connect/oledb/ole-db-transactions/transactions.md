---
title: Transações | Microsoft Docs
description: Transações no Driver do OLE DB para SQL Server
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db-transactions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- OLE DB, transactions
- transactions [OLE DB]
- OLE DB Driver for SQL Server, transactions
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: dd2978ab1778467561c4fab9f246922fb4dfdea2
ms.sourcegitcommit: 9f4330a4b067deea396b8567747a6771f35e6eee
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2018
---
# <a name="transactions"></a>Transactions
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  O Driver OLE DB para SQL Server implementa o suporte de transação local. O consumidor pode usar transações distribuídas ou coordenadas pelo Coordenador de Transações Distribuídas da Microsoft (MS DTC). Para os consumidores que exigem o controle de transação que abrange várias sessões, o Driver OLE DB para SQL Server pode unir transações iniciadas e mantidas pelo MS DTC.  
  
 Por padrão, o Driver OLE DB para SQL Server usa um modo de transação de confirmação automática, onde cada ação discreta na sessão de um consumidor compreende uma transação completa em uma instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. O Driver OLE DB para o modo de confirmação automática do SQL Server é local e transações de confirmação automática nunca englobam mais que uma única sessão.  
  
 O Driver OLE DB para SQL Server expõe o **ITransactionLocal** interface, permitindo que o consumidor usar explicitamente e implicitamente iniciar transações em uma única conexão a uma instância de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. O Driver OLE DB para SQL Server não oferece suporte a transações locais aninhadas.  
  
## <a name="in-this-section"></a>Nesta seção  
  
-   [Dando suporte a transações locais](../../oledb/ole-db-transactions/supporting-local-transactions.md)  
  
-   [Dando suporte a transações distribuídas](../../oledb/ole-db-transactions/supporting-distributed-transactions.md)  
  
-   [Níveis de isolamento &#40;OLE DB&#41;](../../oledb/ole-db-transactions/isolation-levels-ole-db.md)  
  
## <a name="see-also"></a>Consulte também  
 [Driver do OLE DB para SQL Server &#40;OLE DB&#41;](../../oledb/ole-db/oledb-driver-for-sql-server-ole-db.md)  
  
  
