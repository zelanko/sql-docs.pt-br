---
title: Espelhamento de Banco de Dados – permitir o acesso à rede – Autenticação do Windows | Microsoft Docs
ms.custom: ''
ms.date: 05/17/2016
ms.prod: sql
ms.prod_service: high-availability
ms.component: database-mirroring
ms.reviewer: ''
ms.suite: sql
ms.technology: high-availability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Windows authentication [SQL Server]
- database mirroring [SQL Server], security
ms.assetid: 28c8fec5-5feb-4c84-8d72-f2bd1ae3b40d
caps.latest.revision: 34
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: f66217471aa71d4c5552a8354221acc191a0dc09
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="database-mirroring---allow-network-access---windows-authentication"></a>Espelhamento de Banco de Dados – permitir o acesso à rede – Autenticação do Windows
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  O uso da Autenticação do Windows para conectar os pontos de extremidade de espelhamento de banco de dados de duas instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] requer a configuração manual de contas de logon sob as seguintes condições:  
  
-   Se as instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] forem executadas como serviços em diferentes contas de domínio (nos mesmos domínios ou em domínios confiáveis), o logon de cada conta deverá ser criado no **mestre** em cada uma das instâncias de servidor remoto, e esse logon deverá receber permissões CONNECT no ponto de extremidade.  
  
-   Se as instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] forem executadas como a conta de Serviço de Rede, o logon da conta de cada computador host (*DomainName***\\***ComputerName$*) deverá ser criado no **mestre** em cada uma das instâncias de servidor remoto, e esse logon deverá receber permissões CONNECT no ponto de extremidade. Isso é porque uma instância de servidor em execução sob a conta de serviço de rede é autenticada usando a conta de domínio do computador host.  
  
> [!NOTE]  
>  Verifique se há um ponto de extremidade para cada uma das instâncias do servidor. Para obter mais informações, veja [Criar um ponto de extremidade de espelhamento de banco de dados para a Autenticação do Windows &#40;Transact-SQL&#41;](../../database-engine/database-mirroring/create-a-database-mirroring-endpoint-for-windows-authentication-transact-sql.md).  
  
### <a name="to-configure-logins-for-windows-authentication"></a>Para configurar logons para a Autenticação do Windows  
  
1.  Para a conta de usuário de cada instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], crie um logon nas outras instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Use a instrução [CREATE LOGIN](../../t-sql/statements/create-login-transact-sql.md) com a cláusula FROM WINDOWS.  
  
     Para obter mais informações, consulte [Crie um logon](../../relational-databases/security/authentication-access/create-a-login.md).  
  
2.  Além disso, para assegurar que o usuário de logon tenha acesso ao ponto de extremidade, use a instrução [GRANT](../../t-sql/statements/grant-transact-sql.md) para conceder permissões de conexão no ponto de extremidade para o logon. Observe que a concessão de permissões de conexão para o ponto de extremidade não é necessária se o usuário for um Administrador.  
  
     Para obter mais informações, consulte [Conceder uma permissão a uma entidade de segurança](../../relational-databases/security/authentication-access/grant-a-permission-to-a-principal.md).  
  
## <a name="example"></a>Exemplo  
 O exemplo de [!INCLUDE[tsql](../../includes/tsql-md.md)] a seguir criar um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para uma conta de usuário denominada `Otheruser` que pertence a um domínio denominado `Adomain`. O exemplo concede permissões a esse usuário para um ponto de extremidade de espelhamento de banco de dados preexistente denominado `Mirroring_Endpoint`.  
  
```  
USE master;  
GO  
CREATE LOGIN [Adomain\Otheruser] FROM WINDOWS;  
GO  
GRANT CONNECT on ENDPOINT::Mirroring_Endpoint TO [Adomain\Otheruser];  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Visão geral dos grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Espelhamento de banco de dados &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md)   
 [Segurança de transporte para espelhamento de banco de dados e grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../database-engine/database-mirroring/transport-security-database-mirroring-always-on-availability.md)   
 [O ponto de extremidade de espelhamento de banco de dados &#40;SQL Server&#41;](../../database-engine/database-mirroring/the-database-mirroring-endpoint-sql-server.md)  
  
  
