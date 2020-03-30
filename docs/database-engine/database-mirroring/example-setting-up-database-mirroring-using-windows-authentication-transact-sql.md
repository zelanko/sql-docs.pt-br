---
title: Configurar o espelhamento de banco de dados com a autenticação do Windows (T-SQL)
description: Um exemplo que mostra todas as fases necessárias para criar uma sessão de espelhamento de banco de dados com uma testemunha, usando a Autenticação do Windows com o T-SQL (Transact-SQL)
ms.custom: seo-lt-2019
ms.date: 05/17/2016
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- database mirroring [SQL Server], deployment
- Windows authentication [SQL Server]
- authentication [SQL Server], database mirroring
- database mirroring [SQL Server], security
ms.assetid: 35800769-aede-4aac-b077-0e0e487e302f
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 2a263cd161370a4d3f87c673209e82296ec2a28c
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "74822268"
---
# <a name="example-configure-database-mirroring-using-windows-authentication-transact-sql"></a>Exemplo: Configurar o espelhamento de banco de dados usando a autenticação do Windows (Transact-SQL)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Este exemplo mostra todas as fases necessárias para criar uma sessão de espelhamento de banco de dados com uma testemunha, usando a Autenticação do Windows. Os exemplos deste tópico usam o [!INCLUDE[tsql](../../includes/tsql-md.md)]. Note que como uma alternativa para o uso de passos de [!INCLUDE[tsql](../../includes/tsql-md.md)], você pode usar o Assistente para Configurar Segurança de Espelhamento de Banco de Dados para a configuração do espelhamento de banco de dados. Para obter mais informações, veja [Estabelecer uma sessão de espelhamento de banco de dados usando a Autenticação do Windows &#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/establish-database-mirroring-session-windows-authentication.md).  
  
## <a name="prerequisite"></a>Pré-requisito  
 O exemplo usa o banco de dados de exemplo do **AdventureWorks** , que, por padrão, usa o modelo de recuperação simples. Para usar espelhamento de banco de dados com este banco de dados, você deve alterar isso para usar o modelo de recuperação completa. Para fazer isto em [!INCLUDE[tsql](../../includes/tsql-md.md)], use a instrução ALTER DATABASE, como se segue:  
  
```  
USE master;  
GO  
ALTER DATABASE AdventureWorks   
SET RECOVERY FULL;  
GO  
```  
  
 Para saber mais sobre como alterar o modelo de recuperação no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], consulte [Exibir ou alterar o modelo de recuperação de um banco de dados &#40;SQL Server&#41;](../../relational-databases/backup-restore/view-or-change-the-recovery-model-of-a-database-sql-server.md).  
  
### <a name="permissions"></a>Permissões  
 Exige a permissão ALTER no banco de dados e permissão CREATE ENDPOINT ou associação na função de servidor fixa **sysadmin** .  
  
## <a name="example"></a>Exemplo  
 Neste exemplo, os dois parceiros e a testemunha são as instâncias de servidor padrão em três sistemas de computador. As três instâncias de servidor executam o mesmo domínio do Windows, mas a conta do usuário (usada como conta de serviço de inicialização) é diferente para a instância de servidor testemunha do exemplo.  
  
 A tabela a seguir resume os valores usados neste exemplo.  
  
|Função de espelhamento inicial|Sistema de host|Conta de usuário do domínio|  
|----------------------------|-----------------|-------------------------|  
|Principal|PARTNERHOST1|*\<Mydomain>\\<dbousername\>*|  
|Espelho|PARTNERHOST5|*\<Mydomain>\\<dbousername\>*|  
|Witness (testemunha)|WITNESSHOST4|*\<Somedomain>\\<witnessuser\>*|  
  
1.  Crie um ponto de extremidade na instância de servidor principal (instância padrão em PARTNERHOST1).  
  
    ```  
    CREATE ENDPOINT Endpoint_Mirroring  
        STATE=STARTED   
        AS TCP (LISTENER_PORT=7022)   
        FOR DATABASE_MIRRORING (ROLE=PARTNER)  
    GO  
    --Partners under same domain user; login already exists in master.  
    --Create a login for the witness server instance,  
    --which is running as Somedomain\witnessuser:  
    USE master ;  
    GO  
    CREATE LOGIN [Somedomain\witnessuser] FROM WINDOWS ;  
    GO  
    -- Grant connect permissions on endpoint to login account of witness.  
    GRANT CONNECT ON ENDPOINT::Endpoint_Mirroring TO [Somedomain\witnessuser];  
    --Grant connect permissions on endpoint to login account of partners.  
    GRANT CONNECT ON ENDPOINT::Endpoint_Mirroring TO [Mydomain\dbousername];  
    GO  
    ```  
  
2.  Crie um ponto de extremidade na instância de servidor espelho (instância padrão em PARTNERHOST5).  
  
    ```  
    CREATE ENDPOINT Endpoint_Mirroring  
        STATE=STARTED   
        AS TCP (LISTENER_PORT=7022)   
        FOR DATABASE_MIRRORING (ROLE=ALL)  
    GO  
    --Partners under same domain user; login already exists in master.  
    --Create a login for the witness server instance,  
    --which is running as Somedomain\witnessuser:  
    USE master ;  
    GO  
    CREATE LOGIN [Somedomain\witnessuser] FROM WINDOWS ;  
    GO  
    --Grant connect permissions on endpoint to login account of witness.  
    GRANT CONNECT ON ENDPOINT::Endpoint_Mirroring TO [Somedomain\witnessuser];  
    --Grant connect permissions on endpoint to login account of partners.  
    GRANT CONNECT ON ENDPOINT::Endpoint_Mirroring TO [Mydomain\dbousername];  
    GO  
    ```  
  
3.  Crie um ponto de extremidade na instância de servidor testemunha (instância padrão em WITNESSHOST4).  
  
    ```  
    CREATE ENDPOINT Endpoint_Mirroring  
        STATE=STARTED   
        AS TCP (LISTENER_PORT=7022)   
        FOR DATABASE_MIRRORING (ROLE=WITNESS)  
    GO  
    --Create a login for the partner server instances,  
    --which are both running as Mydomain\dbousername:  
    USE master ;  
    GO  
    CREATE LOGIN [Mydomain\dbousername] FROM WINDOWS ;  
    GO  
    --Grant connect permissions on endpoint to login account of partners.  
    GRANT CONNECT ON ENDPOINT::Endpoint_Mirroring TO [Mydomain\dbousername];  
    GO  
    ```  
  
4.  Crie o banco de dados espelho. Para obter mais informações, veja [Preparar um banco de dados espelho para espelhamento &#40;SQL Server&#41;](../../database-engine/database-mirroring/prepare-a-mirror-database-for-mirroring-sql-server.md).  
  
5.  Na instância de servidor espelho em PARTNERHOST5, defina a instância de servidor em PARTNERHOST1 como o parceiro (fazendo dele a instância de servidor principal inicial).  
  
    ```  
    ALTER DATABASE AdventureWorks   
        SET PARTNER =   
        'TCP://PARTNERHOST1.COM:7022'  
    GO  
    ```  
  
6.  Na instância do servidor principal em PARTNERHOST1, defina a instância de servidor em PARTNERHOST5 como o parceiro (fazendo dele a instância de servidor espelho inicial).  
  
    ```  
    ALTER DATABASE AdventureWorks   
        SET PARTNER = 'TCP://PARTNERHOST5.COM:7022'  
    GO  
    ```  
  
7.  No servidor principal, defina a testemunha (que está em WITNESSHOST4).  
  
    ```  
    ALTER DATABASE AdventureWorks   
        SET WITNESS =   
        'TCP://WITNESSHOST4.COM:7022'  
    GO  
    ```  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> Tarefas relacionadas  
  
-   [Preparar um banco de dados espelho para espelhamento &#40;SQL Server&#41;](../../database-engine/database-mirroring/prepare-a-mirror-database-for-mirroring-sql-server.md)  
  
-   [Iniciar o Assistente para Configurar Segurança de Espelhamento de Banco de Dados &#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/start-the-configuring-database-mirroring-security-wizard.md)  
  
-   [Configurar um banco de dados espelho para usar a propriedade confiável &#40;Transact-SQL&#41;](../../database-engine/database-mirroring/set-up-a-mirror-database-to-use-the-trustworthy-property-transact-sql.md)  
  
-   [Permitir que um ponto de extremidade de espelhamento de banco de dados use certificados para conexões de saída &#40;Transact-SQL&#41;](../../database-engine/database-mirroring/database-mirroring-use-certificates-for-outbound-connections.md)  
  
-   [Permitir que um ponto de extremidade de espelhamento de banco de dados use certificados para conexões de entrada &#40;Transact-SQL&#41;](../../database-engine/database-mirroring/database-mirroring-use-certificates-for-inbound-connections.md)  
  
-   [Exemplo: Configurar o espelhamento de banco de dados usando certificados &#40;Transact-SQL&#41;](../../database-engine/database-mirroring/example-setting-up-database-mirroring-using-certificates-transact-sql.md)  
  
## <a name="see-also"></a>Consulte Também  
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [O ponto de extremidade de espelhamento de banco de dados &#40;SQL Server&#41;](../../database-engine/database-mirroring/the-database-mirroring-endpoint-sql-server.md)   
 [Segurança de transporte para espelhamento de banco de dados e grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../database-engine/database-mirroring/transport-security-database-mirroring-always-on-availability.md)   
 [Gerenciar metadados ao disponibilizar um banco de dados em outra instância do servidor &#40;SQL Server&#41;](../../relational-databases/databases/manage-metadata-when-making-a-database-available-on-another-server.md)   
 [Central de segurança do Mecanismo de Banco de Dados do SQL Server e Banco de Dados SQL do Azure](../../relational-databases/security/security-center-for-sql-server-database-engine-and-azure-sql-database.md)  
  
  
