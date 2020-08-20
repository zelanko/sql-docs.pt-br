---
description: Edições e recursos compatíveis do SQL Server 2019 no Linux
title: Edições e recursos com suporte do SQL Server 2019 – Linux
ms.date: 01/08/2020
ms.prod: sql
ms.technology: linux
ms.topic: conceptual
helpviewer_keywords:
- Enterprise Edition [SQL Server]
- Developer Edition [SQL Server]
- default components
- installing SQL Server, components
- Setup [SQL Server], components
- SQL Server, editions
- SQL Server, components
- editions [SQL Server]
- versions [SQL Server]
- Setup [SQL Server], editions
- SQL Server Installation Wizard
- components [SQL Server]
- Standard Edition [SQL Server]
- installing SQL Server, editions
- editions [SQL Server], about edition options
- Setup [SQL Server]
author: VanMSFT
ms.author: vanto
ms.reviewer: mikeray
ms.openlocfilehash: aca10f1cb7d6b3bef1cd44b58f2f68ba01d57a22
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88456831"
---
# <a name="editions-and-supported-features-of-sql-server-2019-on-linux"></a>Edições e recursos compatíveis do SQL Server 2019 no Linux

[!INCLUDE [SQL Server - Linux](../includes/applies-to-version/sql-linux.md)]

Este artigo apresenta detalhes de recursos com suporte nas diferentes edições do SQL Server 2019 no Linux. Para edições e recursos compatíveis do SQL Server no Windows, confira [SQL Server 2019 – Windows](../sql-server/editions-and-components-of-sql-server-version-15.md).  
  
Os requisitos de instalação variam de acordo com as necessidades do aplicativo. As diferentes edições do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] acomodam desempenho, runtime e requisitos de preço exclusivos para organizações e indivíduos. Os componentes do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] que você instala dependem também dos seus requisitos específicos. As seções a seguir ajudarão você a entender como fazer a melhor escolha entre as edições e os componentes disponíveis no [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  

Para notas de versão mais recentes e informações sobre novidades, consulte o seguinte:
- [Notas de versão do SQL Server 2019 no Linux](sql-server-linux-release-notes-2019.md)
- [Novidades no SQL Server 2019 no Linux](sql-server-linux-whats-new-2019.md)

Para obter uma lista dos recursos de SQL Server não disponíveis no Linux, confira [Recursos e serviços sem suporte](#Unsupported).

### <a name="try-sql-server"></a>Experimente o SQL Server.    
    
[Baixe o SQL Server 2019](https://www.microsoft.com/sql-server/sql-server-2019)

## <a name="ssnoversion-editions"></a>Edições do[!INCLUDE[ssNoVersion](../includes/ssNoVersion-md.md)]  
 A tabela a seguir descreve essas edições do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. 
  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] edição|Definição|  
|---------------------------------------|----------------|  
|Enterprise|A oferta Premium, [!INCLUDE[ssNoVersion](../includes/ssNoVersion-md.md)] Enterprise Edition, oferece recursos abrangentes de datacenter de alto nível, com um desempenho muito rápido, permitindo altos níveis de serviço para cargas de trabalho críticas.|  
|Standard|A edição Standard do [!INCLUDE[ssNoVersion](../includes/ssNoVersion-md.md)] fornece gerenciamento de dados básico para departamentos e pequenas empresas executarem seus aplicativos e dá suporte a ferramentas de desenvolvimento comuns para rede local e em nuvem, permitindo o gerenciamento eficiente de bancos de dados com recursos mínimos de TI.|  
|Web|A edição[!INCLUDE[ssNoVersion](../includes/ssNoVersion-md.md)] Web é uma opção de baixo custo total de propriedade para hospedagem de sites e VAPs da Web que fornece recursos de escalabilidade, economia e capacidade de gerenciamento para propriedades da Web de pequeno a grande porte.|  
|Desenvolvedor|A edição[!INCLUDE[ssNoVersion](../includes/ssNoVersion-md.md)] Developer permite que os desenvolvedores criem qualquer tipo de aplicativo com base no [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Ele inclui todas as funcionalidades da edição Enterprise, mas é licenciado para ser usado como um sistema de teste e desenvolvimento, e não como um servidor de produção. O [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Developer é uma opção ideal para pessoas que criam e testam aplicativos.|  
|Express edition|A edição Express é o banco de dados gratuito de nível de entrada, ideal para conhecer e criar aplicativos de área de trabalho e aplicativos controlados por dados de pequenos servidores. É a melhor escolha para fornecedores de software independente, desenvolvedores e interessados que criam aplicativos cliente. Se precisar de recursos mais avançados de banco de dados, o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Express pode ser perfeitamente atualizado para versões mais sofisticadas do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].|  
  
## <a name="using-ssnoversion-with-clientserver-applications"></a>Usando [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] com aplicativos cliente/servidor  

Você pode instalar apenas os componentes cliente do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] em um computador que esteja executando aplicativos cliente/servidor que se conectam diretamente a uma instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. A instalação dos componentes cliente é também uma boa opção se você administra uma instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] em um servidor de banco de dados ou se planeja desenvolver aplicativos no [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
## <a name="ssnoversion-components"></a>Componentes [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]  

O SQL Server 2019 no Linux é compatível com o mecanismo de banco de dados do SQL Server. A tabela a seguir descreve os recursos no mecanismo de banco de dados.   
  
|Componentes de servidor|Descrição|  
|-----------------------|-----------------|  
|[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]|O [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] inclui o [!INCLUDE[ssDE](../includes/ssde-md.md)], o principal serviço para armazenamento, processamento e segurança de dados, replicação, pesquisa de texto completo e ferramentas para gerenciar dados XML e integração de análise de banco de dados.|  

**Edições Developer, Enterprise Core e Evaluation**  
Para saber quais os recursos com suporte nas edições Developer, Enterprise Core e Evaluation, veja os recursos listados para o SQL Server Enterprise Edition nas tabelas a seguir.

A Developer Edition continua a dar suporte a apenas um cliente para o [SQL Server Distributed Replay](../tools/distributed-replay/sql-server-distributed-replay.md). 
  
##  <a name="scale-limits"></a><a name="Cross-BoxScaleLimits"></a> Limites de escala  
  
|Recurso|Enterprise|Standard|Web|Express| 
|-------------|----------------|--------------|---------|------------------------|
|Capacidade máxima de computação usada por uma única instância – [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]<sup>1</sup>|Máximo do sistema operacional|Limitado a menos de 4 soquetes ou 24 núcleos|Limitado a menos de 4 soquetes ou 16 núcleos|Limitado a menos de 1 soquete ou 4 núcleos| 
|Capacidade máxima de computação usada por uma única instância – [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] ou [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]|Máximo do sistema operacional|Limitado a menos de 4 soquetes ou 24 núcleos|Limitado a menos de 4 soquetes ou 16 núcleos|Limitado a menos de 1 soquete ou 4 núcleos|
|Memória máxima para o pool de buffers por instância do [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]|Máximo do sistema operacional|128 GB|64 GB|1410 MB|
|Máximo de memória para cache do segmento Columnstore por instância do [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]|Memória ilimitada| 32 GB| 16 GB| 352 MB|  
|Tamanho de dados máximo otimizado para memória de acordo com banco de dados em [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]|Memória ilimitada| 32 GB| 16 GB| 352 MB|
|Tamanho máximo do banco de dados relacional|524 PB|524 PB|524 PB|10 GB|  
  
<sup>1</sup> A Enterprise Edition com licenciamento baseado em Servidor + CAL (licença de acesso para cliente) (não disponível para novos contratos) é limitada ao máximo de 20 núcleos por instância do SQL Server. Não há limites no modelo de Licenciamento de Servidor Baseado em Núcleo. Para saber mais, confira [Calcular limites de capacidade por edição do SQL Server](../sql-server/compute-capacity-limits-by-edition-of-sql-server.md).  
 
##  <a name="rdbms-high-availability"></a><a name="RDBMSHA"></a> Alta Disponibilidade do RDBMS  
  
|Recurso|Enterprise|Standard|Web|Express|  
|-------------|----------------|--------------|---------|------------------------|  
|Envio de logs|Sim|Sim|Sim|Não|  
|Compactação de backup|Sim|Sim|Não|Não| 
|Instantâneo do banco de dados|Sim|Não|Não|Não|
|Instância do cluster de failover Always On<sup>1</sup>|Sim|Sim|Não|Não| 
|Grupos de disponibilidade Always On<sup>2</sup>|Sim|Não|Não|Não|
|Grupos de disponibilidade básicos <sup>3</sup>|Não|Sim|Não|Não|
|Configuração de grupos de disponibilidade de confirmação de réplica mínima|Sim|Sim|Não|Não|
|Grupo de disponibilidade sem cluster|Sim|Sim|Não|Não|
|Restauração de arquivo e página online|Sim|Não|Não|Não|
|Indexação online|Sim|Não|Não|Não|
|Recompilações de índice online retomáveis|Sim|Não|Não|Não|
|Alteração de esquema online|Sim|Não|Não|Não|
|Recuperação rápida|Sim|Não|Não|Não|
|Backups espelhados|Sim|Não|Não|Não|
|Adição de memória a quente e CPU|Sim|Não|Não|Não|
|Backup criptografado|Sim|Sim|Não|Não|
|Backup híbrido para o Azure (backup para URL)|Sim|Sim|Não|Não|
  
<sup>1</sup> Na Enterprise Edition, o número de nós é o máximo do sistema operacional. Na Edição Standard, há suporte para dois nós. 

<sup>2</sup> Na Enterprise Edition, há suporte para até oito réplicas secundárias, incluindo duas réplicas secundárias síncronas. 

<sup>3</sup> A Standard Edition é compatível com grupos de disponibilidade básicos. Um grupo de disponibilidade básico dá suporte a duas réplicas, com um banco de dados. Para obter mais informações sobre grupos de disponibilidade básicos, consulte [Grupos de Disponibilidade Básicos](../database-engine/availability-groups/windows/basic-availability-groups-always-on-availability-groups.md).    

##  <a name="rdbms-scalability-and-performance"></a><a name="RDBMSSP"></a> Escalabilidade e desempenho do RDBMS  
  
|Recurso|Enterprise|Standard|Web|Express|  
|-------------|----------------|--------------|---------|------------------------| 
|Columnstore <sup>1</sup>|Sim|Sim|Sim|Sim|  
|Binários de objeto grandes em índices columnstore clusterizados|Sim|Sim|Sim|Sim|  
|Recompilação de índice columnstore não clusterizado online|Sim|Não|Não|Não|
|OLTP na memória <sup>1</sup>|Sim|Sim|Sim|Sim|
|Memória principal persistente|Sim|Sim|Sim|Sim|
|Particionamento de tabela e índice|Sim|Sim|Sim|Sim|  
|Compactação de dados|Sim|Sim|Sim|Sim|
|Administrador de Recursos|Sim|Não|Não|Não|  
|Paralelismo de tabela particionada|Sim|Não|Não|Não|
|Memória de página grande com reconhecimento para NUMA e alocação de matriz de buffer|Sim|Não|Não|Não|
|Administração do recurso de E/S|Sim|Não|Não|Não|  
|Durabilidade atrasada|Sim|Sim|Sim|Sim|
|Ajuste Automático|Sim|Não|Não|Não|
|Junções Adaptáveis de Modo de Lote|Sim|Não|Não|Não|
|Comentários de Concessão de Memória do Modo de Lote|Sim|Não|Não|Não|
|Execução Intercalada para Funções com Valor de Tabela de Várias Instruções|Sim|Sim|Sim|Sim|
|Aprimoramentos de inserção em massa|Sim|Sim|Sim|Sim|


<sup>1</sup> Tamanho de dados de OLTP na memória e cache do segmento Columnstore são limitados a quantidade de memória especificada por edição na seção limites de escala. Os graus de máximos de paralelismo é limitado. Os graus de paralelismo do processo (DOP) de criação de um índice são limitados a 2 DOP para a Standard Edition e a 1 DOP para a Web e a Express Editions. Refere-se a índices de columnstore criados em tabelas baseadas em disco e tabelas com otimização de memória.

##  <a name="rdbms-security"></a><a name="RDBMSS"></a> Segurança do RDBMS  
  
|Recurso|Enterprise|Standard|Web|Express|
|-------------|----------------|--------------|---------|------------------------------------| 
|Segurança em nível de linha|Sim|Sim|Sim|Sim|  
|Always Encrypted|Sim|Sim|Sim|Sim| 
|Mascaramento de dados dinâmicos|Sim|Sim|Sim|Sim|   
|Auditoria básica|Sim|Sim|Sim|Sim| 
|Auditoria refinada|Sim|Sim|Sim|Sim| 
|Criptografia transparente do banco de dados|Sim|Sim|Não|Não|   
|Funções definidas pelo usuário|Sim|Sim|Sim|Sim| 
|Bancos de dados independentes|Sim|Sim|Sim|Sim| 
|Criptografia para backups|Sim|Sim|Não|Não|  

##  <a name="rdbms-manageability"></a><a name="RDBMSM"></a> Gerenciamento RDBMS  
  
|Recurso|Enterprise|Standard|Web|Express|   
|-------------|----------------|--------------|---------|------------------------|  
|Conexão dedicada de administrador|Sim|Sim|Sim|Sim, com o sinalizador de rastreamento|   
|Suporte de scripts PowerShell|Sim|Sim|Sim|Sim| 
|Suporte para operações de componente do aplicativo da camada de dados – extrair, implantar, atualizar, excluir|Sim|Sim|Sim|Sim| 
|Automação de política (verificação de agenda e alterações)|Sim|Sim|Sim|Não|  
|Coletor de dados de desempenho|Sim|Sim|Sim|Não|
|Relatórios de desempenho padrão|Sim|Sim|Sim|Não|
|Guias de plano e planejar congelamento para guias de plano|Sim|Sim|Sim|Não| 
|Direcione a consulta de exibições indexadas (usando a dica de NOEXPAND)|Sim|Sim|Sim|Sim| 
|Manutenção automática de exibições indexadas|Sim|Sim|Sim|Não|
|Exibições particionadas distribuídas|Sim|Não|Não|Não| 
|Operações indexadas paralelas|Sim|Não|Não|Não|  
|Uso automático da exibição indexada através do otimizador de consulta|Sim|Não|Não|Não| 
|Verificação de consistência paralela|Sim|Não|Não|Não| 
|Ponto de controle do Utilitário do SQL Server|Sim|Não|Não|Não|    

##  <a name="programmability"></a><a name="Programmability"></a> Programmability  
  
|Recurso|Enterprise|Standard|Web|Express 
|-------------|----------------|--------------|---------|------------------------|  
|JSON|Sim|Sim|Sim|Sim|   
|Repositório de Consultas|Sim|Sim|Sim|Sim|   
|Temporal|Sim|Sim|Sim|Sim|   
|Suporte a XML nativo|Sim|Sim|Sim|Sim| 
|Indexação XML|Sim|Sim|Sim|Sim| 
|Funcionalidades MERGE e UPSERT|Sim|Sim|Sim|Sim|   
|Tipos de dados de Data e Hora|Sim|Sim|Sim|Sim|  
|Suporte à internacionalização|Sim|Sim|Sim|Sim| 
|Pesquisa semântica e de texto completo|Sim|Sim|Sim|Sim|
|Especificação de idioma em consulta|Sim|Sim|Sim|Sim|
|Service Broker (mensagens)|Sim|Sim|Não (Somente cliente)|Não (Somente cliente)|
|pontos de extremidade Transact-SQL|Sim|Sim|Sim|Não|
|Grafo|Sim|Sim|Sim|Sim|  


<sup>1</sup> Expansão com vários nós de computação requer um nó de cabeçalho.

## <a name="integration-services"></a><a name="IS"></a> Integration Services

Para obter informações sobre os recursos do SSIS (Integration Services) compatíveis com as edições do [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)], confira [Recursos do Integration Services compatíveis com as edições do SQL Server](../integration-services/integration-services-features-supported-by-the-editions-of-sql-server.md).

##  <a name="spatial-and-location-services"></a><a name="SLS"></a> Serviços espaciais e de localização  
  
|Nome do recurso|Enterprise|Standard|Web|Express|  
|------------------|----------------|--------------|---------|------------------------------------|------------------------|
|Índices espaciais|Sim|Sim|Sim|Sim|   
|Tipos de dados planares e geodésicos|Sim|Sim|Sim|Sim| 
|Bibliotecas espaciais avançadas|Sim|Sim|Sim|Sim|   
|Importação/exportação de formatos de dados espaciais padrão da indústria|Sim|Sim|Sim|Sim|   

## <a name="unsupported-features--services"></a><a name="Unsupported"></a> Recursos e serviços sem suporte

Os seguintes recursos e serviços não estão disponíveis no SQL Server 2019 no Linux. O suporte para esses recursos será habilitado gradativamente com o passar do tempo.

| Área | Recurso ou serviço sem suporte |
|-----|-----|
| **Mecanismo de banco de dados** | Replicação de mesclagem |
| &nbsp; | Stretch DB |
| &nbsp; | Consulta distribuída com conexões de terceiros |
| &nbsp; | Servidores vinculados a fontes de dados diferentes do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]  |
| &nbsp; | Procedimentos armazenados estendidos do sistema (XP_CMDSHELL etc.) |
| &nbsp; | Filetable, FILESTREAM |
| &nbsp; | Assemblies de CLR com definição de permissão EXTERNAL_ACCESS ou UNSAFE |
| &nbsp; | Buffer Pool Extension |
| **SQL Server Agent** |  Subsistemas: CmdExec, PowerShell, Queue Reader, SSIS, SSAS, SSRS |
| &nbsp; | Alertas |
| &nbsp; | Backup Gerenciado |
| **Alta disponibilidade** | Espelhamento de banco de dados  |
| **Segurança** | Gerenciamento Extensível de Chaves |
| &nbsp; | Autenticação do AD para servidores vinculados | 
| &nbsp; | Autenticação do AD para AGs (grupos de disponibilidade) | 
| **Serviços** | SQL Server Browser |
| &nbsp; | SQL Server R services<sup>1</sup> |
| &nbsp; | StreamInsight |
| &nbsp; | Serviços de análise |
| &nbsp; | Reporting Services |
| &nbsp; | Data Quality Services |
| &nbsp; | Master Data Services |

<sup>1</sup> O SQL Server R tem suporte no SQL Server, mas não há suporte para os serviços do SQL Server R como um pacote separado.
  
## <a name="next-steps"></a>Próximas etapas
 [Edições e recursos com suporte do SQL Server 2017 – Linux](sql-server-linux-editions-and-components-2017.md)  
 [Edições e recursos compatíveis com o SQL Server 2019 – Windows](../sql-server/editions-and-components-of-sql-server-version-15.md)  
 [Edições e recursos compatíveis com o SQL Server 2017 – Windows](../sql-server/editions-and-components-of-sql-server-2017.md)  
 [Edições e recursos compatíveis com o SQL Server 2016 – Windows](../sql-server/editions-and-components-of-sql-server-2016.md)  
 [Instalação do SQL Server](../database-engine/install-windows/installation-for-sql-server-2016.md)  
 [Especificações do produto para SQL Server](https://msdn.microsoft.com/library/6445fd53-6844-4170-a86b-7fe76a9f64cb)


