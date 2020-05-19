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
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 1cdf0cbca45fc12dc5e61e4dca913d2e16af5ab5
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82704470"
---
# <a name="transactions"></a>Transactions
  O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor de OLE DB de cliente nativo implementa o suporte a transações locais. O consumidor pode usar transações distribuídas ou coordenadas pelo Coordenador de Transações Distribuídas da Microsoft (MS DTC). Para consumidores que exigem controle de transação que abrange várias sessões, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor de OLE DB de cliente nativo pode unir transações iniciadas e mantidas pelo MS DTC.  
  
 Por padrão, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor de OLE DB de cliente nativo usa um modo de transação de confirmação automática, em que cada ação discreta em uma sessão de consumidor consiste em uma transação completa em relação a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] modo de confirmação automática do provedor de OLE DB de cliente nativo é local e as transações de confirmação automática nunca abrangem mais do que uma única sessão.  
  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor de OLE DB de cliente nativo expõe a interface **ITransactionLocal** , permitindo que o consumidor Use transações explícitas e implicitamente iniciadas em uma única conexão com uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor de OLE DB de cliente nativo não dá suporte a transações locais aninhadas.  
  
## <a name="in-this-section"></a>Nesta seção  
  
-   [Dando suporte a transações locais](supporting-local-transactions.md)  
  
-   [Dando suporte a transações distribuídas](supporting-distributed-transactions.md)  
  
-   [Níveis de isolamento &#40;OLE DB&#41;](isolation-levels-ole-db.md)  
  
## <a name="see-also"></a>Consulte Também  
 [SQL Server Native Client &#40;OLE DB&#41;](../native-client/ole-db/sql-server-native-client-ole-db.md)  
  
  
