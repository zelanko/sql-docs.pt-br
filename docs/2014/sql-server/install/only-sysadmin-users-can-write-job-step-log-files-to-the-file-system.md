---
title: Somente usuários sysadmin podem gravar arquivos de log de etapa de trabalho no sistema de arquivos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- job step log files [SQL Server Agent]
- log files [SQL Server Agent]
- writing job step log files
ms.assetid: d26a7cef-1a60-4c95-b9df-f8b4fec59f9b
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 84d04729e2f4c00c5d127a706727567c44855cd6
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66093680"
---
# <a name="only-sysadmin-users-can-write-job-step-log-files-to-the-file-system"></a>Somente usuários sysadmin podem gravar arquivos de log da etapa de trabalho no sistema de arquivos
  O [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] grava, opcionalmente, um log para cada etapa de trabalho.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent  
  
## <a name="description"></a>DESCRIÇÃO  
 No [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)], [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o Agent pode gravar logs no sistema de arquivos para trabalhos que pertencem a membros da função de servidor fixa **sysadmin** . Se o proprietário do trabalho não for um membro da função **sysadmin** e se a conta proxy estiver habilitada [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , o Agent poderá gravar logs no sistema de arquivos usando as credenciais da conta proxy.  
  
 Após a atualização, os trabalhos que pertencem a usuários que não são membros da função de servidor fixa **sysadmin** não podem mais gravar logs no sistema de arquivos. Em vez disso, esses usuários podem selecionar a opção para gravar seus logs em uma tabela no banco de dados **msdb** . Os membros da função **sysadmin** ainda podem gravar arquivos de log no sistema de arquivos.  
  
## <a name="corrective-action"></a>Ação corretiva  
 Após a atualização, os trabalhos que são de propriedade de usuários que não são membros da função **sysadmin** continuarão a ser executados, mas os logs não serão criados. Para registrar etapas de trabalho em uma tabela, os usuários que não são membros da função **sysadmin** devem atualizar manualmente seus trabalhos.  
  
 Para obter mais informações, consulte os tópicos ‘Criando trabalhos, ‘Criando etapas de trabalhos' e ‘Manuseando várias etapas de trabalho’ nos Manuais Online do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>Consulte Também  
 [Problemas de atualização do SQL Server Agent](../../../2014/sql-server/install/sql-server-agent-upgrade-issues.md)  
  
  
