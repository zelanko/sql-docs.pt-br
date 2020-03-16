---
title: Conectar-se a um ouvinte do grupo de disponibilidade
description: Contém informações sobre como se conectar ao ouvinte do grupo de disponibilidade Always On, antes e após o failover.
ms.custom: seodec18
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], listeners
- read-only routing
- read-intent connections [AlwaysOn Availability Groups]
- Availability Groups [SQL Server], configuring
- Availability Groups [SQL Server], read-only routing
- Availability Groups [SQL Server], client connectivity
ms.assetid: 76fb3eca-6b08-4610-8d79-64019dd56c44
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: e2116c0a587b82f289f5dba17968f3eb42e47c05
ms.sourcegitcommit: 4baa8d3c13dd290068885aea914845ede58aa840
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/13/2020
ms.locfileid: "79287780"
---
# <a name="connect-to-an-always-on-availability-group-listener"></a>Conectar-se a um ouvinte do grupo de disponibilidade Always On 
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Este artigo contém informações sobre considerações para conectividade do cliente [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] e funcionalidade de failover de aplicativo.  
  
> [!NOTE]  
>  Para a maioria das configurações comuns de ouvinte, você pode criar o primeiro ouvinte de grupo de disponibilidade simplesmente usando instruções [!INCLUDE[tsql](../../../includes/tsql-md.md)] ou cmdlets PowerShell. Para obter mais informações, consulte [Tarefas relacionadas](#RelatedTasks), mais adiante neste tópico.  
  
  
##  <a name="AGlisteners"></a> Ouvintes de grupos de disponibilidade  
 É possível fornecer conectividade de cliente ao banco de dados de um determinado grupo de disponibilidade criando um ouvinte de grupo de disponibilidade. Um ouvinte do grupo de disponibilidade é um VNN (nome de rede virtual) ao qual os clientes podem se conectar para acessar um banco de dados em uma réplica primária ou secundária de um grupo de disponibilidade AlwaysOn. Um ouvinte de grupo de disponibilidade permite que o cliente conecte-se a uma réplica de disponibilidade sem saber o nome da instância física do SQL Server à qual o cliente está se conectando.  A cadeia de conexão de cliente não precisa ser modificada para conectar-se ao local atual de uma réplica primária atual.  
  
 Um ouvinte de grupo de disponibilidade consiste em um nome de ouvinte DNS, designação de porta de ouvinte ou um ou mais endereços IP. Apenas o protocolo TCP tem suporte do ouvinte de grupo de disponibilidade.  O nome DNS do ouvinte também deve ser exclusivo no domínio e no NetBIOS.  Quando você cria um novo ouvinte de grupo de disponibilidade que se torna um recurso em um cluster com um VNN (nome de rede virtual), um VIP (IP virtual) e dependência de grupo de disponibilidade associados. Um cliente usa o DNS para resolver o VNN em vários endereços IP e depois tenta se conectar a cada endereço, até uma solicitação de conexão ser bem-sucedida ou até a solicitação de conexão atingir seu tempo limite.  
  
 Se o roteamento somente leitura estiver configurado para uma ou mais [réplicas secundárias legíveis](../../../database-engine/availability-groups/windows/active-secondaries-readable-secondary-replicas-always-on-availability-groups.md), as conexões do cliente com intenção de leitura à réplica primária serão redirecionadas para uma réplica secundária legível. Além disso, se a réplica primária se tornar offline em uma instância do SQL Server e uma nova réplica primária entrar online em outra instância do SQL Server, o ouvinte de grupo de disponibilidade permitirá que os clientes se conectem à nova réplica primária.  
  
 Para obter informações básicas sobre ouvintes do grupo de disponibilidade, veja [Criar ou configurar um ouvinte do grupo de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md).  
  
  
##  <a name="AGlConfig"></a> Configuração de ouvinte de grupo de disponibilidade  
 Um ouvinte de grupo de disponibilidade é definido pelo seguinte:  
  
 Um nome DNS exclusivo  
 Isso também é conhecido como um VNN (nome de rede virtual). As regras de nomeação do Active Directory para nomes de host DNS se aplicam. Para obter mais informações, consulte o artigo da Base de Dados de Conhecimento [Convenções de nomenclatura no Active Directory para computadores, domínios, sites e unidades organizacionais](https://support.microsoft.com/kb/909264) .  
  
 Um ou mais endereços IP virtuais (VIPs)  
 VIPs são configurados para uma ou mais sub-redes para as quais o grupo de disponibilidade faz failover.  
  
 Configuração do endereço IP  
 Para um ouvinte de grupo de disponibilidade específico, o endereço IP usa o protocolo DHCP ou um ou mais endereços IP estáticos.  
  
-   Protocolo DHCP  
  
     Se um grupo de disponibilidade residir em uma única sub-rede, você poderá configurar todos os endereços IP de ouvinte do grupo de disponibilidade para usar o DHCP. Em ambientes pré-produção, o DHCP oferece uma instalação fácil para um grupo de disponibilidade que não requer recuperação de desastres em um site remoto em uma sub-rede separada. Entretanto, você não deve usar o DHCP junto com um ouvinte de grupo de disponibilidade em um ambiente de produção. O motivo é que, em caso de tempo de inatividade, se a concessão do IP DHCP expirar, será necessário tempo extra para registrar novamente o novo endereço IP DHCP associado ao nome DNS do ouvinte. O tempo extra causará falha na conexão de cliente.  
  
-   Endereços IP estáticos  
  
     Em ambientes de produção, recomendamos que os ouvintes de grupo de disponibilidade usem endereços IP estáticos. Além disso, casos onde grupos de disponibilidade se estendem por sub-redes em um domínio de várias sub-redes, um ouvinte de grupo de disponibilidade deve usar endereços IP estáticos.  
  
 Não há suporte para configurações de redes híbridas e DHCP através de sub-redes para ouvintes de grupo de disponibilidade. Isso ocorre porque, quando há um failover, um IP dinâmico pode expirar ou ser liberado, o que coloca a alta disponibilidade geral em risco.  
  
##  <a name="SelectListenerPort"></a> Selecionando uma porta de ouvinte de grupo de disponibilidade  
 Ao configurar um ouvinte de grupo de disponibilidade, você precisa designar uma porta.  Você pode configurar a porta padrão como 1433 para simplicidade das cadeias de conexão de cliente. Ao usar 1433, você não precisa designar um número de porta em uma cadeia de conexão.   Além disso, como cada ouvinte de grupo de disponibilidade terá um nome de rede virtual separado, cada ouvinte de grupo de disponibilidade configurado em um único WSFC poderá ser configurado para fazer referência à mesma porta padrão de 1433.  
  
 Você também pode designar uma porta de ouvinte sem padrão. Porém isso significa que você também precisará especificar uma porta de destino explicitamente em sua cadeia de conexão ao conectar-se ao ouvinte de grupo de disponibilidade.  Você também precisará da permissão de abertura no firewall para a porta sem padrão.  
  
 Se você usar a porta padrão de 1433 para VNNs de ouvinte de grupo de disponibilidade, você ainda precisará garantir que nenhum outro serviço no nó de cluster esteja usando essa porta; caso contrário, isso causará um conflito de porta.  
  
 Se uma das instâncias do SQL Server já estiver escutando na porta TCP 1433 por meio do ouvinte da instância e não houver nenhum outro serviço (inclusive instâncias adicionais do SQL Server) no computador que escuta na porta 1433, isso não provocará um conflito de porta com o ouvinte de grupo de disponibilidade.  Isso ocorre porque o ouvinte de grupo de disponibilidade pode compartilhar a mesma porta TCP no mesmo processo de serviço.  No entanto, não devem ser configuradas várias instâncias do SQL Server (lado a lado) para escutar na mesma porta.  
  
##  <a name="ConnectToPrimary"></a> Usando um ouvinte para conectar à réplica primária  
 Para usar um ouvinte de grupo de disponibilidade para conectar-se à réplica de disponibilidade para acesso de leitura/gravação, a cadeia de conexão especifica o nome DNS do ouvinte do grupo de disponibilidade.  Se uma réplica primária de grupo de disponibilidade for alterada para uma nova réplica, as conexões existentes que usam o nome da rede de um ouvinte de grupo de disponibilidade serão desconectadas.  As novas conexões ao ouvinte do grupo de disponibilidade são então direcionadas para a nova réplica primária. Um exemplo de uma cadeia de conexão básica para o provedor ADO.NET (System.Data.SqlClient) é o seguinte:  
  
```  
Server=tcp: AGListener,1433;Database=MyDB;Integrated Security=SSPI  
```  
  
 Você ainda pode escolher fazer referência direta à instância de nome do SQL Server das réplicas primárias ou secundárias, em vez de usar o nome do servidor do grupo de disponibilidade, no entanto, se optar por fazer isso, você perderá o benefício de novas conexões que são dirigidas automaticamente para a réplica primária atual.  Você também perderá o benefício de roteamento somente leitura.  
  
##  <a name="ConnectToSecondary"></a> Usando um ouvinte para conectar a uma réplica secundária somente leitura (roteamento somente leitura)  
 *Roteamento somente leitura* refere-se à capacidade do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] de rotear conexões de entrada a um ouvinte de grupo de disponibilidade para uma réplica secundária que é configurada para permitir cargas de trabalho somente leitura. Uma conexão de entrada que faz referência a um nome de ouvinte de grupo de disponibilidade poderá ser roteada automaticamente para uma réplica somente leitura se o seguinte for verdadeiro:  
  
-   Pelo menos uma réplica secundária é definida como acesso somente leitura e cada réplica secundária somente leitura e a réplica primária são configuradas para oferecer suporte ao roteamento somente leitura. Para obter mais informações, veja [Para configurar réplicas de disponibilidade para roteamento somente leitura](#ConfigureARsForROR), mais adiante nesta seção.  

-   A cadeia de conexão faz referência a um banco de dados envolvido no grupo de disponibilidade. Uma alternativa para isso seria o logon usado na conexão ter o banco de dados configurado como seu banco de dados padrão. Para obter mais informações, consulte [este artigo sobre como o algoritmo funciona com o roteamento somente leitura](https://blogs.msdn.microsoft.com/mattn/2012/04/25/calculating-read_only_routing_url-for-alwayson/).

-   A cadeia de conexão faz referência a um ouvinte de grupo de disponibilidade, e a tentativa do aplicativo da conexão de entrada está definida como somente leitura (por exemplo, usando a palavra-chave **Application Intent=ReadOnly** nas cadeias de conexão ODBC ou OLEDB ou nos atributos ou propriedades da conexão). Para obter informações, veja [Tentativa do aplicativo somente leitura e roteamento somente leitura](#ReadOnlyAppIntent), mais adiante nesta seção.  
  
##  <a name="ConfigureARsForROR"></a> Para configurar réplicas de disponibilidade para roteamento somente leitura  
 Um administrador de banco de dados deve configurar as réplicas de disponibilidade como segue:  
  
1.  Para cada réplica de disponibilidade que você deseja configurar como uma réplica secundária legível, um administrador de banco de dados deve configurar os parâmetros a seguir, que entram em vigor somente na função secundária:  
  
    -   O acesso de conexão deve ser definido como "tudo" ou "somente leitura".  
  
    -   A URL de roteamento somente leitura deve ser especificada.  
  
2.  Para cada uma dessas réplicas, uma lista de roteamento somente leitura deve ser especificada para a função primária. Especifique um ou mais nomes de servidor como destinos de roteamento.  
  
####  <a name="RelatedTasksROR"></a> Tarefas relacionadas  
  
-   [Configurar o acesso somente leitura em uma réplica de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/configure-read-only-access-on-an-availability-replica-sql-server.md)  
  
-   [Configurar o roteamento somente leitura para um grupo de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/configure-read-only-routing-for-an-availability-group-sql-server.md)  
  
##  <a name="ReadOnlyAppIntent"></a> Tentativa do aplicativo somente leitura e roteamento somente leitura  
 A propriedade da cadeia de conexão da intenção de aplicativo expressa a solicitação do aplicativo cliente de ser direcionada para uma versão de leitura/gravação ou somente leitura de um banco de dados de grupo de disponibilidade. Para usar o roteamento somente leitura, um cliente deve usar uma tentativa de aplicativo somente leitura na cadeia de conexão ao conectar-se ao ouvinte de grupo de disponibilidade. Sem a tentativa de aplicativo somente leitura, as conexões para o ouvinte de grupo de disponibilidade são direcionadas para o banco de dados na réplica primária.  
  
 O atributo de intenção de aplicativo é armazenado na sessão do cliente durante o logon e a instância do SQL Server processará essa intenção e determinará o que fazer de acordo com a configuração do grupo de disponibilidade e o estado de leitura/gravação atual do banco de dados de destino na réplica secundária.  
  
 Um exemplo de uma cadeia de conexão para o provedor de ADO.NET (System.Data.SqlClient) que designa a intenção de aplicativo somente leitura é o seguinte:  
  
```  
Server=tcp:AGListener,1433;Database=AdventureWorks;Integrated Security=SSPI;ApplicationIntent=ReadOnly  
```  
  
 Neste exemplo de cadeia de conexão, o cliente está tentando conectar-se ao banco de dados AdventureWorks por meio de um ouvinte de grupo de disponibilidade denominado `AGListener` na porta 1433 (você também pode omitir a porta se o ouvinte do grupo de disponibilidade está escutando na 1433).  A cadeia de conexão tem a propriedade **ApplicationIntent** definida como **ReadOnly**, fazendo dela uma *cadeia de conexão de intenção de leitura*.  Sem essa configuração, o servidor não tentaria um roteamento somente leitura da conexão.  
  
 O banco de dados primário do grupo de disponibilidade processa a solicitação de roteamento somente leitura de entrada e tenta localizar uma réplica somente leitura online que esteja unida à réplica primária e configurada para roteamento somente leitura.  O cliente recebe informações de conexão do servidor de réplica primária e conecta-se à réplica somente leitura identificada.  
  
 Observe que a tentativa de aplicativo pode ser enviada de um driver cliente a uma instância de nível inferior do SQL Server.  Neste caso, a tentativa de aplicativo de somente leitura é ignorada e a conexão continua normalmente.  
  
 Você pode ignorar o roteamento somente leitura não definindo a propriedade de conexão da tentativa de aplicativo como **ReadOnly** (quando não designado, o padrão é **ReadWrite** durante o logon) ou conectando-se diretamente à instância de réplica primária do SQL Server em vez de usar o nome do ouvinte do grupo de disponibilidade.  O roteamento somente leitura também não ocorrerá se você conectar-se diretamente a uma réplica somente leitura.  
  
####  <a name="RelatedTasksApps"></a> Tarefas relacionadas  
  
-   [Suporte do SQL Server Native Client à alta disponibilidade e recuperação de desastre](../../../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md)  
  
-   [Usando palavras-chave da cadeia de conexão com o SQL Server Native Client](../../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md)  
  
##  <a name="BypassAGl"></a> Ignorando ouvintes de grupo de disponibilidade  
 Embora os ouvintes de grupo de disponibilidade permitam suporte para redirecionamento de failover e roteamento somente leitura, as conexões de cliente não precisam usá-los. Uma conexão de cliente também pode fazer referência direta à instância do SQL Server em vez de conectar-se ao ouvinte de grupo de disponibilidade.  
  
 Na instância do SQL Server, é irrelevante se a conexão fizer logon usando o ouvinte de grupo de disponibilidade ou usando outro ponto de extremidade da instância.  A instância do SQL Server verificará o estado do banco de dados de destino e permitirá ou não a conectividade com base na configuração do grupo de disponibilidade e no estado atual do banco de dados na instância.  Por exemplo, se um aplicativo cliente conectar-se diretamente a uma instância de porta do SQL Server e conectar-se a um banco de dados de destino hospedado em um grupo de disponibilidade e o banco de dados de destino estiver em estado primário e online, a conectividade terá sucesso.  Se o banco de dados de destino estiver offline ou em um estado de transição, haverá falha na conectividade para o banco de dados.  
  
 Como alternativa, ao migrar de espelhamento de banco de dados para o [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)], os aplicativos podem especificar a cadeia de conexão do espelhamento do banco de dados desde que exista apenas uma réplica secundária e que as conexões de usuário não sejam permitidas. Para obter mais informações, veja [Usando cadeias de conexão de espelhamento de banco de dados com grupos de disponibilidade](#DbmConnectionString), mais adiante nesta seção.  
  
##  <a name="DbmConnectionString"></a> Usando cadeias de conexão de espelhamento de banco de dados com grupos de disponibilidade  
 Se um grupo de disponibilidade tiver apenas uma réplica secundária e não estiver configurado com ALLOW_CONNECTIONS = READ_ONLY ou ALLOW_CONNECTIONS = NONE na réplica secundária, os clientes poderão se conectar à réplica primária usando uma cadeia de conexão de espelhamento de banco de dados. Essa abordagem pode ser útil na migração de um aplicativo existente do espelhamento de banco de dados para um grupo de disponibilidade, contanto que você limite o grupo de disponibilidade a duas réplicas de disponibilidade (uma réplica primária e uma réplica secundária). Se adicionar mais réplicas secundárias, você precisará criar um ouvinte de grupo de disponibilidade para o grupo de disponibilidade e atualizar seus aplicativos para usarem o nome DNS do ouvinte do grupo de disponibilidade.  
  
 Quando cadeias de conexão de espelhamento de banco de dados forem utilizadas, o cliente poderá usar o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ou o provedor de dados .NET Framework para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. A cadeia de conexão oferecida por um cliente deve fornecer, no mínimo, o nome de uma instância de servidor, o *nome de parceiro inicial*, para identificar a instância de servidor que hospeda inicialmente a réplica de disponibilidade à qual você pretende se conectar. Opcionalmente, a cadeia de conexão também pode fornecer o nome de outra instância de servidor, o *nome de parceiro de failover*, para identificar a instância do servidor que hospeda inicialmente a réplica secundária como o nome de parceiro de failover.  
  
 Para obter mais informações sobre cadeias de conexão de espelhamento de banco de dados, veja [Conectar clientes a uma sessão de espelhamento de banco de dados &#40;SQL Server&#41;](../../../database-engine/database-mirroring/connect-clients-to-a-database-mirroring-session-sql-server.md).  
  
##  <a name="CCBehaviorOnFailover"></a> Comportamento de conexões de cliente em failover  
 Quando ocorrer um failover de grupo de disponibilidade, as conexões persistentes ao grupo de disponibilidade são terminadas e o cliente deve estabelecer uma nova conexão para continuar trabalhando com o mesmo banco de dados primário ou banco de dados secundário somente leitura.  Enquanto um failover estiver ocorrendo no lado do servidor, a conectividade com o grupo de disponibilidade pode falhar, forçando o aplicativo cliente a repetir a conexão até que o primário seja colocado completamente online.  
  
 Se o grupo de disponibilidade voltar a ficar online durante a tentativa de conexão de um aplicativo cliente, mas antes do tempo limite da conexão, o driver cliente poderá conectar-se com êxito durante uma de suas tentativas internas e não ocorrerá nenhum erro no aplicativo nesse caso.  
  
##  <a name="SupportAgMultiSubnetFailover"></a> Dando suporte a failovers de várias sub-redes de grupo de disponibilidade  
 Se estiver usando bibliotecas de cliente que dão suporte à opção de conexão MultiSubnetFailover na cadeia de conexão, você poderá otimizar o failover do grupo de disponibilidade para uma sub-rede diferente configurando MultiSubnetFailover como "Verdadeiro" ou "Sim", dependendo da sintaxe do provedor que você está usando.  
  
> [!NOTE]  
>  Essa configuração é recomendável para conexões únicas e de várias sub-redes para ouvintes de grupos de disponibilidade e nomes de instâncias de cluster de failover do SQL Server.  A habilitação dessa opção adiciona mais otimizações, até mesmo para cenários de única sub-rede.  
  
 A opção de conexão **MultiSubnetFailover** funciona apenas com o protocolo de rede TCP e tem suporte apenas para conexão a um ouvinte de grupo de disponibilidade e para qualquer nome de rede virtual que se conecta ao [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)].  
  
 Um exemplo de cadeia de conexão do provedor ADO.NET (System.Data.SqlClient) que habilita o failover de várias sub-redes é o seguinte:  
  
```  
Server=tcp:AGListener,1433;Database=AdventureWorks;Integrated Security=SSPI; MultiSubnetFailover=True  
```  
  
 A opção de conexão **MultiSubnetFailover** deve ser definida como **True** mesmo que o grupo de disponibilidade se estenda apenas por uma única sub-rede.  Isso permite pré-configurar novos clientes para dar suporte ao futuro alcance de sub-redes sem necessidade de alterações futuras na cadeia de conexão de cliente e também otimiza o desempenho de failover para failovers de sub-rede única.  Embora a opção de conexão **MultiSubnetFailover** não seja necessária, ela fornece o benefício de um failover de sub-rede mais rápido.  Isso ocorre porque o driver de cliente tentará abrir um soquete TCP para cada endereço IP em paralelo associado ao grupo de disponibilidade.  O driver de cliente esperará que o primeiro IP responda com êxito e quando o fizer, usa-o para a conexão.  
  
##  <a name="SSLcertificates"></a> Ouvintes de grupo de disponibilidade e certificados SSL  
 Ao conectar-se a um ouvinte de grupo de disponibilidade, se as instâncias participantes do SQL Server usarem certificados SSL junto com criptografia de sessão, o driver de cliente que está fazendo a conexão precisará dar suporte ao Nome Alternativo da Entidade no certificado SSL para forçar a criptografia.  O suporte ao driver do SQL Server para o Nome Alternativo da Entidade do certificado está planejado para ADO.NET (SqlClient), Microsoft JDBC e SNAC (SQL Native Client).  
  
 Um certificado X.509 deve ser configurado para cada nó de servidor participante do cluster de failover com uma lista de todos os ouvintes de grupo de disponibilidade definidos no Nome Alternativo da Entidade do certificado.  
  
 Por exemplo, se o WSFC tiver três ouvintes de grupo de disponibilidade com os nomes `AG1_listener.Adventure-Works.com`, `AG2_listener.Adventure-Works.com`e `AG3_listener.Adventure-Works.com`, o Nome Alternativo da Entidade para o certificado deverá ser definido da seguinte maneira:  
  
```  
CN = ServerFQDN  
SAN = ServerFQDN,AG1_listener.Adventure-Works.com, AG2_listener.Adventure-Works.com, AG3_listener.Adventure-Works.com  
```  
  
##  <a name="SPNs"></a> Ouvintes de grupo de disponibilidade e SPNs (nomes de entidades de segurança de servidor)  
 Um SPN (nome de entidade de segurança de servidor) deve ser configurado no Active Directory por um administrador de domínio para cada nome de ouvinte de grupo de disponibilidade para habilitar o Kerberos para a conexão de cliente com o ouvinte de grupo de disponibilidade. Ao registrar o SPN, você deve usar a conta de serviço da instância de servidor que hospeda a réplica de disponibilidade.  Para que o SPN funcione em todas as réplicas, a mesma conta de serviço deve ser usada para todas as instâncias no cluster do WSFC que hospeda o grupo de disponibilidade.  
  
 Use a ferramenta de linha de comando **setspn** do Windows para configurar o SPN.  Por exemplo, para configurar um SPN para um grupo de disponibilidade denominado `AG1listener.Adventure-Works.com` hospedado em um conjunto de instâncias do SQL Server, todas configuradas para executar sob a conta de domínio `corp/svclogin2`:  
  
```  
setspn -A MSSQLSvc/AG1listener.Adventure-Works.com:1433 corp/svclogin2  
```  
  
 Para obter mais informações sobre o registro manual de um SPN para SQL Server, consulte [Registrar um nome de entidade de serviço para conexões de Kerberos](../../../database-engine/configure-windows/register-a-service-principal-name-for-kerberos-connections.md).  
  
##  <a name="RelatedTasks"></a> Tarefas relacionadas  
  
-   [Conectividade de cliente AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/always-on-client-connectivity-sql-server.md)  
  
-   [Criar ou configurar um ouvinte do grupo de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md)  
  
-   [Exibir propriedades do ouvinte do grupo de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/view-availability-group-listener-properties-sql-server.md)  
  
-   [Remover um ouvinte do grupo de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/remove-an-availability-group-listener-sql-server.md)  
  
-   [Configurar o acesso somente leitura em uma réplica de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/configure-read-only-access-on-an-availability-replica-sql-server.md)  
  
-   [Configurar o roteamento somente leitura para um grupo de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/configure-read-only-routing-for-an-availability-group-sql-server.md)  
  
##  <a name="RelatedContent"></a> Conteúdo relacionado  
  
-   [Guia de soluções AlwaysOn do Microsoft SQL Server para alta disponibilidade e recuperação de desastre](https://go.microsoft.com/fwlink/?LinkId=227600)  
  
-   [Introdução ao ouvinte do grupo de disponibilidade](https://blogs.msdn.microsoft.com/sqlalwayson/2012/01/16/introduction-to-the-availability-group-listener/) (um blog da equipe do AlwaysOn do SQL Server)  
  
-   [Blog da equipe do Always On do SQL Server: o blog oficial da equipe do Always On do SQL Server](https://blogs.msdn.microsoft.com/sqlalwayson/)  
  
## <a name="see-also"></a>Consulte Também  
 [Visão geral dos grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Conectividade de cliente AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/always-on-client-connectivity-sql-server.md)   
 [Sobre o acesso de conexão de cliente a réplicas de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/about-client-connection-access-to-availability-replicas-sql-server.md)   
 [Secundárias ativas: réplicas secundárias legíveis &#40;Grupos de Disponibilidade Always On&#41;](../../../database-engine/availability-groups/windows/active-secondaries-readable-secondary-replicas-always-on-availability-groups.md)   
 [Conectar clientes a uma sessão de espelhamento de banco de dados &#40;SQL Server&#41;](../../../database-engine/database-mirroring/connect-clients-to-a-database-mirroring-session-sql-server.md)  
  
  
