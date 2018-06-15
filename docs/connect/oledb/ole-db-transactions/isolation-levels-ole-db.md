---
title: Níveis de isolamento (OLE DB) | Microsoft Docs
description: Níveis de isolamento (OLE DB)
ms.custom: ''
ms.date: 03/26/2018
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
- OLE DB Driver for SQL Server, transactions
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 0774a7743cc9993b05f1470be31faf482147d282
ms.sourcegitcommit: f16003fd1ca28b5e06d5700e730f681720006816
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35306765"
---
# <a name="isolation-levels-ole-db"></a>Níveis de isolamento (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

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
  
  
