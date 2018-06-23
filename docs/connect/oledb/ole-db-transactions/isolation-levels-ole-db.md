---
title: Níveis de isolamento (OLE DB) | Microsoft Docs
description: Níveis de isolamento (OLE DB)
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb|ole-db-transactions
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- OLE DB, transactions
- isolation levels [OLE DB]
- transactions [OLE DB]
- OLE DB Driver for SQL Server, transactions
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: b015a27fccfdad7b9f20bdac16a3a587f0c026a5
ms.sourcegitcommit: 03ba89937daeab08aa410eb03a52f1e0d212b44f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/16/2018
ms.locfileid: "35690009"
---
# <a name="isolation-levels-ole-db"></a>Níveis de isolamento (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-asdbmi-md](../../../includes/appliesto-ss-asdb-asdw-pdw-asdbmi-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Clientes do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] podem controlar os níveis de isolamento de transação para uma conexão. Para controlar o nível de isolamento da transação, o Driver OLE DB para o consumidor do SQL Server usa:  
  
-   Propriedade DBPROPSET_SESSION DBPROP_SESS_AUTOCOMMITISOLEVELS para o Driver OLE DB para o modo de confirmação automática padrão do SQL Server.  
  
     O Driver OLE DB para o padrão do SQL Server para o nível é DBPROPVAL_TI_READCOMMITTED.  
  
-   O *isoLevel* parâmetro o **itransactionlocal:: Starttransaction** método para transações de confirmação manual locais.  
  
-   O *isoLevel* parâmetro o **itransactiondispenser:: BeginTransaction** transações distribuídas do método de coordenada pelo MS DTC.  
  
 O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] permite acesso de somente leitura ao nível de isolamento de leitura suja. Todos os outros níveis restringem a simultaneidade aplicando bloqueios a objetos do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. À medida que o cliente exigir níveis de simultaneidade maiores, o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] aplica restrições maiores ao acesso simultâneo aos dados. Para manter o nível mais alto de acesso simultâneo aos dados, o Driver OLE DB para o consumidor do SQL Server inteligente deve controlar suas solicitações para níveis de simultaneidade específicos.  
  
> [!NOTE]  
>  O [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] introduziu o nível de isolamento do instantâneo. Para obter mais informações, consulte [trabalhando com isolamento de instantâneo](../../oledb/features/working-with-snapshot-isolation.md).  
  
## <a name="see-also"></a>Consulte também  
 [Transações](../../oledb/ole-db-transactions/transactions.md)  
  
  
