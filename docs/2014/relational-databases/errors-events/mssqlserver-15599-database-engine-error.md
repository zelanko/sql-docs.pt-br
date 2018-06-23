---
title: MSSQLSERVER_15599 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- 15599 (Database Engine error)
ms.assetid: 97e427a9-8587-46ea-954b-974b5df9c223
caps.latest.revision: 8
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 3678e5d075d4d81481aa0e814f85a1de4ad99009
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36122174"
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
  
  