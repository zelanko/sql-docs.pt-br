---
title: Recursos com suporte nas edições do SQL Server 2014 | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 5da61ff5-12b9-48e6-b3c8-0dacca1751c4
author: mightypen
ms.author: genemi
manager: craigg
ms.openlocfilehash: caae4212e2182ae6afde29b0fed1aaee4f05645a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "70176131"
---
# <a name="features-supported-by-the-editions-of-sql-server-2014"></a>Recursos compatíveis com as edições do SQL Server 2014


  Esse tópico fornece detalhes dos recursos que têm suporte na diferentes edições do [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]. 

 > **Observação:** [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] está disponível em uma edição de avaliação para um período de avaliação de 180 dias. Para obter mais informações, consulte o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [Site de avaliação do software](https://go.microsoft.com/fwlink/?LinkId=190955).  
> 
> **Observação:** Para obter recursos com suporte nas edições de avaliação e [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] desenvolvedor, consulte o conjunto de recursos corporativos.  
  
 Para navegar até a tabela de uma tecnologia do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , clique no respectivo link:  
  
 [Limites de escala entre caixas](#CrossBoxScale)  
  
 [Alta disponibilidade](#High_availability)  
  
 [Desempenho e escalabilidade](#Scalability)  
  
 [Segurança](#Enterprise_security)  
  
 [Replicação](#Replication)  
  
 [Ferramentas de gerenciamento](#Mgmt_Tools)  
  
 [Gerenciamento de RDBMS](#RDBMS_mgmt)  
  
 [Ferramentas de desenvolvimento](#Dev_tools)  
  
 [Programação](#Programmability)  
  
 [Serviços de Integração](#SSIS)  
  
 [Integration Services - Adaptadores avançados](#SSIS_AA)  
  
 [Integration Services - Transformações avançadas](#SSIS_AT)  
  
 [Master Data Services](#MDS)  
  
 [data warehouse](#Data_warehouse)  
  
 [Analysis Services](#SSAS)  
  
 [Modelo semântico de BI (multidimensional)](#BISemModel_multi)  
  
 [Modelo semântico de BI (tabular)](#BISemModel_tabular)  
  
 [PowerPivot para SharePoint](#PowerPivot)  
  
 [Mineração de dados](#DataMining)  
  
 [Reporting Services](#Reporting)  
  
 [Clientes de Business Intelligence](#BIClients)  
  
 [Serviços espaciais e de localização](#Spatial)  
  
 [Serviços de banco de dados adicionais](#Add_DBServices)  
  
 [Outros componentes](#Other_Components)  
  
##  <a name="CrossBoxScale"></a>Limites de escala entre caixas  
  
|Nome do recurso|Enterprise|Business Intelligence|Standard|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|Capacidade máxima de computação usada por uma única instância[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] (mecanismo de banco de dados)<sup>1</sup>|Máximo do sistema operacional|Limitado a menos de 4 soquetes ou 16 núcleos|Limitado a menos de 4 soquetes ou 16 núcleos|Limitado a menos de 4 soquetes ou 16 núcleos|Limitado a menos de 1 soquete ou 4 núcleos|Limitado a menos de 1 soquete ou 4 núcleos|Limitado a menos de 1 soquete ou 4 núcleos|  
|Capacidade máxima de computação usada por uma única instância (Analysis Services, Reporting Services) <sup>1</sup>|Máximo do sistema operacional|Máximo do sistema operacional|Limitado a menos de 4 soquetes ou 16 núcleos|Limitado a menos de 4 soquetes ou 16 núcleos|Limitado a menos de 1 soquete ou 4 núcleos|Limitado a menos de 1 soquete ou 4 núcleos|Limitado a menos de 1 soquete ou 4 núcleos|  
|Memória máxima utilizada (por instância do Mecanismo de Banco de Dados do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] )|Máximo do sistema operacional|128 GB|128 GB|64 GB|1 GB|1 GB|1 GB|  
|Memória máxima utilizada (por instância do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)])|Máximo do sistema operacional|Máximo do sistema operacional|64 GB|N/D|N/D|N/D|N/D|  
|Memória máxima utilizada (por instância do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)])|Máximo do sistema operacional|Máximo do sistema operacional|64 GB|64 GB|4 GB|N/D|N/D|  
|Tamanho máximo do banco de dados relacional|524 PB|524 PB|524 PB|524 PB|10 GB|10 GB|10 GB|  
  
 <sup>1</sup> Enterprise Edition com servidor + licenciamento baseado em Cal (licença de acesso para cliente) (não disponível para novos contratos) é limitado a um máximo de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 20 núcleos por instância. Não há limites no modelo de Licenciamento de Servidor Baseado em Núcleo. Para obter mais informações, consulte [computação Capacity Limits by Edition of SQL Server](../sql-server/compute-capacity-limits-by-edition-of-sql-server.md).  
  
##  <a name="High_availability"></a>Alta disponibilidade  
  
|Nome do recurso|Enterprise|Business Intelligence|Standard|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|Suporte do Server Core<sup>1</sup>|Sim|Sim|Sim|Sim|Sim|Sim|Sim|  
|Envio de logs|Sim|Sim|Sim|Sim||||  
|Espelhamento de banco de dados|Sim|Sim (somente segurança completa)|Sim (somente segurança completa)|Somente testemunha|Somente testemunha|Somente testemunha|Somente testemunha|  
|Compactação de backup|Sim|Sim|Sim|||||  
|Instantâneo do banco de dados|Sim|||||||  
|Instâncias de cluster de failover AlwaysOn|Sim (suporte de nó: máximo do sistema operacional|Sim (suporte de nó: 2)|Sim (suporte de nó: 2)|||||  
|Grupos de disponibilidade AlwaysOn|Sim (até oito réplicas secundárias, incluindo duas réplicas secundárias síncronas)|||||||  
|Diretor de Conexão|Sim|||||||  
|Restauração de arquivo e página online|Sim|||||||  
|Indexação online|Sim|||||||  
|Alteração de esquema online|Sim|||||||  
|Recuperação rápida|Sim|||||||  
|Backups espelhados|Sim|||||||  
|Adição de memória a quente e CPU<sup>2</sup>|Sim|||||||  
|Orientador de recuperação de banco de dados|Sim|Sim|Sim|Sim|Sim|Sim|Sim|  
|Backup criptografado|Sim|Sim|Sim|||||  
|Backup inteligente|Sim|Sim|Sim|Não||||  
  
 <sup>1</sup> Para obter mais informações sobre [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] como instalar o no Server Core, consulte [instalar o SQL Server 2014 no Server Core](../database-engine/install-windows/install-sql-server-on-server-core.md).  
  
 <sup>2</sup> Este recurso está disponível somente para 64 bits [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
##  <a name="Scalability"></a>Escalabilidade e desempenho  
  
|Nome do recurso|Enterprise|Business Intelligence|Standard|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|Suporte de várias instâncias|50|50|50|50|50|50|50|  
|Particionamento de tabela e índice|Sim|||||||  
|Compactação de dados|Sim|||||||  
|Administrador de Recursos|Sim|||||||  
|Paralelismo de tabela de partição|Sim|||||||  
|Contêineres de vários fluxos de arquivos|Sim|||||||  
|Memória de página grande com reconhecimento para NUMA e alocação de matriz de buffer|Sim|||||||  
|Extensão do pool de buffers <sup>1</sup>|Sim|Sim|Sim|||||  
|Administração do recurso de E/S|Sim|||||||  
|OLTP na memória <sup>1</sup>|Sim|||||||  
|Durabilidade atrasada|Sim|Sim|Sim|Sim|Sim|Sim|Sim|  
  
 <sup>1</sup> este recurso está disponível somente para 64 bits [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
##  <a name="Enterprise_security"></a> Segurança  
  
|Nome do recurso|Enterprise|Business Intelligence|Standard|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|Auditoria Básica|Sim|Sim|Sim|Sim|Sim|Sim|Sim|  
|Auditoria refinada|Sim|||||||  
|Criptografia transparente do banco de dados|Sim|||||||  
|Gerenciamento Extensível de Chaves|Sim|||||||  
|Funções definidas pelo usuário|Sim|Sim|Sim|Sim|Sim|Sim|Sim|  
|Bancos de dados independentes|Sim|Sim|Sim|Sim|Sim|Sim|Sim|  
|Criptografia para backups|Sim|Sim|Sim|||||  
  
##  <a name="Replication"></a> Replicação  
  
|Nome do recurso|Enterprise|Business Intelligence|Standard|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]controle de alterações|Sim|Sim|Sim|Sim|Sim|Sim|Sim|  
|Replicação de mesclagem|Sim|Sim|Sim|Sim (somente assinante)|Sim (somente assinante)|Sim (somente assinante)|Sim (somente assinante)|  
|Replicação transacional|Sim|Sim|Sim|Sim (somente assinante)|Sim (somente assinante)|Sim (somente assinante)|Sim (somente assinante)|  
|Replicação de instantâneo|Sim|Sim|Sim|Sim (somente assinante)|Sim (somente assinante)|Sim (somente assinante)|Sim (somente assinante)|  
|Assinantes heterogêneos|Sim|Sim|Sim|||||  
|publicação Oracle|Sim|||||||  
|Replicação transacional ponto a ponto|Sim|||||||  
  
##  <a name="Mgmt_Tools"></a>Ferramentas de gerenciamento  
  
|Nome do recurso|Enterprise|Business Intelligence|Standard|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|SQL Management Objects (SMO)|Sim|Sim|Sim|Sim|Sim|Sim|Sim|  
|SQL Configuration Manager|Sim|Sim|Sim|Sim|Sim|Sim|Sim|  
|SQL CMD (ferramenta de prompt de comando)|Sim|Sim|Sim|Sim|Sim|Sim|Sim|  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]Management Studio|Sim|Sim|Sim|Sim|Sim|Sim||  
|Distributed Replay – Ferramenta de Administração|Sim|Sim|Sim|Sim|Sim|Sim||  
|Distributed Replay - Client|Sim|Não|Sim|Sim||||  
|Distributed Replay - Controller|Sim (Enterprise dá suporte a até 16 clientes, o Developer dá suporte a apenas 1 cliente)|Não|Sim (suporte a apenas 1 cliente)|Sim (suporte a apenas 1 cliente)||||  
|SQL Profiler|Sim|Sim|Sim|Não<sup>2</sup>|Não<sup>2</sup>|Não<sup>2</sup>|Não<sup>2</sup>|  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Agent|Sim|Sim|Sim|Sim||||  
|Pacote de gerenciamento do Microsoft System Center Operations Manager|Sim|Sim|Sim|Sim||||  
|Database Tuning Advisor (DTA)|Sim|Sim|Sim<sup>3</sup>|Sim<sup>3</sup>||||  
|Assistente para [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] implantar um banco de dados em uma VM do Azure|Sim|Sim|Sim|Sim|Sim|Sim|Sim|  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]Arquivos de dados no Azure|Sim|Sim|Sim|Sim|Sim|Sim|Sim|  
  
 <sup>2</sup> [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] a Web [!INCLUDE[ssExpress](../includes/ssexpress-md.md)], [!INCLUDE[ssExpress](../includes/ssexpress-md.md)] , com ferramentas, [!INCLUDE[ssExpress](../includes/ssexpress-md.md)] e com serviços avançados podem ser Profiles [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] usando as [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] edições Standard e Enterprise.  
  
 <sup>3</sup> o ajuste está habilitado apenas nos recursos da edição Standard.  
  
##  <a name="RDBMS_mgmt"></a>Gerenciamento de RDBMS  
  
|Nome do recurso|Enterprise|Business Intelligence|Standard|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|Instâncias de usuário|||||Sim|Sim|Sim|  
|LocalDB|||||Sim|Sim||  
|Conexão dedicada de administrador|Sim|Sim|Sim|Sim|Sim (sob sinalizador de rastreamento)|Sim (sob sinalizador de rastreamento)|Sim (sob sinalizador de rastreamento)|  
|Suporte de scripts PowerShell|Sim|Sim|Sim|Sim|Sim|Sim|Sim|  
|Suporte a SysPrep<sup>1</sup>|Sim|Sim|Sim|Sim|Sim|Sim|Sim|  
|Suporte para operações de componente de aplicativo da camada de dados – extrair, implantar, atualizar, excluir|Sim|Sim|Sim|Sim|Sim|Sim|Sim|  
|Automação de política (verificação de agenda e alterações)|Sim|Sim|Sim|Sim||||  
|Coletor de dados de desempenho|Sim|Sim|Sim|Sim||||  
|Capaz de se inscrever como uma instância gerenciada em um gerenciamento com várias instâncias|Sim|Sim|Sim|Sim||||  
|Relatórios de desempenho padrão|Sim|Sim|Sim|Sim||||  
|Guias de plano e planejar congelamento para guias de plano|Sim|Sim|Sim|Sim||||  
|Direcione a consulta de exibições indexadas (usando a dica de NOEXPAND)|Sim|Sim|Sim|Sim||||  
|Manutenção de exibição indexada automática|Sim|Sim|Sim|Sim||||  
|Exibições particionadas distribuídas|Sim|Parcial. As exibições particionadas distribuídas não são atualizáveis|Parcial. As exibições particionadas distribuídas não são atualizáveis|Parcial. As exibições particionadas distribuídas não são atualizáveis|Parcial. As exibições particionadas distribuídas não são atualizáveis|Parcial. As exibições particionadas distribuídas não são atualizáveis|Parcial. As exibições particionadas distribuídas não são atualizáveis|  
|Operações indexadas paralelas|Sim|||||||  
|Uso automático da exibição indexada através do otimizador de consulta|Sim|||||||  
|Verificação de consistência paralela|Sim|||||||  
|Ponto de controle do Utilitário do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]|Sim|||||||  
|Bancos de dados independentes|Sim|Sim|Sim|Sim|Sim|Sim|Sim|  
|Extensão do pool de buffers<sup>2</sup>|Sim|Sim|Sim|||||  
  
 <sup>1</sup> para obter mais informações, consulte [considerações para instalar SQL Server usando o Sysprep](../database-engine/install-windows/considerations-for-installing-sql-server-using-sysprep.md).  
  
 <sup>2</sup> esse recurso está disponível somente para 64 bits [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
##  <a name="Dev_tools"></a>Ferramentas de desenvolvimento  
  
|Nome do recurso|Enterprise|Business Intelligence|Standard|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|[!INCLUDE[msCoName](../includes/msconame-md.md)]Integração do Visual Studio|Sim|Sim|Sim|Sim|Sim|Sim|Sim|  
|Intellisense ([!INCLUDE[tsql](../includes/tsql-md.md)] e MDX)|Sim|Sim|Sim|Sim|Sim|Sim|Sim|  
|[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]|Sim|Sim|Sim|Sim|Sim|||  
|Ferramentas de design e edição de consulta SQL<sup>1</sup>|Sim|Sim|Sim|||||  
|Suporte ao controle de versão<sup>1</sup>|Sim|Sim|Sim|||||  
|Ferramentas de edição, depuração e design MDX<sup>1</sup>|Sim|Sim|Sim|||||  
  
 <sup>1</sup> este recurso não está disponível para a versão de 64 bits da Standard Edition.  
  
##  <a name="Programmability"></a> Programmability  
  
|Nome do recurso|Enterprise|Business Intelligence|Standard|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|Integração do CLR (Common Language Runtime)|Sim|Sim|Sim|Sim|Sim|Sim|Sim|  
|Suporte a XML nativo|Sim|Sim|Sim|Sim|Sim|Sim|Sim|  
|Indexação XML|Sim|Sim|Sim|Sim|Sim|Sim|Sim|  
|MESCLAr & recursos de UPSERT|Sim|Sim|Sim|Sim|Sim|Sim|Sim|  
|suporte a FILESTREAM|Sim|Sim|Sim|Sim|Sim|Sim|Sim|  
|FileTable|Sim|Sim|Sim|Sim|Sim|Sim|Sim|  
|Tipos de dados de Data e Hora|Sim|Sim|Sim|Sim|Sim|Sim|Sim|  
|Suporte à internacionalização|Sim|Sim|Sim|Sim|Sim|Sim|Sim|  
|Pesquisa semântica e de texto completo|Sim|Sim|Sim|Sim|Sim|||  
|Especificação de idioma em consulta|Sim|Sim|Sim|Sim|Sim|||  
|Service Broker (mensagens)|Sim|Sim|Sim|Não (Somente cliente)|Não (Somente cliente)|Não (Somente cliente)|Não (Somente cliente)|  
|[!INCLUDE[tsql](../includes/tsql-md.md)]extremidade|Sim|Sim|Sim|Sim||||  
  
##  <a name="SSIS"></a> Integration Services  
  
|Recurso|Enterprise|Business Intelligence|Standard|Web|Express with Advanced Services|Express with Tools|Express|  
|-------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|Assistente de Importação e Exportação do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]|Sim|Sim|Sim|Sim|Sim|Sim|Sim|  
|Conectores internos de fonte de dados|Sim|Sim|Sim|Sim|Sim|Sim|Sim|  
|Designer de SSIS e runtime|Sim|Sim|Sim|||||  
|Transformações básicas|Sim|Sim|Sim|||||  
|Ferramentas de criação de perfil de dados básicos|Sim|Sim|Sim|||||  
|Serviço Change Data Capture para Oracle da Attunity|Sim|||||||  
|Change Data Capture Designer para Oracle da Attunity|Sim|||||||  
  
###  <a name="SSIS_AA"></a>Adaptadores Integration Services-avançado  
  
|Nome do recurso|Enterprise|Business Intelligence|Standard|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|Destino Oracle de alto desempenho|Sim|||||||  
|Destino Teradata de alto desempenho|Sim|||||||  
|Origem e destino do SAP BW|Sim|||||||  
|Adaptador de destino de treinamento do modelo de mineração de dados|Sim|||||||  
|Adaptador de destino de processamento de dimensões|Sim|||||||  
|Adaptador de destino de processamento de partições|Sim|||||||  
|Componentes do Change Data Capture da Attunity|Sim|||||||  
|Conector para ODBC (Conectividade Aberta de Banco de Dados) da Attunity.|Sim|||||||  
  
###  <a name="SSIS_AT"></a>Transformações Integration Services avançadas  
  
|Nome do recurso|Enterprise|Business Intelligence|Standard|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|Pesquisas persistentes (alto desempenho)|Sim|||||||  
|Transformação de consulta de mineração de dados|Sim|||||||  
|Transformações de pesquisa e agrupamento difuso|Sim|||||||  
|Transformações de extração e pesquisa de termos|Sim|||||||  
  
##  <a name="MDS"></a>Master Data Services  
  
> [!NOTE]  
>  -   O [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] está disponível apenas nas edições de 64 bits somente do Business Intelligence e do Enterprise.  
  
|Recurso|Enterprise|Business Intelligence|Standard|Web|Express with Advanced Services|Express with Tools|Express|  
|-------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|[!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]banco|Sim|Sim||||||  
|[!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]aplicativo Web|Sim|Sim||||||  
  
##  <a name="Data_warehouse"></a>data warehouse  
  
|Nome do recurso|Enterprise|Business Intelligence|Standard|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|Criar cubos sem um banco de dados|Sim|Sim|Sim|||||  
|Gerar automaticamente esquema e data warehouse de preparo|Sim|Sim|Sim|||||  
|captura de dados de alterações|Sim|||||||  
|Otimizações de consulta de junção em estrela|Sim|||||||  
|Configuração escalonável somente leitura do Analysis Services|Sim|||||||  
|Processamento paralelo de consultas em tabelas e índices particionados|Sim|||||||  
|Índices columnstore xVelocity com otimização de memória|Sim|||||||  
|Agregação global do lote|Sim|||||||  
  
##  <a name="SSAS"></a>Analysis Services  
  
|Nome do recurso|Enterprise|Business Intelligence|Standard|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|Bancos de dados compartilhados escalonáveis (Anexar/desanexar, bancos de dados somente leitura)|Sim|Sim||||||  
|Backup/restauração, Anexar/desanexar bancos de dados|Sim|Sim|Sim|||||  
|Sincronizar bancos de dados|Sim|Sim||||||  
|Alta disponibilidade|Sim|Sim|Sim|||||  
|Programabilidade (AMO, ADOMD.Net, OLEDB, XML/A, ASSL)|Sim|Sim|Sim|||||  
  
###  <a name="BISemModel_multi"></a>Modelo semântico de BI (Multidimensional)  
  
|Nome do recurso|Enterprise|Business Intelligence|Standard|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|Medidas semiaditivas|Sim|Sim|Não<sup>1</sup>|||||  
|Hierarquias|Sim|Sim|Sim|||||  
|KPIs|Sim|Sim|Sim|||||  
|perspectivas|Sim|Sim||||||  
|Ações|Sim|Sim|Sim|||||  
|Inteligência de conta|Sim|Sim|Sim|||||  
|Inteligência de dados temporais|Sim|Sim|Sim|||||  
|Rollups personalizados|Sim|Sim|Sim|||||  
|Cubo de write-backs|Sim|Sim|Sim|||||  
|Dimensões de write-back|Sim|Sim||||||  
|Células de Writeback|Sim|Sim|Sim|||||  
|Detalhamento|Sim|Sim|Sim|||||  
|Tipos de hierarquia Avançados (Pai-filho, Hierarquias desbalanceadas)|Sim|Sim|Sim|||||  
|Dimensões avançadas (Dimensões de referência, dimensões muitos para muitos|Sim|Sim|Sim|||||  
|Medidas e dimensões vinculadas|Sim|Sim||||||  
|Translations|Sim|Sim|Sim|||||  
|Agregações|Sim|Sim|Sim|||||  
|Várias partições|Sim|Sim|Sim, até 3|||||  
|Cache pró-ativo|Sim|Sim||||||  
|Assemblies personalizados (procedimentos armazenados)|Sim|Sim|Sim|||||  
|Consultas MDX e scripts|Sim|Sim|Sim|||||  
|Consultas DAX|Sim|Sim||||||  
|Modelo de segurança com base em função|Sim|Sim|Sim|||||  
|Segurança no nível da dimensão e da célula|Sim|Sim|Sim|||||  
|Armazenamento de cadeias de caracteres escalonável|Sim|Sim|Sim|||||  
|Modos de armazenamento MOLAP, ROLAP, HOLAP|Sim|Sim|Sim|||||  
|Transporte de XML binário e compactado|Sim|Sim|Sim|||||  
|Processamento de modo push|Sim|Sim||||||  
|Writeback direto|Sim|Sim||||||  
|Expressões de medida|Sim|Sim||||||  
  
 <sup>1</sup> A medida semiaditiva LastChild tem suporte na edição Standard, mas outras medidas semiaditivas, como None, FirstChild, FirstNonEmpty, LastNonEmpty, AverageOfChildren e ByAccount, não são. Medidas aditivas, como Sum, Count, Min, Max e medidas não aditivas (DistinctCount) têm suporte em todas as edições.  
  
###  <a name="BISemModel_tabular"></a>Modelo semântico de BI (tabular)  
  
|Nome do recurso|Enterprise|Business Intelligence|Standard|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|Hierarquias|Sim|Sim||||||  
|KPIs|Sim|Sim||||||  
|perspectivas|Sim|Sim||||||  
|Translations|Sim|Sim||||||  
|Cálculos DAX, consultas DAX, consultas MDX|Sim|Sim||||||  
|Segurança em nível de linha|Sim|Sim||||||  
|Partições|Sim|Sim||||||  
|Modos de armazenamento Na Memória e DirectQuery (somente Tabelar)|Sim|Sim||||||  
  
###  <a name="PowerPivot"></a>PowerPivot para SharePoint  
  
|Nome do recurso|Enterprise|Business Intelligence|Standard|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|Integração de farm do SharePoint baseado em arquitetura de serviço compartilhado|Sim|Sim||||||  
|Relatório de uso|Sim|Sim||||||  
|Regras de monitoramento de integridade|Sim|Sim||||||  
|Galeria PowerPivot|Sim|Sim||||||  
|Atualização de dados PowerPivot|Sim|Sim||||||  
|Feeds de dados PowerPivot|Sim|Sim||||||  
  
###  <a name="DataMining"></a>Mineração de dados  
  
|Nome do recurso|Enterprise|Business Intelligence|Standard|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|Algoritmos padrão|Sim|Sim|Sim|||||  
|Ferramentas de mineração de dados (assistentes, editores, construtores de consulta)|Sim|Sim|Sim|||||  
|Validação cruzada|Sim|Sim||||||  
|Modelos em subconjuntos filtrados de dados da estrutura de mineração|Sim|Sim||||||  
|Série temporal: combinação personalizada entre métodos ARTXP e ARIMA|Sim|Sim||||||  
|Série temporal: previsão com novos dados|Sim|Sim||||||  
|Consultas de mineração de dados simultâneas ilimitadas|Sim|Sim||||||  
|Configuração avançada & opções de ajuste para algoritmos de mineração de dados|Sim|Sim||||||  
|Suporte para algoritmos de plug-in|Sim|Sim||||||  
|Processamento paralelo de modelo|Sim|Sim||||||  
|Série temporal: previsão de séries cruzadas|Sim|Sim||||||  
|Atributos ilimitados para regras de associação|Sim|Sim||||||  
|Previsão de sequências|Sim|Sim||||||  
|Destinos de várias previsões para Naïve Bayes, rede neural e regressão logística|Sim|Sim||||||  
  
##  <a name="Reporting"></a>Reporting Services  
  
###  <a name="Reporting_features"></a>Recursos de Reporting Services  
  
|Nome do recurso|Enterprise|Business Intelligence|Standard|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|Banco de dados de catálogo com suporte - [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] edition|Standard ou superior|Standard ou superior|Standard ou superior|Web|Express|||  
|Fonte de dados com suporte - [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] edition|Todas as edições do   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]|Todas as edições do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]|Todas as edições do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]|Web|Express|||  
|Servidor de relatório|Sim|Sim|Sim|Sim|Sim|||  
|Designer de Relatórios|Sim|Sim|Sim|Sim|Sim|||  
|Gerenciador de Relatórios|Sim|Sim|Sim|Sim|Sim|||  
|Segurança baseada em função|Sim|Sim|Sim|Sim|Sim|||  
|Exportação do Word e suporte ao texto sem-formatação|Sim|Sim|Sim|Sim|Sim|||  
|Gráficos e medidores aprimorados|Sim|Sim|Sim|Sim|Sim|||  
|Exportar para Excel, PDF e imagens|Sim|Sim|Sim|Sim|Sim|||  
|Autenticação personalizada|Sim|Sim|Sim|Sim|Sim|||  
|Relatar como feeds de dados|Sim|Sim|Sim|Sim|Sim|||  
|Suporte a modelo|Sim|Sim|Sim|Sim||||  
|Criar funções personalizadas para segurança baseada em função|Sim|Sim|Sim|||||  
|Segurança de item de modelo|Sim|Sim|Sim|||||  
|Clickthrough infinito|Sim|Sim|Sim|||||  
|Biblioteca de componentes compartilhados|Sim|Sim|Sim|||||  
|Agendamento e assinaturas de email e compartilhamento de arquivos|Sim|Sim|Sim|||||  
|Histórico de relatórios, execução de instantâneos e armazenamento em cache|Sim|Sim|Sim|||||  
|Integração do SharePoint|Sim|Sim|Sim|||||  
|Suporte de fonte de dados remota e não SQL<sup>1</sup>|Sim|Sim|Sim|||||  
|Extensibilidade RDCE de fonte de dados, entrega e renderização|Sim|Sim|Sim|||||  
|Assinatura de relatórios controladas por dados|Sim|Sim||||||  
|Implantação em expansão (Web farms)|Sim|Sim||||||  
|Alerta<sup>2</sup>|Sim|Sim||||||  
|[!INCLUDE[ssCrescent](../includes/sscrescent-md.md)]<sup>2</sup>|Sim|Sim||||||  
  
 <sup>1</sup> Para obter mais informações sobre as fontes de dados com [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)]suporte no, consulte [fontes de dado com suporte pelo Reporting Services &#40;SSRS&#41;](../reporting-services/create-deploy-and-manage-mobile-and-paginated-reports.md).  
  
 <sup>2</sup> Requer [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] no modo do SharePoint. Para obter mais informações, consulte [Reporting Services instalação do modo sharepoint &#40;sharepoint 2010 e sharepoint 2013&#41;](../reporting-services/install-windows/install-reporting-services-sharepoint-mode.md).  
  
### <a name="report-server-database-server-edition-requirements"></a>Requisitos das edições do servidor de banco de dados do servidor de relatório  
 Na criação de um banco de dados de servidor de relatório, nem todas as edições do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] podem ser usadas para hospedar o banco de dados. A tabela a seguir mostra quais edições do [!INCLUDE[ssDE](../includes/ssde-md.md)] podem ser usadas para edições específicas do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)].  
  
|Para esta edição do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Reporting Services|Use esta edição da instância do Mecanismo de Banco de Dados para hospedar o banco de dados|  
|----------------------------------------------------------------------|---------------------------------------------------------------------------|  
|Enterprise|Edições Standard, Business Intelligence, Enterprise (locais ou remotas)|  
|Business Intelligence|Edições Standard, Business Intelligence, Enterprise (locais ou remotas)|  
|Standard|Edições Standard, Enterprise (local ou remotamente)|  
|Web|Web Edition (apenas localmente)|  
|Express with Advanced Services|Express with Advanced Services (apenas local).|  
|Avaliação|Avaliação|  
  
##  <a name="BIClients"></a>Clientes de Business Intelligence  
 Os seguintes aplicativos cliente de software estão disponíveis na Central de Downloads da Microsoft e são fornecidos para ajudar a criar documentos de Business Intelligence que são executados em uma instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . Quando esses documentos forem hospedados em um ambiente de servidor, use uma edição do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] que tenha suporte para esse tipo de documento. A tabela a seguir identifica qual edição do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] contém os recursos de servidor necessários para hospedar os documentos criados nesses aplicativos cliente.  
  
|Nome do recurso|Enterprise|Business Intelligence|Standard|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|[!INCLUDE[ssRBnoversion](../includes/ssrbnoversion.md)]|Sim|Sim|Sim|||||  
|Suplementos de mineração de dados para Excel e Visio 2010|Sim|Sim|Sim|||||  
|[!INCLUDE[ssGeminiClient](../includes/ssgeminiclient-md.md)]2010|Sim|Sim||||||  
|[!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] [!INCLUDE[ssMDSXLS](../includes/ssmdsxls-md.md)]|Sim|Sim||||||  
  
> [!NOTE]
>  1.  [!INCLUDE[ssGeminiClient](../includes/ssgeminiclient-md.md)]é um suplemento do Excel e não depende do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. No entanto, o [!INCLUDE[ssGeminiShort](../includes/ssgeminishort-md.md)] é necessário para compartilhar e colaborar com pastas de trabalho do [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] no SharePoint e este recurso está disponível como parte das edições [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Enterprise e Business Intelligence.  
> 2.  A tabela acima identifica as edições do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] necessárias para habilitar essas ferramentas cliente; no entanto, esses recursos podem acessar os dados hospedados em qualquer edição do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
##  <a name="Spatial"></a>Serviços espaciais e de localização  
  
|Nome do recurso|Enterprise|Business Intelligence|Standard|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|Índices espaciais|Sim|Sim|Sim|Sim|Sim|Sim|Sim|  
|Tipos de dados planares e geodésicos|Sim|Sim|Sim|Sim|Sim|Sim|Sim|  
|Bibliotecas espaciais avançadas|Sim|Sim|Sim|Sim|Sim|Sim|Sim|  
|Importação/exportação de formatos de dados espaciais padrão da indústria|Sim|Sim|Sim|Sim|Sim|Sim|Sim|  
  
##  <a name="Add_DBServices"></a>Serviços de banco de dados adicionais  
  
|Nome do recurso|Enterprise|Business Intelligence|Standard|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|
  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Assistente de Migração|Sim|Sim|Sim|Sim|Sim|Sim|Sim|  
|Database Mail|Sim|Sim|Sim|Sim||||  
  
##  <a name="Other_Components"></a>Outros componentes  
  
|Nome do recurso|Enterprise|Business Intelligence|Standard|Web|Express with Advanced Services|Express with Tools|Express|  
|------------------|----------------|---------------------------|--------------|---------|------------------------------------|------------------------|-------------|  
|Data Quality Services|Sim|Sim||||||  
|StreamInsight|StreamInsight Premium Edition|StreamInsight Standard Edition|StreamInsight Standard Edition|StreamInsight Standard Edition||||  
|StreamInsight HA|StreamInsight Premium Edition|||||||  
  
## <a name="see-also"></a>Consulte Também  
 [Especificações do produto para o SQL Server 2014](../../2014/getting-started/sql-server-2014-product-specifications.md)   
 [Instalação do SQL Server 2014](../database-engine/install-windows/installation-for-sql-server.md)   
 [Instalação de início rápido do SQL Server 2014](../../2014/getting-started/quick-start-installation-of-sql-server-2014.md)  
  
  
