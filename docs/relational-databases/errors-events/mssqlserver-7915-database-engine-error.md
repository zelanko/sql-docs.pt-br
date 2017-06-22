---
title: MSSQLSERVER_7915 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 7915 (Database Engine error)
ms.assetid: 63338587-7dd3-40e6-b70e-d8ae18fff47b
caps.latest.revision: 16
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: fd2358d9fda87cfe7f1d25dc45ef475606165eb4
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

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
Nenhuma  
  

