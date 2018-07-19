---
title: Criar ou configurar um ouvinte do grupo de disponibilidade (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: high-availability
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.swb.availabilitygroup.newaglistener.general.f1
helpviewer_keywords:
- Availability Groups [SQL Server], listeners
- Availability Groups [SQL Server], client connectivity
ms.assetid: 2bc294f6-2312-4b6b-9478-2fb8a656e645
caps.latest.revision: 52
author: MashaMSFT
ms.author: mathoma
manager: erikre
ms.openlocfilehash: 8c7882dc973f51379483d629a6d02422931de7b1
ms.sourcegitcommit: c582de20c96242f551846fdc5982f41ded8ae9f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/28/2018
ms.locfileid: "37065996"
---
# <a name="create-or-configure-an-availability-group-listener-sql-server"></a>Criar ou configurar um ouvinte de grupo de disponibilidade (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Este tópico descreve como criar ou configurar um único *ouvinte de grupo de disponibilidade* para um Grupo de Disponibilidade AlwaysOn usando o [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], o [!INCLUDE[tsql](../../../includes/tsql-md.md)]ou o PowerShell no [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)].  
  
> [!IMPORTANT]  
>  Para criar o primeiro ouvinte de grupo de disponibilidade de um grupo de disponibilidade, é altamente recomendável ter o [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], o [!INCLUDE[tsql](../../../includes/tsql-md.md)]ou o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] PowerShell. Evite criar um ouvinte diretamente no cluster WSFC, exceto se necessário, por exemplo, para criar um ouvinte adicional.  
  
-   **Antes de começar:**  
  
     [Já existe um ouvinte para esse grupo de disponibilidade?](#DoesListenerExist)  
  
     [Limitações e restrições](#Restrictions)  
  
     [Recomendações](#Recommendations)  
  
     [Pré-requisitos](#Prerequisites)  
  
     [Requisitos para o nome DNS de um ouvinte de grupo de disponibilidade](#DNSnameReqs)  
  
     [Permissões do Windows](#WinPermissions)  
  
     [Permissões do SQL Server](#SqlPermissions)  
  
-   **Para criar ou configurar um ouvinte de grupo de disponibilidade, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [PowerShell](#PowerShellProcedure)  
  
-   **Solução de problemas**  
  
     [Falha ao criar um ouvinte de grupo de disponibilidade devido a cotas do Active Directory](#ADQuotas)  
  
-   **Acompanhamento: após criar um ouvinte do grupo de disponibilidade**  
  
     [Palavra-chave MultiSubnetFailover e recursos associados](#MultiSubnetFailover)  
  
     [Configuração RegisterAllProvidersIP](#RegisterAllProvidersIP)  
  
     [Configuração HostRecordTTL](#HostRecordTTL)  
  
     [Exemplo de script PowerShell para desabilitar RegisterAllProvidersIP e reduzir o TTL](#SampleScript)  
  
     [Recomendações de acompanhamento](#FollowUpRecommendations)  
  
     [Criar um ouvinte adicional para um grupo de disponibilidade (opcional)](#CreateAdditionalListener)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="DoesListenerExist"></a> Já existe um ouvinte para esse grupo de disponibilidade?  
 **Para determinar se um ouvinte já existe para o grupo de disponibilidade**  
  
-   [Exibir propriedades do ouvinte do grupo de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/view-availability-group-listener-properties-sql-server.md)  
  
> [!NOTE]  
>  Se já houver um ouvinte e você desejar criar um ouvinte adicional, consulte [Para criar um ouvinte adicional para um grupo de disponibilidade (opcional)](#CreateAdditionalListener)posteriormente neste tópico.  
  
###  <a name="Restrictions"></a> Limitações e restrições  
  
-   Só é possível criar um ouvinte por grupo de disponibilidade via [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Geralmente, cada grupo de disponibilidade exige somente um ouvinte. No entanto, alguns cenários de cliente exigem vários ouvintes para um grupo de disponibilidade.   Depois de criar um ouvinte pelo SQL Server, você pode usar o Windows PowerShell para clusters de failover ou o Gerenciador de Cluster de Failover do WSFC para criar ouvintes adicionais. Para obter mais informações, consulte [Para criar um ouvinte adicional para um grupo de disponibilidade (opcional)](#CreateAdditionalListener), posteriormente neste tópico.  
  
###  <a name="Recommendations"></a> Recomendações  
 O uso de um endereço IP estático é recomendável, embora não obrigatório, para várias configurações de sub-rede.  
  
###  <a name="Prerequisites"></a> Pré-requisitos  
  
-   Você deve estar conectado à instância do servidor que hospeda a réplica primária.  
  
-   Se estiver configurando um ouvinte de grupo de disponibilidade em várias sub-redes e estiver planejando usar endereços IP estáticos, você precisará obter os endereços IP estáticos de cada sub-rede que hospeda uma réplica de disponibilidade para o grupo de disponibilidade para o qual está criando o ouvinte. Normalmente, você precisará solicitar os endereços IP estáticos aos administradores de rede.  
  
> [!IMPORTANT]  
>  Antes de criar seu primeiro ouvinte, é altamente recomendável ler [Conectividade de cliente AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/always-on-client-connectivity-sql-server.md).  
  
###  <a name="DNSnameReqs"></a> Requisitos para o nome DNS de um ouvinte de grupo de disponibilidade  
 Cada ouvinte de grupo de disponibilidade exige um nome de host DNS que é exclusivo no domínio e no NetBIOS. O nome DNS é um valor da cadeia de caracteres. Este nome pode conter somente caracteres alfanuméricos, traços/hifens (-) e sublinhados (_), em qualquer ordem. Os nomes de host DNS diferenciam maiúsculas de minúsculas. O comprimento máximo é 63 caracteres; no entanto, no [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], o comprimento máximo que você pode especificar é 15 caracteres.  
  
 Nós recomendamos que você especifique uma cadeia de caracteres significativa. Por exemplo, para um grupo de disponibilidade denominado `AG1`, um nome de host de DNS significativo seria `ag1-listener`.  
  
> [!IMPORTANT]  
>  O NetBIOS reconhece somente os primeiros 15 caracteres no dns_name. Se você tiver dois clusters do WSFC que sejam controlados pelo mesmo Active Directory e tentar criar ouvintes de grupo de disponibilidade nos dois clusters usando nomes com mais de 15 caracteres e um prefixo idêntico de 15 caracteres, você obterá um erro relatando que o recurso Nome de Rede virtual não pôde ser colocado online. Para obter informações sobre regras da nomenclatura de prefixos para nomes DNS, consulte [Atribuindo nomes de domínio](http://technet.microsoft.com/library/cc731265\(WS.10\).aspx).  
  
###  <a name="WinPermissions"></a> Permissões do Windows  
  
|Permissões|Link|  
|-----------------|----------|  
|O CNO (nome do objeto de cluster) do cluster WSFC que está hospedando o grupo de disponibilidade deve ter a permissão **Criar Objetos de computador** .<br /><br /> No Active Directory, por padrão, um CNO não tem a permissão **Criar Objetos de computador** explicitamente e pode criar dez VCOs (objetos de computador virtual). Depois que os dez VCOs forem criados, a criação de VCOs adicionais apresentará falha. É possível impedir isso concedendo a permissão explicitamente ao CNO do cluster WSFC. Observe que o VCOs para grupos de disponibilidade que você excluiu não serão excluídos automaticamente no Active Directory e serão incluídos na contagem do limite padrão de dez VCOs, a menos que sejam excluídos manualmente.<br /><br /> Observação: em algumas organizações, a política de segurança proíbe a concessão da permissão **Criar Objetos de computador** a contas de usuário individuais.|*Steps for configuring the account for the person who installs the cluster* (Etapas para configurar a conta para a pessoa que instala o cluster) no [Failover Cluster Step-by-Step Guide: Configuring Accounts in Active Directory](http://technet.microsoft.com/library/cc731002\(WS.10\).aspx#BKMK_steps_installer)<br /><br /> *Steps for prestaging the cluster name account* (Etapas para configurar a conta para a pessoa que instala o cluster) no [Failover Cluster Step-by-Step Guide: Configuring Accounts in Active Directory](http://technet.microsoft.com/library/cc731002\(WS.10\).aspx#BKMK_steps_precreating)|  
|Se sua organização exigir que você pré-configure a conta de computador para um nome de rede virtual de ouvinte, você precisará de associação no grupo **Operador de Conta** ou da assistência de seu administrador de domínio.|*Steps for prestaging an account for a clustered service or application* (Etapas para pré-preparar uma conta para um serviço ou aplicativo clusterizado) no [Failover Cluster Step-by-Step Guide: Configuring Accounts in Active Directory](http://technet.microsoft.com/library/cc731002\(WS.10\).aspx#BKMK_steps_precreating2)(Guia passo a passo do cluster de failover: configurando contas no Active Directory).|  
  
> [!TIP]  
>  Geralmente, é mais simples não pré-preparar a conta de computador para um nome de rede virtual de ouvinte. Se possível, deixe a conta ser criada e configurada automaticamente ao executar o Assistente de Alta Disponibilidade do WSFC.  
  
###  <a name="SqlPermissions"></a> Permissões do SQL Server  
  
|Tarefa|Permissões|  
|----------|-----------------|  
|Para criar um ouvinte de grupo de disponibilidade|Requer a associação na função de servidor fixa **sysadmin** e a permissão de servidor CREATE AVAILABILITY GROUP, a permissão ALTER ANY AVAILABILITY GROUP ou a permissão CONTROL SERVER.|  
|Para modificar um ouvinte de grupo de disponibilidade existente|Requer a permissão ALTER AVAILABILITY GROUP no grupo de disponibilidade, a permissão CONTROL AVAILABILITY GROUP, a permissão ALTER ANY AVAILABILITY GROUP ou a permissão CONTROL SERVER.|  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
> [!TIP]  
>  O [Assistente de Novo Grupo de Disponibilidade](../../../database-engine/availability-groups/windows/use-the-new-availability-group-dialog-box-sql-server-management-studio.md) dá suporte à criação do ouvinte para um novo grupo de disponibilidade.  
  
 **Para criar ou configurar um ouvinte de grupo de disponibilidade**  
  
1.  No Pesquisador de Objetos, conecte-se à instância do servidor que hospeda a réplica primária do grupo de disponibilidade e clique no nome do servidor para expandir a árvore de servidores.  
  
2.  Expanda os nós **Alta Disponibilidade AlwaysOn** e **Grupos de Disponibilidade** .  
  
3.  Clique no grupo de disponibilidade cujo ouvinte você deseja configurar e escolha uma das alternativas a seguir:  
  
    -   Para criar um ouvinte, clique com o botão direito do mouse no nó **Ouvintes do Grupo de Disponibilidade** e selecione o comando **Novo Ouvinte** . Isso abre a caixa de diálogo **Novo Ouvinte do Grupo de Disponibilidade** . Para obter mais informações, consulte [Adicionar Ouvinte do Grupo de Disponibilidade (caixa de diálogo)](#AddAgListenerDialog), posteriormente neste tópico.  
  
    -   Para alterar o número da porta de um ouvinte existente, expanda o nó **Ouvintes do Grupo de Disponibilidade** , clique com o botão direito do mouse no ouvinte e selecione o comando **Propriedades** . Digite o novo número da porta no campo **Porta** e clique em **OK**.  
  
###  <a name="AddAgListenerDialog"></a> Novo Ouvinte do Grupo de Disponibilidade (caixa de diálogo)  
 **Nome DNS do Ouvinte**  
 Especifica o nome de host DNS do ouvinte de grupo de disponibilidade. O nome DNS é uma cadeia de caracteres que deve ser exclusivo no domínio e no NetBIOS. Este nome pode conter somente caracteres alfanuméricos, traços (-) e hífens (_), em qualquer ordem. Os nomes de host DNS diferenciam maiúsculas de minúsculas. O tamanho máximo é de 15 caracteres.  
  
 Para obter mais informações, consulte [Requisitos para o nome DNS de um ouvinte de grupo de disponibilidade](#DNSnameReqs), posteriormente neste tópico.  
  
 **Porta**  
 A porta TCP usada pelo ouvinte.  
  
 **Modo de Rede**  
 Indica o protocolo TCP usado pelo ouvinte, pode ser:  
  
 **DHCP**  
 O ouvinte usará um endereço IP dinâmico que é atribuído por um servidor que executa o Protocolo DHCP. O DHCP está limitado a uma única sub-rede.  
  
> [!IMPORTANT]  
>  Nós não recomendamos o DHCP em ambiente de produção. Se houver um tempo de inatividade e a concessão do IP do DHCP expirar, a hora adicional deverá registrar o novo endereço IP da rede DHCP que está associado ao nome DNS do ouvinte e afetará a conectividade do cliente. No entanto, o DHCP é bom para configurar seu ambiente de desenvolvimento e teste para verificar as funções básicas de grupos de disponibilidade e para integração com seus aplicativos.  
  
 **IP Estático**  
 O ouvinte usará um ou mais endereços IP estáticos. Os endereços IP adicional são opcionais. Para criar um ouvinte do grupo de disponibilidade em várias sub-redes, você deve especificar para cada sub-rede um endereço IP estático na configuração do ouvinte. Entre em contato com seu administrador de rede para obter esses endereços IP estáticos.  
  
 Se você selecionar **IP Estático** , uma grade de sub-rede será exibida abaixo do campo **Modo de Rede** . Essa grade exibe informações sobre cada sub-rede que pode ser acessada por este ouvinte de grupo de disponibilidade. Essa grade estará vazia até que você adicione um endereço IP estático clicando em **Adicionar**.  
  
 As colunas são apresentadas assim:  
  
 **Sub-rede**  
 Exibe o identificador de cada sub-rede que você adiciona ao ouvinte do grupo de disponibilidade.  
  
 **Endereço IP**  
 Exibe o endereço IP de uma determinada sub-rede.  Para uma determinada sub-rede, o endereço IP é um endereço IPv4 ou um endereço IPv6.  
  
 **Adicionar**  
 Clique para adicionar um endereço IP estático a uma sub-rede selecionada ou a outra sub-rede para este ouvinte. Essa ação abre a caixa de diálogo **Adicionar Endereço IP** . Para obter mais informações, consulte o tópico de ajuda [Caixa de diálogo Adicionar Endereço IP &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/add-ip-address-dialog-box-sql-server-management-studio.md).  
  
 **Remover**  
 Clique para remover a sub-rede selecionada deste ouvinte.  
  
 **OK**  
 Clique para criar o ouvinte do grupo de disponibilidade especificado.  
  
##  <a name="TsqlProcedure"></a> Usando o Transact-SQL  
 **Para criar ou configurar um ouvinte de grupo de disponibilidade**  
  
1.  Conecte-se à instância de servidor que hospeda a réplica primária.  
  
2.  Use a opção LISTENER da instrução [CREATE AVAILABILITY GROUP](../../../t-sql/statements/create-availability-group-transact-sql.md) ou a opção ADD LISTENER da instrução [ALTER AVAILABILITY GROUP](../../../t-sql/statements/alter-availability-group-transact-sql.md) .  
  
     O exemplo a seguir adiciona um ouvinte de grupo de disponibilidade a um grupo de disponibilidade existente denominado `MyAg2`. Um nome DNS exclusivo, `MyAg2ListenerIvP6`, é especificado para esse ouvinte. As duas réplicas estão em sub-redes diferentes e, portanto, como recomendado, o ouvinte usa endereços IP estáticos. Para cada uma das duas réplicas de disponibilidade, a cláusula WITH IP especifica um endereço IP estático `2001:4898:f0:f00f::cf3c and 2001:4898:e0:f213::4ce2`, que usa o formato IPv6. Este exemplo também especifica o uso do argumento PORT opcional para especificar a porta `60173` como a porta do ouvinte.  
  
    ```  
    ALTER AVAILABILITY GROUP MyAg2   
          ADD LISTENER ‘MyAg2ListenerIvP6’ ( WITH IP ( ('2001:db88:f0:f00f::cf3c'),('2001:4898:e0:f213::4ce2') ) , PORT = 60173 );   
    GO  
  
    ```  
  
##  <a name="PowerShellProcedure"></a> Usando o PowerShell  
 **Para criar ou configurar um ouvinte de grupo de disponibilidade**  
  
1.  Altere o diretório (**cd**) para a instância de servidor que hospeda a réplica primária.  
  
2.  Para criar ou modificar um ouvinte de grupo de disponibilidade, use um dos cmdlets a seguir:  
  
     **New-SqlAvailabilityGroupListener**  
     Cria um novo ouvinte de grupo de disponibilidade e conecta-o a um grupo de disponibilidade existente.  
  
     Por exemplo, o comando **New-SqlAvailabilityGroupListener** a seguir cria um ouvinte do grupo de disponibilidade denominado `MyListener` para o grupo de disponibilidade `MyAg`. Esse ouvinte usará o endereço IPv4 passado para o parâmetro **-StaticIp** como seu endereço IP virtual.  
  
    ```  
    New-SqlAvailabilityGroupListener -Name MyListener `   
    -StaticIp '192.168.3.1/255.255.252.0' `   
    -Path SQLSERVER:\Sql\Computer\Instance\AvailabilityGroups\MyAg  
  
    ```  
  
     **Set-SqlAvailabilityGroupListener**  
     Modifica a configuração de porta em um ouvinte de grupo de disponibilidade existente.  
  
     Por exemplo, o comando **Set-SqlAvailabilityGroupListener** a seguir define o número da porta para o ouvinte do grupo de disponibilidade denominado `MyListener` para o `1535`. Esta porta é usada para ouvir conexões para o ouvinte.  
  
    ```  
    Set-SqlAvailabilityGroupListener -Port 1535 `   
    -Path SQLSERVER:\Sql\PrimaryServer\InstanceName\AvailabilityGroups\MyAg\AGListeners\MyListener  
  
    ```  
  
     **Add-SqlAGListenerstaticIp**  
     Adiciona um endereço IP estático à configuração de um ouvinte de grupo de disponibilidade existente. O endereço IP poderá ser um endereço IPv4 com sub-rede ou um endereço IPv6.  
  
     Por exemplo, o comando **Add-SqlAGListenerstaticIp** a seguir adiciona um endereço IPv4 estático ao ouvinte do grupo de disponibilidade `MyListener` no grupo de disponibilidade `MyAg`. Este endereço IPv6 serve como o endereço IP virtual do ouvinte na sub-rede `255.255.252.0`. Se o grupo de disponibilidade abranger diversas sub-redes, você deverá adicionar um endereço IP estático para cada sub-rede para o ouvinte.  
  
    ```  
    $path = "SQLSERVER:\SQL\PrimaryServer\InstanceName\AvailabilityGroups\MyAg\AGListeners\ MyListener" `   
    Add-SqlAGListenerstaticIp -Path $path `   
    -StaticIp "2001:0db8:85a3:0000:0000:8a2e:0370:7334"  
    ```  
  
    > [!NOTE]  
    >  Para exibir a sintaxe de um cmdlet, use o cmdlet **Get-Help[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] no ambiente do**  PowerShell. Para obter mais informações, consulte [Get Help SQL Server PowerShell](../../../relational-databases/scripting/get-help-sql-server-powershell.md).  
  
 **Para configurar e usar o provedor do SQL Server PowerShell**  
  
-   [Provedor do SQL Server PowerShell](../../../relational-databases/scripting/sql-server-powershell-provider.md)  
  
## <a name="troubleshooting"></a>Solução de problemas  
  
###  <a name="ADQuotas"></a> Falha ao criar um ouvinte de grupo de disponibilidade devido a cotas do Active Directory  
 Pode haver falha na criação de um novo ouvinte de grupo de disponibilidade porque você atingiu uma cota do Active Directory para a conta da máquina do nó de cluster participante.  Para obter mais informações, consulte os artigos a seguir.  
  
-   [Como solucionar problemas da conta do serviço de cluster quando ela modifica objetos de computador](http://support.microsoft.com/kb/307532)  
  
-   [Cotas do Active Directory](http://technet.microsoft.com/library/cc904295\(WS.10\).aspx)  
  
##  <a name="FollowUp"></a> Acompanhamento: após criar um ouvinte do grupo de disponibilidade  
  
###  <a name="MultiSubnetFailover"></a> Palavra-chave MultiSubnetFailover e recursos associados  
 **MultiSubnetFailover** é uma nova palavra-chave da cadeia de conexão usada para habilitar failover mais rápido com os Grupos de Disponibilidade AlwaysOn e Instâncias de cluster de failover AlwaysOn no SQL Server 2012. Os três sub-recursos a seguir são habilitados quando `MultiSubnetFailover=True` está definido na cadeia de conexão:  
  
-   Um failover de várias sub-redes mais rápido para um ouvinte de várias sub-redes para um Grupo de Disponibilidade AlwaysOn ou instâncias de cluster de failover.  
  
-   Um failover de sub-rede única mais rápido para um ouvinte de sub-rede única para um Grupo de Disponibilidade AlwaysOn ou instâncias de cluster de failover.  
  
    -   Esse recurso é usado ao conectar-se a um ouvinte que tem um IP único em uma única sub-rede. Isso realiza tentativas de conexão de TCP mais agressivas para acelerar os failovers de sub-rede única.  
  
-   A resolução de instância nomeada para uma instância de cluster de failover AlwaysOn de várias sub-redes.  
  
    -   Isso é para adicionar o suporte à resolução de instância nomeada para uma instância de cluster de failover AlwaysOn com diversos pontos de extremidade de sub-rede.  
  
 **Não há suporte para MultiSubnetFailover=True pelo .NET Framework 3.5 ou OLEDB**  
  
 **Problema:** se seu Grupo de Disponibilidade ou Instância de Cluster de Failover tiver um nome de ouvinte (conhecido como o nome da rede ou o Ponto de Acesso para Cliente no Gerenciador de Cluster do WSFC) que dependa dos diversos endereços IP de diferentes sub-redes, e você estiver usando o ADO.NET com .NET Framework 3.5SP1 ou SQL Native Client 11.0 OLEDB, possivelmente 50% das suas solicitações de conexão de cliente para o ouvinte do grupo de disponibilidade atingirão um tempo limite de conexão.  
  
 **Soluções alternativas:** é recomendável que você execute uma das tarefas a seguir.  
  
-   Se você não tiver a permissão para manipular recursos de cluster, altere o tempo limite da conexão para 30 segundos (esse valor resulta em um período de tempo limite TCP de 20 segundos mais um buffer de 10 segundos).  
  
     **Prós**: se ocorrer um failover de sub-rede cruzado, o tempo de recuperação do cliente será rápido.  
  
     **Contras**: metade das conexões de cliente demorarão mais de 20 segundos.  
  
-   Se você tiver permissão para manipular os recursos de cluster, a abordagem mais recomendada é definir o nome de rede do ouvinte do grupo de disponibilidade como `RegisterAllProvidersIP=0`. Para obter mais informações, consulte "Configuração de RegisterAllProvidersIP”, mais adiante nesta seção.  
  
     **Prós:** você não precisa aumentar o valor de tempo limite de conexão de cliente.  
  
     **Contras** : se um failover de sub-rede cruzado ocorrer, o tempo de recuperação do cliente poderá ser de 15 minutos ou mais, dependendo da configuração de **HostRecordTTL** e da configuração da agenda de replicação DNS/AD entre sites.  
  
###  <a name="RegisterAllProvidersIP"></a> Configuração RegisterAllProvidersIP  
 Quando você usa o [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], o [!INCLUDE[tsql](../../../includes/tsql-md.md)]ou o PowerShell para criar um ouvinte de grupo de disponibilidade, o Ponto de Acesso para Cliente é criado no WSFC com a propriedade **RegisterAllProvidersIP** definida como 1 (true). O efeito de esse valor de propriedade depende da cadeia de conexão do cliente, da seguinte maneira:  
  
-   Cadeias de conexão que definem **MultiSubnetFailover** como true  
  
     [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] define a propriedade  **RegisterAllProvidersIP** como 1 para reduzir o tempo de reconexão após um failover para clientes cujas cadeias de conexão de cliente especificam `MultiSubnetFailover = True`, como recomendado. Observe que para usufruir das vantagens do recurso de várias sub-redes do ouvinte, seus clientes podem exigir um provedor de dados que dê suporte à palavra-chave **MultiSubnetFailover** . Para obter informações sobre o suporte do driver para failover de várias sub-redes, consulte [Conectividade de cliente AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/always-on-client-connectivity-sql-server.md).  
  
     Para obter informações sobre clustering de várias sub-redes, consulte [Clustering de várias sub-redes do SQL Server &#40;SQL Server&#41;](../../../sql-server/failover-clusters/windows/sql-server-multi-subnet-clustering-sql-server.md).  
  
    > [!TIP]  
    >  Quando `RegisterAllProvidersIP = 1`, se você executar o Assistente para Validar Configuração do WSFC no cluster WSFC, o assistente gerará a seguinte mensagem de aviso:  
    >   
    >  “A propriedade RegisterAllProviderIP para nome de rede 'Name:<network_name>' é definida como 1. Para a configuração do cluster atual, este valor deve ser definido como 0.”  
    >   
    >  Ignore esta mensagem.  
  
-   Cadeias de conexão que não definem **MultiSubnetFailover** como true  
  
     Quando `RegisterAllProvidersIP = 1`, quaisquer clientes cujas cadeias de conexão não usem `MultiSubnetFailover = True`encontrarão conexões de alta latência. Isso ocorre porque esses clientes tentam conexões com todos os IPs em sequência. Em contrapartida, se **RegisterAllProvidersIP** for alterado para 0, o endereço IP ativo será registrado no Ponto de Acesso para Cliente no cluster WSFC, reduzindo a latência para clientes herdados. Portanto, se você tiver clientes herdados que precisem se conectar a um ouvinte de grupo de disponibilidade e não possa usar a propriedade **MultiSubnetFailover** , recomendamos alterar **RegisterAllProvidersIP** para 0.  
  
    > [!IMPORTANT]  
    >  Quando você cria um ouvinte do grupo de disponibilidade no cluster WSFC (GUI do Gerenciador de Cluster de Failover), **RegisterAllProvidersIP** será 0 (false) por padrão.  
  
###  <a name="HostRecordTTL"></a> Configuração HostRecordTTL  
 Por padrão, os clientes armazenam em cache registros DNS do cluster por 20 minutos.  Os clientes herdados poderão se reconectar mais rapidamente reduzindo a configuração **HostRecordTTL**, a TTL (vida útil) do registro armazenado em cache.  No entanto, a redução da configuração **HostRecordTTL** também pode resultar em maior tráfego para os servidores DN.  
  
###  <a name="SampleScript"></a> Exemplo de script PowerShell para desabilitar RegisterAllProvidersIP e reduzir o TTL  
 O exemplo do PowerShell a seguir demonstra como configurar os parâmetros de cluster **RegisterAllProvidersIP** e **HostRecordTTL** para o recurso de ouvinte.  O registro DNS será armazenado em cache por 5 minutos, e não pelos 20 minutos padrão.  A modificação dos dois parâmetros de cluster pode reduzir o tempo de conexão ao endereço IP correto após um failover para clientes herdados que não podem usar o parâmetro **MultiSubnetFailover** .  Substitua `yourListenerName` pelo nome do ouvinte que você está alterando.  
  
```  
Import-Module FailoverClusters  
Get-ClusterResource yourListenerName | Set-ClusterParameter RegisterAllProvidersIP 0   
Get-ClusterResource yourListenerName|Set-ClusterParameter HostRecordTTL 300  
Stop-ClusterResource yourListenerName  
Start-ClusterResource yourListenerName  
```  
  
 Para obter mais informações sobre os tempos de recuperação durante o failover, consulte [Client Recovery Latency During Failover](../../../sql-server/failover-clusters/windows/sql-server-multi-subnet-clustering-sql-server.md#DNS).  
  
###  <a name="FollowUpRecommendations"></a> Recomendações de acompanhamento  
 Após criar um ouvinte de grupo de disponibilidade:  
  
-   Peça ao administrador da rede para reservar o endereço IP do ouvinte para seu uso exclusivo.  
  
-   Informe o nome do host DNS do ouvinte aos desenvolvedores de aplicativos para uso em cadeias de conexão ao pedir conexões cliente com esse grupo de disponibilidade.  
  
-   Incentive os desenvolvedores a atualizarem cadeias de conexão do cliente para especificar `MultiSubnetFailover = True`, se possível. Para obter informações sobre o suporte do driver para failover de várias sub-redes, consulte [Conectividade de cliente AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/always-on-client-connectivity-sql-server.md).  
  
###  <a name="CreateAdditionalListener"></a> Criar um ouvinte adicional para um grupo de disponibilidade (opcional)  
 Depois de criar um ouvinte pelo SQL Server, você poderá adicionar um ouvinte adicional, da seguinte maneira:  
  
1.  Crie o ouvinte usando uma das ferramentas a seguir:  
  
    -   **Usando o Gerenciador de Cluster de Failover do WSFC:**  
  
        1.  Adicione um ponto de acesso para cliente e configure o endereço IP.  
  
        2.  Faça o ouvinte ficar online.  
  
        3.  Adicione uma dependência para o recurso do grupo de disponibilidade do WSFC.  
  
         Para obter informações sobre as caixas de diálogo e guias do Gerenciador de Cluster de Failover, consulte [Interface do usuário: o snap-in gerenciador de cluster de failover](http://technet.microsoft.com/library/cc772502.aspx).  
  
    -   **Usando o Windows PowerShell para clusters de failover:**  
  
        1.  Use [Add-ClusterResource](http://technet.microsoft.com/library/ee460983.aspx) para criar um nome de rede e os recursos do endereço IP.  
  
        2.  Use [Start-ClusterResource](http://technet.microsoft.com/library/ee461056.aspx) para iniciar o recurso de nome de rede.  
  
        3.  Use [Add-ClusterResourceDependency](http://technet.microsoft.com/library/ee461014.aspx) para definir a dependência entre o nome da rede e o recurso do Grupo de Disponibilidade do SQL Server existente.  
  
         Para obter informações sobre como usar o Windows PowerShell para clusters de failover, consulte [Visão geral de comandos do gerenciador de servidor](http://technet.microsoft.com/library/cc732757.aspx#BKMK_wps).  
  
2.  Inicie a escuta do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] no novo ouvinte. Após criar um ouvinte adicional, conecte a instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que hospeda a réplica principal do grupo de disponibilidade e use [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../../includes/tsql-md.md)]ou PowerShell para modificar a porta do ouvinte.  
  
 Para obter mais informações, consulte [How to create multiple listeners for same availability group](https://blogs.msdn.microsoft.com/sqlalwayson/2012/02/03/how-to-create-multiple-listeners-for-same-availability-group-goden-yao/) (Como criar vários ouvintes para o mesmo grupo de disponibilidade) (um blog da equipe do SQL Server AlwaysOn).  
  
##  <a name="RelatedTasks"></a> Tarefas relacionadas  
  
-   [Exibir propriedades do ouvinte do grupo de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/view-availability-group-listener-properties-sql-server.md)  
  
-   [Remover um ouvinte do grupo de disponibilidade &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/remove-an-availability-group-listener-sql-server.md)  
  
##  <a name="RelatedContent"></a> Conteúdo relacionado  
  
-   [How to create multiple listeners for same availability group](https://blogs.msdn.microsoft.com/sqlalwayson/2012/02/03/how-to-create-multiple-listeners-for-same-availability-group-goden-yao/)  
  
-   [Blog da equipe do AlwaysOn do SQL Server: o blog oficial da equipe do AlwaysOn do SQL Server](https://blogs.msdn.microsoft.com/sqlalwayson/)  
  
## <a name="see-also"></a>Consulte Também  
 [Visão geral dos grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Ouvintes do grupo de disponibilidade, conectividade de cliente e failover de aplicativo &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/listeners-client-connectivity-application-failover.md)   
 [Clustering de várias sub-redes do SQL Server &#40;SQL Server&#41;](../../../sql-server/failover-clusters/windows/sql-server-multi-subnet-clustering-sql-server.md)  
  
  
