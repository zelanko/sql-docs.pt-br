---
title: Acesso à rede para um ponto de extremidade de espelhamento de banco de dados
description: Saiba como permitir o acesso à rede do Windows authenticatino a um ponto de extremidade de espelhamento de banco de dados para SQL Server.
ms.custom: seo-lt-2019
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Windows authentication [SQL Server]
- database mirroring [SQL Server], security
ms.assetid: 28c8fec5-5feb-4c84-8d72-f2bd1ae3b40d
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e40a1eead54fe9d00eaf099410260023229796d0
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "75228572"
---
# <a name="allow-network-access-to-a-database-mirroring-endpoint-using-windows-authentication-sql-server"></a>Permitir o acesso à rede a um ponto de extremidade de espelhamento de banco de dados usando a Autenticação do Windows (SQL Server)
  O uso da Autenticação do Windows para conectar os pontos de extremidade de espelhamento de banco de dados de duas instâncias do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] requer a configuração manual de contas de logon sob as seguintes condições:  
  
-   Se as instâncias do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] forem executadas como serviços em diferentes contas de domínio (nos mesmos domínios ou em domínios confiáveis), o logon de cada conta deverá ser criado no **mestre** em cada uma das instâncias de servidor remoto, e esse logon deverá receber permissões CONNECT no ponto de extremidade.  
  
-   Se as instâncias do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] forem executadas como a conta de Serviço de Rede, o logon da conta de cada computador host (*DomainName***\\***ComputerName$* ) deverá ser criado no **mestre** em cada uma das instâncias de servidor remoto, e esse logon deverá receber permissões CONNECT no ponto de extremidade. Isso é porque uma instância de servidor em execução sob a conta de serviço de rede é autenticada usando a conta de domínio do computador host.  
  
> [!NOTE]  
>  Verifique se há um ponto de extremidade para cada uma das instâncias do servidor. Para obter mais informações, veja [Criar um ponto de extremidade de espelhamento de banco de dados para a Autenticação do Windows &#40;Transact-SQL&#41;](database-mirroring/create-a-database-mirroring-endpoint-for-windows-authentication-transact-sql.md).  
  
### <a name="to-configure-logins-for-windows-authentication"></a>Para configurar logons para a Autenticação do Windows  
  
1.  Para a conta de usuário de cada instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], crie um logon nas outras instâncias do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Use a instrução [CREATE LOGIN](/sql/t-sql/statements/create-login-transact-sql) com a cláusula FROM WINDOWS.  
  
     Para obter mais informações, consulte [Crie um logon](../relational-databases/security/authentication-access/create-a-login.md).  
  
2.  Além disso, para assegurar que o usuário de logon tenha acesso ao ponto de extremidade, use a instrução [GRANT](/sql/t-sql/statements/grant-transact-sql) para conceder permissões de conexão no ponto de extremidade para o logon. Observe que a concessão de permissões de conexão para o ponto de extremidade não é necessária se o usuário for um Administrador.  
  
     Para obter mais informações, consulte [Conceder uma permissão a uma entidade de segurança](../relational-databases/security/authentication-access/grant-a-permission-to-a-principal.md).  
  
## <a name="example"></a>Exemplo  
 O exemplo de [!INCLUDE[tsql](../includes/tsql-md.md)] a seguir criar um logon do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para uma conta de usuário denominada `Otheruser` que pertence a um domínio denominado `Adomain`. O exemplo concede permissões a esse usuário para um ponto de extremidade de espelhamento de banco de dados preexistente denominado `Mirroring_Endpoint`.  
  
```  
USE master;  
GO  
CREATE LOGIN [Adomain\Otheruser] FROM WINDOWS;  
GO  
GRANT CONNECT on ENDPOINT::Mirroring_Endpoint TO [Adomain\Otheruser];  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Visão geral do Grupos de Disponibilidade AlwaysOn &#40;SQL Server&#41;](availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Espelhamento de banco de dados &#40;SQL Server&#41;](database-mirroring/database-mirroring-sql-server.md)   
 [Segurança de transporte para espelhamento de banco de dados e Grupos de Disponibilidade AlwaysOn &#40;SQL Server&#41;](database-mirroring/transport-security-database-mirroring-always-on-availability.md)   
 [O ponto de extremidade de espelhamento de banco de dados &#40;SQL Server&#41;](database-mirroring/the-database-mirroring-endpoint-sql-server.md)  
  
  
