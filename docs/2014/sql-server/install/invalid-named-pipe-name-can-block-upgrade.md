---
title: O nome do pipe nomeado inválido pode bloquear a atualização | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- invalid named pipes [SQL Server]
- named pipes
ms.assetid: 58c2199c-4fdf-4d43-ac1c-842703344b75
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: dddd5da66f09226579a6366baa1a16a6ab00d6bf
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66094189"
---
# <a name="invalid-named-pipe-name-can-block-upgrade"></a>Nome de pipe nomeado inválido pode interromper atualização
  A atualização falhará se o protocolo de pipes nomeados estiver configurado incorretamente.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>DESCRIÇÃO  
 Durante a atualização, o programa de instalação [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] inicia a instância com suporte à memória compartilhada, um pipe nomeado que só aceita conexões locais. Se o nome do pipe especificado no servidor não estiver em branco, ele deverá começar com a cadeia\\\\de\\caracteres ".\pipe" para ser válido. Se o nome de pipe não for válido, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] não iniciará e a instalação falhará.  
  
## <a name="corrective-action"></a>Ação corretiva  
 Use o ** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilitário de rede** para fornecer um nome de pipe válido e, em seguida, execute a instalação.  
  
## <a name="see-also"></a>Consulte Também  
 [Problemas de atualização do Mecanismo de Banco de Dados](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [Supervisor de atualização do SQL Server 2014 &#91;novo&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
