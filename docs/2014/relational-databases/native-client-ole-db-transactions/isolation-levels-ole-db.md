---
title: Níveis de isolamento (OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- OLE DB, transactions
- isolation levels [OLE DB]
- transactions [OLE DB]
- SQL Server Native Client OLE DB provider, transactions
ms.assetid: d70ee72c-6e2a-4bcd-9456-4a697a866361
caps.latest.revision: 32
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ec099f18afd80bd07f059d3e87b18598b36b1117
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37420716"
---
# <a name="isolation-levels-ole-db"></a>Níveis de isolamento (OLE DB)
  Clientes do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] podem controlar os níveis de isolamento de transação para uma conexão. Para controlar o nível de isolamento da transação, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] consumidor do provedor de OLE DB do Native Client usa:  
  
-   Propriedade DBPROP_SESS_AUTOCOMMITISOLEVELS do DBPROPSET_SESSION para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] modo de confirmação automática do padrão de provedor de OLE DB do Native Client.  
  
     O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] padrão do provedor OLE DB do Native Client para o nível é DBPROPVAL_TI_READCOMMITTED.  
  
-   O *isoLevel* parâmetro do **itransactionlocal:: Starttransaction** método transações de confirmação manual locais.  
  
-   O *isoLevel* parâmetro do **itransactiondispenser:: BeginTransaction** transações distribuídas do método para coordenada pelo MS DTC.  
  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] permite acesso de somente leitura ao nível de isolamento de leitura suja. Todos os outros níveis restringem a simultaneidade aplicando bloqueios a objetos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. À medida que o cliente exigir níveis de simultaneidade maiores, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] aplica restrições maiores ao acesso simultâneo aos dados. Para manter o nível mais alto de acesso simultâneo aos dados, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] consumidor do provedor OLE DB do Native Client deve controlar suas solicitações para níveis de simultaneidade específicos de forma inteligente.  
  
> [!NOTE]  
>  O [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] introduziu o nível de isolamento do instantâneo. Para obter mais informações, consulte [trabalhando com isolamento de instantâneo](../native-client/features/working-with-snapshot-isolation.md).  
  
## <a name="see-also"></a>Consulte também  
 [Transações](transactions.md)  
  
  
