---
title: 'Exemplo: configurar o espelhamento de banco de dados usando certificados (Transact-SQL) | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- database mirroring [SQL Server], deployment
- certificates [SQL Server], database mirroring
- authentication [SQL Server], database mirroring
- database mirroring [SQL Server], security
ms.assetid: df489ecd-deee-465c-a26a-6d1bef6d7b66
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 2eb63756a6ddf5e8a47f27f9f3d2f349c0bdf339
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62806747"
---
# <a name="example-setting-up-database-mirroring-using-certificates-transact-sql"></a>Exemplo: Configurando espelhamento de banco de dados usando certificados (Transact-SQL)
  Este exemplo mostra todos os estágios necessários para criar uma sessão de espelhamento de banco de dados com uma autenticação baseada em certificado. Os exemplos deste tópico usam o [!INCLUDE[tsql](../../includes/tsql-md.md)]. A menos que você possa garantir que sua rede está segura, recomendamos o uso de criptografia para conexões de espelhamento de banco de dados.  
  
 Ao copiar um certificado para outro sistema, use um método de cópia seguro. Seja extremamente cauteloso para manter todos os seus certificados em segurança.  
  
##  <a name="example"></a><a name="ExampleH2"></a>Exemplo  
 O exemplo a seguir demonstra o que deve ser feito em um parceiro que reside em HOST_A. Neste exemplo, os dois parceiros são as instâncias de servidor padrão em três sistemas de computador. As duas instâncias de servidor são executadas em domínios não confiáveis do Windows, portanto, é necessária autenticação baseada em certificado.  
  
 A função principal inicial é assumida pelo HOST_A, e a função de espelho é assumida pelo HOST_B.  
  
 A configuração do espelhamento de banco de dados usando certificados envolve quatro estágios gerais, dos quais três – 1, 2 e 4 – são demonstrados por este exemplo. Esses estágios são os seguintes:  
  
1.  [Configurando conexões de saída](#ConfiguringOutboundConnections)  
  
     Este exemplo mostra as etapas para:  
  
    1.  Configurar o Host_A para conexões de saída.  
  
    2.  Configurar o Host_B para conexões de saída.  
  
     Para obter informações sobre esse estágio de configuração do espelhamento de banco de dados, consulte [Permitir que um ponto de extremidade de espelhamento de banco de dados use certificados para conexões de saída &#40;Transact-SQL&#41;](database-mirroring-use-certificates-for-outbound-connections.md).  
  
2.  [Configurando conexões de saída](#ConfigureInboundConnections)  
  
     Este exemplo mostra as etapas para:  
  
    1.  Configurar o Host_A para conexões de entrada.  
  
    2.  Configurar o Host_B para conexões de entrada.  
  
     Para obter informações sobre esse estágio de configuração do espelhamento de banco de dados, consulte [Permitir que um ponto de extremidade de espelhamento de banco de dados use certificados para conexões de entrada &#40;Transact-SQL&#41;](database-mirroring-use-certificates-for-inbound-connections.md).  
  
3.  Criando o banco de dados espelho  
  
     Para obter informações sobre como criar um banco de dados espelho, consulte [Preparar um banco de dados espelho para espelhamento &#40;SQL Server&#41;](prepare-a-mirror-database-for-mirroring-sql-server.md).  
  
4.  [Configurando os parceiros de espelhamento](#ConfigureMirroringPartners)  
  
###  <a name="configuring-outbound-connections"></a><a name="ConfiguringOutboundConnections"></a>Configurando conexões de saída  
 **Para configurar Host_A para conexões de saída**  
  
1.  No banco de dados mestre, crie a chave mestra de banco de dados, se necessário.  
  
    ```  
    USE master;  
    CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<1_Strong_Password!>';  
    GO  
    ```  
  
2.  Faça um certificado para esta instância de servidor.  
  
    ```  
    USE master;  
    CREATE CERTIFICATE HOST_A_cert   
       WITH SUBJECT = 'HOST_A certificate';  
    GO  
    ```  
  
3.  Crie um ponto de extremidade de espelhamento para a instância de servidor que usa o certificado.  
  
    ```  
    CREATE ENDPOINT Endpoint_Mirroring  
       STATE = STARTED  
       AS TCP (  
          LISTENER_PORT=7024  
          , LISTENER_IP = ALL  
       )   
       FOR DATABASE_MIRRORING (   
          AUTHENTICATION = CERTIFICATE HOST_A_cert  
          , ENCRYPTION = REQUIRED ALGORITHM AES  
          , ROLE = ALL  
       );  
    GO  
    ```  
  
4.  Faça backup do certificado de HOST_A e copie-o para outro sistema, HOST_B.  
  
    ```  
    BACKUP CERTIFICATE HOST_A_cert TO FILE = 'C:\HOST_A_cert.cer';  
    GO  
    ```  
  
5.  Usando qualquer método de cópia seguro, copie C:\HOST_A_cert.cer para HOST_B.  
  
 **Para configurar Host_B para conexões de saída**  
  
1.  No banco de dados mestre, crie a chave mestra de banco de dados, se necessário.  
  
    ```  
    USE master;  
    CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<Strong_Password_#2>';  
    GO  
    ```  
  
2.  Faça um certificado na instância de servidor HOST_B.  
  
    ```  
    CREATE CERTIFICATE HOST_B_cert   
       WITH SUBJECT = 'HOST_B certificate for database mirroring';  
    GO  
    ```  
  
3.  Crie um ponto de extremidade de espelhamento para a instância de servidor em HOST_B.  
  
    ```  
    CREATE ENDPOINT Endpoint_Mirroring  
       STATE = STARTED  
       AS TCP (  
          LISTENER_PORT=7024  
          , LISTENER_IP = ALL  
       )   
       FOR DATABASE_MIRRORING (   
          AUTHENTICATION = CERTIFICATE HOST_B_cert  
          , ENCRYPTION = REQUIRED ALGORITHM AES  
          , ROLE = ALL  
       );  
    GO  
    ```  
  
4.  Faça backup de certificado de HOST_B.  
  
    ```  
    BACKUP CERTIFICATE HOST_B_cert TO FILE = 'C:\HOST_B_cert.cer';  
    GO   
    ```  
  
5.  Usando qualquer método de cópia seguro, copie C:\HOST_ B_cert.cer para HOST_A.  
  
 Para obter mais informações, consulte [Permitir que um ponto de extremidade de espelhamento de banco de dados use certificados para conexões de saída &#40;Transact-SQL&#41;](database-mirroring-use-certificates-for-outbound-connections.md).  
  
###  <a name="configuring-inbound-connections"></a><a name="ConfigureInboundConnections"></a>Configurando conexões de entrada  
 **Para configurar Host_A para conexões de entrada**  
  
1.  Crie um logon em HOST_A para HOST_B.  
  
    ```  
    USE master;  
    CREATE LOGIN HOST_B_login WITH PASSWORD = '1Sample_Strong_Password!@#';  
    GO  
    ```  
  
2.  --Crie um usuário para aquele logon.  
  
    ```  
    CREATE USER HOST_B_user FOR LOGIN HOST_B_login;  
    GO  
    ```  
  
3.  --Associe o certificado ao usuário.  
  
    ```  
    CREATE CERTIFICATE HOST_B_cert  
       AUTHORIZATION HOST_B_user  
       FROM FILE = 'C:\HOST_B_cert.cer'  
    GO  
    ```  
  
4.  Conceda permissão CONNECT no logon para o ponto de extremidade de espelhamento remoto.  
  
    ```  
    GRANT CONNECT ON ENDPOINT::Endpoint_Mirroring TO [HOST_B_login];  
    GO  
    ```  
  
 **Para configurar Host_B para conexões de entrada**  
  
1.  Crie um logon em HOST_B para HOST_A.  
  
    ```  
    USE master;  
    CREATE LOGIN HOST_A_login WITH PASSWORD = '=Sample#2_Strong_Password2';  
    GO  
    ```  
  
2.  Crie um usuário para aquele logon.  
  
    ```  
    CREATE USER HOST_A_user FOR LOGIN HOST_A_login;  
    GO  
    ```  
  
3.  --Associe o certificado ao usuário.  
  
    ```  
    CREATE CERTIFICATE HOST_A_cert  
       AUTHORIZATION HOST_A_user  
       FROM FILE = 'C:\HOST_A_cert.cer'  
    GO  
    ```  
  
4.  Conceda permissão CONNECT no logon para o ponto de extremidade de espelhamento remoto.  
  
    ```  
    GRANT CONNECT ON ENDPOINT::Endpoint_Mirroring TO [HOST_A_login];  
    GO  
    ```  
  
> [!IMPORTANT]  
>  Se tiver a intenção de executar em modo de alta segurança com failover automático, você deve repetir as mesmas etapas de configuração para configurar a testemunha para conexões de saída e de entrada. Quando uma testemunha está envolvida, a configuração de conexões de entrada e de saída requer a configuração de logons e usuários para a testemunha nos dois parceiros, e vice-versa.  
  
 Para obter mais informações, consulte [Permitir que um ponto de extremidade de espelhamento de banco de dados use certificados para conexões de entrada &#40;Transact-SQL&#41;](database-mirroring-use-certificates-for-inbound-connections.md).  
  
### <a name="creating-the-mirror-database"></a>Criando o banco de dados espelho  
 Para obter informações sobre como criar um banco de dados espelho, consulte [Preparar um banco de dados espelho para espelhamento &#40;SQL Server&#41;](prepare-a-mirror-database-for-mirroring-sql-server.md).  
  
###  <a name="configuring-the-mirroring-partners"></a><a name="ConfigureMirroringPartners"></a>Configurando os parceiros de espelhamento  
  
1.  Na instância de servidor espelho em HOST_B, defina a instância de servidor em HOST_A como o parceiro (fazendo dele a instância de servidor principal inicial). Substitua um endereço de rede válido por `TCP://HOST_A.Mydomain.Corp.Adventure-Works``.com:7024`. Para obter mais informações, consulte [Especificar um endereço de rede do servidor &#40;Espelhamento de banco de dados&#41;](specify-a-server-network-address-database-mirroring.md).  
  
    ```  
    --At HOST_B, set server instance on HOST_A as partner (principal server):  
    ALTER DATABASE AdventureWorks   
        SET PARTNER = 'TCP://HOST_A.Mydomain.Corp.Adventure-Works.com:7024';  
    GO  
    ```  
  
2.  Na instância de servidor principal em HOST_A, defina a instância de servidor em HOST_B como o parceiro (fazendo dele a instância de servidor espelho inicial). Substitua um endereço de rede válido por `TCP://HOST_B.Mydomain.Corp.Adventure-Works.com:7024`.  
  
    ```  
    --At HOST_A, set server instance on HOST_B as partner (mirror server).  
    ALTER DATABASE AdventureWorks   
        SET PARTNER = 'TCP://HOST_B.Mydomain.Corp.Adventure-Works.com:7024';  
    GO  
    ```  
  
3.  Esse exemplo assume que a sessão estará sendo executada em modo de alto desempenho. Para configurar esta sessão para modo de alto desempenho, na instância de servidor principal (em HOST_A), defina segurança de transação como OFF.  
  
    ```  
    --Change to high-performance mode by turning off transacton safety.  
    ALTER DATABASE AdventureWorks   
        SET PARTNER SAFETY OFF  
    GO  
    ```  
  
    > [!NOTE]  
    >  Se você pretende executar em modo de alta segurança com failover automático, deixe a segurança da transação definida como completa (a configuração padrão) e adicione a testemunha assim que possível após a execução da segunda instrução SET Partner **'*`partner_server`*'** . Observe que a testemunha deve ser configurada primeiro para conexões de saída e de entrada.  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> Tarefas relacionadas  
  
-   [Preparar um banco de dados espelho para espelhamento &#40;SQL Server&#41;](prepare-a-mirror-database-for-mirroring-sql-server.md)  
  
-   [Permitir que um ponto de extremidade de espelhamento de banco de dados use certificados para conexões de entrada &#40;Transact-SQL&#41;](database-mirroring-use-certificates-for-inbound-connections.md)  
  
-   [Permitir que um ponto de extremidade de espelhamento de banco de dados use certificados para conexões de saída &#40;Transact-SQL&#41;](database-mirroring-use-certificates-for-outbound-connections.md)  
  
-   [Gerenciamento de logons e trabalhos após a troca de função &#40;SQL Server&#41;](../../sql-server/failover-clusters/management-of-logins-and-jobs-after-role-switching-sql-server.md)  
  
-   [Gerenciar metadados ao disponibilizar um banco de dados em outra instância do servidor &#40;SQL Server&#41;](../../relational-databases/databases/manage-metadata-when-making-a-database-available-on-another-server.md) (SQL Server)  
  
-   [Solução de problemas de configuração de espelhamento de banco de dados &#40;SQL Server&#41;](troubleshoot-database-mirroring-configuration-sql-server.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Segurança de transporte para espelhamento de banco de dados e Grupos de Disponibilidade AlwaysOn &#40;SQL Server&#41;](transport-security-database-mirroring-always-on-availability.md)   
 [Especifique um endereço de rede de servidor &#40;espelhamento de banco de dados&#41;](specify-a-server-network-address-database-mirroring.md)   
 [O ponto de extremidade de espelhamento de banco de dados &#40;SQL Server&#41;](the-database-mirroring-endpoint-sql-server.md)   
 [Usar certificados para um ponto de extremidade de espelhamento de banco de dados &#40;Transact-SQL&#41;](use-certificates-for-a-database-mirroring-endpoint-transact-sql.md)   
 [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)   
 [Central de segurança do Mecanismo de Banco de Dados do SQL Server e Banco de Dados SQL do Azure](../../relational-databases/security/security-center-for-sql-server-database-engine-and-azure-sql-database.md)  
  
  
