---
title: Configurar o Firewall do Windows para permitir acesso ao SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 06/22/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- Windows Firewall ports
- WMI firewall ports
- Windows Firewall [Database Engine]
- firewall systems, configuring
- advfirewall
- firewall systems
- rules firewall
- firewall systems, overview and port list
- 1433 TCP port
- portopening using netsh
- ports [SQL Server], TCP
- netsh to open firewall ports
ms.assetid: f55c6a0e-b6bd-4803-b51a-f3a419803024
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 7b254c1e7d814af64117343d98d3275e5ac66d64
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48128986"
---
# <a name="configure-the-windows-firewall-to-allow-sql-server-access"></a>Configure the Windows Firewall to Allow SQL Server Access
  Os sistemas de Firewall ajudam a impedir o acesso não autorizado aos recursos do computador. Se um firewall estiver ativado mas não corretamente configurado, as tentativas de conexão ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] poderão ser bloqueadas.  
  
 Para acessar uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] através de um firewall, é necessário configurar o firewall no computador que está executando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . O firewall é um componente do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows. Você também pode instalar um firewall de outra empresa. Este tópico discute como configurar o firewall do Windows, mas os princípios básicos se aplicam a outros programas de firewall.  
  
> [!NOTE]  
>  Este tópico apresenta uma visão geral da configuração do firewall e resume informações de interesse de um administrador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para obter mais informações sobre o firewall e informações sobre firewall autoritativo, consulte a documentação do firewall, como [Windows Firewall with Advanced Security and IPsec](http://go.microsoft.com/fwlink/?LinkID=116904).  
  
 Os usuários que já estão familiarizados com o item **Firewall do Windows** no Painel de Controle e com o snap-in Firewall do Windows com Segurança Avançada do MMC (Console de Gerenciamento Microsoft) e sabem as configurações de firewall que desejam definir podem passar diretamente para os tópicos desta lista:  
  
-   [Configurar um Firewall do Windows para acesso ao Mecanismo de Banco de Dados](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md)  
  
-   [Configurar o Firewall do Windows para permitir o acesso ao Analysis Services](../../../2014/analysis-services/instances/configure-the-windows-firewall-to-allow-analysis-services-access.md)  
  
-   [Configurar um firewall para acesso ao servidor de relatório](../../reporting-services/report-server/configure-a-firewall-for-report-server-access.md)  
  

  
##  <a name="BKMK_basic"></a> Informações básicas sobre o firewall  
 Os firewalls inspecionam pacotes recebidos e os comparam a um conjunto de regras. Se as regras autorizarem o pacote, o firewall o transmitirá ao protocolo TCP/IP para processamento adicional. Se as regras não autorizarem o pacote, o firewall o descartará e, se o log estiver habilitado, criará uma entrada em seu arquivo de log.  
  
 A lista de tráfego permitido é preenchida de uma das seguintes maneiras:  
  
-   Quando o computador que tem o firewall habilitado inicia a comunicação, o firewall cria uma entrada na lista de forma que a resposta seja permitida. A resposta recebida é considerada tráfego solicitado, e você não precisa configurá-la.  
  
-   Um administrador configura as exceções do firewall. Isto permite acesso a determinados programas executados em seu computador ou acesso a portas de conexão especificadas do computador. Nesse caso, o computador aceita tráfego de entrada não solicitado quando funciona como servidor, ouvinte ou item par. Esse é o tipo de configuração que deve ser concluída para que se possa estabelecer conexão com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Escolher a estratégia de firewall é uma tarefa mais complexa do que simplesmente decidir se uma dada porta deve ficar aberta ou fechada. Ao elaborar uma estratégia de firewall para sua empresa, é importante que você considere todas as regras e opções de configuração disponíveis. Este tópico não examina todas as possíveis opções de firewall. É recomendável analisar os seguintes documentos:  
  
 [Guia de Introdução ao Firewall do Windows com Segurança Avançada](http://go.microsoft.com/fwlink/?LinkId=116080)  
  
 [Windows Firewall with Advanced Security Design Guide](http://go.microsoft.com/fwlink/?LinkId=116904)  
  
 [Introduction to Server and Domain Isolation](http://go.microsoft.com/fwlink/?LinkId=116081)  
  
##  <a name="BKMK_default"></a> Configurações padrão do firewall  
 A primeira etapa do planejamento da configuração do firewall é determinar o status atual do firewall do sistema operacional. Se o sistema operacional foi atualizado de uma versão anterior, as configurações de firewall anteriores podem ter sido preservadas. Além disso, as configurações de firewall podem ter sido alteradas por outro administrador ou por uma Política de Grupo do seu domínio.  
  
> [!NOTE]  
>  A ativação do firewall afetará outros programas que acessam este computador, como o compartilhamento de arquivos e impressoras, e conexões de área de trabalho remota. Os administradores devem considerar todos os aplicativos que estão em execução no computador antes de ajustar as configurações do firewall.  
  
##  <a name="BKMK_programs"></a> Programas para configurar o firewall  
 Há três maneiras de configurar o Firewall do Windows.  
  
-   **Item Firewall do Windows no Painel de Controle**  
  
     O item **Firewall do Windows** pode ser aberto do Painel de Controle.  
  
    > [!IMPORTANT]  
    >  Alterações feitas no item **Firewall do Windows** do Painel de Controle afetam somente o perfil atual. Dispositivos móveis, como laptops, não devem usar o item **Firewall do Windows** do Painel de Controle, uma vez que o perfil pode mudar quando conectado em uma configuração diferente. Assim, o perfil anteriormente configurado não terá efeito. Para obter mais informações sobre perfis, consulte [Guia de introdução ao Firewall do Windows com Segurança Avançada](http://go.microsoft.com/fwlink/?LinkId=116080).  
  
     O item **Firewall do Windows** no Painel de Controle permite configurar opções básicas. Entre elas estão as seguintes:  
  
    -   Ativar ou desativar o item **Firewall do Windows** no Painel de Controle  
  
    -   Habilitar e desabilitar regras  
  
    -   Conceder exceções para portas e programas  
  
    -   Definir algumas restrições de escopo  
  
     O item **Firewall do Windows** no Painel de Controle é mais apropriado para usuários que não têm experiência em configuração de firewall e que estão configurando opções básicas do firewall para computadores que não são móveis. Você também pode abrir o **Firewall do Windows** item no painel de controle do `run` comando usando o procedimento a seguir:  
  
    #### <a name="to-open-the-windows-firewall-item"></a>Para abrir o item Firewall do Windows  
  
    1.  No menu **Iniciar** , clique em **Executar**e digite `firewall.cpl`.  
  
    2.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
-   **Console de Gerenciamento Microsoft (MMC)**  
  
     O snap-in do MMC Firewall do Windows com Segurança Avançada permite definir configurações de firewall mais avançadas. Este snap-in apresenta a maioria das opções de firewall de um jeito fácil de usar, além de todos os perfis de firewall. Para obter mais informações, veja [Usando o snap-in Firewall do Windows com Segurança Avançada](#BKMK_WF_msc) , mais adiante neste tópico.  
  
-   **netsh**  
  
     A ferramenta **netsh.exe** pode ser usada por um administrador para configurar e monitorar computadores baseados no Windows em um prompt de comando ou por meio de um arquivo em lotes **.** Com a ferramenta **netsh** , você pode direcionar os comandos de contexto inseridos para o auxiliar apropriado que, em seguida, executará o comando. Um auxiliar é um arquivo .dll (Dynamic Link Library) que estende a funcionalidade da ferramenta **netsh** fornecendo configuração, monitoramento e suporte para um ou mais serviços, utilitários ou protocolos. Todos os sistemas operacionais que dão suporte ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] têm um auxiliar de firewall. [!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)] também possui um auxiliar avançado de firewall chamado **advfirewall**. Os detalhes sobre como usar o **netsh** não são abordados neste tópico. No entanto, muitas das opções de configuração descritas podem ser configuradas usando o **netsh**. Por exemplo, execute o seguinte script em um prompt de comando para abrir a porta TCP 1433:  
  
    ```  
    netsh firewall set portopening protocol = TCP port = 1433 name = SQLPort mode = ENABLE scope = SUBNET profile = CURRENT  
    ```  
  
     Um exemplo semelhante usando o auxiliar do Firewall do Windows para Segurança Avançada:  
  
    ```  
    netsh advfirewall firewall add rule name = SQLPort dir = in protocol = tcp action = allow localport = 1433 remoteip = localsubnet profile = DOMAIN  
    ```  
  
     Para obter mais informações sobre o **netsh**, consulte os seguintes links:  
  
    -   [Como usar a ferramenta Netsh.exe e as opções de linha de comando](http://support.microsoft.com/kb/242468)  
  
    -   [Como usar o contexto de "netsh advfirewall firewall" em vez do contexto "netsh firewall" para controlar o comportamento do Firewall do Windows no Windows Server 2008 e no Windows Vista](http://support.microsoft.com/kb/947709)  
  
    -   [Comando "netsh firewall" juntamente com o parâmetro "perfil = all" não configura o perfil público em um computador com Windows Vista](http://support.microsoft.com/kb/947213)  
  
## <a name="ports-used-by-includessnoversionincludesssnoversion-mdmd"></a>Portas usadas pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 As tabelas a seguir podem ajudar a identificar as portas que são usadas pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
###  <a name="BKMK_ssde"></a> Ports Used By the Database Engine  
 A tabela a seguir lista as portas que são mais usadas pelo [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
|Cenário|Porta|Comentários|  
|--------------|----------|--------------|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] executando sobre TCP|Porta TCP 1433|Esta é a porta mais comum permitida pelo firewall. Ela se aplica a conexões de rotina com a instalação padrão do [!INCLUDE[ssDE](../../includes/ssde-md.md)]ou com uma instância nomeada, que é a única em execução no computador. (Existem considerações especiais para instâncias nomeadas. Veja [Portas dinâmicas](#BKMK_dynamic_ports) , mais adiante neste tópico.)|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] na configuração padrão|A porta TCP é uma porta dinâmica determinada no momento em que o [!INCLUDE[ssDE](../../includes/ssde-md.md)] é iniciado.|Consulte a discussão abaixo, na seção [Portas dinâmicas](#BKMK_dynamic_ports). A porta UDP 1434 pode ser necessária para o Serviço Navegador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] quando você usa instâncias nomeadas.|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] quando configuradas para usar uma porta fixa|O número de porta configurado pelo administrador.|Consulte a discussão abaixo, na seção [Portas dinâmicas](#BKMK_dynamic_ports).|  
|Conexão de Administrador Dedicada|Porta TCP 1434 para a instância padrão. Outras portas são usadas para instâncias nomeadas. Verifique o número da porta no log de erros.|Por padrão, as conexões remotas com a Conexão de Administrador Dedicada (DAC) não são habilitadas. Para habilitar a DAC remota, use a faceta Configuração da Área da Superfície. Para obter mais informações, consulte [Surface Area Configuration](../../relational-databases/security/surface-area-configuration.md).|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Serviço Navegador|Porta UDP 1434|O serviço Navegador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verifica se há conexões de entrada com uma instância nomeada e informa para o cliente o número da porta TCP que corresponde a essa instância nomeada. Normalmente o serviço Navegador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é iniciado sempre que são usadas instâncias nomeadas do [!INCLUDE[ssDE](../../includes/ssde-md.md)] . O serviço Navegador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não precisa ser iniciado se o cliente está configurado para se conectar à porta específica da instância nomeada.|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] executando em um ponto de extremidade HTTP.|Pode ser especificada quando um ponto de extremidade HTTP é criado. O padrão é a porta TCP 80 para tráfego CLEAR_PORT e 443 para tráfego SSL_PORT.|Usada para uma conexão HTTP por meio de uma URL.|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] executando sobre um ponto de extremidade HTTPS|Porta TCP 443|Usada para uma conexão HTTPS por meio de uma URL. HTTPS é uma conexão HTTP que usa o protocolo SSL.|  
|[!INCLUDE[ssSB](../../includes/sssb-md.md)]|Porta TCP 4022. Para verificar a porta usada, execute a seguinte consulta:<br /><br /> `SELECT name, protocol_desc, port, state_desc`<br /><br /> `FROM sys.tcp_endpoints`<br /><br /> `WHERE type_desc = 'SERVICE_BROKER'`|Não existe uma porta padrão para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssSB](../../includes/sssb-md.md)], mas esta é a configuração convencional usada nos exemplos dos Manuais Online.|  
|Espelhamento de banco de dados|Porta escolhida pelo administrador. Para determinar a porta, execute a seguinte consulta:<br /><br /> `SELECT name, protocol_desc, port, state_desc FROM sys.tcp_endpoints`<br /><br /> `WHERE type_desc = 'DATABASE_MIRRORING'`|Não existe uma porta padrão para o espelhamento de banco de dados, mas os exemplos dos Manuais Online usam a porta TCP 7022. É muito importante evitar interromper um ponto de extremidade de espelhamento em uso, principalmente no modo de alta segurança com failover automático. Sua configuração de firewall deve evitar dividir o quorum. Para obter mais informações, consulte [Especificar um endereço de rede do servidor &#40;Espelhamento de banco de dados&#41;](../../database-engine/database-mirroring/specify-a-server-network-address-database-mirroring.md).|  
|Replicação|As conexões de replicação com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usam as portas normais típicas do [!INCLUDE[ssDE](../../includes/ssde-md.md)] (porta TCP 1433 para a instância padrão etc.)<br /><br /> A sincronização da Web e o acesso FTP/UNC para instantâneo de replicação exigem a abertura de portas adicionais no firewall. Para transferir o esquema e os dados iniciais de um local para outro, a replicação pode usar o FTP (porta TCP 21) ou sincronizar via HTTP (porta TCP 80) ou Compartilhamento de Arquivos. O compartilhamento de arquivos usa a porta UDP 137 e 138, e a porta TCP 139 caso esteja usando o NetBIOS. O compartilhamento de arquivos usa a porta TCP 445.|Para sincronização por HTTP, a replicação usa o ponto de extremidade do IIS (portas configuráveis, mas o padrão é a porta 80), mas o processo do IIS se conecta ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] back-end através das portas padrão (1433 para a instância padrão).<br /><br /> Durante a sincronização da Web usando FTP, a transferência por FTP ocorre entre o IIS e o publicador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , e não entre o assinante e o IIS.|  
|[!INCLUDE[tsql](../../includes/tsql-md.md)] depurador|Porta TCP 135<br /><br /> Consulte [Considerações especiais sobre a porta 135](#BKMK_port_135)<br /><br /> A exceção [IPsec](#BKMK_IPsec) também pode ser necessária.|Se estiver usando [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)], no computador host [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] , você também deverá adicionar **Devenv.exe** à lista Exceções e abrir a porta TCP 135.<br /><br /> Se estiver usando o [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], no computador host [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] , você também deverá adicionar **ssms.exe** à lista Exceções e abrir a porta TCP 135. Para obter mais informações, consulte [configurar o depurador do Transact-SQL](../../relational-databases/scripting/configure-firewall-rules-before-running-the-tsql-debugger.md).|  
  
 Para obter instruções passo a passo para configurar o Firewall do Windows para o [!INCLUDE[ssDE](../../includes/ssde-md.md)], veja [Configurar um Firewall do Windows para acesso ao Mecanismo de Banco de Dados](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md).  
  
####  <a name="BKMK_dynamic_ports"></a> Portas dinâmicas  
 Por padrão, as instâncias nomeadas (incluindo [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]) usam portas dinâmicas. Isso significa que sempre que o [!INCLUDE[ssDE](../../includes/ssde-md.md)] é iniciado, identifica uma porta disponível e usa esse número de porta. Se a instância nomeada for a única instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] instalada, provavelmente ele usará a porta TCP 1433. Se outras instâncias do [!INCLUDE[ssDE](../../includes/ssde-md.md)] estiverem instaladas, provavelmente ele usará outra porta TCP. Como a porta selecionada pode mudar cada vez que o [!INCLUDE[ssDE](../../includes/ssde-md.md)] é iniciado, é difícil configurar o firewall para permitir acesso para o número de porta correto. Portanto, se um firewall for usado, é recomendável reconfigurar o [!INCLUDE[ssDE](../../includes/ssde-md.md)] para usar sempre o mesmo número de porta. Isso é chamado de porta fixa ou porta estática. Para obter mais informações, veja [Configurar um servidor para escuta em uma porta TCP específica &#40;SQL Server Configuration Manager&#41;](../../database-engine/configure-windows/configure-a-server-to-listen-on-a-specific-tcp-port.md).  
  
 Uma alternativa à configuração de uma instância nomeada para escutar em uma porta fixa é criar uma exceção no firewall para um programa do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] como o **sqlservr.exe** (para o [!INCLUDE[ssDE](../../includes/ssde-md.md)]). Isso pode ser conveniente, mas o número da porta não será exibido na coluna **Porta Local** da página **Regras de Entrada** quando você usar o snap-in Firewall do Windows com Segurança Avançada do MMC. Isso pode tornar mais difícil auditar quais portas estão abertas. Outra consideração é que um service pack ou atualização cumulativa pode alterar o caminho para o executável do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , o que invalidará a regra do firewall.  
  
> [!NOTE]  
>  O procedimento a seguir usa o item **Firewall do Windows** no Painel de Controle. O snap-in Firewall do Windows com Segurança Avançada do MMC pode configurar uma regra mais complexa. Isso inclui configurar uma exceção de serviço, que pode ser útil para proporcionar defesa mais vigorosa. Veja abaixo [Usando o snap-in Firewall do Windows com Segurança Avançada](#BKMK_WF_msc) .  
  
###### <a name="to-add-a-program-exception-to-the-firewall-using-the-windows-firewall-item-in-control-panel"></a>Para adicionar uma exceção de programa ao firewall usando o item Firewall do Windows no Painel de Controle  
  
1.  Na guia **Exceções** do item **Firewall do Windows** , clique em **Adicionar um programa**.  
  
2.  Navegue até o local da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que você deseja permitir através do firewall, por exemplo **C:\Program Files\Microsoft SQL Server\MSSQL12. < nome_da_instância > \MSSQL\Binn**, selecione  **sqlservr.exe**e, em seguida, clique em **aberto**.  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
 Para obter mais informações sobre pontos de extremidade, veja [Configurar o Mecanismo de Banco de Dados para escutar em várias portas TCP](../../database-engine/configure-windows/configure-the-database-engine-to-listen-on-multiple-tcp-ports.md) e [Exibições de catálogo de pontos de extremidade &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/endpoints-catalog-views-transact-sql).  
  
###  <a name="BKMK_ssas"></a> Portas usadas pelo Analysis Services  
 A tabela a seguir lista as portas que são mais usadas pelo [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
|Recurso|Porta|Comentários|  
|-------------|----------|--------------|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|Porta TCP 2383 para a instância padrão|A porta padrão para a instância padrão do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Serviço Navegador|A porta TCP 2382 só é necessária para uma instância nomeada do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|As solicitações de conexão de clientes para uma instância nomeada do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que não especificam um número de porta são direcionadas para a 2382, que é a porta em que o Navegador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] escuta. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] redireciona a solicitação à porta usada pela instância nomeada.|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] configurado para uso por IIS/HTTP<br /><br /> (O Serviço PivotTable® usa HTTP ou HTTPS)|Porta TCP 80|Usada para uma conexão HTTP por meio de uma URL.|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] configurado para uso por IIS/HTTPS<br /><br /> (O Serviço PivotTable® usa HTTP ou HTTPS)|Porta TCP 443|Usada para uma conexão HTTPS por meio de uma URL. HTTPS é uma conexão HTTP que usa o protocolo SSL.|  
  
 Se usuários acessarem o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] por meio do IIS ou da Internet, você deverá abrir a porta em que o IIS está escutando e especificá-la na cadeia de conexão do cliente. Nesse caso, nenhuma porta deve ser aberta para acessar diretamente o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. A porta padrão 2389 e a porta 2382 devem ser limitadas juntas com todas as outras portas que não são necessárias.  
  
 Para obter instruções passo a passo para configurar o Firewall do Windows para o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], veja [Configurar o Firewall do Windows para permitir acesso ao Analysis Services](../../../2014/analysis-services/instances/configure-the-windows-firewall-to-allow-analysis-services-access.md).  
  
###  <a name="BKMK_ssrs"></a> Portas usadas pelo Reporting Services  
 A tabela a seguir lista as portas que são mais usadas pelo [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
|Recurso|Porta|Comentários|  
|-------------|----------|--------------|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Serviços Web|Porta TCP 80|Usada para uma conexão HTTP com o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] por meio de uma URL. Não é recomendável usar a regra pré-configurada **Serviços da World Wide Web (HTTP)**. Para obter mais informações, consulte a seção [Interação com outras regras do firewall](#BKMK_other_rules) abaixo.|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] configurado para uso por HTTPS|Porta TCP 443|Usada para uma conexão HTTPS por meio de uma URL. HTTPS é uma conexão HTTP que usa o protocolo SSL. Não é recomendável usar a regra pré-configurada **Serviços Seguros da World Wide Web (HTTPS)**. Para obter mais informações, consulte a seção [Interação com outras regras do firewall](#BKMK_other_rules) abaixo.|  
  
 Quando o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] se conecta a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] ou [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], você também deve abrir as portas apropriadas para esses serviços. Para obter instruções passo a passo para configurar o Firewall do Windows para o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], veja [Configurar um Firewall para acesso ao Servidor de Relatório](../../reporting-services/report-server/configure-a-firewall-for-report-server-access.md).  
  
###  <a name="BKMK_ssis"></a> Portas usadas pelo Integration Services  
 A tabela a seguir lista as portas que são usadas pelo serviço [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
|Recurso|Porta|Comentários|  
|-------------|----------|--------------|  
|[!INCLUDE[msCoName](../../includes/msconame-md.md)] chamadas de procedimento remoto (MS RPC)<br /><br /> Usada pelo tempo de execução do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .|Porta TCP 135<br /><br /> Consulte [Considerações especiais sobre a porta 135](#BKMK_port_135)|O serviço [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] usa o DCOM na porta 135. O Gerenciador de Controle de Serviços usa a porta 135 para executa tarefas como iniciar e parar o serviço [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] e transmitir solicitações de controle ao serviço em execução. O número da porta não pode ser alterado.<br /><br /> Esta porta só precisa ser aberta se você está se conectando a uma instância remota do serviço [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] a partir do [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] ou de um aplicativo personalizado.|  
  
 Para obter instruções passo a passo para configurar o Firewall do Windows para o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], veja [Configurar um Firewall do Windows para acessar o Serviço SSIS](../../../2014/integration-services/configure-a-windows-firewall-for-access-to-the-ssis-service.md).  
  
###  <a name="BKMK_additional_ports"></a> Portas e serviços adicionais  
 A tabela a seguir lista portas e serviços dos quais o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode depender.  
  
|Cenário|Porta|Comentários|  
|--------------|----------|--------------|  
|Instrumentação de Gerenciamento do Windows<br /><br /> Para obter mais informações sobre a WMI, consulte [WMI Provider for Configuration Management Concepts](../../relational-databases/wmi-provider-configuration/wmi-provider-for-configuration-management.md).|A WMI é executada como parte de um host de serviço compartilhado com portas atribuídas por DCOM. A WMI pode estar usando a porta TCP 135.<br /><br /> Consulte [Considerações especiais sobre a porta 135](#BKMK_port_135)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager usa a WMI para listar e gerenciar serviços. É recomendável usar o grupo de regras pré-configuradas **WMI (Instrumentação de Gerenciamento do Windows)**. Para obter mais informações, consulte a seção [Interação com outras regras do firewall](#BKMK_other_rules) abaixo.|  
|[!INCLUDE[msCoName](../../includes/msconame-md.md)] MS DTC (Coordenador de Transações Distribuídas)|Porta TCP 135<br /><br /> Consulte [Considerações especiais sobre a porta 135](#BKMK_port_135)|Se o seu aplicativo usa transações distribuídas, talvez seja necessário configurar o firewall para permitir que o tráfego do Coordenador de Transações Distribuídas da [!INCLUDE[msCoName](../../includes/msconame-md.md)] (MS DTC) flua entre instâncias separadas do MS DTC e entre o MS DTC e gerenciadores de recursos, como o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. É recomendável usar o grupo de regras pré-configuradas **Coordenador de Transações Distribuídas** .<br /><br /> Quando um único MS DTC compartilhado é configurado para o cluster inteiro em um grupo de recursos separado, você deve adicionar sqlservr.exe como uma exceção ao firewall.|  
|O botão Procurar do [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] usa UDP para se conectar ao Serviço Navegador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter mais informações, veja [Serviço SQL Server Browser &#40;Mecanismo de Banco de Dados e SSAS&#41;](../../database-engine/configure-windows/sql-server-browser-service-database-engine-and-ssas.md).|Porta UDP 1434|UDP é um protocolo sem-conexão.<br /><br /> O firewall tem uma configuração, chamada [Propriedade UnicastResponsesToMulticastBroadcastDisabled da Interface INetFwProfile](http://go.microsoft.com/fwlink/?LinkId=118371) , que controla seu comportamento no que diz respeito a respostas unicast para uma solicitação UDP difusão (ou multicast).  Ele tem dois comportamentos:<br /><br /> Se a configuração for TRUE, não serão permitidas respostas unicast para uma difusão. A enumeração de serviços falhará.<br /><br /> Se a configuração for FALSE (padrão), serão permitidas respostas unicast durante 3 segundos. O período de tempo não é configurável. em uma rede congestionada ou de alta latência, ou para servidores com grandes cargas, as tentativas de enumerar instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] podem retornar uma lista parcial, o que pode enganar os usuários.|  
|Tráfego IPsec|Portas UDP 500 e 4500|Se a política do domínio exigir que as comunicações de rede sejam feitas por meio de IPsec, você também deverá adicionar as portas UDP 4500 e 500 à lista de exceções. IPsec é uma opção que usa o **Assistente para Nova Regra de Entrada** no snap-in Firewall do Windows. Para obter mais informações, veja [Usando o snap-in Firewall do Windows com Segurança Avançada](#BKMK_WF_msc) abaixo.|  
|Usando a Autenticação do Windows com domínios confiáveis|Os firewalls devem ser configurados para permitir solicitações de autenticação.|Para obter mais informações, consulte [Como configurar um firewall para domínios e relações de confiança](http://support.microsoft.com/kb/179442/).|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e clustering do Windows|O clustering requer portas adicionais que não estão diretamente relacionadas ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|Para obter mais informações, consulte [Enable a network for cluster use](http://go.microsoft.com/fwlink/?LinkId=118372).|  
|Namespaces URL reservados na API de servidor HTTP (HTTP.SYS)|Provavelmente a porta TCP 80, mas podem ser configurados para outras portas. Para obter informações gerais, consulte [Configuring HTTP and HTTPS](http://go.microsoft.com/fwlink/?LinkId=118373).|Para obter informações específicas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sobre como reservar um ponto de extremidade HTTP.SYS usando HttpCfg.exe, veja [Sobre reservas e registro de URL &#40;SSRS Configuration Manager&#41;](../../reporting-services/install-windows/about-url-reservations-and-registration-ssrs-configuration-manager.md).|  
  
##  <a name="BKMK_port_135"></a> Considerações especiais sobre a porta 135  
 Quando você usa RPC com TCP/IP ou com UDP/IP como transporte, as portas de entrada costumam ser atribuídas dinamicamente para serviços do sistema de acordo com a necessidade; as portas TCP/IP e UDP/IP maiores que a 1024 são usadas. Essas portas normalmente são chamadas informalmente de “portas RPC aleatórias”. Nesses casos, os clientes RPC dependem do mapeador de ponto de extremidade RPC para saber quais portas dinâmicas foram atribuídas ao servidor. Para alguns serviços baseados em RPC, você pode configurar uma porta específica em vez de deixar que a RPC atribua uma dinamicamente. Você também pode diminuir o intervalo de portas que a RPC atribui dinamicamente, seja qual for o serviço. Como a porta 135 é usada para muitos serviços, ela é invadida por usuários mal-intencionados com bastante frequência. Quando abrir a porta 135, considere a possibilidade de restringir o escopo da regra do firewall.  
  
 Para obter mais informações sobre a porta 135, consulte as seguintes referências:  
  
-   [Visão geral de serviços e requisitos de porta de rede para o sistema do Windows Server](http://support.microsoft.com/kb/832017)  
  
-   [Solucionando erros de Mapeador de ponto de extremidade RPC utilizando as ferramentas de suporte do Windows Server 2003 do CD do produto](http://support.microsoft.com/kb/839880)  
  
-   [RPC (Chamada de Procedimento Remoto)](http://go.microsoft.com/fwlink/?LinkId=118375)  
  
-   [Como configurar a alocação de porta dinâmica da RPC para funcionar com os firewalls](http://support.microsoft.com/kb/154596/)  
  
##  <a name="BKMK_other_rules"></a> Interação com outras regras do firewall  
 O Firewall do Windows usa regras e grupos de regras para estabelecer sua configuração. Cada regra ou grupo de regras geralmente está associado a um determinado programa ou serviço, que, por sua vez, pode modificar ou excluir a regra sem que você saiba. Por exemplo, o grupo de regras **Serviços da World Wide Web (HTTP)** e **Serviços Seguros da World Wide Web (HTTPS)** está associado ao IIS. Se essas regras foram habilitadas, as portas 80 e 443 serão abertas, e os recursos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que dependem delas funcionarão corretamente. Porém, os administradores que configuram o IIS podem modificar ou desabilitar essas regras. Por isso, se você estiver usando as portas 80 ou 443 para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], deverá criar sua própria regra ou seu próprio grupo de regras que mantenha a configuração de porta desejada, independentemente das outras regras do IIS.  
  
 O snap-in Firewall do Windows com Segurança Avançada do MMC permite qualquer tráfego que corresponda a qualquer regra de permissão aplicável. Assim, se houver duas regras que se aplicam à porta 80 (com parâmetros diferentes), o tráfego que corresponder a uma delas será permitido. Portanto, se uma regra permitir o tráfego pela porta 80 da sub-rede local e outra regra permitir o tráfego de qualquer endereço, o resultado é que todo o tráfego para a porta 80 será permitido independentemente da origem. Para gerenciar o acesso ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]com eficiência, os administradores devem revisar periodicamente todas as regras de firewall habilitadas no servidor.  
  
##  <a name="BKMK_profiles"></a> Visão geral de perfis do firewall  
 Os perfis de firewall são discutidos no [Guia de introdução ao Firewall do Windows com Segurança Avançada](http://go.microsoft.com/fwlink/?LinkId=116080) na seção **Firewall de host com reconhecimento de local de rede**. Para resumir, os sistemas operacionais identificam e memorizam cada uma das redes com as quais se conectam no que diz respeito à conectividade, às conexões e à categoria.  
  
 Há três tipos de local de rede no Firewall do Windows com Segurança Avançada:  
  
-   Domínio. O Windows pode autenticar o acesso ao controlador de domínio do domínio em que o computador ingressou.  
  
-   Público. Diferentemente das redes de domínio, todas as redes são inicialmente classificadas como públicas. Redes que representam conexões diretas à Internet ou estão em locais públicos, como aeroportos e cafés, devem ser configuradas como públicas.  
  
-   Privado. Uma rede identificada por um usuário ou aplicativo como privada. Somente redes confiáveis devem ser identificadas como redes privadas. Os usuários normalmente desejam identificar redes domésticas ou de pequena empresa como privadas.  
  
 O administrador pode criar um perfil para cada tipo de local de rede, com cada perfil contendo políticas de firewall diferentes. Somente um perfil é aplicado a qualquer momento. A ordem de perfis é aplicada da seguinte maneira:  
  
1.  Se todas as interfaces forem autenticadas no controlador de domínio para o domínio do qual o computador é membro, será aplicado o perfil de domínio.  
  
2.  Se todas as interfaces forem autenticadas no controlador de domínio ou conectadas a redes classificadas como locais de rede privados, será aplicado o perfil privado.  
  
3.  Caso contrário, será aplicado o perfil público.  
  
 Use o snap-in Firewall do Windows com Segurança Avançada do MMC para exibir e configurar todos os perfis do firewall. O item **Firewall do Windows** no Painel de Controle configura apenas o perfil atual.  
  
##  <a name="BKMK_additional_settings"></a> Configurações adicionais do firewall usando o item Firewall do Windows no Painel de Controle  
 As exceções que você adiciona ao firewall podem restringir a abertura da porta a conexões de entrada de computadores específicos ou da sub-rede local. Essa restrição do escopo da abertura de porta pode reduzir o nível de exposição do seu computador a usuários mal-intencionados e é recomendável.  
  
> [!NOTE]  
>  Se você usar o item **Firewall do Windows** no Painel de Controle configurará apenas o perfil do firewall.  
  
#### <a name="to-change-the-scope-of-a-firewall-exception-using-the-windows-firewall-item-in-control-panel"></a>Para alterar o escopo de uma exceção do firewall usando o item Firewall do Windows no Painel de Controle  
  
1.  No item **Firewall do Windows** do Painel de Controle, selecione um programa ou porta na guia **Exceções** e clique em **Propriedades** ou em **Editar**.  
  
2.  Na caixa de diálogo **Editar um Programa** ou **Editar uma Porta** , clique em **Alterar Escopo**.  
  
3.  Escolha uma das seguintes opções:  
  
    -   **Qualquer computador (inclusive na Internet)**  
  
         Não recomendável. Isso permitirá que qualquer computador que pode se dirigir a seu computador se conecte ao programa ou à porta especificada. Esta configuração pode ser necessária para permitir a apresentação de informações a usuários anônimos na Internet, mas aumenta sua exposição a usuários mal-intencionados. Sua exposição pode ser ainda maior se você habilitar esta configuração e também permitir NAT transversal, como a opção Permitir percurso de borda.  
  
    -   **Somente minha rede (sub-rede)**  
  
         Esta configuração é mais segura do que **Qualquer computador**. Somente computadores da sub-rede local da sua rede podem se conectar ao programa ou à porta.  
  
    -   **Lista personalizada:**  
  
     Somente computadores que têm os endereços IP contidos na lista podem se conectar. Esta configuração pode ser mais segura do que **Somente minha rede (sub-rede)**, mas os computadores cliente que usam DHCP podem alterar o endereço IP ocasionalmente. Por isso o computador desejado não poderá se conectar. Outro computador, que você não pretendia autorizar, pode aceitar o endereço IP listado e se conectar. A opção **Lista personalizada** pode ser apropriada para listar outros servidores configurados para usar um endereço IP fixo, mas os endereços IP podem ser falsificados por um invasor. Restringir regras de firewall é um procedimento apenas tão seguro quanto sua infraestrutura de rede.  
  
##  <a name="BKMK_WF_msc"></a> Usando o snap-in Firewall do Windows com Segurança Avançada  
 Outras configurações avançadas do firewall podem ser definidas usando o snap-in do MMC Firewall do Windows com Segurança Avançada. O snap-in inclui um assistente de regra e expõe configurações adicionais que não estão disponível no item **Firewall do Windows** do Painel de Controle. Essas configurações incluem:  
  
-   Configurações de criptografia  
  
-   Restrições de serviços  
  
-   Restrição de conexões de computadores por nome  
  
-   Restrição de conexões para usuários ou perfis específicos  
  
-   Percurso de borda que permita que o tráfego ignore os roteadores de conversão de endereço de rede (NAT)  
  
-   Configuração de regras de saída  
  
-   Configuração de regras de segurança  
  
-   Exigência de IPsec para conexões de entrada  
  
#### <a name="to-create-a-new-firewall-rule-using-the-new-rule-wizard"></a>Para criar uma nova regra de firewall usando o assistente de Nova Regra  
  
1.  No menu Iniciar, clique em **Executar**, digite **WF.msc**e clique em **OK**.  
  
2.  No painel esquerdo do **Firewall do Windows com Segurança Avançada**, clique com o botão direito do mouse em **Regras de Entrada**e clique em **Nova Regra**.  
  
3.  Complete o **Assistente de Nova Regra de Entrada** usando as configurações desejadas.  
  
##  <a name="BKMK_troubleshooting"></a> Solucionando problemas de configurações do firewall  
 As seguintes ferramentas e técnicas podem ser úteis para solucionar problemas de firewall:  
  
-   O status efetivo da porta é a combinação de todas as regras relacionadas a ela. Quando se tenta bloquear o acesso por uma porta, pode ser útil revisar todas as regras que citam o número da porta. Para isso, use o snap-in Firewall do Windows com Segurança Avançada do MMC e classifique as regras de entrada e de saída por número de porta.  
  
-   Revise as portas que estão ativas no computador em que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está em execução. Esse processo inclui a verificação de quais portas TCP/IP estão sendo escutadas e também a verificação do status das portas.  
  
     Para verificar quais portas estão sendo escutadas, use o utilitário de linha de comando **netstat** . Além de exibir as conexões TCP ativas, o utilitário **netstat** também exibe uma variedade de estatísticas e informações de IP.  
  
    #### <a name="to-list-which-tcpip-ports-are-listening"></a>Para listar quais portas TCP/IP estão escutando  
  
    1.  Abra a janela do prompt de comando.  
  
    2.  No prompt de comando, digite `netstat -n -a`.  
  
         A opção **-n** instrui o **netstat** para exibir numericamente o endereço e o número da porta das conexões TCP ativas. A opção **-a** instrui o **netstat** a exibir as portas TCP e UDP escutadas pelo computador.  
  
-   O utilitário **PortQry** pode ser usado para relatar o status das portas TCP/IP como escutando, não escutando ou filtrado. (Com o status filtrado, a porta pode ou não estar escutando; esse status indica que o utilitário não recebeu uma resposta da porta.) O utilitário **PortQry** está disponível para download no [Centro de Download da Microsoft](http://go.microsoft.com/fwlink/?LinkId=28590).  
  
## <a name="see-also"></a>Consulte também  
 [Visão geral de serviços e requisitos de porta de rede para o sistema do Windows Server](http://support.microsoft.com/kb/832017)  
  
  
