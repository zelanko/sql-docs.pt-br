---
title: Níveis de isolamento (Driver do OLE DB) | Microsoft Docs
description: Saiba como um consumidor do Driver do OLE DB para SQL Server pode controlar o nível de isolamento de transação para uma conexão.
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- OLE DB, transactions
- isolation levels [OLE DB]
- transactions [OLE DB]
- OLE DB Driver for SQL Server, transactions
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 87b3a348a7219eda5868223b167b2ecf851c2079
ms.sourcegitcommit: c95f3ef5734dec753de09e07752a5d15884125e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/25/2020
ms.locfileid: "88861879"
---
# <a name="isolation-levels-ole-db"></a>Níveis de isolamento (OLE DB)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Clientes do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] podem controlar os níveis de isolamento de transação para uma conexão. Para controlar o nível de isolamento de transação, o consumidor do Driver do OLE DB para SQL Server usa:  
  
-   A propriedade DBPROP_SESS_AUTOCOMMITISOLEVELS de DBPROPSET_SESSION para o modo de confirmação automática padrão do OLE DB Driver for SQL Server.  
  
     O padrão do Driver do OLE DB para SQL Server para o nível é DBPROPVAL_TI_READCOMMITTED.  
  
-   O parâmetro *isoLevel* do método **ITransactionLocal::StartTransaction** para transações de confirmação manual locais.  
  
-   O parâmetro *isoLevel* do método **ITransactionDispenser::BeginTransaction** para transações distribuídas coordenadas do MS DTC.  
  
 O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] permite acesso de somente leitura ao nível de isolamento de leitura suja. Todos os outros níveis restringem a simultaneidade aplicando bloqueios a objetos do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. À medida que o cliente exigir níveis de simultaneidade maiores, o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] aplica restrições maiores ao acesso simultâneo aos dados. Para manter o nível mais alto de acesso simultâneo aos dados, o consumidor do OLE DB Driver for SQL Server deve controlar suas solicitações de forma inteligente para níveis de simultaneidade específicos.  
  
> [!NOTE]  
>  O [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] introduziu o nível de isolamento do instantâneo. Para obter mais informações, confira [Trabalhando com o isolamento de instantâneos](../../oledb/features/working-with-snapshot-isolation.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Transações](../../oledb/ole-db-transactions/transactions.md)  
  
  
