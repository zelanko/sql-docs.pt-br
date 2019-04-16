---
title: Nome de pipe nomeado inválido pode bloquear a atualização | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- invalid named pipes [SQL Server]
- named pipes
ms.assetid: 58c2199c-4fdf-4d43-ac1c-842703344b75
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ad261d8d7680be7111e79a1b7a7f3291c2139308
ms.sourcegitcommit: 46a2c0ffd0a6d996a3afd19a58d2a8f4b55f93de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/15/2019
ms.locfileid: "59582809"
---
# <a name="invalid-named-pipe-name-can-block-upgrade"></a>Nome de pipe nomeado inválido pode interromper atualização
  A atualização falhará se o protocolo de pipes nomeados estiver configurado incorretamente.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>Descrição  
 Durante a atualização, o programa de instalação inicia a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] instância com suporte de memória compartilhada, um pipe nomeado que aceita apenas conexões locais. Se o nome do pipe especificado no servidor não está em branco, ele deve começar com a cadeia de caracteres "\\\\. \pipe\\" seja válido. Se o nome de pipe não for válido, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] não iniciará e a instalação falhará.  
  
## <a name="corrective-action"></a>Ação corretiva  
 Use o  **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilitário de rede** para fornecer um nome de pipe válido e, em seguida, execute a instalação.  
  
## <a name="see-also"></a>Consulte também  
 [Problemas de atualização de mecanismo de banco de dados](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [Supervisor de atualização do SQL Server 2014 &#91;novo&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
