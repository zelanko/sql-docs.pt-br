---
title: Conectar-se a um ouvinte do grupo de disponibilidade
description: Contém informações sobre como se conectar a um ouvinte de grupo de disponibilidade Always On, por exemplo, como se conectar à réplica primária e a uma réplica secundária somente leitura ou usar TLS/SSL e Kerberos.
ms.custom: contperfq1
ms.date: 02/27/2020
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: how-to
helpviewer_keywords:
- Availability Groups [SQL Server], listeners
- read-only routing
- read-intent connections [AlwaysOn Availability Groups]
- Availability Groups [SQL Server], configuring
- Availability Groups [SQL Server], read-only routing
- Availability Groups [SQL Server], client connectivity
ms.assetid: 76fb3eca-6b08-4610-8d79-64019dd56c44
author: cawrites
ms.author: chadam
ms.openlocfilehash: b26671e24cb0419f6737d1f41a5eb2a168dcfe7b
ms.sourcegitcommit: 54cd97a33f417432aa26b948b3fc4b71a5e9162b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/13/2020
ms.locfileid: "94584209"
---
# <a name="connect-to-an-always-on-availability-group-listener"></a>Conectar-se a um ouvinte do grupo de disponibilidade Always On 
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  
Depois de ter [configurado o ouvinte do grupo de disponibilidade](create-or-configure-an-availability-group-listener-sql-server.md), você precisará atualizar sua cadeia de conexão para conectar-se ao ouvinte do grupo de disponibilidade Always On. Isso roteará o tráfego do seu aplicativo automaticamente para a réplica pretendida sem precisar atualizar manualmente a cadeia de conexão após cada failover. 
  

##  <a name="connect-to-the-primary-replica"></a><a name="ConnectToPrimary"></a> Conectar-se à réplica primária  

Especifique o nome DNS do ouvinte do grupo de disponibilidade na cadeia de conexão para conectar-se à réplica primária para acesso de leitura/gravação. 

Por exemplo, para conectar-se à réplica primária no SQL Server Management Studio por meio do ouvinte, insira o nome DNS do ouvinte no campo nome do servidor: 

![Conectar-se ao ouvinte no SSMS](media/listeners-client-connectivity-application-failover/connect-to-listener-in-ssms.png)


Durante um failover, quando a réplica primária é alterada, as conexões existentes com o ouvinte são desconectadas e novas conexões são roteadas para a nova réplica primária.  

Um exemplo de uma cadeia de conexão básica para o provedor ADO.NET (System.Data.SqlClient): 
  
```  
Server=tcp: AGListener,1433;Database=MyDB;Integrated Security=SSPI  
```  

Você pode verificar a qual réplica você está conectado no momento por meio do ouvinte executando o seguinte comando T-SQL (Transact-SQL):

```sql
SELECT @@SERVERNAME
```

Por exemplo, quando SQLVM1 é minha réplica primária: 

![Verificar conectividade da réplica](media/listeners-client-connectivity-application-failover/replica-server-name.png)


Você ainda pode se conectar diretamente à instância do SQL Server usando o nome de instância da réplica primária ou secundária, em vez de usar o ouvinte do grupo de disponibilidade. No entanto, você perderá o benefício de novas conexões serem roteadas automaticamente para a nova réplica primária atual. Além disso, você perderá o benefício do roteamento somente leitura, em que as conexões especificadas com `read-intent` são roteadas automaticamente para a réplica secundária para leitura. 

##  <a name="connect-to-a-read-only-replica"></a><a name="ConnectToSecondary"></a> Conectar-se a uma réplica somente leitura 

O _roteamento somente leitura_ refere-se ao roteamento automático de conexões de ouvinte de entrada para uma réplica secundária para leitura configurada para permitir cargas de trabalho somente leitura. 

As conexões serão roteadas automaticamente para a réplica somente leitura se o seguinte for verdadeiro: 
 
-   Pelo menos uma réplica secundária é definida como acesso somente leitura e cada réplica secundária somente leitura e a réplica primária são [configuradas para oferecer suporte ao roteamento somente leitura](configure-read-only-routing-for-an-availability-group-sql-server.md). 

-   A cadeia de conexão faz referência a um banco de dados envolvido no grupo de disponibilidade. Uma alternativa para isso seria o logon usado na conexão ter o banco de dados configurado como seu banco de dados padrão. Para obter mais informações, consulte [este artigo sobre como o algoritmo funciona com o roteamento somente leitura](/archive/blogs/mattn/calculating-read_only_routing_url-for-alwayson).

-   A cadeia de conexão faz referência a um ouvinte de grupo de disponibilidade, e a tentativa do aplicativo da conexão de entrada está definida como somente leitura (por exemplo, usando a palavra-chave **Application Intent=ReadOnly** nas cadeias de conexão ODBC ou OLEDB ou nos atributos ou propriedades da conexão). 

O atributo de intenção de aplicativo é armazenado na sessão do cliente durante o logon e a instância do SQL Server processará essa intenção e determinará o que fazer de acordo com a configuração do grupo de disponibilidade e o estado de leitura/gravação atual do banco de dados de destino na réplica secundária.  

Por exemplo, para conectar-se a uma réplica somente leitura usando o SQL Server Management Studio, selecione **Opções** na caixa de diálogo **Conectar-se ao Servidor**, selecione a guia **Parâmetros de Conexão Adicionais** e, em seguida, especifique `ApplicationIntent=ReadOnly` na caixa de texto:

![Conexão somente leitura no SSMS](media/listeners-client-connectivity-application-failover/read-only-intent-in-ssms.png)
  
Um exemplo de uma cadeia de conexão para o provedor de ADO.NET (System.Data.SqlClient) que designa a intenção de aplicativo somente leitura: 

```  
Server=tcp:AGListener;Database=AdventureWorks;Integrated Security=SSPI;ApplicationIntent=ReadOnly  
```  
  
Para obter mais informações, confira [Configurar o acesso somente leitura em uma réplica de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/configure-read-only-access-on-an-availability-replica-sql-server.md)  

## <a name="non-default-port"></a>Porta não padrão

Ao criar o ouvinte, você designa uma porta para o ouvinte usar. Se a porta for a porta 1433 padrão, você não precisará especificar um número da porta ao se conectar ao ouvinte. No entanto, se a porta não for 1433, ela deverá ser especificada na cadeia de conexão no formato de `listenername,port`, como:

![Conectar-se com uma porta não padrão](media/listeners-client-connectivity-application-failover/specify-port-in-ssms.png)

Um exemplo de uma cadeia de conexão para o provedor ADO.NET (System.Data.SqlClient) que especifica uma porta não padrão para o ouvinte: 

```  
Server=tcp:AGListener,1445;Database=AdventureWorks;Integrated Security=SSPI 
```  

##  <a name="bypass-listeners"></a><a name="BypassAGl"></a> Ignorar ouvintes  

Embora os ouvintes de grupo de disponibilidade permitam suporte para redirecionamento de failover e roteamento somente leitura, as conexões de cliente não precisam usá-los. Uma conexão de cliente também pode fazer referência direta à instância do SQL Server em vez de conectar-se ao ouvinte de grupo de disponibilidade.  
  
Na instância do SQL Server, é irrelevante se a conexão fizer logon usando o ouvinte de grupo de disponibilidade ou usando outro ponto de extremidade da instância.  A instância do SQL Server verificará o estado do banco de dados de destino e permitirá ou não a conectividade com base na configuração do grupo de disponibilidade e no estado atual do banco de dados na instância.  Por exemplo, se um aplicativo cliente conectar-se diretamente a uma instância de porta do SQL Server e conectar-se a um banco de dados de destino hospedado em um grupo de disponibilidade e o banco de dados de destino estiver em estado primário e online, a conectividade terá sucesso.  Se o banco de dados de destino estiver offline ou em um estado de transição, haverá falha na conectividade para o banco de dados.  
  
Como alternativa, ao migrar de espelhamento de banco de dados para o [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)], os aplicativos podem especificar a cadeia de conexão do espelhamento do banco de dados desde que exista apenas uma réplica secundária e que as conexões de usuário não sejam permitidas. 

##  <a name="database-mirroring-connection-strings"></a><a name="DbmConnectionString"></a> Cadeias de conexão de espelhamento de banco de dados 
 Se um grupo de disponibilidade tiver apenas uma réplica secundária e não estiver configurado com ALLOW_CONNECTIONS = READ_ONLY ou ALLOW_CONNECTIONS = NONE na réplica secundária, os clientes poderão se conectar à réplica primária usando uma cadeia de conexão de espelhamento de banco de dados. Essa abordagem pode ser útil na migração de um aplicativo existente do espelhamento de banco de dados para um grupo de disponibilidade, contanto que você limite o grupo de disponibilidade a duas réplicas de disponibilidade (uma réplica primária e uma réplica secundária). Se adicionar mais réplicas secundárias, você precisará criar um ouvinte de grupo de disponibilidade para o grupo de disponibilidade e atualizar seus aplicativos para usarem o nome DNS do ouvinte do grupo de disponibilidade.  
  
 Quando cadeias de conexão de espelhamento de banco de dados forem utilizadas, o cliente poderá usar o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ou o provedor de dados .NET Framework para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. A cadeia de conexão oferecida por um cliente deve fornecer, no mínimo, o nome de uma instância de servidor, o *nome de parceiro inicial*, para identificar a instância de servidor que hospeda inicialmente a réplica de disponibilidade à qual você pretende se conectar. Opcionalmente, a cadeia de conexão também pode fornecer o nome de outra instância de servidor, o *nome de parceiro de failover*, para identificar a instância do servidor que hospeda inicialmente a réplica secundária como o nome de parceiro de failover.  
  
 Para obter mais informações sobre cadeias de conexão de espelhamento de banco de dados, veja [Conectar clientes a uma sessão de espelhamento de banco de dados &#40;SQL Server&#41;](../../../database-engine/database-mirroring/connect-clients-to-a-database-mirroring-session-sql-server.md).  
  
  
##  <a name="multi-subnet-failovers"></a><a name="SupportAgMultiSubnetFailover"></a> Failover de várias sub-redes  
 
 Se estiver usando bibliotecas de cliente que dão suporte à opção de conexão MultiSubnetFailover na cadeia de conexão, você poderá otimizar o failover do grupo de disponibilidade para uma sub-rede diferente configurando MultiSubnetFailover como "Verdadeiro" ou "Sim", dependendo da sintaxe do provedor que você está usando.  
  
> [!NOTE]  
>  Essa configuração é recomendável para conexões únicas e de várias sub-redes para ouvintes de grupos de disponibilidade e nomes de instâncias de cluster de failover do SQL Server.  A habilitação dessa opção adiciona mais otimizações, até mesmo para cenários de única sub-rede.  
  
 A opção de conexão **MultiSubnetFailover** funciona apenas com o protocolo de rede TCP e tem suporte apenas para conexão a um ouvinte de grupo de disponibilidade e para qualquer nome de rede virtual que se conecta ao [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)].  
  
 Um exemplo de cadeia de conexão do provedor ADO.NET (System.Data.SqlClient) que habilita o failover de várias sub-redes é o seguinte:  
  
```  
Server=tcp:AGListener,1433;Database=AdventureWorks;Integrated Security=SSPI; MultiSubnetFailover=True  
```  
  
 A opção de conexão **MultiSubnetFailover** deve ser definida como **True** mesmo que o grupo de disponibilidade se estenda apenas por uma única sub-rede.  Isso permite pré-configurar novos clientes para dar suporte ao futuro alcance de sub-redes sem necessidade de alterações futuras na cadeia de conexão de cliente e também otimiza o desempenho de failover para failovers de sub-rede única.  Embora a opção de conexão **MultiSubnetFailover** não seja necessária, ela fornece o benefício de um failover de sub-rede mais rápido.  Isso ocorre porque o driver de cliente tentará abrir um soquete TCP para cada endereço IP em paralelo associado ao grupo de disponibilidade.  O driver de cliente esperará que o primeiro IP responda com êxito e quando o fizer, usa-o para a conexão.  
  
##  <a name="listeners--tlsssl-certificates"></a><a name="SSLcertificates"></a> Ouvintes e certificados TLS/SSL  

Durante a conexão a um ouvinte de grupo de disponibilidade, se as instâncias participantes do SQL Server usarem certificados TLS/SSL junto com criptografia de sessão, o driver de cliente que está fazendo a conexão precisará dar suporte ao Nome Alternativo da Entidade no certificado TLS/SSL para forçar a criptografia.  O suporte ao driver do SQL Server para o Nome Alternativo da Entidade do certificado está planejado para ADO.NET (SqlClient), Microsoft JDBC e SNAC (SQL Native Client).  
  
Um certificado X.509 deve ser configurado para cada nó de servidor participante do cluster de failover com uma lista de todos os ouvintes de grupo de disponibilidade definidos no Nome Alternativo da Entidade do certificado. 

O formato dos valores do certificado é: 

```  
CN = Server.FQDN  
SAN = Server.FQDN,Listener1.FQDN,Listener2.FQDN
```

Por exemplo, você têm os seguintes valores: 

```
Servername: Win2019   
Instance: SQL2019   
AG: AG2019   
Listener: Listener2019   
Domain: contoso.com  (which is also the FQDN)
```

Para um WSFC que tem um único grupo de disponibilidade, o certificado deve ter o FQDN (nome de domínio totalmente qualificado) do servidor e o FQDN do ouvinte: 

```
CN: Win2019.contoso.com
SAN: Win2019.contoso.com, Listener2019.contoso.com 
```

Com essa configuração, suas conexões à instância (`WIN2019\SQL2019`) ou ao ouvinte (`Listener2019`) serão criptografadas. 

Dependendo de como a rede está configurada, há um pequeno subconjunto de clientes que talvez precisem adicionar o NetBIOS também à SAN. Nesse caso, os valores do certificado devem ser: 

```
CN: Win2019.contoso.com
SAN: Win2019,Win2019.contoso.com,Listener2019,Listener2019.contoso.com
```

Se o WSFC tiver três ouvintes do grupo de disponibilidade, como: Listener1, Listener2, Listener3

Os valores do certificado deverão ser: 

```
CN: Win2019.contoso.com
SAN: Win2019.contoso.com,Listener1.contoso.com,Listener2.contoso.com,Listener3.contoso.com
```
  
  
##  <a name="listeners-and-kerberos-spns"></a><a name="SPNs"></a> Ouvintes e Kerberos (SPNs) 

Um administrador de domínio deve configurar um SPN (nome da entidade de serviço) no Active Directory para cada ouvinte do grupo de disponibilidade para habilitar o Kerberos para conexões de cliente com o ouvinte. Ao registrar o SPN, você deve usar a conta de serviço da instância de servidor que hospeda a réplica de disponibilidade. Para que o SPN funcione em todas as réplicas, a mesma conta de serviço deve ser usada para todas as instâncias no cluster do WSFC que hospeda o grupo de disponibilidade.  
  
 Use a ferramenta de linha de comando **setspn** do Windows para configurar o SPN.  Por exemplo, para configurar um SPN para um grupo de disponibilidade denominado `AG1listener.Adventure-Works.com` hospedado em um conjunto de instâncias do SQL Server, todas configuradas para executar sob a conta de domínio `corp\svclogin2`:  
  
```  
setspn -A MSSQLSvc/AG1listener.Adventure-Works.com:1433 corp\svclogin2  
```  
  
 Para obter mais informações sobre o registro manual de um SPN para SQL Server, consulte [Registrar um nome de entidade de serviço para conexões de Kerberos](../../../database-engine/configure-windows/register-a-service-principal-name-for-kerberos-connections.md).  
  


## <a name="next-steps"></a>Próximas etapas

Depois de conectar-se com êxito ao ouvinte, considere descarregar [cargas de trabalho somente leitura](overview-of-always-on-availability-groups-sql-server.md) e [backups](configure-backup-on-availability-replicas-sql-server.md) para a réplica secundária para aprimorar o desempenho. Você também pode examinar várias [estratégias de monitoramento do grupo de disponibilidade](monitoring-of-availability-groups-sql-server.md) para garantir a integridade do seu grupo de disponibilidade. 

Para obter mais informações sobre grupos de disponibilidade, confira a [Visão geral dos grupos de disponibilidade Always On &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md).