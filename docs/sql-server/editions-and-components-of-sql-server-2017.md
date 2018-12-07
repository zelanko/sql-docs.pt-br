---
title: Edições e recursos com suporte do SQL Server 2017 | Microsoft Docs
ms.custom: ''
ms.date: 11/11/2017
ms.prod: sql
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
ms.assetid: ''
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: '>= sql-server-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: b512abcb57cc65cc3335504d706a87bf582467c7
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52544047"
---
# <a name="editions-and-supported-features-of-sql-server-2017"></a>Edições e recursos com suporte do SQL Server 2017
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

Este tópico fornece detalhes de recursos com suporte nas diferentes edições do SQL Server 2017. 

Para obter informações sobre as versões anteriores, consulte:

* [SQL Server 2016](editions-and-components-of-sql-server-2016.md).  
* [SQL Server 2014](https://msdn.microsoft.com/library/cc645993(v=sql.120).aspx).

  
Os requisitos de instalação variam de acordo com as necessidades do aplicativo. As diferentes edições do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] acomodam desempenho, tempo de execução e requisitos de preço exclusivos para organizações e indivíduos. Os componentes do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] que você instala dependem também dos seus requisitos específicos. As seções a seguir ajudarão você a entender como fazer a melhor escolha entre as edições e os componentes disponíveis no [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  

A edição Evaluation do SQL Server está disponível por um período de avaliação de 180 dias.  
  
Para notas de versão mais recentes e informações sobre novidades, consulte o seguinte:
- [Notas de versão do SQL Server 2017](../sql-server/sql-server-2017-release-notes.md)
- [Novidades no SQL Server 2017](../sql-server/what-s-new-in-sql-server-2017.md)

### <a name="try-sql-server"></a>Experimente o SQL Server.    
    
> [![Baixar no Centro de Avaliação](../analysis-services/media/download.png)](https://www.microsoft.com/evalcenter/evaluate-sql-server-2017-ctp/) **[Baixar o SQL Server 2017 no Centro de Avaliação](https://www.microsoft.com/evalcenter/evaluate-sql-server-2017-ctp/)**    

<!---    
> ![Azure Virtual Machine small](../analysis-services/media/azure-virtual-machine-small.png) **[Spin up a Virtual Machine with SQL Server 2016 already installed](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.SQL2016SP1-WS2016?tab=Overview?wt.mc_id=sqL16_vm)**   
--->

## <a name="includessnoversionincludesssnoversion-mdmd-editions"></a>Edições do[!INCLUDE[ssNoVersion](../includes/ssNoVersion-md.md)]   
 A tabela a seguir descreve essas edições do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. 
  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] edição|Definição|  
|---------------------------------------|----------------|  
|Enterprise|A oferta premium, a edição [!INCLUDE[ssNoVersion](../includes/ssNoVersion-md.md)] Enterprise fornece recursos de datacenter abrangentes de alta tecnologia com desempenho incrivelmente rápido, virtualização ilimitada e business intelligence de ponta a ponta – oferecendo altos níveis de serviço para cargas de trabalho críticas e acesso a visões de dados para usuários finais.|  
|Standard|A edição [!INCLUDE[ssNoVersion](../includes/ssNoVersion-md.md)] Standard fornece gerenciamento de dados básicos e bancos de dados de business intelligence para departamentos e pequenas empresas executarem seus aplicativos e dá suporte a ferramentas de desenvolvimento comuns para rede local e em nuvem – permitindo o gerenciamento eficiente de bancos de dados com mínimos recursos de TI.|  
|Web|A edição[!INCLUDE[ssNoVersion](../includes/ssNoVersion-md.md)] Web é uma opção de baixo custo total de propriedade para hospedagem de sites e VAPs da Web que fornece recursos de escalabilidade, economia e capacidade de gerenciamento para propriedades da Web de pequeno a grande porte.|  
|Desenvolvedor|A edição[!INCLUDE[ssNoVersion](../includes/ssNoVersion-md.md)] Developer permite que os desenvolvedores criem qualquer tipo de aplicativo com base no [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Ele inclui todas as funcionalidades da edição Enterprise, mas é licenciado para ser usado como um sistema de teste e desenvolvimento, e não como um servidor de produção. O [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Developer é uma opção ideal para pessoas que criam e testam aplicativos.|  
|Edições Express|A edição Express é o banco de dados gratuito de nível de entrada, ideal para conhecer e criar aplicativos de área de trabalho e aplicativos controlados por dados de pequenos servidores. É a melhor escolha para fornecedores de software independente, desenvolvedores e interessados que criam aplicativos cliente. Se precisar de recursos mais avançados de banco de dados, o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Express pode ser perfeitamente atualizado para versões mais sofisticadas do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. O [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Express LocalDB é uma versão leve do Express que tem todos os seus recursos de programação, é executado no modo de usuário e tem uma instalação rápida e sem nenhuma configuração e uma lista curta de pré-requisitos.|  
  
## <a name="using-includessnoversionincludesssnoversion-mdmd-with-an-internet-server"></a>Usando o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] com um servidor de Internet  
 Em um servidor de Internet, como um servidor que executa o IIS (Serviços de Informações da Internet), você instalará normalmente as ferramentas cliente do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . Essas ferramentas incluem os componentes cliente de conectividade usados por um aplicativo que se conecta a uma instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
>[!NOTE]
>Apesar de ser possível instalar uma instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] em um computador que executa o IIS, isso é feito normalmente apenas para pequenos sites da Web que possuem um único computador servidor. A maioria dos sites da Web possui sistemas IIS de camada intermediária em um servidor ou em clusters de servidores e bancos de dados em um servidor diferente ou em uma federação de servidores.  
  
## <a name="using-includessnoversionincludesssnoversion-mdmd-with-clientserver-applications"></a>Usando [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] com aplicativos cliente/servidor  
 Você pode instalar apenas os componentes cliente do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] em um computador que esteja executando aplicativos cliente/servidor que se conectam diretamente a uma instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. A instalação dos componentes cliente é também uma boa opção se você administra uma instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] em um servidor de banco de dados ou se planeja desenvolver aplicativos no [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
 A opção de ferramentas cliente instala os seguintes recursos do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] : componentes compatíveis com versões anteriores, [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], componentes de conectividade, ferramentas de gerenciamento, Software Development Kit e componentes dos Manuais Online do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . Para obter mais informações, consulte [Instalar o SQL Server](../database-engine/install-windows/install-sql-server.md).  
  
## <a name="deciding-among-includessnoversionincludesssnoversion-mdmd-components"></a>Decidindo entre os componentes do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]  
 Use a página Seleção de Recursos do Assistente de Instalação do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para selecionar os componentes a serem incluídos em uma instalação do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Por padrão, nenhum dos recursos na árvore está selecionado.  
  
 Use as informações nas tabelas a seguir para determinar o conjunto de recursos mais adequado às suas necessidades.  
  
|Componentes de servidor|Descrição|  
|-----------------------|-----------------|  
|[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]|[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] inclui [!INCLUDE[ssDE](../includes/ssde-md.md)], o serviço principal para armazenamento, processamento e proteção de dados, replicação, pesquisa de texto completo, ferramentas para gerenciar dados XML e relacionais, na integração da análise de banco de dados e na integração do PolyBase para acesso ao Hadoop e a outras fontes de dados heterogêneas, bem como o servidor [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS).|  
|[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]|[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] inclui as ferramentas para criação e gerenciamento de aplicativos OLAP (processamento analítico online) e de mineração de dados.|  
|[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]|O[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] inclui componentes de servidor e cliente por criar, gerenciar e implantar relatórios tabulares, de matriz, gráficos e de forma livre. O[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] também é uma plataforma extensível que você pode usar para desenvolver aplicativos de relatório.|  
|[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]|[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] é um conjunto de ferramentas gráficas e objetos programáveis para mover, copiar e transformar dados. Ele também inclui o componente [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) para o [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)].|  
|[!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]|O[!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] (MDS) é a solução do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para gerenciamento de dados mestre. O MDS pode ser configurado para gerenciar qualquer domínio (produtos, clientes, contas) e inclui hierarquias, segurança granular, transações, controle de versão de dados e regras de negócio, bem como um [!INCLUDE[ssMDSXLS](../includes/ssmdsxls-md.md)] que pode ser usado para gerenciar dados.|  
|Serviços de Machine Learning (No Banco de Dados)|Os Serviços de Machine Learning (No Banco de Dados) oferecem suporte a soluções escalonáveis de aprendizado de máquina por meio de fontes de dados empresariais. No SQL Server 2016, havia suporte para a linguagem R. O SQL Server 2017 oferece suporte às linguagens R e Python.|
|Servidor do Machine Learning (Autônomo)|O Servidor do Machine Learning (Autônomo) oferece suporte à implantação de soluções de aprendizado de máquina distribuídas e escalonáveis em várias plataformas, usando várias fontes de dados empresariais, inclusive Linux e Hadoop. No SQL Server 2016, havia suporte para a linguagem R. O SQL Server 2017 oferece suporte às linguagens R e Python.|

  
|Ferramentas de gerenciamento|Descrição|  
|----------------------|-----------------|  
|[!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]|O[!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] é um ambiente integrado para acessar, configurar, gerenciar, administrar e desenvolver os componentes do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. O[!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] permite que os desenvolvedores e administradores de todos os níveis utilizem o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].<br /><br /> Baixe e instale o <br />                [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] de  [Baixar o SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx)|  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Configuration Manager|O[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Configuration Manager fornece gerenciamento básico de configuração para serviços, protocolos do servidor, protocolos do cliente e aliases do cliente do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] |  
|[!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)]|[!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] fornece uma interface gráfica do usuário para monitorar uma instância do [!INCLUDE[ssDE](../includes/ssde-md.md)] ou do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].|  
|[!INCLUDE[ssDE](../includes/ssde-md.md)] Orientador de Otimização|O Orientador de Otimização do[!INCLUDE[ssDE](../includes/ssde-md.md)] ajuda a criar conjuntos de índices, exibições indexadas e partições ideais.|  
|Cliente Data Quality|Fornece uma interface gráfica do usuário altamente simples e intuitiva para se conectar ao servidor DQS e executar operações de limpeza de dados. Ele também permite monitorar centralmente várias atividades executadas durante a operação de limpeza de dados.|  
|[!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]|O[!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] oferece um IDE para criar soluções para os componentes de Business Intelligence: [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]e [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)].<br /><br /> (Antes chamado de Business Intelligence Development Studio).<br /><br /> O[!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] também inclui "Projetos de banco de dados" que oferecem um ambiente integrado para desenvolvedores de banco de dados realizarem seu trabalho de design de banco de dados para qualquer plataforma [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] (no local e fora do local) no Visual Studio. Os desenvolvedores de banco de dados podem usar o Gerenciador de Servidores aprimorado no Visual Studio para criar ou editar facilmente objetos de banco de dados e dados, ou executar consultas.|  
|Componentes de conectividade|Instala componentes para comunicação entre clientes e servidores, e bibliotecas de rede para DB-Library, ODBC e OLE DB.|  
  
|Documentação|Descrição|  
|-------------------|-----------------|  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Manuais Online|Documentação principal do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].| 

**Edições Developer e Evaluation**  
Para saber quais os recursos com suporte nas edições Developer e Evaluation, consulte os recursos listados para o SQL Server Enterprise Edition nas tabelas abaixo.

A Developer edition continua a dar suporte a apenas um cliente para o [SQL Server Distributed Replay](../tools/distributed-replay/sql-server-distributed-replay.md). 
  
##  <a name="Cross-BoxScaleLimits"></a> Limites de escala  
  
|Recurso|Enterprise|Standard|Web|Express with Advanced Services|Express| 
|-------------|----------------|--------------|---------|------------------------------------|------------------------|
|Capacidade máxima de computação usada por uma única instância – [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]<sup>1</sup>|Máximo do sistema operacional|Limitado a menos de 4 soquetes ou 24 núcleos|Limitado a menos de 4 soquetes ou 16 núcleos|Limitado a menos de 1 soquete ou 4 núcleos|Limitado a menos de 1 soquete ou 4 núcleos| 
|Capacidade máxima de computação usada por uma única instância – [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] ou [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]|Máximo do sistema operacional|Limitado a menos de 4 soquetes ou 24 núcleos|Limitado a menos de 4 soquetes ou 16 núcleos|Limitado a menos de 1 soquete ou 4 núcleos|Limitado a menos de 1 soquete ou 4 núcleos|  
|Memória máxima para o pool de buffers por instância do [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]|Máximo do sistema operacional|128 GB|64 GB|1410 MB|1410 MB|
|Máximo de memória para cache do segmento Columnstore por instância do [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]|Memória ilimitada| 32 GB| 16 GB| 352 MB| 352 MB|  
|Tamanho de dados máximo otimizado para memória de acordo com banco de dados em [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]|Memória ilimitada| 32 GB| 16 GB| 352 MB| 352 MB|  
|Memória máxima utilizada por instância de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]|Máximo do sistema operacional|Tabela: 16 GB<br /><br /> MOLAP: 64 GB|N/A|N/A|N/A|  
|Memória máxima utilizada por instância de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]|Máximo do sistema operacional|64 GB|64 GB|4 GB|N/A|
|Tamanho máximo do banco de dados relacional|524 PB|524 PB|524 PB|10 GB|10 GB|  
  
<sup>1</sup> O Enterprise Edition com Servidor + licenciamento baseado em CAL (Licença de Acesso para Cliente) (não disponível para novos contratos) é limitado ao máximo de 20 núcleos por instância do SQL Server. Não há limites no modelo de Licenciamento de Servidor Baseado em Núcleo. Para saber mais, confira [Compute Capacity Limits by Edition of SQL Server](../sql-server/compute-capacity-limits-by-edition-of-sql-server.md).  
 
##  <a name="RDBMSHA"></a> Alta Disponibilidade do RDBMS  
  
|Recurso|Enterprise|Standard|Web|Express with Advanced Services|Express|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------|  
|Suporte do Server Core <sup>1</sup>|Sim|Sim|Sim|Sim|Sim|  
|Envio de logs|Sim|Sim|Sim|não|não|  
|Espelhamento de banco de dados|Sim|Sim<br /><br /> Somente segurança completa|Somente testemunha|Somente testemunha|Somente testemunha| 
|Compactação de backup|Sim|Sim|não|não|não| 
|Instantâneo do banco de dados|Sim|Sim|Sim|Sim|Sim|
|Instâncias do cluster de failover do AlwaysOn<sup>2</sup>|Sim|Sim|não|não|não|  
|Grupos de disponibilidade AlwaysOn<sup>3</sup>|Sim|não|não|não|não|
|Grupos de disponibilidade básicos <sup>4</sup>|não|Sim|não|não|não|
|Restauração de arquivo e página online|Sim|não|não|não|não|
|Indexação online|Sim|não|não|não|não|
|Recompilações de índice online retomáveis|Sim|não|não|não|não|
|Alteração de esquema online|Sim|não|não|não|não|
|Recuperação rápida|Sim|não|não|não|não|
|Backups espelhados|Sim|não|não|não|não|
|Adição de memória a quente e CPU|Sim|não|não|não|não|
|Supervisor de recuperação de banco de dados|Sim|Sim|Sim|Sim|Sim|
|Backup criptografado|Sim|Sim|não|não|não|
|Backup híbrido para o Microsoft Azure (backup para URL)|Sim|Sim|não|não|não|
|Grupo de disponibilidade sem cluster|Sim|Sim|não|não|não|não|
|Configuração de grupos de disponibilidade de confirmação de réplica mínima|Sim|Sim|Sim|não|não|não|
  

<sup>1</sup> Para obter mais informações sobre a instalação do SQL Server no Server Core, consulte [Instalar o SQL Server no Server Core](../database-engine/install-windows/install-sql-server-on-server-core.md). 

<sup>2</sup> Na Enterprise Edition, o número de nós é o máximo do sistema operacional. Na Standard Edition, há suporte para dois nós. 

<sup>3</sup> Na Enterprise Edition, há suporte para até oito réplicas secundárias, incluindo duas réplicas secundárias síncronas. 

<sup>4</sup> A Standard dá suporte a grupos de disponibilidade básicos. Um grupo de disponibilidade básico dá suporte a duas réplicas, com um banco de dados. Para obter mais informações sobre grupos de disponibilidade básicos, consulte [Grupos de Disponibilidade Básicos](../database-engine/availability-groups/windows/basic-availability-groups-always-on-availability-groups.md).  


##  <a name="RDBMSSP"></a> Escalabilidade e desempenho do RDBMS  
  
|Recurso|Enterprise|Standard|Web|Express with Advanced Services|Express|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------| 
|Columnstore <sup>1</sup>|Sim|Sim|Sim|Sim|Sim|  
|Binários de objeto grandes em índices columnstore clusterizados|Sim|Sim|Sim|Sim|Sim|  
|Recompilação de índice columnstore não clusterizado online|Sim|não|não|não|não|
|OLTP na memória <sup>1</sup>|Sim|Sim|Sim|Sim, <sup>2</sup>|Sim|
|Stretch Database|Sim|Sim|Sim|Sim|Sim|
|Memória principal persistente|Sim|Sim|Sim|Sim|Sim|
|Suporte de várias instâncias|50|50|50|50|50|
|Particionamento de tabela e índice|Sim|Sim|Sim|Sim|Sim|  
|Compactação de dados|Sim|Sim|Sim|Sim|Sim|
|Administrador de Recursos|Sim|não|não|não|não|  
|Paralelismo de tabela particionada|Sim|não|não|não|não|
|Contêineres de vários fluxos de arquivos|Sim|Sim|Sim|Sim|Sim|
|Memória de página grande com reconhecimento para NUMA e alocação de matriz de buffer|Sim|não|não|não|não|
|Buffer Pool Extension|Sim|Sim|não|não|não|
|Administração do recurso de E/S|Sim|não|não|não|não|  
|Durabilidade atrasada|Sim|Sim|Sim|Sim|Sim|
|Ajuste Automático|Sim|não|não|não|não|
|Junções Adaptáveis de Modo de Lote|Sim|não|não|não|não|
|Comentários de Concessão de Memória do Modo de Lote|Sim|não|não|não|não|
|Execução Intercalada para Funções com Valor de Tabela de Várias Instruções|Sim|Sim|Sim|Sim|Sim|
|Aprimoramentos de inserção em massa|Sim|Sim|Sim|Sim|Sim|


<sup>1</sup> Tamanho de dados de OLTP na memória e cache do segmento Columnstore são limitados a quantidade de memória especificada por edição na seção limites de escala. Os graus de máximos de paralelismo é limitado. Os graus de paralelismo do processo (DOP) de criação de um índice é limitado a 2 DOP para a Standard Edition e 1 DOP para a Web e a Express Editions. Refere-se a índices de columnstore criados em tabelas baseadas em disco e tabelas com otimização de memória.

<sup>2</sup> Esse recurso não está incluído na opção de instalação LocalDB.

##  <a name="RDBMSS"></a> Segurança do RDBMS  
  
|Recurso|Enterprise|Standard|Web|Express|Express with Advanced Services|  
|-------------|----------------|--------------|---------|-------------|------------------------------------| 
|Segurança em nível de linha|Sim|Sim|Sim|Sim|Sim|  
|Sempre Criptografado|Sim|Sim|Sim|Sim|Sim| 
|Mascaramento de dados dinâmicos|Sim|Sim|Sim|Sim|Sim|   
|Auditoria básica|Sim|Sim|Sim|Sim|Sim| 
|Auditoria refinada|Sim|Sim|Sim|Sim|Sim| 
|Criptografia transparente do banco de dados|Sim|não|não|não|não|   
|Gerenciamento extensível de chaves|Sim|não|não|não|não| 
|Funções definidas pelo usuário|Sim|Sim|Sim|Sim|Sim| 
|Bancos de dados independentes|Sim|Sim|Sim|Sim|Sim| 
|Criptografia para backups|Sim|Sim|não|não|não|  

##  <a name="Replication"></a> Replication  
  
|Recurso|Enterprise|Standard|Web|Express with Advanced Services|Express|   
|-------------|----------------|--------------|---------|------------------------------------|------------------------| 
|Assinantes heterogêneos|Sim|Sim|não|não|não|  
|Replicação de mesclagem|Sim|Sim|Sim (somente assinante)|Sim (somente assinante)|Sim (somente assinante)|   
|publicação Oracle|Sim|não|não|não|não| 
|Replicação transacional ponto a ponto|Sim|não|não|não|não|   
|Replicação de instantâneo|Sim|Sim|Sim (somente assinante)|Sim (somente assinante)|Sim (somente assinante)|   
|Controle de alterações do SQL Server|Sim|Sim|Sim|Sim|Sim| 
|Replicação transacional|Sim|Sim|Sim (somente assinante)|Sim (somente assinante)|Sim (somente assinante)|   
|Replicação transacional no Azure|Sim|Sim|não|não|não|   
|Assinatura atualizável de replicação transacional|Sim|não|não|não|não|  
  
##  <a name="SSMS"></a> Ferramentas de gerenciamento  
  
|Recurso|Enterprise|Standard|Web|Express with Advanced Services|Express| 
|-------------|----------------|--------------|---------|------------------------------------|------------------------|  
|SQL Management Objects (SMO)|Sim|Sim|Sim|Sim|Sim|  
|SQL Configuration Manager|Sim|Sim|Sim|Sim|Sim|   
|SQL CMD (ferramenta de prompt de comando)|Sim|Sim|Sim|Sim|Sim|      
|Distributed Replay – Ferramenta de Administração|Sim|Sim|Sim|Sim|não|  
|Distributed Replay – Cliente|Sim|Sim|Sim|não|não|  
|Distributed Replay - Controller|Sim (Até 16 clientes)|Sim (1 cliente)|Sim (1 cliente)|não|não|   
|SQL Profiler|Sim|Sim|Não <sup>1</sup>|Não <sup>1</sup>|Não <sup>1</sup>|  
|SQL Server Agent|Sim|Sim|Sim|não|não| 
|Pacote de gerenciamento do Microsoft System Center Operations Manager|Sim|Sim|Sim|não|não|  
|Database Tuning Advisor (DTA)|Sim|Sim <sup>2</sup>|Sim <sup>2</sup>|não|não|      
  
 <sup>1</sup> SQL Server Web, SQL Server Express, SQL Server Express with Tools e SQL Server Express with Advanced Services podem ter o perfil criado usando as edições SQL Server Enterprise e Standard.  
  
 <sup>2</sup> Ajuste habilitado somente em recursos da edição Standard  
  
##  <a name="RDBMSM"></a> Gerenciamento RDBMS  
  
|Recurso|Enterprise|Standard|Web|Express with Advanced Services|Express|   
|-------------|----------------|--------------|---------|------------------------------------|------------------------|  
|Instâncias de usuário|não|não|não|Sim|Sim| 
|LocalDB|não|não|não|Sim|não| 
|Conexão dedicada de administrador|Sim|Sim|Sim|Sim, com o sinalizador de rastreamento|Sim, com o sinalizador de rastreamento|   
|Suporte a SysPrep <sup>1</sup>|Sim|Sim|Sim|Sim|Sim| 
|Suporte de scripts PowerShell<sup>2</sup>|Sim|Sim|Sim|Sim|Sim| 
|Suporte para operações de componente do aplicativo da camada de dados – extrair, implantar, atualizar, excluir|Sim|Sim|Sim|Sim|Sim| 
|Automação de política (verificação de agenda e alterações)|Sim|Sim|Sim|não|não|   
|Coletor de dados de desempenho|Sim|Sim|Sim|não|não| 
|Pode se inscrever como uma instância gerenciada no gerenciamento de várias instâncias|Sim|Sim|Sim|não|não|   
|Relatórios de desempenho padrão|Sim|Sim|Sim|não|não| 
|Guias de plano e planejar congelamento para guias de plano|Sim|Sim|Sim|não|não|   
|Direcione a consulta de exibições indexadas (usando a dica de NOEXPAND)|Sim|Sim|Sim|Sim|Sim| 
|Manutenção automática de exibições indexadas|Sim|Sim|Sim|não|não| 
|Exibições particionadas distribuídas|Sim|não|não|não|não| 
|Operações indexadas paralelas|Sim|não|não|não|não|  
|Uso automático da exibição indexada através do otimizador de consulta|Sim|não|não|não|não| 
|Verificação de consistência paralela|Sim|não|não|não|não| 
|Ponto de controle do Utilitário do SQL Server|Sim|não|não|não|não|    
|Extensão do pool de buffers|Sim|Sim|não|não|não| 
  
 <sup>1</sup> Para obter mais informações, veja [Considerações para instalação do SQL Server usando SysPrep](../database-engine/install-windows/considerations-for-installing-sql-server-using-sysprep.md).  
 
 <sup>2</sup> No Linux, os scripts do PowerShell têm suporte de computadores Windows que direcionam SQL Servers no Linux. 
##  <a name="DevTools"></a> Ferramentas de desenvolvimento  
  
|Recurso|Enterprise|Standard|Web|Express with Advanced Services|Express| 
|-------------|----------------|--------------|---------|------------------------------------|------------------------| 
|Integração do Microsoft Visual Studio|Sim|Sim|Sim|Sim|Sim| 
|Intellisense (Transact-SQL e MDX)|Sim|Sim|Sim|Sim|Sim| 
|SQL Server Data Tools (SSDT)|Sim|Sim|Sim|Sim|não|    
|Ferramentas de design, depuração e edição do MDX|Sim|Sim|não|não|não|   
  
##  <a name="Programmability"></a> Programmability  
  
|Recurso|Enterprise|Standard|Web|Express with Advanced Services|Express 
|-------------|----------------|--------------|---------|------------------------------------|------------------------|  
|Integração básica do R <sup>1</sup>|Sim|Sim|Sim|Sim|não|   
|Integração avançada do R <sup>2</sup>|Sim|não|não|não|não| 
|Integração Básica do Python|Sim|Sim|Sim|Sim|não|
|Integração Avançada do Python|Sim|não|não|não|não| 
|Servidor do Machine Learning (Autônomo)|Sim|não|não|não|não|   
|Nó de computação do PolyBase|Sim|Sim <sup>3</sup>|Sim <sup>3</sup>|Sim <sup>3</sup>|Sim <sup>3</sup> | 
|Nó de cabeçalho do PolyBase|Sim|não|não|não|não| 
|JSON|Sim|Sim|Sim|Sim|Sim|   
|Repositório de Consultas|Sim|Sim|Sim|Sim|Sim|   
|Temporal|Sim|Sim|Sim|Sim|Sim|   
|Integração do CLR (Common Language Runtime)|Sim|Sim|Sim|Sim|Sim|   
|Suporte a XML nativo|Sim|Sim|Sim|Sim|Sim| 
|Indexação XML|Sim|Sim|Sim|Sim|Sim| 
|Funcionalidades MERGE e UPSERT|Sim|Sim|Sim|Sim|Sim|   
|suporte a FILESTREAM|Sim|Sim|Sim|Sim|Sim| 
|FileTable|Sim|Sim|Sim|Sim|Sim| 
|Tipos de dados de Data e Hora|Sim|Sim|Sim|Sim|Sim|  
|Suporte à internacionalização|Sim|Sim|Sim|Sim|Sim| 
|Pesquisa semântica e de texto completo|Sim|Sim|Sim|Sim|não| 
|Especificação de idioma em consulta|Sim|Sim|Sim|Sim|não|   
|Service Broker (mensagens)|Sim|Sim|Não (Somente cliente)|Não (Somente cliente)|Não (Somente cliente)|   
|pontos de extremidade Transact-SQL|Sim|Sim|Sim|não|não| 
|Gráfico|Sim|Sim|Sim|Sim|Sim|  


<sup>1</sup> A integração básica é limitada a dois núcleos e conjuntos de dados na memória. 

<sup>2</sup> A integração avançada pode utilizar todos os núcleos disponíveis para processamento paralelo de conjuntos de dados em qualquer tamanho sujeito aos limites de hardware. 

<sup>3</sup> A expansão com vários nós de computação requer um nó de cabeçalho.


## <a name="IS"></a> Integration Services

Para obter informações sobre os recursos do SSIS (SQL Server Integration Services) compatíveis com as edições do [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)], consulte [Recursos do Integration Services compatíveis com as edições do SQL Server](../integration-services/integration-services-features-supported-by-the-editions-of-sql-server.md).

##  <a name="MDS"></a> Master Data Services  
 Para obter mais informações sobre o [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] e os recursos do Data Quality Services compatíveis com as edições do [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)], consulte [Recursos do Master Data Services e do Data Quality Services compatíveis com as edições do SQL Server](../master-data-services/master-data-services-and-data-quality-services-features-support.md). 

  
##  <a name="DW"></a> Data warehouse  
  
|Recurso|Enterprise|Standard|Web|Express with Advanced Services|Express|   
|-------------|----------------|--------------|---------|------------------------------------|------------------------| 
|Criar cubos sem um banco de dados|Sim|Sim|não|não|não |   
|Gerar automaticamente esquema e data warehouse de preparo|Sim|Sim|não|não|não| 
|captura de dados de alterações|Sim|Sim|não|não|não| 
|Otimizações de consulta de junção em estrela|Sim|não|não|não|não| 
|Configuração escalonável somente leitura do Analysis Services|Sim|não|não|não|não| 
|Processamento paralelo de consultas em tabelas e índices particionados|Sim|não|não|não|não|   
|Agregação em lote global|Sim|não|não|não|não| 

##  <a name="SSAS"></a> Analysis Services  
  
Para obter informações sobre os recursos do Analysis Services compatíveis com as edições do [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)], consulte [Recursos do Analysis Services compatíveis com as edições do SQL Server](../analysis-services/analysis-services-features-supported-by-the-editions-of-sql-server-2016.md). 
  
##  <a name="BIMD"></a> Modelo semântico de BI (Multidimensional)  
  
Para obter informações sobre os recursos do Analysis Services compatíveis com as edições do [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)], consulte [Recursos do Analysis Services compatíveis com as edições do SQL Server](../analysis-services/analysis-services-features-supported-by-the-editions-of-sql-server-2016.md).
   
##  <a name="BIT"></a> Modelo semântico de BI (Tabular)  
  
Para obter informações sobre os recursos do Analysis Services compatíveis com as edições do [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)], consulte [Recursos do Analysis Services compatíveis com as edições do SQL Server](../analysis-services/analysis-services-features-supported-by-the-editions-of-sql-server-2016.md).
  
##  <a name="PPSP"></a> Power Pivot for SharePoint  
  
Para obter mais informações sobre os recursos do Power Pivot para SharePoint compatíveis com as edições do [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)], consulte [Recursos do Analysis Services compatíveis com as edições do SQL Server](../analysis-services/analysis-services-features-supported-by-the-editions-of-sql-server-2016.md).
  
##  <a name="DM"></a> Mineração de dados  
  
Para obter mais informações sobre os recursos de Mineração de dados compatíveis com as edições do [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)], consulte [Recursos do Analysis Services compatíveis com as edições do SQL Server](../analysis-services/analysis-services-features-supported-by-the-editions-of-sql-server-2016.md).
  
##  <a name="SSRS"></a> Reporting Services  
  
Para obter mais informações sobre os recursos do Reporting Services compatíveis com as edições do [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)], consulte [Recursos do Reporting Services compatíveis com as edições do SQL Server](../reporting-services/reporting-services-features-supported-by-the-editions-of-sql-server-2016.md).

##  <a name="BIC"></a> Clientes de business intelligence  

Para obter informações sobre os recursos do Business Intelligence Client compatíveis com as edições do [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)], consulte [Recursos do Analysis Services compatíveis com as edições do SQL Server](../analysis-services/analysis-services-features-supported-by-the-editions-of-sql-server-2016.md) ou [Recursos do Reporting Services compatíveis com as edições do SQL Server](../reporting-services/reporting-services-features-supported-by-the-editions-of-sql-server-2016.md).
  
##  <a name="SLS"></a> Serviços espaciais e de localização  
  
|Nome do recurso|Enterprise|Standard|Web|Express with Advanced Services|Express|  
|------------------|----------------|--------------|---------|------------------------------------|------------------------|
|Índices espaciais|Sim|Sim|Sim|Sim|Sim|   
|Tipos de dados planares e geodésicos|Sim|Sim|Sim|Sim|Sim| 
|Bibliotecas espaciais avançadas|Sim|Sim|Sim|Sim|Sim|   
|Importação/exportação de formatos de dados espaciais padrão da indústria|Sim|Sim|Sim|Sim|Sim|   
  
##  <a name="ADS"></a> Database Services adicionais  
  
|Nome do recurso|Enterprise|Standard|Web|Express with Advanced Services|Express|   
|------------------|----------------|--------------|---------|------------------------------------|------------------------| 
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Assistente de Migração|Sim|Sim|Sim|Sim|Sim|   
|Database Mail|Sim|Sim|Sim|não|não| 
  
##  <a name="Other"></a> Outros componentes  
  
|Nome do recurso|Enterprise|Standard|Web|Express with Advanced Services|Express|   
|------------------|----------------|--------------|---------|------------------------------------|------------------------|  
|StreamInsight|StreamInsight Premium Edition|StreamInsight Standard Edition|StreamInsight Standard Edition|não|não| 
|StreamInsight HA|StreamInsight Premium Edition|não|não|não|não|   

> [![Download SSMS](../analysis-services/media/download.png)](../ssms/download-sql-server-management-studio-ssms.md) **[Download the latest version of SQL Server Management Studio](../ssms/download-sql-server-management-studio-ssms.md)**     
  
## <a name="next-steps"></a>Próximas etapas 
 [Especificações de produto para o SQL Server](https://msdn.microsoft.com/library/6445fd53-6844-4170-a86b-7fe76a9f64cb)   
 [Instalação do SQL Server](../database-engine/install-windows/installation-for-sql-server-2016.md)  
 
[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]

[!INCLUDE[contribute-to-content](../includes/paragraph-content/contribute-to-content.md)]
