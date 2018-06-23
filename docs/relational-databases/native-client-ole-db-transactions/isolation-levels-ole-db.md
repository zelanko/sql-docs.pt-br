---
title: Níveis de isolamento (OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- OLE DB, transactions
- isolation levels [OLE DB]
- transactions [OLE DB]
- SQL Server Native Client OLE DB provider, transactions
ms.assetid: d70ee72c-6e2a-4bcd-9456-4a697a866361
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: d1870c4f9f348c9d1b2ca52b94ee38a3e5d38190
ms.sourcegitcommit: a78fa85609a82e905de9db8b75d2e83257831ad9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2018
ms.locfileid: "35698067"
---
# <a name="isolation-levels-ole-db"></a>Níveis de isolamento (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Clientes do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] podem controlar os níveis de isolamento de transação para uma conexão. Para controlar o nível de isolamento da transação, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] consumidor do provedor de OLE DB Native Client usa:  
  
-   Propriedade DBPROP_SESS_AUTOCOMMITISOLEVELS do DBPROPSET_SESSION para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] modo de confirmação automática do Native Client OLE DB provider padrão.  
  
     O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] padrão do provedor OLE DB Native Client para o nível é DBPROPVAL_TI_READCOMMITTED.  
  
-   O *isoLevel* parâmetro o **itransactionlocal:: Starttransaction** método para transações de confirmação manual locais.  
  
-   O *isoLevel* parâmetro o **itransactiondispenser:: BeginTransaction** transações distribuídas do método de coordenada pelo MS DTC.  
  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] permite acesso de somente leitura ao nível de isolamento de leitura suja. Todos os outros níveis restringem a simultaneidade aplicando bloqueios a objetos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. À medida que o cliente exigir níveis de simultaneidade maiores, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] aplica restrições maiores ao acesso simultâneo aos dados. Para manter o nível mais alto de acesso simultâneo aos dados, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] consumidor do provedor OLE DB Native Client deve controlar suas solicitações para níveis de simultaneidade específicos de forma inteligente.  
  
> [!NOTE]  
>  O [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] introduziu o nível de isolamento do instantâneo. Para obter mais informações, consulte [trabalhando com isolamento de instantâneo](../../relational-databases/native-client/features/working-with-snapshot-isolation.md).  
  
## <a name="see-also"></a>Consulte também  
 [Transações](../../relational-databases/native-client-ole-db-transactions/transactions.md)  
  
  
