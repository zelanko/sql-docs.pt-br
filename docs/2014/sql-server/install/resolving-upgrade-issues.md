---
title: Solucionando problemas de atualização | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- installing Upgrade Advisor
- Upgrade Advisor [SQL Server], reference
- component issue resolution [Upgrade Advisor]
- resolving upgrade issues
- upgrade blocks [Upgrade Advisor]
- detecting upgrade issues
- finding upgrade issues
- Upgrade Advisor [SQL Server], blocking issues
- configurations preventing upgrading [Upgrade Advisor]
- locating upgrade issues
- blocking issues [Upgrade Advisor]
- issues preventing upgrading [Upgrade Advisor]
- Setup [Upgrade Advisor]
- SQL Server Upgrade Advisor, reference
- analyzing system [Upgrade Advisor], resolving issues
- settings preventing upgrading [Upgrade Advisor]
- upgrade issue reference [Upgrade Advisor]
- identifying upgrade issues
- fixing upgrade issues [Upgrade Advisor]
ms.assetid: 113eb435-8d36-4ed6-9790-b5e4c14809c8
caps.latest.revision: 37
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: a428ddc49d047e9aac42f506917176eee977d0d6
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37244056"
---
# <a name="resolving-upgrade-issues"></a>Solucionando problemas de atualização
  Os tópicos desta seção descrevem os problemas de atualização que podem ser detectados e os que não podem, mas que talvez afetem a atualização ou a experiência pós-atualização. Esses problemas foram organizados por componente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="in-this-section"></a>Nesta seção  
  
-   [Problemas de atualização detectados recentemente](../../../2014/sql-server/install/late-breaking-upgrade-issues.md)  
  
-   [Problemas de atualização do Mecanismo de Banco de Dados](../../../2014/sql-server/install/database-engine-upgrade-issues.md)  
  
-   [Problemas de atualização da Pesquisa de Texto Completo](../../../2014/sql-server/install/full-text-search-upgrade-issues.md)  
  
-   [Problemas na atualização da replicação](../../../2014/sql-server/install/replication-upgrade-issues.md)  
  
-   [Problemas de atualização do Reporting Services &#40;Supervisor de atualização&#41;](../../../2014/sql-server/install/reporting-services-upgrade-issues-upgrade-advisor.md)  
  
-   [Problemas de atualização do SQL Server Agent](../../../2014/sql-server/install/sql-server-agent-upgrade-issues.md)  
  
## <a name="issues-that-prevent-upgrading"></a>Problemas que impedem a atualização  
 Algumas configurações ou definições em uma versão anterior do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] podem impedir a atualização para o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Se a Instalação detectar esses problemas ao instalar o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], ela interromperá o processo de atualização e solicitará que você execute o Supervisor de Atualização e corrija os impedimentos.  
  
### [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
 Se as tarefas a seguir forem listadas no relatório de atualização do [!INCLUDE[ssDE](../../includes/ssde-md.md)], você deverá executar as ações necessárias antes de atualizar para o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]:  
  
-   [Desanexar identificação 32767 do banco de dados](../../../2014/sql-server/install/detach-database-id-32767.md)  
  
-   [Renomear logons que coincidem com nomes de funções fixas do servidor](../../../2014/sql-server/install/rename-logins-matching-fixed-server-role-names.md)  
  
-   [Renomear usuário sys](../../../2014/sql-server/install/rename-user-sys.md)  
  
-   [Usar sp_rename para renomear o nome do índice duplicado](../../../2014/sql-server/install/use-sp-rename-to-rename-duplicate-index-name.md)  
  
## <a name="see-also"></a>Consulte também  
 [Supervisor de atualização do SQL Server 2014 &#91;novo&#93;](/sql/2014/sql-server/install/sql-server-2014-upgrade-advisor)  
  
  
