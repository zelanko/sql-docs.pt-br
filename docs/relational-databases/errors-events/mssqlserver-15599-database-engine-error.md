---
title: MSSQLSERVER_15599 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 15599 (Database Engine error)
ms.assetid: 97e427a9-8587-46ea-954b-974b5df9c223
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 35ad5fd021845a0f528ed1a46aac61b93da015c8
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "68100409"
---
# <a name="mssqlserver_15599"></a>MSSQLSERVER_15599
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do Produto|SQL Server|  
|ID do evento|15599|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|SEC_LOCAL_TEMP_AUDIT_PERMISSIONS|  
|Texto da mensagem|Auditoria e permissões não podem ser definidas em objetos temporários locais.|  
  
## <a name="explanation"></a>Explicação  
Auditoria e permissões não têm nenhum efeito quando definidas para objetos temporários locais ou globais. As instruções não resultam em um erro (as operações retornarão com êxito), mas não têm efeito.  
  
Esse comportamento não mudou. No entanto, a partir do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], essa mensagem informativa alerta o usuário.  
  
## <a name="user-action"></a>Ação do usuário  
Nenhuma ação é necessária, mas considere remover as instruções que tentam definir auditoria ou permissões em objetos temporários locais ou globais.  
  
