---
title: Edições e componentes do SQL Server 2014 | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- Enterprise Edition [SQL Server]
- Developer Edition [SQL Server]
- 32-bit vs. 64-bit editions [SQL Server]
- default components
- Workgroup Edition [SQL Server]
- Internet servers [SQL Server]
- installing SQL Server, components
- Setup [SQL Server], components
- SQL Server, editions
- SQL Server, components
- client/server applications [SQL Server]
- editions [SQL Server]
- versions [SQL Server]
- Setup [SQL Server], editions
- SQL Server Installation Wizard
- components [SQL Server]
- Standard Edition [SQL Server]
- 64-bit edition [SQL Server]
- IIS [SQL Server]
- installing SQL Server, editions
- editions [SQL Server], about edition options
- Setup [SQL Server]
ms.assetid: e5186f02-dd91-47d0-8fa4-de3f41c76903
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 9610dc1cc729dc555d42c0dfe5eeb117f9cfba18
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62806332"
---
# <a name="editions-and-components-of-sql-server-2014"></a>Edições e componentes do SQL Server 2014
  Os requisitos de instalação variam de acordo com as necessidades do aplicativo. As diferentes edições do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] acomodam desempenho, runtime e requisitos de preço exclusivos para organizações e indivíduos. Os componentes do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] que você instala dependem também dos seus requisitos específicos. As seções a seguir ajudarão você a entender como fazer a melhor escolha entre as edições e os componentes disponíveis no [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
## <a name="principal-editions-of-sscurrent"></a>Principais edições do [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]  
 A tabela a seguir descreve as edições principais do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Para obter mais informações, consulte [Features Supported by the Editions of SQL Server 2014](../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)  
  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] edição|Definição|  
|---------------------------------------|----------------|  
|Enterprise (64 bits e 32 bits)|A oferta premium, a edição [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] Enterprise fornece recursos de datacenter abrangentes de alta tecnologia com desempenho incrivelmente rápido, virtualização ilimitada e business intelligence de ponta a ponta – oferecendo altos níveis de serviço para cargas de trabalho críticas e acesso a visões de dados para usuários finais.|  
|Business Intelligence (64 bits e 32 bits)|A edição [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] Business Intelligence fornece uma plataforma abrangente que permite que as empresas criem e implantem soluções BI seguras, flexíveis e gerenciáveis. Ele oferece funcionalidade empolgante, como visualização e exploração de dados baseada em navegador; recursos poderosos de mashup de dados e gerenciamento de integração aprimorado.|  
|Standard (64 bits e 32 bits)|A edição [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] Standard fornece gerenciamento de dados básicos e bancos de dados de business intelligence para departamentos e pequenas empresas executarem seus aplicativos e dá suporte a ferramentas de desenvolvimento comuns para rede local e em nuvem – permitindo o gerenciamento eficiente de bancos de dados com mínimos recursos de TI.|  
  
## <a name="specialized-editions-of-sscurrent"></a>Edições especializadas do [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]  
 As edições especializadas do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] são destinadas às cargas de trabalho comerciais. A tabela a seguir descreve as edições especializadas do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] edição|Descrição|  
|---------------------------------------|-----------------|  
|Web (64 bits e 32 bits)|A edição[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] Web é uma opção de baixo custo total de propriedade para hospedagem de sites e VAPs da Web que fornece recursos de escalabilidade, economia e capacidade de gerenciamento para propriedades da Web de pequeno a grande porte.|  
  
## <a name="breadth-editions-of-sscurrent"></a>Edições de amplitude do [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]  
 As edições de amplitude do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] foram criadas para cenários de cliente específicos e são oferecidas GRATUITAMENTE ou a um custo irrisório. A tabela a seguir descreve as edições de amplitude do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] edição|Descrição|  
|---------------------------------------|-----------------|  
|Developer (64 bits e 32 bits)|A edição[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] Developer permite que os desenvolvedores criem qualquer tipo de aplicativo com base no [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Ele inclui todas as funcionalidades da edição Enterprise, mas é licenciado para ser usado como um sistema de teste e desenvolvimento, e não como um servidor de produção. O [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Developer é uma opção ideal para pessoas que criam e testam aplicativos.|  
|Edições Express (64 e 32 bits)|A edição [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] Express é o banco de dados básico gratuito, ideal para conhecer e criar aplicativos de desktop e plicativos controlados por dados de pequenos servidores. É a melhor escolha para fornecedores de software independente, desenvolvedores e interessados que criam aplicativos cliente. Se precisar de recursos mais avançados de banco de dados, o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Express pode ser perfeitamente atualizado para versões mais sofisticadas do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. O[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Express LocalDB, uma versão leve do Express que tem todos os seus recursos de programação, embora seja executado no modo de usuário, e tenha uma instalação rápida e sem nenhuma configuração e uma lista curta de pré-requisitos.|  
  
## <a name="using-ssnoversion-with-an-internet-server"></a>Usando o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] com um servidor de Internet  
 Em um servidor de Internet, como um servidor que executa o IIS (Serviços de Informações da Internet), você instalará normalmente as ferramentas cliente do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . Essas ferramentas incluem os componentes cliente de conectividade usados por um aplicativo que se conecta a uma instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
> [!NOTE]  
>  Apesar de ser possível instalar uma instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] em um computador que executa o IIS, isso é feito normalmente apenas para pequenos sites da Web que possuem um único computador servidor. A maioria dos sites da Web possui sistemas IIS de camada intermediária em um servidor ou em clusters de servidores e bancos de dados em um servidor diferente ou em uma federação de servidores.  
  
## <a name="using-ssnoversion-with-clientserver-applications"></a>Usando o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] com aplicativos cliente/servidor  
 Você pode instalar apenas os componentes cliente do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] em um computador que esteja executando aplicativos cliente/servidor que se conectam diretamente a uma instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. A instalação dos componentes cliente é também uma boa opção se você administra uma instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] em um servidor de banco de dados ou se planeja desenvolver aplicativos no [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
 A opção de ferramentas cliente instala os seguintes recursos do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] : componentes compatíveis com versões anteriores, [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], componentes de conectividade, ferramentas de gerenciamento, Software Development Kit e componentes dos Manuais Online do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . Para obter mais informações, consulte [instalar SQL Server 2014 do assistente de instalação &#40;&#41;de ](../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md)instalação.  
  
## <a name="deciding-among-ssnoversion-components"></a>Decidindo entre os componentes do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]  
 Use a página Seleção de Recursos do Assistente de Instalação do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para selecionar os componentes a serem incluídos em uma instalação do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Por padrão, nenhum dos recursos na árvore está selecionado.  
  
 Use as informações nas tabelas a seguir para determinar o conjunto de recursos mais adequado às suas necessidades.  
  
|Componentes de servidor|Descrição|  
|-----------------------|-----------------|  
|[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]|[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]inclui o [!INCLUDE[ssDE](../includes/ssde-md.md)], o serviço principal para armazenar, processar e proteger dados, replicação, pesquisa de texto completo, ferramentas para gerenciar dados XML e relacionais e o [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) Server.|  
|[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]|[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] inclui as ferramentas para criação e gerenciamento de aplicativos OLAP (processamento analítico online) e de mineração de dados.|  
|[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]|O[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] inclui componentes de servidor e cliente por criar, gerenciar e implantar relatórios tabulares, de matriz, gráficos e de forma livre. O[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] também é uma plataforma extensível que você pode usar para desenvolver aplicativos de relatório.|  
|[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]|[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] é um conjunto de ferramentas gráficas e objetos programáveis para mover, copiar e transformar dados. Ele também inclui o componente [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) para o [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)].|  
|[!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]|O[!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] (MDS) é a solução do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para gerenciamento de dados mestre. O MDS pode ser configurado para gerenciar qualquer domínio (produtos, clientes, contas) e inclui hierarquias, segurança granular, transações, controle de versão de dados e regras de negócio, bem como um [!INCLUDE[ssMDSXLS](../includes/ssmdsxls-md.md)] que pode ser usado para gerenciar dados.|  
  
|Ferramentas de gerenciamento|Descrição|  
|----------------------|-----------------|  
|[!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]|O[!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] é um ambiente integrado para acessar, configurar, gerenciar, administrar e desenvolver os componentes do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. O[!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] permite que os desenvolvedores e administradores de todos os níveis utilizem o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].|  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Configuration Manager|O[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Configuration Manager fornece gerenciamento básico de configuração para serviços, protocolos do servidor, protocolos do cliente e aliases do cliente do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]|  
|[!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)]|[!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] fornece uma interface gráfica do usuário para monitorar uma instância do [!INCLUDE[ssDE](../includes/ssde-md.md)] ou do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].|  
|[!INCLUDE[ssDE](../includes/ssde-md.md)] Orientador de Otimização|O Orientador de Otimização do[!INCLUDE[ssDE](../includes/ssde-md.md)] ajuda a criar conjuntos de índices, exibições indexadas e partições ideais.|  
|Cliente Data Quality|Fornece uma interface gráfica do usuário altamente simples e intuitiva para se conectar ao servidor DQS e executar operações de limpeza de dados. Ele também permite monitorar centralmente várias atividades executadas durante a operação de limpeza de dados.|  
|[!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]|O[!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] oferece um IDE para criar soluções para os componentes de Business Intelligence: [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]e [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)].<br /><br /> (Antes chamado de Business Intelligence Development Studio).<br /><br /> O[!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] também inclui "Projetos de banco de dados" que oferecem um ambiente integrado para desenvolvedores de banco de dados realizarem seu trabalho de design de banco de dados para qualquer plataforma [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] (no local e fora do local) no Visual Studio. Os desenvolvedores de banco de dados podem usar o Gerenciador de Servidores aprimorado no Visual Studio para criar ou editar facilmente objetos de banco de dados e dados, ou executar consultas.|  
|Componentes de conectividade|Instala componentes para comunicação entre clientes e servidores, e bibliotecas de rede para DB-Library, ODBC e OLE DB.|  
  
|Documentação|Descrição|  
|-------------------|-----------------|  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Manuais Online|Documentação principal do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].|  
  
## <a name="see-also"></a>Consulte Também  
 [Planejando uma instalação do SQL Server](install/planning-a-sql-server-installation.md)   
 [Instale o SQL Server 2014 do assistente de instalação &#40;a instalação&#41;](../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md)  
  
  
