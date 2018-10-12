---
title: Espelhamento de Banco de Dados – estabelecer a sessão – Autenticação do Windows | Microsoft Docs
ms.custom: ''
ms.date: 05/17/2016
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Windows authentication [SQL Server]
- database mirroring [SQL Server], security
ms.assetid: 143c68a5-589f-4e7f-be59-02707e1a430a
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: fd3762adabe4098d48bfd5352a0a159672b76ecd
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47599094"
---
# <a name="database-mirroring---establish-session---windows-authentication"></a>Espelhamento de Banco de Dados – estabelecer a sessão – Autenticação do Windows
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Em vez disso, use [!INCLUDE[ssHADR](../../includes/sshadr-md.md)].  
  
 Depois que o banco de dados espelho estiver preparado (consulte [Preparar um banco de dados espelho para espelhamento &#40;SQL Server&#41;](../../database-engine/database-mirroring/prepare-a-mirror-database-for-mirroring-sql-server.md)), você poderá estabelecer uma sessão de espelhamento de banco de dados. As instâncias do servidor principal, espelho e testemunha devem ser instâncias de servidor separadas que deveriam estar em sistemas host separados.  
  
> [!IMPORTANT]  
>  Recomendamos que você configure um espelhamento de banco de dados em períodos de pouca atividade porque a configuração de espelhamento pode comprometer o desempenho.  
  
> [!NOTE]  
>  Uma determinada instância do servidor pode participar de várias sessões de espelhamento de banco de dados simultâneas com os mesmos parceiros ou diferentes. Uma instância do servidor pode ser um parceiro em algumas sessões e uma testemunha em outras sessões. A instância do servidor espelho deve estar executando a mesma edição do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] como a instância do servidor principal. O espelhamento de banco de dados não está disponível em todas as edições do [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter uma lista de recursos com suporte nas edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte [Recursos com suporte nas edições do SQL Server 2016](~/sql-server/editions-and-supported-features-for-sql-server-2016.md). Além disso, é altamente recomendável que elas sejam executadas em sistemas comparáveis que possam controlar cargas de trabalho idênticas.  
  
### <a name="to-establish-a-database-mirroring-session"></a>Para estabelecer uma sessão de espelhamento de banco de dados  
  
1.  Crie o banco de dados espelho. Para obter mais informações, consulte [Preparar um banco de dados espelho para espelhamento &#40;SQL Server&#41;](../../database-engine/database-mirroring/prepare-a-mirror-database-for-mirroring-sql-server.md).  
  
2.  Defina a segurança em cada instância do servidor.  
  
     Cada instância do servidor em uma sessão de espelhamento de banco de dados exige um ponto de extremidade de espelhamento de banco de dados. Se o ponto de extremidade não existir, você deve criá-lo.  
  
    > [!NOTE]  
    >  A forma de autenticação usada para o espelhamento de banco de dados por uma instância do servidor é uma propriedade do ponto de extremidade de espelhamento de banco de dados. Dois tipos de segurança de transporte estão disponíveis para o espelhamento de banco de dados: autenticação do Windows ou autenticação com certificado. Para obter mais informações, consulte [Segurança de transporte para espelhamento de banco de dados e grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../database-engine/database-mirroring/transport-security-database-mirroring-always-on-availability.md).  
  
     Em cada servidor parceiro, assegure que existe um ponto de extremidade de espelhamento de banco de dados. Independentemente do número de sessões de espelhamento a dar suporte, a instância do servidor só pode ter um ponto de extremidade de espelhamento de banco de dados. Se você pretende usar essa instância do servidor exclusivamente para parceiros em sessões de espelhamento de banco de dados, você poderá atribuir a função de parceiro ao ponto de extremidade (ROLE**=** PARTNER). Se você também pretende usar essa instância do servidor exclusivamente para testemunhas em sessões de espelhamento de banco de dados, você poderá definir o papel de parceiro ao ponto de extremidade como ALL.  
  
     Para executar uma instrução SET PARTNER, o STATE dos pontos de extremidade de ambos os parceiros deve ser definido como STARTED.  
  
     Para saber se uma instância do servidor tem um ponto de extremidade de espelhamento de banco de dados e saber sua função e estado, nessa instância, use a seguinte instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] :  
  
    ```  
    SELECT role_desc, state_desc FROM sys.database_mirroring_endpoints  
    ```  
  
    > [!IMPORTANT]  
    >  Não reconfigure um ponto de extremidade de espelhamento de banco de dados em uso. Se um ponto de extremidade do espelhamento de banco de dados já existir e estiver em uso, recomendamos que você use esse ponto de extremidade para cada sessão na instância do servidor. Cancelando um ponto de extremidade em uso pode fazer o ponto de extremidade reinicializar, interrompendo as conexões das sessões existentes, que podem aparecer como um erro às outras instâncias do servidor. Isso é particularmente importante em modo de alta segurança com failover automático no qual a reconfiguração de um ponto de extremidade em um parceiro poderia provocar um failover. Além disso, se uma testemunha foi definida para uma sessão, cancelar o ponto de extremidade de espelhamento de banco de dados poderá fazer com que o servidor principal daquela sessão perca quorum; se isso acontecer, o banco de dados será colocado offline e seus usuários serão desconectados. Para obter mais informações, consulte [Quorum: como uma testemunha afeta a disponibilidade do banco de dados &#40;Espelhamento de Banco de Dados&#41;](../../database-engine/database-mirroring/quorum-how-a-witness-affects-database-availability-database-mirroring.md).  
  
     Se o parceiro não tiver um ponto de extremidade, consulte [Criar um ponto de extremidade de espelhamento de banco de dados para a Autenticação do Windows &#40;Transact-SQL&#41;](../../database-engine/database-mirroring/create-a-database-mirroring-endpoint-for-windows-authentication-transact-sql.md).  
  
3.  Se as instâncias de servidor estiverem sendo executadas em contas do usuário de domínio diferentes, cada uma exigirá um logon no banco de dados **mestre** dos outros. Se o logon não existir, você deve criá-lo. Para obter mais informações, consulte [Permitir o acesso à rede a um ponto de extremidade de espelhamento de banco de dados usando a Autenticação do Windows &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-allow-network-access-windows-authentication.md).  
  
4.  Para definir o servidor principal como parceiro no banco de dados espelho, conecte-se ao servidor espelho e emita a seguinte instrução:  
  
     ALTER DATABASE *\<database_name\>* SET PARTNER **=**_\<server\_network\_address\>_  
  
     em que _\<database\_name\>_ é o nome do banco de dados a ser espelhado (esse nome é o mesmo em ambos os parceiros) e _\<server\_network\_address\>_ é o endereço de rede de servidor do servidor principal.  
  
     A sintaxe para um endereço de rede do servidor é a seguinte:  
  
     TCP<b>\://</b>_\<system-address\>_<b>\:</b>_\<port\>_  
  
     em que _\<system-address>_ é uma cadeia de caracteres que identifica sem ambiguidade o sistema de computador de destino e _\<port>_ é o número da porta usada pelo ponto de extremidade de espelhamento da instância do servidor parceiro. Para obter mais informações, consulte [Especificar um endereço de rede do servidor &#40;Espelhamento de banco de dados&#41;](../../database-engine/database-mirroring/specify-a-server-network-address-database-mirroring.md).  
  
     Por exemplo, na instância do servidor espelho, a seguinte instrução ALTER DATABASE define o parceiro como a instância do servidor principal original. O nome de banco de dados é **AdventureWorks**, o endereço de sistema é DBSERVER1 - o nome de sistema do parceiro - e a porta usada pelo ponto de extremidade de espelhamento de banco de dados do parceiro é 7022:  
  
    ```  
    ALTER DATABASE AdventureWorks   
       SET PARTNER = 'TCP://DBSERVER1:7022'  
    ```  
  
     Essa instrução prepara o servidor espelho para formar uma sessão quando é contatado pelo servidor principal.  
  
5.  Para definir o servidor espelho como parceiro no banco de dados principal, conecte-se ao servidor principal e emita a seguinte instrução:  
  
     ALTER DATABASE _\<database\_name\>_ SET PARTNER **=**_\<server\_network\_address\>_  
  
     Para obter mais informações, consulte a etapa 4.  
  
     Por exemplo, na instância do servidor principal, a seguinte instrução ALTER DATABASE define o parceiro como a instância do servidor espelho original. O nome do banco de dados é **AdventureWorks**, o endereço do sistema é DBSERVER2 - o nome de sistema do parceiro - e a porta usada pelo ponto de extremidade de espelhamento de banco de dados do parceiro é 7025:  
  
    ```  
    ALTER DATABASE AdventureWorks SET PARTNER = 'TCP://DBSERVER2:7022'  
    ```  
  
     Inserir essa instrução no servidor principal inicia a sessão de espelhamento de banco de dados.  
  
6.  Por padrão, uma sessão é definida como segurança de transação completa (SAFETY é definido como FULL), que inicia a sessão no modo síncrono de segurança alta, sem failover automático. Você pode reconfigurar a sessão para ser executada em modo de segurança alta com failover automático ou em modo assíncrono de alto desempenho, como se segue:  
  
    -   **Modo de segurança alta com failover automático**  
  
         Se você quiser que uma sessão de modo de segurança alta dê suporte a failover automático, acrescente uma instância do servidor testemunha. Para obter mais informações, consulte [Adicionar uma testemunha de espelhamento de banco de dados usando a Autenticação do Windows &#40;Transact-SQL&#41;](../../database-engine/database-mirroring/add-a-database-mirroring-witness-using-windows-authentication-transact-sql.md).  
  
    -   **Modo de alto desempenho**  
  
         Alternativamente, se você não quiser failover automático e preferir enfatizar o desempenho em vez da disponibilidade, desative a segurança de transação. Para obter mais informações, consulte [Alterar a segurança da transação em uma sessão de espelhamento de banco de dados &#40;Transact-SQL&#41;](../../database-engine/database-mirroring/change-transaction-safety-in-a-database-mirroring-session-transact-sql.md).  
  
        > [!NOTE]  
        >  Em modo de alto desempenho, WITNESS deverá ser definido como OFF. Para obter mais informações, consulte [Quorum: como uma testemunha afeta a disponibilidade do banco de dados &#40;Espelhamento de Banco de Dados&#41;](../../database-engine/database-mirroring/quorum-how-a-witness-affects-database-availability-database-mirroring.md).  
  
## <a name="example"></a>Exemplo  
  
> [!NOTE]  
>  O exemplo seguinte estabelece uma sessão de espelhamento de banco de dados entre parceiros para um banco de dados espelho existente. Para obter informações sobre como criar um banco de dados espelho, consulte [Preparar um banco de dados espelho para espelhamento &#40;SQL Server&#41;](../../database-engine/database-mirroring/prepare-a-mirror-database-for-mirroring-sql-server.md).  
  
 O exemplo mostra as etapas básicas para criar uma sessão de espelhamento de banco de dados sem uma testemunha. Os dois parceiros são as instâncias de servidor padrão em dois sistemas de computador (PARTNERHOST1 e PARTNERHOST5). As duas instâncias do parceiro executam a mesma conta do usuário no domínio Windows (MYDOMAIN\dbousername).  
  
1.  Na instância do servidor principal (instância padrão em PARTNERHOST1), crie um ponto de extremidade dê suporte a todas as funções que usam a porta 7022:  
  
    ```  
    --create an endpoint for this instance  
    CREATE ENDPOINT Endpoint_Mirroring  
        STATE=STARTED   
        AS TCP (LISTENER_PORT=7022)   
        FOR DATABASE_MIRRORING (ROLE=ALL)  
    GO  
    --Partners under same domain user; login already exists in master.  
    ```  
  
    > [!NOTE]  
    >  Para encontrar um exemplo de como configurar um logon, consulte [Permitir o acesso à rede a um ponto de extremidade de espelhamento de banco de dados usando a Autenticação do Windows &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-allow-network-access-windows-authentication.md).  
  
2.  Na instância do servidor espelho (instância padrão em PARTNERHOST5), crie um ponto de extremidade que dê suporte a todas as funções que usam a porta 7022:  
  
    ```  
    --create an endpoint for this instance  
    CREATE ENDPOINT Endpoint_Mirroring  
        STATE=STARTED   
        AS TCP (LISTENER_PORT=7022)   
        FOR DATABASE_MIRRORING (ROLE=ALL)  
    GO  
    --Partners under same domain user; login already exists in master.  
    ```  
  
3.  Na instância do servidor principal (em PARTNERHOST1), faça o backup do banco de dados:  
  
    ```  
    BACKUP DATABASE AdventureWorks   
        TO DISK = 'C:\AdvWorks_dbmirror.bak'   
        WITH FORMAT  
    GO  
    ```  
  
4.  Na instância do servidor espelho (em `PARTNERHOST5`), restaure o banco de dados:  
  
    ```  
    RESTORE DATABASE AdventureWorks   
        FROM DISK = 'Z:\AdvWorks_dbmirror.bak'   
        WITH NORECOVERY  
    GO  
    ```  
  
5.  Depois que você criar o backup de banco de dados completo, você deve criar um backup do log no banco de dados principal. Por exemplo, a seguinte instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] faz o backup do log ao mesmo arquivo usado pelo backup de banco de dados precedente:  
  
    ```  
    BACKUP LOG AdventureWorks   
        TO DISK = 'C:\AdventureWorks.bak'   
    GO  
    ```  
  
6.  Antes de poder iniciar o espelhamento, é necessário aplicar o backup de log exigido (e qualquer backup de log subsequente).  
  
     Por exemplo, a seguinte instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] restaura o primeiro log de C:\AdventureWorks.bak:  
  
    ```  
    RESTORE LOG AdventureWorks   
        FROM DISK = 'C:\ AdventureWorks.bak'   
        WITH FILE=1, NORECOVERY  
    GO  
    ```  
  
7.  Na instância do servidor espelho, defina a instância do servidor em PARTNERHOST1 como o parceiro (fazendo dele o servidor principal inicial):  
  
    ```  
    USE master;  
    GO  
    ALTER DATABASE AdventureWorks   
        SET PARTNER =   
        'TCP://PARTNERHOST1:7022'  
    GO  
    ```  
  
    > [!IMPORTANT]  
    >  Por padrão, uma sessão de espelhamento de banco de dados é executada modo síncrono, o que depende de ter uma transação de segurança completa (SAFETY é definido como FULL). Para fazer com que uma sessão seja executada em modo assíncrono, de alto desempenho, defina SAFETY como OFF. Para obter mais informações, consulte [Database Mirroring Operating Modes](../../database-engine/database-mirroring/database-mirroring-operating-modes.md).  
  
8.  Na instância do servidor principal, defina a instância do servidor em `PARTNERHOST5` como o parceiro (fazendo dele o servidor espelho inicial):  
  
    ```  
    USE master;  
    GO  
    ALTER DATABASE AdventureWorks   
        SET PARTNER = 'TCP://PARTNERHOST5:7022'  
    GO  
    ```  
  
9. Opcionalmente, se você pretender usar modo de segurança alta com failover automático, configure a instância do servidor testemunha. Para obter mais informações, consulte [Adicionar uma testemunha de espelhamento de banco de dados usando a Autenticação do Windows &#40;Transact-SQL&#41;](../../database-engine/database-mirroring/add-a-database-mirroring-witness-using-windows-authentication-transact-sql.md).  
  
> [!NOTE]  
>  Para obter um exemplo completo mostrando a configuração da segurança, o preparo do banco de dados espelho, a configuração de parceiros e a adição de uma testemunha, consulte [Configurando o espelhamento de banco de dados &#40;SQL Server&#41;](../../database-engine/database-mirroring/setting-up-database-mirroring-sql-server.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Configurando o espelhamento de banco de dados &#40;SQL Server&#41;](../../database-engine/database-mirroring/setting-up-database-mirroring-sql-server.md)   
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [Permitir o acesso à rede a um ponto de extremidade de espelhamento de banco de dados usando a Autenticação do Windows &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-allow-network-access-windows-authentication.md)   
 [Preparar um banco de dados espelho para espelhamento &#40;SQL Server&#41;](../../database-engine/database-mirroring/prepare-a-mirror-database-for-mirroring-sql-server.md)   
 [Criar um ponto de extremidade de espelhamento de banco de dados para a Autenticação do Windows &#40;Transact-SQL&#41;](../../database-engine/database-mirroring/create-a-database-mirroring-endpoint-for-windows-authentication-transact-sql.md)   
 [Espelhamento de banco de dados e envio de logs &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-and-log-shipping-sql-server.md)   
 [Espelhamento de banco de dados &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md)   
 [Espelhamento e replicação de banco de dados &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-and-replication-sql-server.md)   
 [Configurando o espelhamento de banco de dados &#40;SQL Server&#41;](../../database-engine/database-mirroring/setting-up-database-mirroring-sql-server.md)   
 [Especificar um endereço de rede do servidor &#40;espelhamento de banco de dados&#41;](../../database-engine/database-mirroring/specify-a-server-network-address-database-mirroring.md)   
 [Modos de operação de espelhamento de banco de dados](../../database-engine/database-mirroring/database-mirroring-operating-modes.md)  
  
  

