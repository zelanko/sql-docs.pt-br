---
title: Requisitos para atualização para o SQL Server 2008 em um controlador de domínio da conta de serviço | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- domain controllers
- service accounts
- network service accounts
- local service accounts
ms.assetid: 574245b6-11e2-4849-b0ca-836d673ecd0d
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: bb703e42edcbf128ff78ca294e08fc487f06d8f8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66092261"
---
# <a name="service-account-requirements-for-upgrading-to-sql-server-2008-on-a-domain-controller"></a>Requisitos da conta de serviço para atualização para o SQL Server 2008 em um controlador de domínio
  O Supervisor de atualização detectou uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em execução em uma conta de serviço de rede ou serviço Local em um [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)] controlador de domínio. Quando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está instalado em um controlador de domínio do [!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)], os serviços do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não podem executar em privilégios de conta de Serviço Local ou Serviço de Rede.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="corrective-action"></a>Ação corretiva  
 Certifique-se de que todas as contas de serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] estão atribuídas a contas de Domínio ou Sistema Local. Caso essa alteração não seja feita antes da atualização, a Instalação será interrompida. As contas de serviço do Gravador do SQL, o Auxiliar do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] os Serviços Auxiliares do Active Directory são exceções, pois eles são codificados para a conta de Serviço de Rede e não podem ser alterados.  
  
## <a name="see-also"></a>Consulte também  
 [Problemas de atualização de mecanismo de banco de dados](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [Supervisor de atualização do SQL Server 2014 &#91;novo&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
