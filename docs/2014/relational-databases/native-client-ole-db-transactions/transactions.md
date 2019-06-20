---
title: Transações | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- OLE DB, transactions
- transactions [OLE DB]
- SQL Server Native Client OLE DB provider, transactions
ms.assetid: 3b41e33a-c1ca-4b2a-9464-312b0ed3ca89
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: dca9b7a3289390b1d1e20e1b0d18c23b44b87617
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63213899"
---
# <a name="transactions"></a>Transações
  O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor OLE DB do Native Client implementa o suporte de transação local. O consumidor pode usar transações distribuídas ou coordenadas pelo Coordenador de Transações Distribuídas da Microsoft (MS DTC). Para os consumidores que necessitam de controle de transações que englobe várias sessões, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor OLE DB do Native Client pode unir transações iniciadas e mantidas pelo MS DTC.  
  
 Por padrão, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor do OLE DB do Native Client usa um modo de transação de confirmação automática, onde cada ação discreta na sessão de um consumidor consiste em uma transação completa em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] modo de confirmação automática do provedor OLE DB do Native Client é local, e transações de confirmação automática nunca englobam mais que uma única sessão.  
  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor do OLE DB do Native Client expõe a **ITransactionLocal** interface, permitindo que o consumidor use explicitamente e implicitamente iniciar transações em uma única conexão a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor de OLE DB do Native Client não oferece suporte a transações locais aninhadas.  
  
## <a name="in-this-section"></a>Nesta seção  
  
-   [Dando suporte a transações locais](supporting-local-transactions.md)  
  
-   [Dando suporte a transações distribuídas](supporting-distributed-transactions.md)  
  
-   [Níveis de isolamento &#40;OLE DB&#41;](isolation-levels-ole-db.md)  
  
## <a name="see-also"></a>Consulte também  
 [SQL Server Native Client &#40;OLE DB&#41;](../native-client/ole-db/sql-server-native-client-ole-db.md)  
  
  
