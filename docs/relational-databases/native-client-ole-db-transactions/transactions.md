---
title: Transações (provedor de OLE DB de cliente nativo)
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: b6f9f0f1e8cebdbfc8a586ee1192a820c141b790
ms.sourcegitcommit: df1f0f2dfb9452f16471e740273cd1478ff3100c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/29/2020
ms.locfileid: "87395740"
---
# <a name="transactions-in-sql-server-native-client"></a>Transações no SQL Server Native Client
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor de OLE DB de cliente nativo implementa o suporte a transações locais. O consumidor pode usar transações distribuídas ou coordenadas pelo Coordenador de Transações Distribuídas da Microsoft (MS DTC). Para consumidores que exigem controle de transação que abrange várias sessões, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor de OLE DB de cliente nativo pode unir transações iniciadas e mantidas pelo MS DTC.  
  
 Por padrão, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor de OLE DB de cliente nativo usa um modo de transação de confirmação automática, em que cada ação discreta em uma sessão de consumidor consiste em uma transação completa em relação a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] modo de confirmação automática do provedor de OLE DB de cliente nativo é local e as transações de confirmação automática nunca abrangem mais do que uma única sessão.  
  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor de OLE DB de cliente nativo expõe a interface **ITransactionLocal** , permitindo que o consumidor Use transações explícitas e implicitamente iniciadas em uma única conexão com uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor de OLE DB de cliente nativo não dá suporte a transações locais aninhadas.  
  
## <a name="in-this-section"></a>Nesta seção  
  
-   [Dando suporte a transações locais](../../relational-databases/native-client-ole-db-transactions/supporting-local-transactions.md)  
  
-   [Dando suporte a transações distribuídas](../../relational-databases/native-client-ole-db-transactions/supporting-distributed-transactions.md)  
  
-   [Níveis de isolamento &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-transactions/isolation-levels-ole-db.md)  
  
## <a name="see-also"></a>Consulte Também  
 [SQL Server Native Client &#40;OLE DB&#41;](../../relational-databases/native-client/ole-db/sql-server-native-client-ole-db.md)  
  
  
