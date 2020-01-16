---
title: Configurar uma testemunha
description: 'Descreve como configurar uma testemunha de espelhamento de banco de dados com a autenticação do Windows usando o Transact-SQL. '
ms.custom: seo-lt-2019
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- witness [SQL Server], establishing
- Windows authentication [SQL Server]
- database mirroring [SQL Server], witness
ms.assetid: bf5e87df-91a4-49f9-ae88-2a6dcf644510
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 4616e2c10657e1af8db9c706c518fdf690618303
ms.sourcegitcommit: f8cf8cc6650a22e0b61779c20ca7428cdb23c850
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/04/2019
ms.locfileid: "74822303"
---
# <a name="add-a-database-mirroring-witness-using-windows-authentication-transact-sql"></a>Adicionar uma testemunha de espelhamento de banco de dados usando a Autenticação do Windows (Transact-SQL)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Para definir uma testemunha para um banco de dados, o proprietário do banco de dados nomeia uma instância do Mecanismo de Banco de Dados para a função de servidor testemunha. A instância do servidor testemunha pode ser executada no mesmo computador que a instância do servidor principal ou espelho, mas isso reduz a robustez de failover automático substancialmente.  
  
 A localização da testemunha em um computador separado é altamente recomendável. Uma determinada instância do servidor pode participar de várias sessões de espelhamento de banco de dados simultâneos com os mesmos ou diferentes parceiros. Um determinado servidor pode ser um parceiro em algumas sessões e uma testemunha em outras sessões.  
  
 A testemunha é planejada exclusivamente para um modo de alta segurança com failover automático. Antes de você definir uma testemunha, recomendamos enfaticamente que verifique se a propriedade SAFETY está definida atualmente como FULL.  
  
> [!IMPORTANT]  
>  É recomendável configurar um espelhamento de banco de dados fora do horário de pico, pois a configuração pode afetar o desempenho.  
  
## <a name="establish-a-witness"></a>Estabelecer uma testemunha  
  
1.  Na instância do servidor testemunha, verifique se existe um ponto de extremidade para espelhamento de banco de dados. Independentemente do número de sessões de espelhamento com suporte, a instância do servidor só deve ter um ponto de extremidade do espelhamento de banco de dados. Se você pretende usar essa instância de servidor exclusivamente como testemunha nas sessões de espelhamento de banco de dados, atribua a função de testemunha ao ponto de extremidade (ROLE **=** WITNESS). Se você também pretender usar essa instância do servidor como testemunha em uma ou mais sessões de espelhamento de banco de dados, atribua a função do ponto de extremidade como ALL.  
  
     Para executar uma instrução SET WITNESS, a sessão de espelhamento de banco de dados já deve ter começado (entre parceiros), e o STATE do ponto de extremidade da testemunha deve estar definido como STARTED.  
  
     Para saber se uma instância do servidor testemunha tem seu ponto de extremidade do espelhamento de banco de dados e conhecer sua função e estado, nessa instância, use a seguinte instrução Transact-SQL:  
  
    ```  
    SELECT role_desc, state_desc FROM sys.database_mirroring_endpoints  
    ```  
  
    > [!IMPORTANT]  
    >  Se um ponto de extremidade do espelhamento de banco de dados já existir e estiver em uso, recomendamos que você use esse ponto de extremidade para cada sessão na instância do servidor. Descartando um ponto de extremidade em uso atrapalha o funcionamento das conexões das sessões existentes. Se uma testemunha foi definida para uma sessão, descartar o ponto de extremidade do espelhamento de banco de dados poderá fazer com que o servidor principal daquela sessão perca quorum; se isso acontecer, o banco de dados será colocado offline e seus usuários serão desconectados. Para obter mais informações, confira [Quorum: Como uma testemunha afeta a disponibilidade do banco de dados &#40;Espelhamento de Banco de Dados&#41;](../../database-engine/database-mirroring/quorum-how-a-witness-affects-database-availability-database-mirroring.md).  
  
     Se a testemunha não tiver um ponto de extremidade, veja [Criar um ponto de extremidade de espelhamento de banco de dados para a Autenticação do Windows &#40;SQL Server&#41;](../../database-engine/database-mirroring/create-a-database-mirroring-endpoint-for-windows-authentication-transact-sql.md).  
  
2.  Se as instâncias do parceiro estiverem sendo executadas em contas de usuário de domínio diferentes, crie um logon para cada uma das diferentes contas no banco de dados mestre de cada instância. Para obter mais informações, consulte [Permitir o acesso à rede a um ponto de extremidade de espelhamento de banco de dados usando a Autenticação do Windows &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-allow-network-access-windows-authentication.md).  
  
3.  Conecte-se ao servidor principal e emita a seguinte instrução:  
  
     ALTER DATABASE *<database_name>* SET WITNESS **=** _<server_network_address>_  
  
     em que *<database_name>* é o nome do banco de dados a ser espelhado (esse nome é o mesmo em ambos os parceiros), e *<server_network_address>* é o endereço de rede de servidor da instância de servidor testemunha.  
  
     A sintaxe para um endereço de rede do servidor é a seguinte:  
  
     TCP<b>://</b> _\<system-address>_ <b>:</b> _\<port>_  
  
     em que \<*system-address>* é uma cadeia de caracteres que identifica sem ambiguidade o sistema de computador de destino e \<*port>* é o número da porta usada pelo ponto de extremidade de espelhamento da instância do servidor parceiro. Para obter mais informações, consulte [Especificar um endereço de rede do servidor &#40;Espelhamento de banco de dados&#41;](../../database-engine/database-mirroring/specify-a-server-network-address-database-mirroring.md).  
  
     Por exemplo, na instância do servidor principal, a seguinte instrução ALTER DATABASE define a testemunha. O nome do banco de dados é **AdventureWorks**, o endereço do sistema é DBSERVER3 (o nome do sistema testemunha) e a porta usada pelo ponto de extremidade de espelhamento do banco de dados da testemunha é `7022`:  
  
    ```  
    ALTER DATABASE AdventureWorks   
      SET WITNESS = 'TCP://DBSERVER3:7022'  
    ```  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir estabelece uma testemunha do espelhamento de dados. Na instância do servidor testemunha (instância padrão em `WITNESSHOST4`):  
  
1.  Crie um ponto de extremidade para essa instância do servidor para a função WITNESS usando apenas a porta `7022`.  
  
    ```  
    CREATE ENDPOINT Endpoint_Mirroring  
        STATE=STARTED   
        AS TCP (LISTENER_PORT=7022)   
        FOR DATABASE_MIRRORING (ROLE=WITNESS)  
    GO  
    ```  
  
2.  Crie um logon para conta de usuário de domínio de instâncias de parceiro, se diferente; por exemplo, suponha que a testemunha está sendo executada como `SOMEDOMAIN\witnessuser`, mas os parceiros estão sendo executados como `MYDOMAIN\dbousername`. Crie um logon para os parceiros, como segue:  
  
    ```  
    --Create a login for the partner server instances,  
    --which are both running as MYDOMAIN\dbousername:  
    USE master ;  
    GO  
    CREATE LOGIN [MYDOMAIN\dbousername] FROM WINDOWS ;  
    GO  
    --Grant connect permissions on endpoint to login account   
    --of partners  
    GRANT CONNECT ON ENDPOINT::Endpoint_Mirroring TO [MYDOMAIN\dbousername];  
    GO  
    ```  
  
3.  Em cada uma das instâncias de servidor de parceiro, crie um logon para a instância do servidor testemunha:  
  
    ```  
    --Create a login for the witness server instance,  
    --which is running as SOMEDOMAIN\witnessuser:  
    USE master ;  
    GO  
    CREATE LOGIN [SOMEDOMAIN\witnessuser] FROM WINDOWS ;  
    GO  
    --Grant connect permissions on endpoint to login account   
    --of partners  
    GRANT CONNECT ON ENDPOINT::Endpoint_Mirroring TO [SOMEDOMAIN\witnessuser];  
    GO  
    ```  
  
4.  No servidor principal, defina a testemunha (que está em `WITNESSHOST4`):  
  
    ```  
    ALTER DATABASE AdventureWorks   
        SET WITNESS =   
        'TCP://WITNESSHOST4:7022'  
    GO  
    ```  
  
> [!NOTE]  
>  O endereço de rede do servidor indica a instância do servidor de destino pelo número da porta que mapeia para o ponto de extremidade do espelhamento da instância.  
  
 Para obter um exemplo completo mostrando a configuração da segurança, o preparo do banco de dados espelho, a configuração de parceiros e a adição de uma testemunha, consulte [Configurando o espelhamento de banco de dados &#40;SQL Server&#41;](../../database-engine/database-mirroring/setting-up-database-mirroring-sql-server.md).  
  
## <a name="see-also"></a>Consulte Também  
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [Permitir o acesso à rede a um ponto de extremidade de espelhamento de banco de dados usando a Autenticação do Windows &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-allow-network-access-windows-authentication.md)   
 [Criar um ponto de extremidade de espelhamento de banco de dados para a Autenticação do Windows &#40;Transact-SQL&#41;](../../database-engine/database-mirroring/create-a-database-mirroring-endpoint-for-windows-authentication-transact-sql.md)   
 [Estabelecer uma sessão de espelhamento de banco de dados com a Autenticação do Windows &#40;Transact-SQL&#41;](../../database-engine/database-mirroring/database-mirroring-establish-session-windows-authentication.md)   
 [Remover a testemunha de uma sessão de espelhamento de banco de dados &#40;SQL Server&#41;](../../database-engine/database-mirroring/remove-the-witness-from-a-database-mirroring-session-sql-server.md)   
 [Testemunha de espelhamento de banco de dados](../../database-engine/database-mirroring/database-mirroring-witness.md)  
  
  
