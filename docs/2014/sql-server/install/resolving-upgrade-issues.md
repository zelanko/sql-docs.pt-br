---
title: Resolvendo problemas de atualização | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
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
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 85de606ecea93aba80714d4266e9897dd856879f
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66092496"
---
# <a name="resolving-upgrade-issues"></a>Solucionando problemas de atualização
  Os tópicos desta seção descrevem os problemas de atualização que podem ser detectados e os que não podem, mas que talvez afetem a atualização ou a experiência pós-atualização. Esses problemas foram organizados por componente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="in-this-section"></a>Nesta seção  
  
-   [Problemas detectados recentemente que podem interromper a instalação](../../../2014/sql-server/install/late-breaking-upgrade-issues.md)  
  
-   [Problemas de atualização do Mecanismo de Banco de Dados](../../../2014/sql-server/install/database-engine-upgrade-issues.md)  
  
-   [Problemas de atualização da Pesquisa de Texto Completo](../../../2014/sql-server/install/full-text-search-upgrade-issues.md)  
  
-   [Problemas na atualização da replicação](../../../2014/sql-server/install/replication-upgrade-issues.md)  
  
-   [Problemas de atualização do Reporting Services &#40;o supervisor de atualização&#41;](../../../2014/sql-server/install/reporting-services-upgrade-issues-upgrade-advisor.md)  
  
-   [Problemas de atualização do SQL Server Agent](../../../2014/sql-server/install/sql-server-agent-upgrade-issues.md)  
  
## <a name="issues-that-prevent-upgrading"></a>Problemas que impedem a atualização  
 Algumas configurações ou definições em uma versão anterior do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] podem impedir a atualização para o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Se a Instalação detectar esses problemas ao instalar o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], ela interromperá o processo de atualização e solicitará que você execute o Supervisor de Atualização e corrija os impedimentos.  
  
### [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
 Se as tarefas a seguir forem listadas no relatório de atualização do [!INCLUDE[ssDE](../../includes/ssde-md.md)], você deverá executar as ações necessárias antes de atualizar para o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]:  
  
-   [Desanexar identificação 32767 do banco de dados](../../../2014/sql-server/install/detach-database-id-32767.md)  
  
-   [Renomear logons que coincidem com nomes de funções fixas do servidor](../../../2014/sql-server/install/rename-logins-matching-fixed-server-role-names.md)  
  
-   [Renomear usuário sys](../../../2014/sql-server/install/rename-user-sys.md)  
  
-   [Usar sp_rename para renomear o nome do índice duplicado](../../../2014/sql-server/install/use-sp-rename-to-rename-duplicate-index-name.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Supervisor de atualização do SQL Server 2014 &#91;novo&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
