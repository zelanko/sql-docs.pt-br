---
title: Níveis de isolamento (OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
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
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 0d8d549d2619fa3804d6228ece1498169e9a66fa
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47739804"
---
# <a name="isolation-levels-ole-db"></a>Níveis de isolamento (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Clientes do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] podem controlar os níveis de isolamento de transação para uma conexão. Para controlar o nível de isolamento da transação, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] consumidor do provedor de OLE DB do Native Client usa:  
  
-   Propriedade DBPROP_SESS_AUTOCOMMITISOLEVELS do DBPROPSET_SESSION para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] modo de confirmação automática do padrão de provedor de OLE DB do Native Client.  
  
     O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] padrão do provedor OLE DB do Native Client para o nível é DBPROPVAL_TI_READCOMMITTED.  
  
-   O parâmetro *isoLevel* do método **ITransactionLocal::StartTransaction** para transações de confirmação manual locais.  
  
-   O parâmetro *isoLevel* do método **ITransactionDispenser::BeginTransaction** para transações distribuídas coordenadas do MS DTC.  
  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] permite acesso de somente leitura ao nível de isolamento de leitura suja. Todos os outros níveis restringem a simultaneidade aplicando bloqueios a objetos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. À medida que o cliente exigir níveis de simultaneidade maiores, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] aplica restrições maiores ao acesso simultâneo aos dados. Para manter o nível mais alto de acesso simultâneo aos dados, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] consumidor do provedor OLE DB do Native Client deve controlar suas solicitações para níveis de simultaneidade específicos de forma inteligente.  
  
> [!NOTE]  
>  O [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] introduziu o nível de isolamento do instantâneo. Para obter mais informações, confira [Trabalhando com o isolamento de instantâneos](../../relational-databases/native-client/features/working-with-snapshot-isolation.md).  
  
## <a name="see-also"></a>Consulte também  
 [Transações](../../relational-databases/native-client-ole-db-transactions/transactions.md)  
  
  
