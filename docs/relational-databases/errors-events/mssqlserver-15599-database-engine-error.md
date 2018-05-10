---
title: MSSQLSERVER_15599 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: errors-events
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 15599 (Database Engine error)
ms.assetid: 97e427a9-8587-46ea-954b-974b5df9c223
caps.latest.revision: 8
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 01ad3f136b948fc9d62d863a91c9c1b9a571edea
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
---
# <a name="mssqlserver15599"></a>MSSQLSERVER_15599
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|15599|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|SEC_LOCAL_TEMP_AUDIT_PERMISSIONS|  
|Texto da mensagem|Auditoria e permissões não podem ser definidas em objetos temporários locais.|  
  
## <a name="explanation"></a>Explicação  
Auditoria e permissões não têm nenhum efeito quando definidas para objetos temporários locais ou globais. As instruções não resultam em um erro (as operações retornarão com êxito), mas não têm efeito.  
  
Esse comportamento não mudou. No entanto, a partir do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], essa mensagem informativa alerta o usuário.  
  
## <a name="user-action"></a>Ação do usuário  
Nenhuma ação é necessária, mas considere remover as instruções que tentam definir auditoria ou permissões em objetos temporários locais ou globais.  
  
