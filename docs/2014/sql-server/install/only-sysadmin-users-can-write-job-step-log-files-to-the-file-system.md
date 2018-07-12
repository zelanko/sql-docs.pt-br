---
title: Somente usuários sysadmin podem gravar arquivos de log de etapa de trabalho no sistema de arquivos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- job step log files [SQL Server Agent]
- log files [SQL Server Agent]
- writing job step log files
ms.assetid: d26a7cef-1a60-4c95-b9df-f8b4fec59f9b
caps.latest.revision: 24
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 6b31dace7b76d068187b495d6e63517967a6c0f9
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37151947"
---
# <a name="only-sysadmin-users-can-write-job-step-log-files-to-the-file-system"></a>Somente usuários sysadmin podem gravar arquivos de log da etapa de trabalho no sistema de arquivos
  O [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] grava, opcionalmente, um log para cada etapa de trabalho.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent  
  
## <a name="description"></a>Description  
 Na [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)], [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent pode gravar logs de sistema de arquivos para trabalhos que são de propriedade de membros da **sysadmin** função de servidor fixa. Se o proprietário do trabalho não for um membro do **sysadmin** função e se a conta proxy está habilitada, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent pode gravar logs no sistema de arquivos usando as credenciais da conta proxy.  
  
 Após a atualização, os trabalhos pertencentes a usuários que não são membros do **sysadmin** função fixa de servidor não pode gravar logs no sistema de arquivos. Em vez disso, esses usuários podem selecionar a opção para gravar seus logs em uma tabela na **msdb** banco de dados. Os membros de **sysadmin** função ainda pode gravar arquivos de log do sistema de arquivos.  
  
## <a name="corrective-action"></a>Ação corretiva  
 Após a atualização, os trabalhos pertencentes a usuários que não são membros do **sysadmin** função continuará a ser executado, mas os logs não serão criados. Para etapas de trabalho de log para uma tabela, os usuários que não são membros do **sysadmin** função deve atualizar manualmente seus trabalhos.  
  
 Para obter mais informações, consulte os tópicos ‘Criando trabalhos, ‘Criando etapas de trabalhos' e ‘Manuseando várias etapas de trabalho’ nos Manuais Online do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>Consulte também  
 [Problemas de atualização do SQL Server Agent](../../../2014/sql-server/install/sql-server-agent-upgrade-issues.md)  
  
  
