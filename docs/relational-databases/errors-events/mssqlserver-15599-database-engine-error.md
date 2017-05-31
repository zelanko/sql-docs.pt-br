---
title: MSSQLSERVER_15599 | Microsoft Docs
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
- 15599 (Database Engine error)
ms.assetid: 97e427a9-8587-46ea-954b-974b5df9c223
caps.latest.revision: 8
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: aa0d5c203907702e20ca9c780baad266b3def320
ms.contentlocale: pt-br
ms.lasthandoff: 04/11/2017

---
# <a name="mssqlserver15599"></a>MSSQLSERVER_15599
  
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
  

