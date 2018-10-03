---
title: Conjuntos de linhas de esquema do Analysis Services | Microsoft Docs
ms.date: 10/01/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: schema-rowsets
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 4ec9d6c75ef1d3cdc8effdc44861eed5971ced60
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48116676"
---
# <a name="analysis-services-schema-rowsets"></a>Conjuntos de linhas de esquema do Analysis Services
[!INCLUDE[ssas-appliesto-sqlas-all-aas](../../includes/ssas-appliesto-sqlas-all-aas.md)]

  Conjuntos de linhas de esquema são tabelas predefinidas que contêm informações sobre objetos do Analysis Services e o estado do servidor, inclusive esquema de banco de dados, sessões ativas, conexões, comandos e trabalhos executados no servidor. Você pode consultar as tabelas de conjunto de linhas de esquema em uma janela de script XML/UM no SQL Server Management Studio, executar uma consulta de DMV em relação a um conjunto de linhas de esquema ou criar um aplicativo personalizado que incorpora informações de conjunto de linhas de esquema (por exemplo, um aplicativo de relatório que recupera a lista de dimensões disponíveis que podem ser usadas para criar um relatório).  
  
> [!NOTE]  
>  Se você estiver usando conjuntos de linhas de esquema no XML/A script, as informações retornadas na *resultado* parâmetro do [Discover](../../analysis-services/xmla/xml-elements-methods-discover.md) método é estruturado de acordo com os layouts da coluna de conjunto de linhas descritos neste seção. O provedor do [!INCLUDE[msCoName](../../includes/msconame-md.md)] XML for Analysis (XMLA) dá suporte a conjuntos de linhas requeridos pela Especificação do XML for Analysis. O provedor do XMLA também dá suporte a alguns dos conjuntos de linhas de esquema padrão para os provedores de fonte de dados OLE DB, OLE DB para OLAP e OLE DB para Mineração de Dados. Os conjuntos de linhas suportados são descritos nos tópicos a seguir.  

Conjuntos de linhas de esquema são descritos nos dois protocolos do SQL Server Analysis Services:   

[[MS-SSAS-T]: protocolo Tabular do SQL Server Analysis Services](https://msdn.microsoft.com/library/mt719260) -descreve os conjuntos de linhas de esquema para modelos tabulares nos níveis de compatibilidade 1200 e superior.

[[MS-SSAS]: protocolo do SQL Server Analysis Services](https://msdn.microsoft.com/library/ee320606) -descreve os conjuntos de linhas de esquema para modelos multidimensionais e tabulares nos níveis de compatibilidade 1100 e 1103.

## <a name="rowsets-described-in-the-ms-ssas-t-sql-server-analysis-services-tabular-protocol"></a>Conjuntos de linhas descritos em [MS-SSAS-T]: protocolo Tabular do SQL Server Analysis Services

|Conjunto de linhas  |Description  |
|---------|---------|
|[TMSCHEMA_ANNOTATIONS](https://msdn.microsoft.com/library/mt704370)|Fornece informações sobre os objetos de anotação no modelo.|
|[TMSCHEMA_ATTRIBUTE_HIERARCHIES](https://msdn.microsoft.com/library/mt704362)     |   Fornece informações sobre os objetos AttributeHierarchy para uma coluna.      |
|[TMSCHEMA_COLUMNS](https://msdn.microsoft.com/library/mt704373)    |  Fornece informações sobre os objetos de coluna em cada tabela.       |
|[TMSCHEMA_COLUMN_PERMISSIONS](https://msdn.microsoft.com/library/mt842440)|Fornece informações sobre os objetos ColumnPermission em cada tabela de permissão.|
|[TMSCHEMA_CULTURES](https://msdn.microsoft.com/library/mt719125)|Fornece informações sobre os objetos de cultura no modelo.|
|[TMSCHEMA_DATA_SOURCES](https://msdn.microsoft.com/library/mt719191)   |   Fornece informações sobre os objetos de fonte de dados no modelo.      |
|[TMSCHEMA_DETAIL_ROWS_DEFINITIONS](https://msdn.microsoft.com/library/mt825017)|Fornece informações sobre os objetos DetailRowsDefinition no modelo.|
|[TMSCHEMA_EXPRESSIONS](https://msdn.microsoft.com/library/mt825015)|Fornece informações sobre os objetos de expressão no modelo.|
|[TMSCHEMA_EXTENDED_PROPERTIES](https://msdn.microsoft.com/library/mt842451)|Fornece informações sobre os objetos ExtendedProperty no modelo.|
|[TMSCHEMA_HIERARCHIES](https://msdn.microsoft.com/library/mt719136)    |    Fornece informações sobre os objetos de hierarquia em cada tabela.     |
|[TMSCHEMA_KPIS](https://msdn.microsoft.com/library/mt719002)     |    Fornece informações sobre os objetos KPI no modelo.     |
|[TMSCHEMA_LEVELS](https://msdn.microsoft.com/library/mt719038)     |   Fornece informações sobre os objetos de nível de cada hierarquia.      |
|[TMSCHEMA_LINGUISTIC_METADATA](https://msdn.microsoft.com/library/mt719169)|Fornece informações sobre os sinônimos para objetos no modelo para uma cultura específica|
|[TMSCHEMA_MEASURES](https://msdn.microsoft.com/library/mt719218)     |    Fornece informações sobre os objetos de medida em cada tabela.     |
|[TMSCHEMA_MODEL](https://msdn.microsoft.com/library/mt719042)    |  Especifica um objeto de modelo no banco de dados.       |
|[TMSCHEMA_OBJECT_TRANSLATIONS](https://msdn.microsoft.com/library/mt719119)|Fornece informações sobre as traduções de objetos diferentes para uma cultura.|
|[TMSCHEMA_PARTITIONS](https://msdn.microsoft.com/library/mt704375)     |     Fornece informações sobre os objetos de partição em cada tabela.    |
|[TMSCHEMA_PERSPECTIVE_COLUMNS](https://msdn.microsoft.com/library/mt719164)     |   Fornece informações sobre os objetos PerspectiveColumn em cada objeto PerspectiveTable.      |
|[TMSCHEMA_PERSPECTIVE_HIERARCHIES](https://msdn.microsoft.com/library/mt719104)     |  Fornece informações sobre os objetos PerspectiveHierarchy em cada objeto PerspectiveTable.       |
|[TMSCHEMA_PERSPECTIVE_MEASURES](https://msdn.microsoft.com/library/mt719135)     |    Fornece informações sobre os objetos PerspectiveMeasure em cada objeto PerspectiveTable.     |
|[TMSCHEMA_PERSPECTIVE_TABLES](https://msdn.microsoft.com/library/mt719272)     |    Fornece informações sobre objetos de tabela em uma perspectiva.     |
|[TMSCHEMA_PERSPECTIVES](https://msdn.microsoft.com/library/mt704340)     |     Fornece informações sobre os objetos de perspectiva no modelo.    |
|[TMSCHEMA_RELATIONSHIPS](https://msdn.microsoft.com/library/mt704355)     |    Fornece informações sobre objetos de relação no modelo.     |
|[TMSCHEMA_ROLE_MEMBERSHIPS](https://msdn.microsoft.com/library/mt704584)     |  Fornece informações sobre os objetos RoleMembership em cada função.      |
|[TMSCHEMA_ROLES](https://msdn.microsoft.com/library/mt719267)    |   Fornece informações sobre os objetos de função no modelo.      |
|[TMSCHEMA_TABLE_PERMISSIONS](https://msdn.microsoft.com/library/mt704347)    |    Fornece informações sobre os objetos TablePermission em cada função.     |
|[TMSCHEMA_TABLES](https://msdn.microsoft.com/library/mt719250)     |   Fornece informações sobre objetos de tabela no modelo.      |
|[TMSCHEMA_VARIATIONS](https://msdn.microsoft.com/library/mt825008)|Fornece informações sobre os objetos de variação em cada coluna.|

## <a name="rowsets-described-in-the-ms-ssas-sql-server-analysis-services-protocol"></a>Conjuntos de linhas descritos nos [MS-SSAS]: protocolo do SQL Server Analysis Services

|Conjunto de linhas|Description|  
|------------|-----------------|  
|[DBSCHEMA_CATALOGS](https://msdn.microsoft.com/library/ee302115)|Descreve os catálogos que são acessíveis no servidor.|  
|[DBSCHEMA_COLUMNS](https://msdn.microsoft.com/library/ee301789)|Retorna uma linha para cada medida, cada atributo de dimensão de cubo e cada coluna do conjunto de linhas de esquema, exposto como uma coluna.|  
|[DBSCHEMA_PROVIDER_TYPES](https://msdn.microsoft.com/library/ee301696)|Identifica os tipos de dados (base) suportados pelo servidor.|  
|[DBSCHEMA_TABLES](https://msdn.microsoft.com/library/ee320843)|Retorna as dimensões, grupos de medidas ou expostos como tabelas de conjuntos de linhas do esquema.|  
|[DISCOVER_CALC_DEPENDENCY](https://msdn.microsoft.com/library/hh770226)| Retorna informações sobre a dependência de cálculo para um objeto que é especificada em um banco de dados de tabela ou em uma consulta DAX que é executada em um banco de dados Tabular. |  
|[DISCOVER_COMMAND_OBJECTS](https://msdn.microsoft.com/library/ee320662)|Oferece uso de recursos e informações de atividade sobre os objetos em uso pelo comando referenciado.|  
|[DISCOVER_COMMANDS](https://msdn.microsoft.com/library/ee320715)|Oferece uso do recurso e informações de atividade sobre os comandos em execução ou sobre os últimos comandos executados nas conexões abertas no servidor.|  
|[DISCOVER_CONNECTIONS](https://msdn.microsoft.com/library/ee301889)|Oferece uso de recursos e de informações de atividade sobre as conexões atualmente abertas no servidor.|  
|[DISCOVER_CSDL_METADATA](https://msdn.microsoft.com/library/gg587670)|Retorna informações sobre metadados de banco de dados para bancos de dados na memória.|  
|[DISCOVER_DATASOURCES](https://msdn.microsoft.com/library/ee320285)|Retorna uma lista das fontes de dados que estão disponíveis no servidor.|
|[DISCOVER_DB_CONNECTIONS](https://msdn.microsoft.com/library/ee320467)|Oferece uso de recursos e de informações de atividade sobre as conexões abertas no momento do servidor para um banco de dados.|  
|[DISCOVER_DIMENSION_STAT](https://msdn.microsoft.com/library/ee320284)|retorna estatísticas sobre a dimensão especificada.|  
|[DISCOVER_ENUMERATORS](https://msdn.microsoft.com/library/ee302012)|Retorna uma lista de nomes, tipos de dados e valores de enumeração dos enumeradores que recebem suporte do provedor do XMLA para uma fonte de dados específica.|  
|[DISCOVER_INSTANCES](https://msdn.microsoft.com/library/ee320541)|Descreve as instâncias no servidor.|  
|[DISCOVER_JOBS](https://msdn.microsoft.com/library/ee320363)|Oferece informações sobre os trabalhos ativos em execução no servidor. O trabalho é uma parte do comando que executa uma tarefa específica em nome desse comando.|  
|[DISCOVER_KEYWORDS &AMP;#40;XMLA&AMP;#41;](https://msdn.microsoft.com/library/ee301719)|Retorna informações sobre palavras-chave reservadas pelo servidor do XMLA.|  
|[DISCOVER_LITERALS](https://msdn.microsoft.com/library/ee301320)|Retorna informações sobre literais suportados pelo servidor.|  
|[DISCOVER_LOCATIONS](https://msdn.microsoft.com/library/ee302024)|Retorna informações sobre o conteúdo de um arquivo de backup. |
|[DISCOVER_LOCKS](https://msdn.microsoft.com/library/ee320398)|Oferece informações sobre os bloqueios atuais no servidor.|  
|[DISCOVER_MASTER_KEY](https://msdn.microsoft.com/library/ee301825)|Retorna a chave de criptografia mestra do servidor.|
|[DISCOVER_MEMORYGRANT](https://msdn.microsoft.com/library/ee320945)|Retorna uma lista de concessões de cota de memória interna que são usadas por trabalhos atualmente em execução no servidor.|  
|[DISCOVER_MEMORYUSAGE](https://msdn.microsoft.com/library/ee320910)|Retorna as estatísticas DISCOVER_MEMORYUSAGE de vários objetos alocados pelo servidor.|  
|[DISCOVER_OBJECT_ACTIVITY](https://msdn.microsoft.com/library/ee320661)|Oferece uso de recursos por objeto desde o início do serviço.|  
|[DISCOVER_OBJECT_MEMORY_USAGE](https://msdn.microsoft.com/library/ee320910)|Retorna as estatísticas DISCOVER_MEMORYUSAGE de vários objetos alocados pelo servidor.|  
|[DISCOVER_PARTITION_DIMENSION_STAT](https://msdn.microsoft.com/library/ee320268)|Retorna estatísticas sobre a dimensão associada a uma partição.|  
|[DISCOVER_PARTITION_STAT](https://msdn.microsoft.com/library/ee320483)|Retorna estatísticas sobre agregações em uma partição específica.|  
|[DISCOVER_PERFORMANCE_COUNTERS](https://msdn.microsoft.com/library/ee320809)|Retorna o valor de um ou mais contadores de desempenho especificados. |  
|[DISCOVER_PROPERTIES](https://msdn.microsoft.com/library/ee320589)|Retorna uma lista de informações e valores sobre as propriedades que são compatíveis com o servidor da fonte de dados especificado.|  
|[DISCOVER_RING_BUFFERS](https://msdn.microsoft.com/library/mt719204)|Retorna informações sobre os buffers de anel de XEvent atuais no servidor.|
|[DISCOVER_SCHEMA_ROWSETS](https://msdn.microsoft.com/library/ee320478)|Retorna os nomes, restrições, descrição e outras informações para todas as solicitações de descoberta.|  
|[DISCOVER_SESSIONS](https://msdn.microsoft.com/library/ee301962)|Oferece uso de recursos e de informações de atividade sobre as sessões atualmente abertas no servidor.|  
|[DISCOVER_STORAGE_TABLE_COLUMN_SEGMENTS](https://msdn.microsoft.com/library/ee320710)|Retorna informações sobre segmentos de coluna usado para armazenar dados para tabelas na memória.|  
|[DISCOVER_STORAGE_TABLE_COLUMNS](https://msdn.microsoft.com/library/ee302101)|Contém informações sobre as colunas usadas para representar as colunas de uma tabela na memória.|  
|[DISCOVER_STORAGE_TABLES](https://msdn.microsoft.com/library/ee302014)|Retorna estatísticas sobre tabelas na memória disponíveis para o servidor.|  
|[DISCOVER_TRACE_COLUMNS]()||  
|[DISCOVER_TRACE_DEFINITION_PROVIDERINFO](https://msdn.microsoft.com/library/ee301342)|Contém linhas de esquema DISCOVER_TRACE_COLUMNS.|  
|[DISCOVER_TRACE_EVENT_CATEGORIES](https://msdn.microsoft.com/library/ee320442)|Contém linhas de esquema DISCOVER_TRACE_EVENT_CATEGORIES.|  
|[DISCOVER_TRACES](https://msdn.microsoft.com/library/ee301643)|Contém o conjunto de linhas de esquema DISCOVER_TRACES.|  
|[DISCOVER_TRANSACTIONS](https://msdn.microsoft.com/library/ee301363)|Retorna o conjunto atual de transações pendentes no sistema.|  
|[DISCOVER_XEVENT_TRACE_DEFINITION](https://msdn.microsoft.com/library/mt704568)|Fornece informações sobre os rastreamentos XEvent atualmente ativos no servidor.|  
|[DISCOVER_XEVENT_PACKAGES](https://msdn.microsoft.com/library/mt704569)|Fornece informações sobre os pacotes de XEvent que são descritas no servidor.|
|[DISCOVER_XEVENT_OBJECTS](https://msdn.microsoft.com/library/mt704543)|Fornece informações sobre os objetos de XEvent que são descritas no servidor.|
|[DISCOVER_XEVENT_OBJECT_COLUMNS](https://msdn.microsoft.com/library/mt719352)|Fornece informações sobre o esquema de objetos de XEvent que são descritas no servidor.|
|[DISCOVER_XEVENT_SESSIONS](https://msdn.microsoft.com/library/mt704397)|Fornece informações sobre as sessões de XEvent atuais no servidor.|
|[DISCOVER_XEVENT_SESSION_TARGETS](https://msdn.microsoft.com/library/mt704564)|Fornece informações sobre os destinos da sessão XEvent atuais no servidor.|
|[DISCOVER_XML_METADATA](https://msdn.microsoft.com/library/ee301560)|Retorna um conjunto de linhas com uma linha e uma coluna. |
|[DMSCHEMA_MINING_COLUMNS](https://msdn.microsoft.com/library/ee301664)|Descreve as colunas individuais de todos os modelos de mineração de dados descritos são implantados no servidor.|  
|[DMSCHEMA_MINING_FUNCTIONS](https://msdn.microsoft.com/library/ee320415)|Descreve as funções de mineração de dados que são compatíveis com os algoritmos de mineração de dados que estão disponíveis em um servidor que está executando o Analysis Services.|  
|[DMSCHEMA_MINING_MODEL_CONTENT](https://msdn.microsoft.com/library/ee302124)|Permite que o aplicativo cliente procure o conteúdo de um modelo de mineração de dados treinados.|  
|[DMSCHEMA_MINING_MODEL_CONTENT_PMML](https://msdn.microsoft.com/library/ee320692)|Retorna a estrutura XML do modelo de mineração. O formato da cadeia de caracteres XML segue o padrão de PMML 2.1.|  
|[DMSCHEMA_MINING_MODEL_XML](https://msdn.microsoft.com/library/ee301916)|Retorna a estrutura XML do modelo de mineração. O formato da cadeia de caracteres XML segue o padrão de PMML 2.1.|  
|[DMSCHEMA_MINING_MODELS](https://msdn.microsoft.com/library/ee320603)|Enumera os modelos de mineração de dados implantados no servidor.|  
|[DMSCHEMA_MINING_SERVICE_PARAMETERS](https://msdn.microsoft.com/library/ee320378)|Oferece uma lista de parâmetros que podem ser usados na configuração do comportamento de cada algoritmo de mineração de dados instalado no servidor.|  
|[DMSCHEMA_MINING_SERVICES](https://msdn.microsoft.com/library/ee320487)|Fornece informações sobre cada algoritmo de mineração de dados com suporte no servidor.|  
|[DMSCHEMA_MINING_STRUCTURE_COLUMNS](https://msdn.microsoft.com/library/ee320277)|Descreve as colunas individuais de todas as estruturas de mineração implantadas no servidor.|  
|[DMSCHEMA_MINING_STRUCTURES](https://msdn.microsoft.com/library/ee320704)|Enumera informações sobre as estruturas de mineração no catálogo atual.|  
|[MDSCHEMA_ACTIONS](https://msdn.microsoft.com/library/ee320890)|Descreve as ações que podem estar disponíveis para o aplicativo cliente.|
|[MDSCHEMA_CUBES](https://msdn.microsoft.com/library/ee301304)|Descreve a estrutura de cubos dentro de um banco de dados. Perspectivas também são retornadas nesse esquema.|
|[MDSCHEMA_DIMENSIONS](https://msdn.microsoft.com/library/ee301366)|Descreve as dimensões em um banco de dados.|  
|[MDSCHEMA_FUNCTIONS](https://msdn.microsoft.com/library/mt719467)|Retorna informações sobre as funções que estão atualmente disponíveis para uso nas linguagens DAX e MDX.|
|[MDSCHEMA_HIERARCHIES](https://msdn.microsoft.com/library/ee320250)|Descreve cada hierarquia dentro de determinada dimensão.|  
|[MDSCHEMA_INPUT_DATASOURCES](https://msdn.microsoft.com/library/ee301386)|Descreve os objetos de fonte de dados descritos no banco de dados.|  
|[MDSCHEMA_KPIS](https://msdn.microsoft.com/library/ee320406)|Descreve os KPIs em um banco de dados.|  
|[MDSCHEMA_LEVELS](https://msdn.microsoft.com/library/ee320746)|Descreve cada nível dentro de uma hierarquia específica.|  
|[MDSCHEMA_MEASUREGROUP_DIMENSIONS](https://msdn.microsoft.com/library/ee320977)|Enumera as dimensões de grupos de medidas.|  
|[MDSCHEMA_MEASURESGROUPS](https://msdn.microsoft.com/library/ee320601)|Descreve os grupos de medidas dentro de um banco de dados.|  
|[MDSCHEMA_MEASURES](https://msdn.microsoft.com/library/ee301871)|Descreve cada medida.|  
|[MDSCHEMA_MEMBERS](https://msdn.microsoft.com/library/ee320960)|Descreve os membros dentro de um banco de dados.|  
|[MDSCHEMA_PROPERTIES](https://msdn.microsoft.com/library/ee320393)|Descreve as propriedades de membros e propriedades de célula.|  
|[MDSCHEMA_SETS](https://msdn.microsoft.com/library/ee301356)|Descreve todos os conjuntos são descritos no momento em um banco de dados, incluindo conjuntos com escopo de sessão.|  

  
  
