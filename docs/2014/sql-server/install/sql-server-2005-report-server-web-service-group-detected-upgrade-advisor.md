---
title: Grupo de serviço Web servidor de relatório do SQL Server 2005 detectado (Supervisor de atualização) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- deployment [Reporting Services]
ms.assetid: 699d24eb-7756-4b41-9294-ef1a94b2f267
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 4f379675a4d7b37b9eab69598f7c04bc57306d46
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66092105"
---
# <a name="sql-server-2005-report-server-web-service-group-detected-upgrade-advisor"></a>Grupo do serviço Web do servidor de relatório do SQL Server 2005 foi detectado (Supervisor de Atualização)
  O Supervisor de atualização detectou que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instância está associada um [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] grupo do serviço Web servidor de relatório.  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .|  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
## <a name="description"></a>Descrição  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] não usa o [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] grupo do serviço Web servidor de relatório. Quando você fizer a atualização do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] para o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], esse grupo de serviço será excluído e as listas de controle de acesso (ACLs) personalizadas desse grupo ou de usuários que pertencem a ele não serão mantidas durante a atualização.  
  
## <a name="corrective-action"></a>Ação corretiva  
 Antes da atualização, faça um backup de todas as ACLs personalizadas ou usuários pertencentes ao grupo de serviço Web do servidor de relatório do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. Para fazer isso, você pode usar o **Icacls.exe** ferramenta de linha de comando na [!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)] SP2 e posterior ou a ferramenta de linha de comando de Cacls.exe nos sistemas de operacionais Windows anteriores ao [!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)] SP2. Para obter mais informações sobre a sintaxe dessas ferramentas, consulte a documentação do Windows. Concluída a instalação com êxito, aplique as ACLs personalizadas ou os usuários ao grupo do Windos do servidor de relatório do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] da instância do servidor de relatório. O [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] grupo de Windows do servidor de relatório assume a forma de SQLServerReportServerUser$\<*computer_name*>$\<*instance_name*>.  
  
## <a name="see-also"></a>Consulte também  
 [Problemas de atualização do Reporting Services &#40;Supervisor de atualização&#41;](../../../2014/sql-server/install/reporting-services-upgrade-issues-upgrade-advisor.md)  
  
  
