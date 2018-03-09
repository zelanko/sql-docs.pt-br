---
title: ICommand (OLE DB) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-ole-db-interfaces
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- ICommand [SQL Server Native Client]
ms.assetid: 5e24b3a0-0658-44fc-b653-f4c52f9eb328
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 7ff800871ddd6b298fa80f626650b3789ebf26a2
ms.sourcegitcommit: a0aa5e611a0e6ebb74ac1e2f613e8916dc7a7617
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/24/2018
---
# <a name="icommand-ole-db"></a>ICommand (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Este tópico aborda o comportamento OLE DB que é específico do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client.  
  
## <a name="icommandexecute"></a>ICommand::Execute  
 Inserir dados maiores do que o tamanho de uma coluna normalmente resulta em um erro. No entanto, existem situações em que S_OK será retornado, mas *dwStatus* será definido como DBSTATUS_S_TRUNCATED. Isso geralmente ocorre quando os dados são inseridos com parâmetros, e a coluna não é grande o suficiente para manter os dados e **ICommandWithParameters::SetParameterInfo** não foi chamado.  
  
## <a name="see-also"></a>Consulte também  
 [Interfaces &#40; OLE DB &#41;](http://msdn.microsoft.com/library/34c33364-8538-45db-ae41-5654481cda93)  
  
  
