---
title: Antes de instalar o clustering de failover | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- clusters [SQL Server], preinstallation checklist
- installing failover clusters
- failover clustering [SQL Server], preinstallation checklist
ms.assetid: a655225d-8c54-4b30-95fd-31f588167899
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: cc959fa8406453230ee133bf6183fa3dc1ba51f1
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/13/2018
ms.locfileid: "53355791"
---
# <a name="before-installing-failover-clustering"></a>Antes de instalar o cluster de failover
  Antes de instalar um cluster de failover do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], você deve selecionar o hardware e o sistema operacional nos quais o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] será executado. Você também deve configurar o WSFC (Clustering de Failover do Windows Server) e examinar a rede, a segurança e as considerações sobre outros softwares que serão executados no cluster de failover.  
  
 Se um cluster do Windows tiver uma unidade de disco local e a mesma letra de unidade também for usada em um ou mais nós de cluster como uma unidade compartilhada, você não poderá instalar o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] nessa unidade.  
  
 Talvez você queira também examinar os tópicos a seguir para saber mais sobre conceitos de clustering de failover, recursos e tarefas do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
|Descrição do Tópico|Tópico|  
|-----------------------|-----------|  
|Descreve conceitos de cluster de failover do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e fornece links para conteúdo e tarefas associadas.|[Instâncias de Cluster de Failover do AlwaysOn (SQL Server)](../windows/always-on-failover-cluster-instances-sql-server.md)|  
|Descreve conceitos de política de failover do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e fornece links para configurar a política de failover para se adequar aos seus requisitos organizacionais.|[Failover Policy for Failover Cluster Instances](../windows/failover-policy-for-failover-cluster-instances.md)|  
|Descreve como manter seu cluster de failover [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] existente.|[Administração e manutenção da instância de cluster de failover](../windows/failover-cluster-instance-administration-and-maintenance.md)|  
|Explica como instalar o [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] em um Windows Server Failover Cluster (WSFC).|[Como criar clusters do SQL Server Analysis Services](https://go.microsoft.com/fwlink/p/?LinkId=396548)|  
  
  
  
##  <a name="BestPractices"></a> Práticas recomendadas  
  
-   Examine [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)][Notas de versão](https://go.microsoft.com/fwlink/?LinkId=296445)  
  
-   Instale o software de pré-requisito. Antes de executar a Instalação para instalar ou atualizar para o [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)], instale os pré-requisitos a seguir para reduzir o tempo de instalação. É possível instalar software de pré-requisito em cada nó de cluster de failover e, em seguida, reiniciar os nós uma vez antes de executar a Instalação.  
  
    -   O Windows PowerShell já não é instalado pela Instalação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . O Windows PowerShell 2.0 é um pré-requisito da instalação dos componentes do [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)][!INCLUDE[ssDE](../../../includes/ssde-md.md)] e do [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]. Se o Windows PowerShell 2.0 não estiver presente no computador, você poderá habilitá-lo seguindo as instruções da página sobre [estrutura de gerenciamento do Windows](https://go.microsoft.com/fwlink/?LinkId=186214).  
  
    -   O .NET Framework 3.5 SP1 não é mais instalado pelo [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], mas pode ser necessário durante a instalação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] em sistemas operacionais antigos do Windows. Para obter mais informações, veja [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)][Notas de versão](https://go.microsoft.com/fwlink/?LinkId=296445).  
  
    -   **[!INCLUDE[msCoName](../../../includes/msconame-md.md)] Pacote de atualização:** Para evitar que o computador seja reinicializado devido à instalação do .NET Framework 4 durante a instalação, a instalação do [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] requer que uma atualização do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] seja instalada no computador.  Se você estiver instalando o [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)] no Windows 7 SP1 ou [!INCLUDE[firstref_longhorn](../../../includes/firstref-longhorn-md.md)] SP2, essa atualização será incluída. Se você estiver instalando em um sistema operacional Windows mais antigo, baixe-o em [Microsoft Update para .NET Framework 4.0 no Windows Vista e Windows Server 2008](https://go.microsoft.com/fwlink/?LinkId=198093).  
  
    -   .NET Framework 4: O .NET Framework 4 é instalado em um sistema operacional clusterizado. Para reduzir o tempo de instalação, convém instalar o .NET Framework 4 antes de executar a Instalação.  
  
    -   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Arquivos de suporte à Instalação. Você pode instalar esses arquivos executando o SqlSupport.msi localizado na mídia de instalação do [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] .  
  
-   Verifique se o software antivírus não está instalado no cluster do WSFC. Para obter mais informações, veja o artigo da Base de Dados de Conhecimento da [!INCLUDE[msCoName](../../../includes/msconame-md.md)] , [Software antivírus que não está ciente do cluster pode causar problemas com serviços de cluster](https://go.microsoft.com/fwlink/?LinkId=116986).  
  
-   Ao nomear um grupo de clusters para a instalação de cluster de failover, você não deve usar nenhum dos seguintes caracteres no nome do grupo de clusters:  
  
    -   Operador menor que (\<)  
  
    -   Operador maior que (>)  
  
    -   Aspas duplas (")  
  
    -   Aspas simples (')  
  
    -   E comercial (&)  
  
     Verifique também se os nomes de grupos de clusters não contêm caracteres sem suporte.  
  
-   Verifique se todos os nós de cluster estão configurados de forma idêntica, inclusive COM+, letras de unidade de disco e usuários no grupo de administradores.  
  
-   Verifique se você limpou os logs do sistema em todos os nós e se exibiu os logs do sistema novamente. Verifique se os logs estão livres de quaisquer mensagens de erro antes de continuar.  
  
-   Antes de instalar ou atualizar um cluster de failover do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , desabilite todos os aplicativos e serviços que talvez possam usar os componentes do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] durante a instalação, mas deixe os recursos de disco online.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] A Instalação define automaticamente dependências entre o grupo de clusters do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e os discos que estarão no cluster de failover. Não defina dependências para discos antes da Instalação.  
  
    -   Durante a instalação do Cluster de Failover do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , o objeto de computador (contas de computador do Active Directory) para o Nome do Recurso de Rede do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] é criado. Em um cluster do [!INCLUDE[firstref_longhorn](../../../includes/firstref-longhorn-md.md)] , a conta do nome de cluster (conta de computador do próprio cluster) precisa ter permissões para criar objetos de computador. Para obter mais informações, veja [Configurando contas no Active Directory](https://technet.microsoft.com/library/cc731002\(WS.10\).aspx).  
  
    -   Se estiver usando o compartilhamento de arquivo SMB como opção de armazenamento, a conta de Instalação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] deve ter SeSecurityPrivilege no servidor de arquivo. Para fazer isso, usando o console Política de Segurança Local no servidor de arquivos, adicione a conta de instalação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] aos direitos de **Gerenciar a auditoria e o log de segurança** .  
  
 
  
##  <a name="Hardware"></a> Verifique sua solução de hardware  
  
-   Se a solução de cluster incluir nós de clusters dispersos geograficamente, deverão ser verificados itens adicionais, como latência de rede e suporte a disco compartilhado.  
  
    -   Para obter mais informações sobre o [!INCLUDE[firstref_longhorn](../../../includes/firstref-longhorn-md.md)] e o [!INCLUDE[winserver2008r2](../../../includes/winserver2008r2-md.md)], veja [Validando hardware para um cluster de failover](https://go.microsoft.com/fwlink/?LinkId=196817) e [Política de suporte para clusters de failover do Windows](https://go.microsoft.com/fwlink/?LinkId=196818).  
  
-   Verifique se o disco onde o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] será instalado não está descompactado nem criptografado. Se você tentar instalar o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] em uma unidade compactada ou criptografada, ocorrerá falha na Instalação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
-   As configurações de SAN também têm suporte nas edições do [!INCLUDE[firstref_longhorn](../../../includes/firstref-longhorn-md.md)] e [!INCLUDE[winserver2008r2](../../../includes/winserver2008r2-md.md)] Advanced Server e do Datacenter Server. A categoria "Dispositivo de Cluster/Multi-cluster" do Catálogo do Windows e da Lista de Compatibilidade de Hardware lista o conjunto de dispositivos de armazenamento compatíveis com SAN que foram testados e que têm suporte como unidades de armazenamento de SAN com vários clusters do WSFC anexados. Execute a validação de cluster depois de localizar os componentes certificados.  
  
-   O Compartilhamento de Arquivos SMB também tem suporte para a instalação de arquivos de dados. Para obter mais informações, veja [Tipos de armazenamento de arquivos de dados](../../install/hardware-and-software-requirements-for-installing-sql-server.md#StorageTypes).  
  
    > [!WARNING]  
    >  Se estiver usando o Windows File Server como um armazenamento de compartilhamento de arquivo SMB, a conta de Instalação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] deverá ter SeSecurityPrivilege no servidor de arquivo. Para fazer isso, usando o console Política de Segurança Local no servidor de arquivos, adicione a conta de instalação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] aos direitos de **Gerenciar a auditoria e o log de segurança** .  
    >   
    >  Se você estiver usando o armazenamento de compartilhamento de arquivo SMB em local que não seja o Windows File Server, consulte o fornecedor de armazenamento para obter uma configuração equivalente no servidor de arquivos.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] dá suporte a pontos de montagem.  
  
     Um volume montado ou ponto de montagem permite usar uma única letra de unidade para fazer referência a muitos discos ou volumes. Se você tiver um letra D: de unidade que faça referência a um disco ou volume normal, poderá conectar ou "montar" discos ou volumes adicionais como diretórios com a letra D: de unidade sem os discos ou volumes adicionais que exigem suas próprias letras de unidade.  
  
     Considerações adicionais sobre ponto de montagem para cluster de failover do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] :  
  
    -   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] A Instalação exige que a unidade base de uma unidade montada tenha uma letra da unidade associada. Para instalações de cluster de failover, esta unidade base deve ser uma unidade clusterizada. GUIDs de volume não têm suporte nesta versão.  
  
    -   A unidade base, aquela com a letra de unidade, não pode ser compartilhada entre instâncias de cluster de failover. Essa é uma restrição normal para clusters de failover, mas não é uma restrição em servidores autônomos, com várias instâncias.  
  
    -   As instalações clusterizadas do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] são limitadas ao número de letras de unidade disponíveis. Supondo que somente uma letra de unidade seja usada para o sistema operacional, e que todas as outras letras de unidade estejam disponíveis como unidades de cluster normais ou unidades de cluster que hospedam pontos de montagem, você fica limitado a um máximo de 25 instâncias do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] por cluster de failover.  
  
        > [!TIP]  
        >  O limite de 25 instâncias pode ser superado usando a opção de compartilhamento de arquivos SMB. Se você usar o compartilhamento de arquivos SMB como a opção de armazenamento, poderá instalar até 50 instâncias de cluster de failover [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
    -   Formatar uma unidade depois de montar unidades adicionais não tem suporte.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] só dá suporte a Disco Local para a instalação de arquivos tempdb. Verifique se o caminho especificado para os dados tempdb e os arquivos de log são válidos em todos os nós de cluster. Durante o failover, se os diretórios tempdb não estiverem disponíveis no nó do destino de failover, o recurso do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] não ficará online. Para obter mais informações, veja [Tipos de armazenamento de arquivos de dados](../../install/hardware-and-software-requirements-for-installing-sql-server.md#StorageTypes) e [Configuração do Mecanismo de Banco de Dados – Diretórios de dados](../../install/database-engine-configuration-data-directories.md).  
  
-   Se você implantar um cluster de failover do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] em componentes de tecnologia iSCSI, é recomendável tomar o cuidado necessário. Para obter mais informações, veja [Suporte do SQL Server em componentes de tecnologia iSCSI](https://go.microsoft.com/fwlink/?LinkId=116960).  
  
-   Para obter mais informações, veja [Política de suporte do SQL Server para Microsoft Clustering](https://go.microsoft.com/fwlink/?LinkId=116958).  
  
-   Para obter mais informações sobre a configuração da unidade de quorum adequada, veja [Informações sobre configuração da unidade de quorum](https://go.microsoft.com/fwlink/?LinkId=196816).  
  
-   Para instalar um cluster de failover do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] quando os arquivos de instalação de origem do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e o cluster existirem em domínios diferentes, copie os arquivos de instalação no domínio atual disponível para o cluster de failover do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
  
  
##  <a name="Security"></a> Examine as considerações sobre segurança  
  
-   Para usar criptografia, instale o certificado de servidor com o nome DNS totalmente qualificado do cluster do WSFC em todos os nós no cluster de failover do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Por exemplo, se você tiver um cluster de dois nós, com nós nomeados "Test1.DomainName.com" e "Test2.DomainName.com" e uma instância de cluster de failover do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] denominada"Virtsql", deverá obter um certificado para "Virtsql.DomainName.com" e instalar o certificado nos nós test1 e test2. Em seguida, você pode marcar a caixa de seleção **Forçar criptografia de protocolo** no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Configuration Manager para configurar o cluster de failover para criptografia.  
  
    > [!IMPORTANT]  
    >  Não marque a caixa de seleção **Forçar criptografia de protocolo** até que tenha instalado os certificados em todos os nós participantes da instância de cluster de failover.  
  
-   Para instalações do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] em configurações lado a lado com versões anteriores, os serviços do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] devem usar contas localizadas somente no grupo de domínios global. Além disso, as contas usadas por serviços do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] não devem aparecer no grupo de Administradores local. O não cumprimento dessa diretriz resultará em comportamento de segurança inesperado.  
  
-   Para criar um cluster de failover, você deve ser um administrador local com permissões para fazer logon como um serviço e para atuar como parte do sistema operacional em todos os nós da instância de cluster de failover.  
  
-   No [!INCLUDE[nextref_longhorn](../../../includes/nextref-longhorn-md.md)], os SIDs de serviço são gerados automaticamente para uso com os serviços do [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] . Para instâncias de cluster de failover do [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] atualizadas a partir de versões anteriores do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], os grupos de domínio existentes e as configurações de ACL serão preservados.  
  
-   Os grupos de domínios devem estar no mesmo domínio que as contas do computador. Por exemplo, se o computador onde o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] será instalado estiver no domínio SQLSVR, que é um filho do domínio MYDOMAIN, especifique um grupo no domínio SQLSVR. O domínio SQLSVR pode conter contas de usuário de MYDOMAIN.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] O clustering de failover não pode ser instalado quando os nós de clusters são controladores de domínio.  
  
-   Examine o conteúdo de [Considerações sobre segurança para uma instalação do SQL Server](../../install/security-considerations-for-a-sql-server-installation.md).  
  
-   Para habilitar a autenticação Kerberos com o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], veja [Como usar a autenticação Kerberos no SQL Server](https://support.microsoft.com/kb/319723) na Base de Dados de Conhecimento [!INCLUDE[msCoName](../../../includes/msconame-md.md)] .  
  
  
  
##  <a name="Network"></a> Examine as considerações sobre rede, porta e firewall  
  
-   Verifique se você desabilitou o NetBIOS para todas as placas de rede privada antes de começar a Instalação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
-   O nome de rede e o endereço IP do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] não deve ser usado para nenhum outro propósito, como compartilhamento de arquivos. Para criar um recurso de compartilhamento de arquivos, use um endereço IP e um nome de rede diferente e exclusivo para o recurso.  
  
    > [!IMPORTANT]  
    >  É recomendável não usar compartilhamentos de arquivos em unidades de dados, pois eles podem afetar o comportamento e o desempenho do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
-   Embora o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] dê suporte a Pipes Nomeados e a Soquetes TCP/IP sobre TCP/IP em um cluster, é recomendável usar Soquetes TCP/IP em uma configuração clusterizada.  
  
-   O servidor ISA não tem suporte no Clustering do Windows e, consequentemente, também não tem suporte em clusters de failover do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
-   O serviço de Registro Remoto deve estar ativo e em execução.  
  
-   A Administração Remota deve estar habilitada.  
  
-   Para a porta [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , use o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Configuration Manager para verificar a configuração de rede do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para o protocolo TCP/IP da instância que você deseja desbloquear. Você deve habilitar a porta TCP para IPALL, se desejar se conectar ao [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] usando TCP após a instalação. Por padrão, o SQL Browser escuta na porta UDP 1434.  
  
-   As operações de configuração do cluster de failover incluem uma regra que verifica a ordem de associação da rede. Embora as ordens de associação possam parecer corretas, é possível que você tenha desabilitado ou "tornado fantasma" as configurações de NIC no sistema. Configurações de NIC "fantasma" podem afetar a ordem de associação e fazer com que a regra de ordem de associação emita um aviso. Para evitar essa situação, use as seguintes etapas para identificar e remover adaptadores de rede desabilitados:  
  
    1.  Em um prompt de comando, digite: set devmgr_Show_Nonpersistent_Devices=1.  
  
    2.  Digite e execute: start Devmgmt.msc.  
  
    3.  Expanda a lista de adaptadores de rede. Apenas os adaptadores físicos devem estar na lista. Se você tiver um adaptador de rede desabilitado, a instalação reportará uma falha referente à regra de ordem de associação da rede. Painel de Controle/Conexões de Rede também mostrará que o adaptador foi desabilitado. Confirme se as Configurações de Rede no Painel de Controle mostram a mesma lista de adaptadores físicos habilitados que devmgmt.msc.  
  
    4.  Remova os adaptadores de rede desabilitados antes de executar a Instalação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
    5.  Após o término da instalação, volte para Conexões de Rede no Painel de Controle e desabilite todos os adaptadores de rede que não estiverem em uso.  
  
  
  
##  <a name="OS_Support"></a> Verifique seu sistema operacional  
 Verifique se o sistema operacional está instalado corretamente e se foi projetado para dar suporte a clustering de failover. A tabela a seguir é uma lista das edições do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e dos sistemas operacionais com suporte para elas.  
  
|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] edição|[!INCLUDE[firstref_longhorn](../../../includes/firstref-longhorn-md.md)] Enterprise|[!INCLUDE[firstref_longhorn](../../../includes/firstref-longhorn-md.md)] Datacenter Server|[!INCLUDE[winserver2008r2](../../../includes/winserver2008r2-md.md)] Enterprise|[!INCLUDE[winserver2008r2](../../../includes/winserver2008r2-md.md)] Datacenter Server|  
|---------------------------------------|------------------------------------------------|-------------------------------------------------------|----------------------------------------------|-----------------------------------------------------|  
|[!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)] Enterprise (64 bits) x64<sup>1</sup>|Sim|Sim|Sim<sup>2</sup>|Sim<sup>2</sup>|  
|[!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)] Enterprise (32 bits)|Sim|Sim|||  
|[!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] – bits) Developer (64|Sim|Sim|Sim <sup>2</sup>|Sim <sup>2</sup>|  
|[!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] Developer (32 bits)|Sim|Sim|||  
|[!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] Standard (64 bits)|Sim|Sim|Sim|Sim|  
|[!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] Standard (32 bits)|Sim|Sim|||  
  
 <sup>1</sup> [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] clusters não têm suporte no modo WOW. Isso inclui atualizações de versões anteriores de clusters de failover do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que haviam sido instaladas originalmente no WOW. Para esses itens, a única opção de atualização é instalar a nova versão lado a lado e migrar.  
  
 <sup>2</sup> tem suporte para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] clustering de failover de várias sub-redes.  
  
  
  
##  <a name="MultiSubnet"></a> Considerações adicionais para configurações de várias sub-redes  
 As seções a seguir descrevem os requisitos a serem considerados ao instalar um cluster de failover de várias sub-redes do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Uma configuração de várias sub-redes envolve o clustering em várias sub-redes, envolvendo, assim, o uso de vários endereços IP e alterações em dependências de recurso do endereço IP.  
  
### <a name="includessnoversionincludesssnoversion-mdmd-edition-and-operating-system-considerations"></a>[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Considerações sobre a edição e o sistema operacional  
  
-   Para obter informações sobre as edições do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que dão suporte a cluster de failover de várias sub-redes do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], consulte [Recursos com suporte nas edições do SQL Server 2014](../../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md).  
  
-   Para criar um cluster de failover de várias sub-redes do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , você deve criar primeiro o cluster de failover multissite do [!INCLUDE[winserver2008r2](../../../includes/winserver2008r2-md.md)] em várias sub-redes.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] O cluster de failover depende do cluster de failover do Windows Server para assegurar que as condições de dependência IP sejam válidas se houver um failover.  
  
-   [!INCLUDE[winserver2008r2](../../../includes/winserver2008r2-md.md)] exige que todos os servidores de cluster estejam no mesmo domínio do Active Directory. Portanto, o cluster de failover de várias sub-redes do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] requer que todos os nós de cluster estejam no mesmo domínio do Active Directory mesmo que estejam em sub-redes diferentes.  
  
#### <a name="ip-address-and-ip-address-resource-dependencies"></a>Endereço IP e dependências de recurso de endereço IP  
  
1.  A dependência de recurso de endereço IP é definida como OR em uma configuração de várias sub-redes. Para obter mais informações, veja [Criar um novo cluster de failover do SQL Server &#40;Instalação&#41;](create-a-new-sql-server-failover-cluster-setup.md)  
  
2.  Não há suporte para dependências de endereço IP AND-OR mistas. Por exemplo, não há suporte para \<IP1> AND \<IP2> OR \<IP3>.  
  
3.  Não há suporte para mais de um endereço IP por sub-rede.  
  
     Se você decidir usar mais de um endereço IP configurado para a mesma sub-rede, poderá perceber falhas de conexão de cliente durante a inicialização do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
#### <a name="related-content"></a>Conteúdo relacionado  
 Para obter mais informações sobre o failover de multissite do [!INCLUDE[winserver2008r2](../../../includes/winserver2008r2-md.md)] , veja o [Site sobre clustering de failover do Windows Server 2008 R2](https://technet.microsoft.com/library/ff182338\(v=WS.10\).aspx) e o artigo [Design de um serviço ou aplicativo clusterizado em um cluster de failover de multissite](https://go.microsoft.com/fwlink/?LinkId=177873).  
  
##  <a name="WSFC"></a> Configurar um cluster de failover do Windows Server  
  
-   [!INCLUDE[msCoName](../../../includes/msconame-md.md)] O WSFC (Serviço de Cluster) deve ser configurado em, pelo menos, um nó de cluster de servidores. Você também deve executar o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Enterprise, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Business Intelligence ou [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Standard com o WSFC. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Enterprise dá suporte a clusters de failover com até 16 nós. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Business Intelligence e o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Standard dão suporte a clusters de failover com dois nós.  
  
-   O recurso DLL para o serviço [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] exporta duas funções usadas pelo Gerenciador de Cluster WSFC para verificar a disponibilidade do recurso do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Para obter mais informações, veja [Política de failover para instâncias de cluster de failover](../windows/failover-policy-for-failover-cluster-instances.md).  
  
-   O WSFC deve ser capaz de verificar se a instância clusterizada de failover está em execução usando a verificação IsAlive. Isso requer conexão com o servidor usando uma conexão confiável. Por padrão, a conta que executa o serviço de cluster não é configurada como um administrador em nós no cluster e o grupo BUILTIN\Administradores não tem permissão para fazer logon no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Essas configurações serão alteradas apenas se você alterar as permissões nos nós de cluster.  
  
-   Configure o DNS (Serviço de Nomes de Domínio) ou o WINS (Serviço de Cadastramento na Internet do Windows). Um servidor DNS ou WINS deve estar em execução no ambiente onde o cluster de failover do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] será instalado. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] A Instalação exige o registro de serviço de nomes de domínio dinâmico da referência virtual da interface IP do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . A configuração do servidor DNS deve permitir que nós de cluster registrem dinamicamente um mapa de endereço IP online para Nome de Rede. Se o registro dinâmico não puder ser concluído, ocorrerá falha na Instalação e ela será revertida. Para obter mais informações, confira [este artigo da Base de Dados de Conhecimento](https://support.microsoft.com/kb/947048)  
  
  
  
##  <a name="MSDTC"></a> Instalar o Coordenador de Transações Distribuídas da [!INCLUDE[msCoName](../../../includes/msconame-md.md)]  
 Antes de instalar o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] em um cluster de failover, determine se o recurso de cluster do MSDTC (Coordenador de Transações Distribuídas da [!INCLUDE[msCoName](../../../includes/msconame-md.md)] ) deve ser criado. Se você estiver instalando somente o [!INCLUDE[ssDE](../../../includes/ssde-md.md)], o recurso de cluster do MSDTC não será necessário. Se estiver instalando o [!INCLUDE[ssDE](../../../includes/ssde-md.md)] e o SSIS, os Componentes da Estação de Trabalho, ou se usar transações distribuídas, você deverá instalar o MSDTC. Observe que o MSDTC não é necessário para instâncias somente do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
 No [!INCLUDE[firstref_longhorn](../../../includes/firstref-longhorn-md.md)] e no [!INCLUDE[winserver2008r2](../../../includes/winserver2008r2-md.md)], você pode instalar várias instâncias do MSDTC em um único cluster de failover. A primeira instância do MSDTC instalada será a instância padrão de cluster do MSDTC. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] aproveitará as vantagens de uma instância do MSDTC instalada no grupo de recursos do cluster local do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] usando a instância do MSDTC automaticamente. Porém, podem ser mapeados aplicativos individuais para qualquer instância do MSDTC no cluster.  
  
 As regras a seguir serão aplicadas para uma instância do MSDTC a ser escolhida pelo [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]:  
  
-   Usar o MSDTC instalado no grupo local ou  
  
-   Usar a instância mapeada do MSDTC ou  
  
-   Usar a instância padrão de cluster do MSDTC ou  
  
-   Usar a instância do MSDTC instalada no computador local  
  
> [!IMPORTANT]  
>  Se a instância do MSDTC instalada no grupo de clusters local do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] falhar, o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] não tentará usar a instância de cluster padrão nem a instância do computador local do MSDTC automaticamente. Você precisaria remover completamente a instância do MSDTC com falha do grupo do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para usar outra instância do MSDTC. Da mesma forma, se você criar um mapeamento para o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e a instância mapeada do MSDTC falhar, suas transações distribuídas também falharão. Se você desejar que o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] use outra instância do MSDTC, deverá adicionar uma instância do MSDTC ao grupo de cluster local do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ou excluir o mapeamento.  
  
### <a name="configure-includemsconameincludesmsconame-mdmd-distributed-transaction-coordinator"></a>Configurar o Coordenador de Transações Distribuídas da [!INCLUDE[msCoName](../../../includes/msconame-md.md)]  
 Após instalar o sistema operacional e configurar o cluster, você deve configurar o MSDTC para funcionar em um cluster usando o Administrador de Cluster. A falha no MSDTC de cluster não bloqueará a Instalação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , mas a funcionalidade do aplicativo [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] poderá ser afetada se o MSDTC não for configurado corretamente.  
  
  
  
## <a name="see-also"></a>Consulte também  
 [Requisitos de hardware e Software para instalação do SQL Server 2014](../../install/hardware-and-software-requirements-for-installing-sql-server.md)   
 [Verificar parâmetros do Verificador de Configuração do Sistema](../../../database-engine/install-windows/check-parameters-for-the-system-configuration-checker.md)   
 [Administração e manutenção da instância de cluster de failover](../windows/failover-cluster-instance-administration-and-maintenance.md)  
  
  
