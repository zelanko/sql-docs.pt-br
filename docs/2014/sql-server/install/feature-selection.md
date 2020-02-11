---
title: Seleção de recursos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- feature selection, Setup
helpviewer_keywords:
- SQL Server Installation Wizard, Components to Install page
- Components to Install page [SQL Server Installation Wizard]
ms.assetid: 73182088-153b-4634-a060-d14d1fd23b70
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 0b516d76c1c814cb70215bfe37f3cddb60e614d5
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66095217"
---
# <a name="feature-selection"></a>Seleção de recursos
  Use as caixas de seleção da página **Seleção de Recursos** do Assistente de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para selecionar componentes para sua instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="installing-includessnoversionincludesssnoversion-mdmd-features"></a>Instalando recursos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 Na página **Seleção de Recursos** , os recursos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] estão separados em duas seções principais: **Recursos da Instância** e **Recursos Compartilhados**.  
  
 Os **recursos de instância** referem-se aos componentes que são instalados uma vez para cada instância, de forma que você tenha várias cópias deles (uma para cada instância). Cada instância pode ser uma versão separada com um nível de patch diferente. Quando você instalar um patch, se for um service pack, um hotfix ou uma atualização cumulativa, ele atualizará apenas os arquivos de uma instância em determinada máquina, mais os recursos compartilhados caso não tenham sido atualizados.  
  
 **Recursos compartilhados** refere-se a recursos que são comuns em todas as instâncias em um determinado computador. Cada um desses recursos compartilhados foi criado para ser compatível com versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] com suporte (service packs, atualizações cumulativas e hotfixes) que podem ser instaladas paralelamente.  
  
> [!NOTE]  
>  Clusters de failover: ** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ** Os [!INCLUDE[ssDE](../../includes/ssde-md.md)] componentes [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e são os únicos [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] recursos que dão suporte ao clustering de failover. Você pode instalar outros componentes, como o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ou o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]em um nó de cluster de failover, mas eles não dão suporte a cluster, e seus serviços não realizarão failover se o nó de cluster de failover ficar offline. Para obter mais informações, consulte [instâncias de cluster de failover do AlwaysOn &#40;SQL Server&#41;](../failover-clusters/windows/always-on-failover-cluster-instances-sql-server.md).  
  
### <a name="instance-features"></a>Recursos da Instância  
 É exibida uma descrição para cada grupo de componentes no painel **Descrição** quando você o seleciona. Você pode selecionar qualquer combinação de caixas de seleção. Para continuar, você deve fazer uma seleção.  
  
|Recursos|DESCRIÇÃO|  
|--------------|-----------------|  
|[!INCLUDE[ssDE](../../includes/ssde-md.md)] Serviços|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]inclui o [!INCLUDE[ssDE](../../includes/ssde-md.md)], o serviço principal para armazenar, processar e proteger dados, replicação, pesquisa de texto completo, ferramentas para gerenciar dados XML e relacionais e o [!INCLUDE[ssDQSnoversion](../../includes/ssdqsnoversion-md.md)] (DQS) Server. Estes são os recursos do mecanismo de banco de dados:<br /><br /> O [!INCLUDE[ssDE](../../includes/ssde-md.md)] é o serviço principal para armazenamento, processamento e segurança de dados.<br /><br /> Replicação: opcional: a replicação é um conjunto de tecnologias para copiar e distribuir dados e objetos de um banco de dados para outro e, em seguida, sincronizar entre os bancos de dados para manter a consistência.<br /><br /> Pesquisa de Texto Completo: (opcional) a Pesquisa de Texto Completo fornece funcionalidade para realizar consultas de texto completo em dados baseados em caracteres não criptografados nas tabelas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> 
  [!INCLUDE[ssDQSnoversion](../../includes/ssdqsnoversion-md.md)]: Opcional: o [!INCLUDE[ssDQSnoversion](../../includes/ssdqsnoversion-md.md)] (DQS) é uma solução de limpeza de dados que permite descobrir dados inconsistentes e incorretos na fonte de dados. Essa solução fornece modos interativos e assistidos por computador de limpar seus dados. Marque esta caixa de seleção para instalar o servidor DQS. Depois de concluir a instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , você terá de executar o arquivo DQSInstaller.exe para *concluir* a instalação do servidor DQS. Se você instalou a instância padrão do SQL Server, esse arquivo estará disponível em c:\Arquivos de\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]programas \MSSQL12. MSSQLSERVER\MSSQL\Binn.<br /><br /> <br /><br /> Clusters de failover: ** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ** Os componentes de replicação e pesquisa de texto completo são necessários e selecionados automaticamente pela instalação [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para instalações de clustering de failover quando você seleciona serviços de mecanismo de banco de dados.|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] inclui as ferramentas para criação e gerenciamento de aplicativos OLAP (processamento analítico online) e de mineração de dados.|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]-Nativo|O modo Nativo do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] inclui componentes de servidor e cliente para criar, gerenciar e implantar relatórios de tabelas, de matriz, gráficos e de forma livre. O[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] também é uma plataforma extensível que você pode usar para desenvolver aplicativos de relatório.|  
  
> [!IMPORTANT]
>  1.  A Instalação não configura o balanceamento de carga e o endereçamento de URL única para vários nós em uma implantação em expansão do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Para concluir uma implantação de expansão, você deve usar o Windows Server, o [!INCLUDE[msCoName](../../includes/msconame-md.md)] Application Center ou software de gerenciamento de cluster de terceiros. Para obter mais informações sobre como configurar a implantação do Web farm, consulte [Configurando Reporting Services para implantação em expansão](https://go.microsoft.com/fwlink/?LinkId=199448) (https://go.microsoft.com/fwlink/?LinkId=199448).  
> 2.  Para obter os requisitos de navegador dos componentes do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], consulte [Planejando o suporte a navegador do Reporting Services e Power View &#40;Reporting Services 2014&#41;](../../../2014/reporting-services/browser-support-for-reporting-services-and-power-view.md).  
> 3.  Não há suporte ao [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] em configurações lado a lado na plataforma de 64 bits e no subsistema de 32 bits (WOW64) de uma servidor de 64 bits ao mesmo tempo.  
  
### <a name="shared-features"></a>Recursos compartilhados  
 Os recursos compartilhados por todas as instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em um único computador são instalados em um único diretório. São elas:  
  
|Recurso|DESCRIÇÃO|  
|-------------|-----------------|  
|
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] – SharePoint|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]O modo do SharePoint é um aplicativo baseado em servidor para criar, gerenciar e entregar relatórios para email, vários formatos de arquivo e formas interativas baseadas na Web. O modo do SharePoint integra a exibição de relatórios e experiência de gerenciamento de relatórios com produtos do SharePoint. Para obter mais informações, veja [Servidor de relatório do Reporting Services &#40;Modo do SharePoint&#41;](../../../2014/reporting-services/reporting-services-report-server-sharepoint-mode.md).|  
|Suplemento[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Add-in for SharePoint Products|O suplemento do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para produtos do SharePoint inclui componentes de gerenciamento e interface do usuário para integrar um produto do SharePoint com um servidor de relatórios [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] no modo SharePoint. Para obter mais informações, consulte [onde encontrar o suplemento de Reporting Services para produtos do SharePoint](../../reporting-services/install-windows/where-to-find-the-reporting-services-add-in-for-sharepoint-products.md).|  
|Cliente Data Quality|O Cliente Data Quality é um aplicativo autônomo que se conecta ao servidor de DQS. Ele fornece uma interface gráfica intuitiva do usuário para executar operações de limpeza de dados e correspondência de dados, e para realizar tarefas administrativas no DQS.|  
|Conectividade das ferramentas de cliente|As Ferramentas de Cliente incluem componentes para a comunicação entre clientes e servidores, incluindo bibliotecas de rede para DB-Library, OLEDB para OLAP, ODBC, ADODB e ADOMD+.|  
|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]|
  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] é um conjunto de ferramentas gráficas e objetos programáveis para mover, copiar e transformar dados.|  
|Compatibilidade das ferramentas de cliente com versões anteriores|A compatibilidade de versões anteriores de ferramentas de cliente inclui os seguintes componentes:<br /><br /> SQL Distributed Management Objects (SQL-DMO). Para obter mais informações, consulte [Recursos do SQL Server descontinuados no SQL Server 2014](../../../2014/getting-started/discontinued-sql-server-features-in-sql-server-2014.md).<br /><br /> DSO (Decision Support Objects). Para obter mais informações, consulte [Alterações recentes em recursos do Analysis Services no SQL Server 2014](../../../2014/analysis-services/breaking-changes-to-analysis-services-features-in-sql-server-2014.md).|  
|SDK de Ferramentas de cliente|Inclui o Software Development Kit que contém recursos para programadores.|  
|Componentes de documentação|Os componentes de documentação incluem os componentes para exibir e gerenciar o conteúdo da ajuda.|  
|Ferramentas de Gerenciamento - Básicas|**Ferramentas de gerenciamento-básicas:** Isso inclui o seguinte:<br /><br /> [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]suporte para o [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)], o utilitário **sqlcmd** e o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor do PowerShell<br /><br /> **Ferramentas de gerenciamento-completo:** Isso inclui os seguintes componentes, além dos componentes na versão básica:<br /><br /> Suporte do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]<br /><br /> [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]<br /><br /> Database Engine Tuning Advisor<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Gerenciamento de utilitário|  
|Distributed Replay Controller|O controlador Distributed Replay orquestra as ações dos clientes de reprodução distribuída. Cada ambiente de Distributed Replay pode conter apenas uma instância de controlador. Para obter mais informações, consulte [SQL Server Distributed Replay](../../tools/distributed-replay/sql-server-distributed-replay.md).|  
|Distributed Replay Client|Os clientes do Distributed Replay trabalham juntos para simular cargas de trabalho em uma instância do SQL Server. Pode haver um ou mais clientes em cada ambiente do Distributed Replay. Para obter mais informações, consulte [SQL Server Distributed Replay](../../tools/distributed-replay/sql-server-distributed-replay.md).|  
|SDK de Conectividade de Cliente do SQL|Inclui o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client (ODBC/OLE DB) SDK para desenvolvimento de aplicativos de banco de dados.|  
|[!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]|O [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] é uma plataforma para integrar dados de sistemas discrepantes em uma organização em uma única fonte de dados mestre para fins de exatidão e auditoria. A opção [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] instala o [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)], assemblies, um snap-in do Windows PowerShell, pastas e arquivos de aplicativos e serviços Web.|  
  
 Por padrão, os componentes compartilhados são instalados em %Arquivos de Programas%Microsoft SQL Server\\. Para alterar o caminho de instalação, clique no botão **Procurar** . Se você alterar o caminho de instalação de um componente compartilhado, também o altera para outros componentes compartilhados. As instalações subsequentes instalarão componentes compartilhados no mesmo local que a instalação original.  
  
 **Diretório raiz da instância** – por padrão, o diretório raiz da instância é\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\C:\Program Files. Para especificar um diretório raiz não padrão, clique no botão **Procurar** ou forneça um nome de caminho.  
  
 Em sistemas operacionais com base em x64, você pode especificar onde os componentes de 64 bits serão instalados e onde no subsistema de 32 bits WOW64 os componentes serão instalados.  
  
## <a name="disk-space-requirements"></a>Requisitos de espaço em disco  
 Use a página Resumo de Custo de Disco para examinar os requisitos de espaço em disco para os recursos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] selecionados para a instalação.  
  
### <a name="options"></a>Opções  
 Se o espaço em disco necessário for muito alto, considere as seguintes opções:  
  
-   Altere os diretórios de instalação para uma unidade com mais espaço em disco.  
  
-   Altere os recursos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para a instalação.  
  
-   Crie mais espaço livre na unidade especificada movendo outros arquivos ou aplicativos.  
  
## <a name="installing-adventureworks-sample-databases"></a>Instalando bancos de dados de exemplo AdventureWorks  
 Por padrão, os bancos de dados de exemplo e o código de exemplo não são instalados como parte da instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para obter mais informações sobre como instalar bancos de dados de exemplo e código de exemplo, consulte o [Microsoft SQL Server projetos da comunidade & exemplos](https://go.microsoft.com/fwlink/?LinkId=87843) (https://go.microsoft.com/fwlink/?LinkId=87843).  
  
 Informações adicionais sobre exemplos estarão disponíveis depois que o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] for instalado. No menu **Iniciar** , clique em **todos os programas**, ** [!INCLUDE[msCoName](../../includes/msconame-md.md)] **clique em, clique em **documentação e tutoriais**e, em seguida, clique em ** [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] exemplos visão geral**.  
  
## <a name="see-also"></a>Consulte Também  
 [Edições e componentes do SQL Server 2014](../editions-and-components-of-sql-server-2016.md)  
  
  
