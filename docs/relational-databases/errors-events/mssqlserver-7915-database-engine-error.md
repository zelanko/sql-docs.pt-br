---
title: MSSQLSERVER_7915 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 7915 (Database Engine error)
ms.assetid: 63338587-7dd3-40e6-b70e-d8ae18fff47b
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 653deb1710937d37a11688d41eb378c0650e0a20
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47803474"
---
# <a name="mssqlserver7915"></a>MSSQLSERVER_7915
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
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
None  
  
