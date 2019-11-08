---
title: Transações | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
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
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d54dbe8e3df6e930ebd026e638d0a21f2f88f32e
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/07/2019
ms.locfileid: "73772561"
---
# <a name="transactions"></a>Transações
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  O provedor de OLE DB [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client implementa o suporte a transações locais. O consumidor pode usar transações distribuídas ou coordenadas pelo Coordenador de Transações Distribuídas da Microsoft (MS DTC). Para consumidores que precisam de controle de transação que abrange várias sessões, o provedor de OLE DB do cliente nativo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode unir transações iniciadas e mantidas pelo MS DTC.  
  
 Por padrão, o provedor de OLE DB [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nativo do cliente usa um modo de transação de confirmação automática, em que cada ação discreta em uma sessão de consumidor consiste em uma transação completa em uma instância de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O modo de confirmação automática do provedor de OLE DB do cliente nativo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é local e as transações de confirmação automática nunca abrangem mais do que uma única sessão.  
  
 O provedor de OLE DB [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client expõe a interface **ITransactionLocal** , permitindo que o consumidor Use transações de inicialização explícita e implícita em uma única conexão com uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O provedor de OLE DB de cliente nativo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não dá suporte a transações locais aninhadas.  
  
## <a name="in-this-section"></a>Nesta seção  
  
-   [Dando suporte a transações locais](../../relational-databases/native-client-ole-db-transactions/supporting-local-transactions.md)  
  
-   [Dando suporte a transações distribuídas](../../relational-databases/native-client-ole-db-transactions/supporting-distributed-transactions.md)  
  
-   [Níveis &#40;de isolamento OLE DB&#41;](../../relational-databases/native-client-ole-db-transactions/isolation-levels-ole-db.md)  
  
## <a name="see-also"></a>Consulte também  
 [SQL Server Native Client &#40;OLE DB&#41;](../../relational-databases/native-client/ole-db/sql-server-native-client-ole-db.md)  
  
  
