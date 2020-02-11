---
title: MSSQLSERVER_7915 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 7915 (Database Engine error)
ms.assetid: 63338587-7dd3-40e6-b70e-d8ae18fff47b
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: fb60bfa05e75c06b7da04042aa1abfbd42b756c0
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62761903"
---
# <a name="mssqlserver_7915"></a>MSSQLSERVER_7915
    
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do Produto|SQL Server|  
|ID do evento|7915|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|DBCC2_REPAIR_IAM_CHAIN_REBUILT|  
|Texto da mensagem|Correção: a cadeia IAM relativa à ID de objeto O_ID, ID de índice I_ID, ID de partição PN_ID, ID de unidade de alocação A_ID (tipo TYPE), ficou truncada antes da página P_ID e será recriada.|  
  
## <a name="explanation"></a>Explicação  
 Essa é uma mensagem informativa enviada pela cláusula REPAIR que indica que foi aplicado um patch à cadeia IAM especificada para que ela pudesse ser reconstruída. Essa aplicação de patch pode ter exigido a alocação de um novo cabeçalho da cadeia IAM ou a remoção de páginas inválidas da cadeia.  
  
## <a name="user-action"></a>Ação do usuário  
 Nenhum  
  
  
