---
title: Configurar o Mecanismo de Banco de Dados para escutar em várias portas TCP | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- ports [SQL Server], multiple
- TDS
- listen on multiple ports
- endpoints [SQL Server], TDS
- adding ports
- tabular data stream
- multiple ports
ms.assetid: 8e955033-06ef-403f-b813-3d8241b62f1f
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 3055750ac7f52c4dfaaae3cef94021d9d024a50a
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "68012724"
---
# <a name="configure-the-database-engine-to-listen-on-multiple-tcp-ports"></a>Configurar o Mecanismo de Banco de Dados para escuta em várias portas TCP
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Este tópico descreve como configurar o [!INCLUDE[ssDE](../../includes/ssde-md.md)] para escutar em diversas portas TCP no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o SQL Server Configuration Manager. Quando TCP/IP está habilitado para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o [!INCLUDE[ssDE](../../includes/ssde-md.md)] escutará conexões de entrada em um ponto de conexão que consiste em um endereço IP e número de porta TCP. Os procedimentos a seguir criam um ponto de extremidade de protocolo TDS, de forma que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] escutará em uma porta TCP adicional.  
  
 Possíveis razões para criar um segundo ponto de extremidade de protocolo TDS são:  
  
-   Aumentar a segurança configurando o firewall para restringir o acesso ao ponto de extremidade padrão para computadores cliente locais em uma sub-rede específica. Manter o acesso à Internet do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para que sua equipe de suporte crie um novo ponto de extremidade que o firewall expõe para a Internet, restringindo os direitos de conexão a este ponto de extremidade para sua equipe de suporte ao servidor.  
  
-   Ajustar as conexões para processadores específicos ao usar Acesso de Memória Não uniforme (NUMA).  
  
 A configuração de um ponto de extremidade de protocolo TDS consiste nas seguintes etapas, que podem ser efetuadas em qualquer ordem:  
  
-   Crie o ponto de extremidade de protocolo TDS para a porta TCP e restaure o acesso ao ponto de extremidade padrão, se apropriado.  
  
-   Conceda acesso ao ponto de extremidade para as entidades de servidor desejadas.  
  
-   Especifique o número da porta TCP para o endereço IP selecionado.  
  
 Para obter mais informações sobre as configurações padrão do Firewall do Windows e uma descrição das portas TCP que afetam o Mecanismo de Banco de Dados, o Analysis Services, o Reporting Services e o Integration Services, veja [Configurar o Firewall do Windows para permitir acesso ao SQL Server](../../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md).  
  
##  <a name="SSMSProcedure"></a>  
  
#### <a name="to-create-a-tds-endpoint"></a>Criar um ponto de extremidade de protocolo TDS  
  
-   Emita a seguinte instrução para criar um ponto de extremidade chamado **CustomConnection** para a porta 1500 de todos os endereços TCP disponíveis no servidor.  
  
    ```  
    USE master;  
    GO  
    CREATE ENDPOINT [CustomConnection]  
    STATE = STARTED  
    AS TCP  
       (LISTENER_PORT = 1500, LISTENER_IP =ALL)  
    FOR TSQL() ;  
    GO  
    ```  
  
 Ao criar um ponto de extremidade [!INCLUDE[tsql](../../includes/tsql-md.md)] novo, as permissões de conexão para o grupo **público** são revogadas para o ponto de extremidade de protocolo TDS padrão. Se o acesso ao grupo **público** for necessário para o ponto de extremidade padrão, aplique novamente esta permissão usando a instrução `GRANT CONNECT ON ENDPOINT::[TSQL Default TCP] to [public];` .  
  
#### <a name="to-grant-access-to-the-endpoint"></a>Conceder acesso ao ponto de extremidade  
  
-   Emita a seguinte instrução para conceder acesso ao ponto de extremidade **CustomConnection** para o grupo SQLSupport no domínio da corporação.  
  
    ```  
    GRANT CONNECT ON ENDPOINT::[CustomConnection] to [corp\SQLSupport] ;  
    GO  
    ```  
  
#### <a name="to-configure-the-sql-server-database-engine-to-listen-on-an-additional-tcp-port"></a>Configurar o Mecanismo de Banco de Dados do SQL Server para efetuar a escuta em uma porta TCP adicional  
  
1.  No SQL Server Configuration Manager, expanda **Configuração de Rede do SQL Server** e clique em **Protocolos para** _<instance_name>_ .  
  
2.  Expanda **Protocolos para** _<instance_name>_ e clique em **TCP/IP**.  
  
3.  No painel direito, clique com o botão direito do mouse em cada endereço IP desabilitado que você deseja habilitar e clique em **Habilitar**.  
  
4.  Clique com o botão direito do mouse em **IPAll**e clique em **Propriedades**.  
  
5.  Na caixa **Porta TCP** , digite as portas nas quais deseja que o [!INCLUDE[ssDE](../../includes/ssde-md.md)] efetue a escura, separadas por vírgulas. Em nosso exemplo, se a porta padrão 1433 estiver listada, digite **,1500** para que a caixa leia **1433,1500**e clique em **OK**.  
  
    > [!NOTE]  
    >  Se você não estiver habilitando a porta em todos os endereços IP, configure a porta adicional na caixa de propriedades para apenas o endereço desejado. Em seguida, no painel de console, clique com o botão direito do mouse em **TCP/IP**, clique em **Propriedades**e, na caixa **Escutar Tudo** , selecione **Não**.  
  
6.  No painel esquerdo, clique em **Serviços do SQL Server**.  
  
7.  No painel direito, clique com o botão direito do mouse em **SQL Server** _<instance_name>_ e clique em **Reiniciar**.  
  
     Quando o [!INCLUDE[ssDE](../../includes/ssde-md.md)] reiniciar, o log de erros listará as portas nas quais o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está escutando.  
  
#### <a name="to-connect-to-the-new-endpoint"></a>Conectar-se ao novo ponto de extremidade  
  
-   Emita a instrução a seguir para se conectar ao ponto de extremidade **CustomConnection** da instância padrão do SQL Server no servidor chamado ACCT, usando uma conexão confiável, e assumindo que o usuário é membro do grupo [corp\SQLSupport].  
  
    ```  
    sqlcmd -SACCT,1500  
    ```  
  
## <a name="see-also"></a>Consulte Também  
 [CREATE ENDPOINT &#40;Transact-SQL&#41;](../../t-sql/statements/create-endpoint-transact-sql.md)   
 [DROP ENDPOINT &#40;Transact-SQL&#41;](../../t-sql/statements/drop-endpoint-transact-sql.md)   
 [Permissões GRANT do ponto de extremidade &#40;Transact-SQL&#41;](../../t-sql/statements/grant-endpoint-permissions-transact-sql.md)   
 [Mapear portas TCP/IP para nós NUMA &#40;SQL Server&#41;](../../database-engine/configure-windows/map-tcp-ip-ports-to-numa-nodes-sql-server.md)  
  
  
