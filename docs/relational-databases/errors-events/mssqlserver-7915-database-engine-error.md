---
title: MSSQLSERVER_7915 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords: 7915 (Database Engine error)
ms.assetid: 63338587-7dd3-40e6-b70e-d8ae18fff47b
caps.latest.revision: "16"
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.openlocfilehash: b0b8d1752a64451824195426c241d19472483570
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="mssqlserver7915"></a>MSSQLSERVER_7915
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|7915|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|DBCC2_REPAIR_IAM_CHAIN_REBUILT|  
|Texto da mensagem|Correção: a cadeia IAM relativa à ID de objeto O_ID, ID de índice I_ID, ID de partição PN_ID, ID de unidade de alocação A_ID (tipo TYPE), ficou truncada antes da página P_ID e será recriada.|  
  
## <a name="explanation"></a>Explicação  
Essa é uma mensagem informativa enviada pela cláusula REPAIR que indica que foi aplicado um patch à cadeia IAM especificada para que ela pudesse ser reconstruída. Essa aplicação de patch pode ter exigido a alocação de um novo cabeçalho da cadeia IAM ou a remoção de páginas inválidas da cadeia.  
  
## <a name="user-action"></a>Ação do usuário  
Nenhum.  
  
