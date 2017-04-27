---
title: "Edições e recursos com suporte para o SQL Server 2016 | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 01/31/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
keywords:
- "edição do SQL"
ms.assetid: 5da61ff5-12b9-48e6-b3c8-0dacca1751c4
caps.latest.revision: 175
author: sabotta
ms.author: carlasab
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: b9b9db3ca911b8fd8eed6304b9d3a8f51e9e9ba2
ms.lasthandoff: 04/11/2017

---
# <a name="editions-and-supported-features-for-sql-server-2016"></a>Edições e recursos com suporte para SQL Server 2016
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Esse tópico fornece detalhes dos recursos que têm suporte na diferentes edições do [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)].  
  
 A edição Evaluation do SQL Server está disponível por um período de avaliação de 180 dias.  
  
 Para notas de versão mais recentes e informações sobre novidades, consulte o seguinte:
- [Notas de versão do SQL Server 2016](../sql-server/sql-server-2016-release-notes.md)
- [Novidades no SQL Server 2016](../sql-server/what-s-new-in-sql-server-2016.md)

    
 **Experimente o SQL Server 2016!**    
    
 > [![Download from Evaluation Center](../analysis-services/media/download.png)](https://www.microsoft.com/en-us/evalcenter/evaluate-sql-server-2016) **[Download SQL Server 2016  from the Evaluation Center](https://www.microsoft.com/en-us/evalcenter/evaluate-sql-server-2016)**    
    
> ![Azure Virtual Machine small](../analysis-services/media/azure-virtual-machine-small.png) **[Spin up a Virtual Machine with SQL Server 2016 already installed](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.SQL2016SP1-WS2016?tab=Overview?wt.mc_id=sqL16_vm)**    
    
**Edições Developer e Evaluation**  
 Para saber quais os recursos com suporte nas edições Developer e Evaluation, consulte os recursos listados para o SQL Server Enterprise Edition nas tabelas abaixo.
Para obter uma lista de recursos que foram adicionados à edição Developer para o [!INCLUDE[ssSQL15](../includes/sssql15-md.md)] SP1, consulte [Edições do SQL Server 2016 SP1](https://aka.ms/uw6cw4).   
  
##  <a name="Cross-BoxScaleLimits"></a> Scale Limits  
  
|Recurso|Enterprise|Standard|Web|Express with Advanced Services|Express| 
|-------------|----------------|--------------|---------|------------------------------------|------------------------|
|Capacidade máxima de computação usada por uma única instância – [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]<sup>1</sup>|Máximo do sistema operacional|Limitado a menos de 4 soquetes ou 24 núcleos|Limitado a menos de 4 soquetes ou 16 núcleos|Limitado a menos de 1 soquete ou 4 núcleos|Limitado a menos de 1 soquete ou 4 núcleos| 
|Capacidade máxima de computação usada por uma única instância – [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] ou [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]|Máximo do sistema operacional|Limitado a menos de 4 soquetes ou 24 núcleos|Limitado a menos de 4 soquetes ou 16 núcleos|Limitado a menos de 1 soquete ou 4 núcleos|Limitado a menos de 1 soquete ou 4 núcleos|  
|Memória máxima para o pool de buffers por instância do [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]|Máximo do sistema operacional|128 GB|64 GB|1410 MB|1410 MB|
|Máximo de memória para cache do segmento Columnstore por instância do [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]|Memória ilimitada| 32 GB<sup>2</sup>| 16 GB<sup>2</sup>| 352 MB<sup>2</sup>| 352 MB<sup>2</sup>|  
|Tamanho de dados máximo otimizado para memória de acordo com banco de dados em [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]|Memória ilimitada| 32 GB<sup>2</sup>| 16 GB<sup>2</sup>| 352 MB<sup>2</sup>| 352 MB<sup>2</sup>|  
|Memória máxima utilizada por instância de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]|Máximo do sistema operacional|Tabela: 16 GB<br /><br /> MOLAP: 64 GB|N/A|N/A|N/A|  
|Memória máxima utilizada por instância de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]|Máximo do sistema operacional|64 GB|64 GB|4 GB|N/A|
|Tamanho máximo do banco de dados relacional|524 PB|524 PB|524 PB|10 GB|10 GB|  
  
<sup>1</sup> O Enterprise Edition com Servidor + licenciamento baseado em CAL (Licença de Acesso para Cliente) (não disponível para novos contratos) é limitado ao máximo de 20 núcleos por instância do SQL Server. Não há limites no modelo de Licenciamento de Servidor Baseado em Núcleo. Para saber mais, confira [Compute Capacity Limits by Edition of SQL Server](../sql-server/compute-capacity-limits-by-edition-of-sql-server.md).  
  
<sup>2</sup> Aplica-se a [!INCLUDE[ssSQL15](../includes/sssql15-md.md)] SP1. 

##  <a name="RDBMSHA"></a> RDBMS High Availability  
  
|Recurso|Enterprise|Standard|Web|Express with Advanced Services|Express|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------|  
|Suporte do Server Core <sup>1</sup>|Sim|Sim|Sim|Sim|Sim|  
|Envio de logs|Sim|Sim|Sim|Não|Não|  
|Espelhamento de banco de dados|Sim|Sim<br /><br /> Somente segurança completa|Somente testemunha|Somente testemunha|Somente testemunha| 
|Compactação de backup|Sim|Sim|Não|Não|Não| 
|Instantâneo do banco de dados|Sim|Sim <sup>3</sup>|Sim <sup>3</sup>|Sim <sup>3</sup>|Sim <sup>3</sup>|
|Instâncias do cluster de failover do AlwaysOn|Sim<br /><br /> O número de nós é o máximo do sistema operacional|Sim<br /><br /> Suporte para 2 nós|Não|Não|Não|  
|Grupos de disponibilidade AlwaysOn|Sim<br /><br /> Até 8 réplicas secundárias, incluindo 2 réplicas secundárias síncronas|Não|Não|Não|Não|
|Grupos de disponibilidade básicos <sup>2</sup>|Não|Sim<br /><br /> Suporte para 2 nós|Não|Não|Não|
|Restauração de arquivo e página online|Sim|Não|Não|Não|Não|
|Indexação online|Sim|Não|Não|Não|Não|
|Alteração de esquema online|Sim|Não|Não|Não|Não|
|Recuperação rápida|Sim|Não|Não|Não|Não|
|Backups espelhados|Sim|Não|Não|Não|Não|
|Adição de memória a quente e CPU|Sim|Não|Não|Não|Não|
|Supervisor de recuperação de banco de dados|Sim|Sim|Sim|Sim|Sim|
|Backup criptografado|Sim|Sim|Não|Não|Não|
|Backup híbrido para o Microsoft Azure (backup para URL)|Sim|Sim|Não|Não|Não|  
  
 <sup>1</sup> Para obter mais informações sobre como instalar o SQL Server 2016 no Server Core, veja [Instalar o SQL Server 2016 no Server Core](../database-engine/install-windows/install-sql-server-on-server-core.md). 

<sup>2</sup> Para obter mais informações sobre Grupos de disponibilidade básicos, consulte [Grupos de disponibilidade básicos](../database-engine/availability-groups/windows/basic-availability-groups-always-on-availability-groups.md).  

<sup>3</sup> Aplica-se a [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] 2016 SP1.
  
##  <a name="RDBMSSP"></a> RDBMS Scalability and Performance  
  
|Recurso|Enterprise|Standard|Web|Express with Advanced Services|Express|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------| 
|Columnstore <sup>1</sup>|Sim|Sim <sup>2</sup>|Sim <sup>2</sup>|Sim<sup>2</sup>|Sim<sup>2</sup>|  
|OLTP na memória <sup>1</sup>|Sim|Sim <sup>2</sup>|Sim <sup>2</sup>|Sim <sup>2</sup>, <sup>3</sup>|Sim <sup>2</sup>|
|Stretch Database|Sim|Sim|Sim|Sim|Sim|
|Memória principal persistente|Sim|Sim|Sim|Sim|Sim|
|Suporte de várias instâncias|50|50|50|50|50|
|Particionamento de tabela e índice|Sim|Sim <sup>2</sup>|Sim <sup>2</sup>|Sim <sup>2</sup>|Sim <sup>2</sup>|  
|Compactação de dados|Sim|Sim <sup>2</sup>|Sim <sup>2</sup>|Sim <sup>2</sup>|Sim <sup>2</sup>|
|Administrador de Recursos|Sim|Não|Não|Não|Não|  
|Paralelismo de tabela particionada|Sim|Não|Não|Não|Não|
|Contêineres de vários fluxos de arquivos|Sim|Sim <sup>2</sup>|Sim <sup>2</sup>|Sim <sup>2</sup>|Sim <sup>2</sup>|
|Memória de página grande com reconhecimento para NUMA e alocação de matriz de buffer|Sim|Não|Não|Não|Não|
|Extensão do pool de buffers|Sim|Sim|Não|Não|Não|
|Administração do recurso de E/S|Sim|Não|Não|Não|Não|  
|Durabilidade atrasada|Sim|Sim|Sim|Sim|Sim|

<sup>1</sup> Tamanho de dados de OLTP na memória e cache do segmento Columnstore são limitados a quantidade de memória especificada por edição na seção limites de escala. Os graus de máximos de paralelismo é limitado. Os graus de paralelismo do processo (DOP) de criação de um índice é limitado a 2 DOP para a Standard Edition e 1 DOP para a Web e a Express Editions. Refere-se a índices de columnstore criados em tabelas baseadas em disco e tabelas com otimização de memória.

<sup>2</sup> Aplica-se a [!INCLUDE[ssSQL15](../includes/sssql15-md.md)] SP1. 

<sup>3</sup> Esse recurso não está incluído na opção de instalação LocalDB.
##  <a name="RDBMSS"></a> RDBMS Security  
  
|Recurso|Enterprise|Standard|Web|Express|Express with Advanced Services|  
|-------------|----------------|--------------|---------|-------------|------------------------------------| 
|Segurança em nível de linha|Sim|Sim|Sim <sup>1</sup>|Sim <sup>1</sup>|Sim <sup>1</sup>|  
|Sempre Criptografado|Sim|Sim <sup>1</sup>|Sim <sup>1</sup>|Sim <sup>1</sup>|Sim <sup>1</sup>| 
|Mascaramento de dados dinâmicos|Sim|Sim|Sim <sup>1</sup>|Sim <sup>1</sup>|Sim <sup>1</sup>|   
|Auditoria básica|Sim|Sim|Sim|Sim|Sim| 
|Auditoria refinada|Sim|Sim <sup>1</sup>|Sim <sup>1</sup>|Sim <sup>1</sup>|Sim <sup>1</sup>| 
|Criptografia transparente do banco de dados|Sim|Não|Não|Não|Não|   
|Gerenciamento extensível de chaves|Sim|Não|Não|Não|Não| 
|Funções definidas pelo usuário|Sim|Sim|Sim|Sim|Sim| 
|Bancos de dados independentes|Sim|Sim|Sim|Sim|Sim| 
|Criptografia para backups|Sim|Sim|Não|Não|Não|  

<sup>1</sup> Aplica-se a [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] 2016 SP1.  
##  <a name="Replication"></a> Replication  
  
|Recurso|Enterprise|Standard|Web|Express with Advanced Services|Express|   
|-------------|----------------|--------------|---------|------------------------------------|------------------------| 
|Assinantes heterogêneos|Sim|Sim|Não|Não|Não|  
|Replicação de mesclagem|Sim|Sim|Sim (somente assinante)|Sim (somente assinante)|Sim (somente assinante)|   
|publicação Oracle|Sim|Não|Não|Não|Não| 
|Replicação transacional ponto a ponto|Sim|Não|Não|Não|Não|   
|Replicação de instantâneo|Sim|Sim|Sim (somente assinante)|Sim (somente assinante)|Sim (somente assinante)|   
|Controle de alterações do SQL Server|Sim|Sim|Sim|Sim|Sim| 
|Replicação transacional|Sim|Sim|Sim (somente assinante)|Sim (somente assinante)|Sim (somente assinante)|   
|Replicação transacional no Azure|Sim|Sim|Não|Não|Não|   
|Assinatura atualizável de replicação transacional|Sim|Não|Não|Não|Não|  
  
##  <a name="SSMS"></a> Management Tools  
  
|Recurso|Enterprise|Standard|Web|Express with Advanced Services|Express| 
|-------------|----------------|--------------|---------|------------------------------------|------------------------|  
|SQL Management Objects (SMO)|Sim|Sim|Sim|Sim|Sim|  
|SQL Configuration Manager|Sim|Sim|Sim|Sim|Sim|   
|SQL CMD (ferramenta de prompt de comando)|Sim|Sim|Sim|Sim|Sim|      
|Distributed Replay – Ferramenta de Administração|Sim|Sim|Sim|Sim|Não|  
|Distributed Replay – Cliente|Sim|Sim|Sim|Não|Não|  
|Distributed Replay - Controller|Sim (Até 16 clientes)|Sim (1 cliente)|Sim (1 cliente)|Não|Não|   
|SQL Profiler|Sim|Sim|Não <sup>1</sup>|Não <sup>1</sup>|Não <sup>1</sup>|  
|SQL Server Agent|Sim|Sim|Sim|Não|Não| 
|Pacote de gerenciamento do Microsoft System Center Operations Manager|Sim|Sim|Sim|Não|Não|  
|Database Tuning Advisor (DTA)|Sim|Sim <sup>2</sup>|Sim <sup>2</sup>|Não|Não|      
  
 <sup>1</sup> SQL Server Web, SQL Server Express, SQL Server Express with Tools e SQL Server Express with Advanced Services podem ter o perfil criado usando as edições SQL Server Enterprise e Standard.  
  
 <sup>2</sup> Ajuste habilitado somente em recursos da edição Standard  
  
##  <a name="RDBMSM"></a> RDBMS Manageability  
  
|Recurso|Enterprise|Standard|Web|Express with Advanced Services|Express|   
|-------------|----------------|--------------|---------|------------------------------------|------------------------|  
|Instâncias de usuário|Não|Não|Não|Sim|Sim| 
|LocalDB|Não|Não|Não|Sim|Não| 
|Conexão dedicada de administrador|Sim|Sim|Sim|Sim, com o sinalizador de rastreamento|Sim, com o sinalizador de rastreamento|   
|Suporte de scripts PowerShell|Sim|Sim|Sim|Sim|Sim| 
|Suporte a SysPrep <sup>1</sup>|Sim|Sim|Sim|Sim|Sim| 
|Suporte para operações de componente do aplicativo da camada de dados – extrair, implantar, atualizar, excluir|Sim|Sim|Sim|Sim|Sim| 
|Automação de política (verificação de agenda e alterações)|Sim|Sim|Sim|Não|Não|   
|Coletor de dados de desempenho|Sim|Sim|Sim|Não|Não| 
|Pode se inscrever como uma instância gerenciada no gerenciamento de várias instâncias|Sim|Sim|Sim|Não|Não|   
|Relatórios de desempenho padrão|Sim|Sim|Sim|Não|Não| 
|Guias de plano e planejar congelamento para guias de plano|Sim|Sim|Sim|Não|Não|   
|Direcione a consulta de exibições indexadas (usando a dica de NOEXPAND)|Sim|Sim|Sim|Sim|Sim| 
|Manutenção automática de exibições indexadas|Sim|Sim|Sim|Não|Não| 
|Exibições particionadas distribuídas|Sim|Não|Não|Não|Não| 
|Operações indexadas paralelas|Sim|Não|Não|Não|Não|  
|Uso automático da exibição indexada através do otimizador de consulta|Sim|Não|Não|Não|Não| 
|Verificação de consistência paralela|Sim|Não|Não|Não|Não| 
|Ponto de controle do Utilitário do SQL Server|Sim|Não|Não|Não|Não|    
|Extensão do pool de buffers|Sim|Sim|Não|Não|Não| 
  
 <sup>1</sup> Para obter mais informações, veja [Considerações para instalação do SQL Server usando SysPrep](../database-engine/install-windows/considerations-for-installing-sql-server-using-sysprep.md).  
 
<sup>2</sup> Aplica-se a [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] 2016 SP1. 
  
##  <a name="DevTools"></a> Development Tools  
  
|Recurso|Enterprise|Standard|Web|Express with Advanced Services|Express| 
|-------------|----------------|--------------|---------|------------------------------------|------------------------| 
|Integração do Microsoft Visual Studio|Sim|Sim|Sim|Sim|Sim| 
|Intellisense (Transact-SQL e MDX)|Sim|Sim|Sim|Sim|Sim| 
|SQL Server Data Tools (SSDT)|Sim|Sim|Sim|Sim|Não|    
|Ferramentas de design, depuração e edição do MDX|Sim|Sim|Não|Não|Não|   
  
##  <a name="Programmability"></a> Programmability  
  
|Recurso|Enterprise|Standard|Web|Express with Advanced Services|Express 
|-------------|----------------|--------------|---------|------------------------------------|------------------------|  
|Integração básica do R|Sim|Sim|Sim|Sim|Não|   
|Integração avançada do R|Sim|Não|Não|Não|Não| 
|R Server (Autônomo)|Sim|Não|Não|Não|Não|   
|Nó de computação do Polybase|Sim|Sim <sup>1</sup>|Sim <sup>1</sup>, <sup>2</sup>|Sim <sup>1</sup>, <sup>2</sup>|Sim <sup>1</sup>, <sup>2</sup>| 
|Nó de cabeçalho do Polybase|Sim|Não|Não|Não|Não| 
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
|Pesquisa semântica e de texto completo|Sim|Sim|Sim|Sim|Não| 
|Especificação de idioma em consulta|Sim|Sim|Sim|Sim|Não|   
|Service Broker (mensagens)|Sim|Sim|Não (Somente cliente)|Não (Somente cliente)|Não (Somente cliente)|   
|pontos de extremidade Transact-SQL|Sim|Sim|Sim|Não|Não| 

<sup>1</sup> Expansão com vários nós de computação requer um nó de cabeçalho.

<sup>2</sup> Aplica-se a [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] 2016 SP1.
  
## <a name="IS"></a> Integration Services

Para obter informações sobre os recursos do SSIS (Integration Services) com suporte nas edições do [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)], consulte [Recursos do Integration Services com suporte nas edições do SQL Server](../integration-services/integration-services-features-supported-by-the-editions-of-sql-server.md).

##  <a name="MDS"></a> Master Data Services  
 Para obter informações sobre o [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] e os recursos do Data Quality Services com suporte nas edições do [!INCLUDE[ssCurrent_md](../includes/sscurrent-md.md)], consulte [Recursos do Master Data Services e do Data Quality Services com suporte nas edições do SQL Server 2016](../master-data-services/master-data-services-and-data-quality-services-features-support.md). 

  
##  <a name="DW"></a> Data Warehouse  
  
|Recurso|Enterprise|Standard|Web|Express with Advanced Services|Express|   
|-------------|----------------|--------------|---------|------------------------------------|------------------------| 
|Criar cubos sem um banco de dados|Sim|Sim|Não|Não|Não |   
|Gerar automaticamente esquema e data warehouse de preparo|Sim|Sim|Não|Não|Não| 
|Change Data Capture|Sim|Sim <sup>1</sup>|Não|Não|Não| 
|Otimizações de consulta de junção em estrela|Sim|Não|Não|Não|Não| 
|Configuração escalonável somente leitura do Analysis Services|Sim|Não|Não|Não|Não| 
|Processamento paralelo de consultas em tabelas e índices particionados|Sim|Não|Não|Não|Não|   
|Agregação em lote global|Sim|Não|Não|Não|Não| 

<sup>1</sup> Aplica-se a [!INCLUDE[ssSQL15_md](../includes/sssql15-md.md)] SP1.  
##  <a name="SSAS"></a> Analysis Services  
  
Para obter informações sobre os recursos do Analysis Services com suporte nas edições do [!INCLUDE[ssCurrent_md](../includes/sscurrent-md.md)], consulte [Recursos do Analysis Services com suporte nas edições do SQL Server 2016](../analysis-services/analysis-services-features-supported-by-the-editions-of-sql-server-2016.md). 
  
##  <a name="BIMD"></a> BI Semantic Model (Multi Dimensional)  
  
Para obter informações sobre os recursos do Analysis Services com suporte nas edições do [!INCLUDE[ssCurrent_md](../includes/sscurrent-md.md)], consulte [Recursos do Analysis Services com suporte nas edições do SQL Server 2016](../analysis-services/analysis-services-features-supported-by-the-editions-of-sql-server-2016.md).
   
##  <a name="BIT"></a> BI Semantic Model (Tabular)  
  
Para obter informações sobre os recursos do Analysis Services com suporte nas edições do [!INCLUDE[ssCurrent_md](../includes/sscurrent-md.md)], consulte [Recursos do Analysis Services com suporte nas edições do SQL Server 2016](../analysis-services/analysis-services-features-supported-by-the-editions-of-sql-server-2016.md).
  
##  <a name="PPSP"></a> Power Pivot for SharePoint  
  
Para obter informações sobre os recursos do Power Pivot para SharePoint com suporte nas edições do [!INCLUDE[ssCurrent_md](../includes/sscurrent-md.md)], consulte [Recursos do Analysis Services com suporte nas edições do SQL Server 2016](../analysis-services/analysis-services-features-supported-by-the-editions-of-sql-server-2016.md).
  
##  <a name="DM"></a> Data Mining  
  
Para obter informações sobre os recursos do Data Mining com suporte nas edições do [!INCLUDE[ssCurrent_md](../includes/sscurrent-md.md)], consulte [Recursos do Analysis Services com suporte nas edições do SQL Server 2016](../analysis-services/analysis-services-features-supported-by-the-editions-of-sql-server-2016.md).
  
##  <a name="SSRS"></a> Reporting Services  
  
Para obter informações sobre os recursos do Reporting Services com suporte nas edições do [!INCLUDE[ssCurrent_md](../includes/sscurrent-md.md)], consulte [Recursos do Reporting Services com suporte nas edições do SQL Server 2016](../reporting-services/reporting-services-features-supported-by-the-editions-of-sql-server-2016.md).

##  <a name="BIC"></a> Business Intelligence Clients  

Para obter informações sobre os recursos do Cliente de Business Intelligence com suporte nas edições do [!INCLUDE[ssCurrent_md](../includes/sscurrent-md.md)], consulte [Recursos do Analysis Services com suporte nas edições do SQL Server 2016](../analysis-services/analysis-services-features-supported-by-the-editions-of-sql-server-2016.md) ou [Recursos do Reporting Services com suporte nas edições do SQL Server 2016](../reporting-services/reporting-services-features-supported-by-the-editions-of-sql-server-2016.md).
  
##  <a name="SLS"></a> Spatial and Location Services  
  
|Nome do recurso|Enterprise|Standard|Web|Express with Advanced Services|Express|  
|------------------|----------------|--------------|---------|------------------------------------|------------------------|
|Índices espaciais|Sim|Sim|Sim|Sim|Sim|   
|Tipos de dados planares e geodésicos|Sim|Sim|Sim|Sim|Sim| 
|Bibliotecas espaciais avançadas|Sim|Sim|Sim|Sim|Sim|   
|Importação/exportação de formatos de dados espaciais padrão da indústria|Sim|Sim|Sim|Sim|Sim|   
  
##  <a name="ADS"></a> Additional Database Services  
  
|Nome do recurso|Enterprise|Standard|Web|Express with Advanced Services|Express|   
|------------------|----------------|--------------|---------|------------------------------------|------------------------| 
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Assistente de Migração|Sim|Sim|Sim|Sim|Sim|   
|Database Mail|Sim|Sim|Sim|Não|Não| 
  
##  <a name="Other"></a> Other Components  
  
|Nome do recurso|Enterprise|Standard|Web|Express with Advanced Services|Express|   
|------------------|----------------|--------------|---------|------------------------------------|------------------------|  
|StreamInsight|StreamInsight Premium Edition|StreamInsight Standard Edition|StreamInsight Standard Edition|Não|Não| 
|StreamInsight HA|StreamInsight Premium Edition|Não|Não|Não|Não|   
  
> [![Download SSMS](../analysis-services/media/download.png)](https://msdn.microsoft.com/library/mt238290.aspx) **[Download the latest version of SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx)**    
  
## <a name="see-also"></a>Consulte também  
 [Especificações do produto para SQL Server 2016](http://msdn.microsoft.com/library/6445fd53-6844-4170-a86b-7fe76a9f64cb)   
 [Instalação do SQL Server 2016](../database-engine/install-windows/installation-for-sql-server-2016.md)  
  
  

