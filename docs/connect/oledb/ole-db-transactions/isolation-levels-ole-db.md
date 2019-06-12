---
title: Níveis de isolamento (OLE DB) | Microsoft Docs
description: Níveis de isolamento (OLE DB)
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
author: pmasl
ms.author: pelopes
manager: jroth
ms.openlocfilehash: 0a7e06fe0888767d653f40148efb324f89456460
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66766215"
---
# <a name="isolation-levels-ole-db"></a>Níveis de isolamento (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Clientes do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] podem controlar os níveis de isolamento de transação para uma conexão. Para controlar o nível de isolamento da transação, o Driver OLE DB para o consumidor do SQL Server usa:  
  
-   A propriedade DBPROP_SESS_AUTOCOMMITISOLEVELS de DBPROPSET_SESSION para o modo de confirmação automática padrão do OLE DB Driver for SQL Server.  
  
     O Driver OLE DB para o padrão do SQL Server para o nível é DBPROPVAL_TI_READCOMMITTED.  
  
-   O parâmetro *isoLevel* do método **ITransactionLocal::StartTransaction** para transações de confirmação manual locais.  
  
-   O parâmetro *isoLevel* do método **ITransactionDispenser::BeginTransaction** para transações distribuídas coordenadas do MS DTC.  
  
 O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] permite acesso de somente leitura ao nível de isolamento de leitura suja. Todos os outros níveis restringem a simultaneidade aplicando bloqueios a objetos do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. À medida que o cliente exigir níveis de simultaneidade maiores, o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] aplica restrições maiores ao acesso simultâneo aos dados. Para manter o nível mais alto de acesso simultâneo aos dados, o consumidor do OLE DB Driver for SQL Server deve controlar suas solicitações de forma inteligente para níveis de simultaneidade específicos.  
  
> [!NOTE]  
>  O [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] introduziu o nível de isolamento do instantâneo. Para obter mais informações, confira [Trabalhando com o isolamento de instantâneos](../../oledb/features/working-with-snapshot-isolation.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Transactions](../../oledb/ole-db-transactions/transactions.md)  
  
  
