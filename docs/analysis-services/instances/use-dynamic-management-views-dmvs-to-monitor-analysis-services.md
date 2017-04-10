---
title: "Usar DMVs (Exibi&#231;&#245;es de Gerenciamento Din&#226;mico) para monitorar o Analysis Services | Microsoft Docs"
ms.custom: ""
ms.date: "03/16/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 22b82b2d-867f-4ebf-9288-79d1cdd62f18
caps.latest.revision: 16
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 16
---
# Usar DMVs (Exibi&#231;&#245;es de Gerenciamento Din&#226;mico) para monitorar o Analysis Services
  As DMVs (Exibições de Gerenciamento Dinâmico) do Analysis Services são estruturas de consulta que expõem informações sobre as operações do servidor local e a integridade do servidor. A estrutura da consulta é uma interface para conjuntos de linhas de esquema que retornam metadados e informações de monitoramento sobre uma instância do Analysis Services.  
  
 Para a maioria das consultas DMV, use uma instrução **SELECT** e o esquema **$System** com um conjunto de linhas de esquema XML/A.  
  
```  
SELECT * FROM $System.<schemaRowset>  
```  
  
 As consultas DMV retornam informações sobre o estado atual do servidor no momento em que a consulta foi executada. Para monitorar as operações em tempo real, use o rastreamento. Para obter mais informações, consulte [Use SQL Server Profiler to Monitor Analysis Services](../../analysis-services/instances/use-sql-server-profiler-to-monitor-analysis-services.md).  
  
 Este tópico inclui as seguintes seções:  
  
 [Benefícios do uso de consultas DMV](#bkmk_ben)  
  
 [Exemplos e cenários](#bkmk_ex)  
  
 [Sintaxe da consulta](#bkmk_syn)  
  
 [Ferramentas e permissões](#bkmk_tools)  
  
 [Referência de DMV](#bkmk_ref)  
  
##  <a name="bkmk_ben"></a> Benefícios do uso de consultas DMV  
 As consultas DMV retornam informações sobre operações e consumo de recursos que não estão disponíveis por outros meios.  
  
 As consultas de DMV são uma alternativa à execução de comandos XML/UM Discover. Para a maioria dos administradores, gravar uma consulta DMV é mais simples porque a sintaxe dessa consulta se baseia em SQL. Além disso, o conjunto de resultados é retornado em um formato de tabela que torna mais fácil a leitura e a cópia.  
  
##  <a name="bkmk_ex"></a> Exemplos e cenários  
 Uma consulta DMV pode ajudá-lo a responder perguntas sobre sessões ativas e conexões e quais objetos estão consumindo a maior parte da CPU ou da memória em um determinado momento. Esta seção fornece exemplos de cenários em que as consultas DMV são geralmente mais usadas. Você também pode examinar o [Guia de Operações do SQL Server 2008 R2 Analysis Services](http://go.microsoft.com/fwlink/?LinkID=225539&clcid=0x409) para obter insights sobre como usar consultas DMV para monitorar uma instância de servidor.  
  
 `Select * from $System.discover_object_activity` /** Esta consulta relata a atividade do objeto desde a última vez em que o serviço foi iniciado. Por exemplo, para consultas baseadas nesta DMV, consulte [New System.Discover_Object_Activity](http://go.microsoft.com/fwlink/?linkid=221322).  
  
 `Select * from $System.discover_object_memory_usage` /** Esta consulta relata o consumo de memória por objeto.  
  
 `Select * from $System.discover_sessions` /** Esta consulta relata as sessões ativas, incluindo o usuário e a duração da sessão.  
  
 `Select * from $System.discover_locks` /** Esta consulta retorna um instantâneo dos bloqueios usados em um momento específico.  
  
##  <a name="bkmk_syn"></a> Sintaxe da consulta  
 O mecanismo de consulta para DMVs é o analisador de Mineração de Dados. A sintaxe da consulta DMV se baseia na instrução [SELECT &#40;DMX&#41;](../../dmx/select-dmx.md).  
  
 Embora a sintaxe da consulta DMV se baseie em uma instrução SQL SELECT, ela não oferece suporte à sintaxe completa de uma instrução SELECT. Em especial, não há suporte para JOIN, GROUP BY, LIKE, CAST e CONVERT.  
  
```  
SELECT [DISTINCT] [TOP <n>] <select list>  
FROM $System.<schemaRowset>  
[WHERE <condition expression>]  
[ORDER BY <expression>[DESC|ASC]]  
```  
  
 O exemplo a seguir para DISCOVER_CALC_DEPENDENCY demonstra o uso da cláusula WHERE para fornecer um parâmetro à consulta:  
  
```  
SELECT * FROM $System.DISCOVER_CALC_DEPENDENCY  
WHERE OBJECT_TYPE = 'ACTIVE_RELATIONSHIP'  
```  
  
 Alternativamente, para conjuntos de linhas de esquema que têm restrições, a consulta deve incluir a função SYSTEMRESTRICTSCHEMA. O exemplo a seguir retorna metadados de CSDL sobre modelos de tabela em execução em um servidor de modo de tabela. Observe que CATALOG_NAME diferencia maiúsculas e minúsculas:  
  
```  
Select * from SYSTEMRESTRICTSCHEMA ($System.Discover_csdl_metadata, [CATALOG_NAME] = 'Adventure Works DW')  
```  
  
##  <a name="bkmk_tools"></a> Ferramentas e permissões  
 Você deve ter permissões de administrador de sistema na instância do Analysis Services para consultar uma DMV.  
  
 Você pode usar qualquer aplicativo cliente que tenha suporte para consultas MDX ou DMX, incluindo o SQL Server Management Studio, um relatório do Reporting Services ou um PerformancePoint Dashboard.  
  
 Para executar uma consulta DMV a partir do Management Studio, conecte-se à instância que você deseja consultar e clique em **Nova Consulta**. Você pode executar uma consulta em uma janela de consulta MDX ou DMX.  
  
##  <a name="bkmk_ref"></a> Referência de DMV  
 Nem todos os conjuntos de linhas de esquema têm uma interface DMV. Para retornar uma lista de todos os conjuntos de linhas de esquema que possam ser consultadas usando DMV, execute a consulta a seguir.  
  
```  
SELECT * FROM $System.DBSchema_Tables   
WHERE TABLE_TYPE = 'SCHEMA'   
ORDER BY TABLE_NAME ASC  
```  
  
> [!NOTE]  
>  Se não houver uma DMV disponível para determinado conjunto de linhas, o servidor retornará o seguinte erro: “O tipo de solicitação \<schemarowset> não foi reconhecido pelo servidor”. Todos os outros erros apontam para problemas com a sintaxe.  
  
|Conjunto de linhas|Description|  
|------------|-----------------|  
|[Conjunto de linhas DBSCHEMA_CATALOGS](../../analysis-services/schema-rowsets/ole-db/dbschema-catalogs-rowset.md)|Retorna uma lista de bancos de dados do Analysis Services na conexão atual.|  
|[Conjunto de linhas de DBSCHEMA_COLUMNS](../../analysis-services/schema-rowsets/ole-db/dbschema-columns-rowset.md)|Retorna uma lista de todas as colunas no banco de dados atual. Você pode usar esta lista para construir uma consulta DMV.|  
|[Conjunto de linhas DBSCHEMA_PROVIDER_TYPES](../../analysis-services/schema-rowsets/ole-db/dbschema-provider-types-rowset.md)|Retorna propriedades sobre os tipos de dados base para os quais o provedor de dados OLE DB oferece suporte.|  
|[Conjunto de linhas DBSCHEMA_TABLES](../../analysis-services/schema-rowsets/ole-db/dbschema-tables-rowset.md)|Retorna uma lista de todas as tabelas no banco de dados atual. Você pode usar esta lista para construir uma consulta DMV.|  
|[Conjunto de linhas DISCOVER_CALC_DEPENDENCY](../../analysis-services/schema-rowsets/xml/discover-calc-dependency-rowset.md)|Retorna uma lista de colunas e tabelas usadas em um modelo que têm dependências em outras colunas e tabelas.|  
|[Conjunto de linhas DISCOVER_COMMAND_OBJECTS](../../analysis-services/schema-rowsets/xml/discover-command-objects-rowset.md)|Fornece informações de uso de recurso e atividade sobre objetos em uso pelo comando referenciado.|  
|[Conjunto de linhas DISCOVER_COMMANDS](../../analysis-services/schema-rowsets/xml/discover-commands-rowset.md)|Fornece informações de uso de recurso e atividade sobre o comando em execução no momento.|  
|[Conjunto de linhas DISCOVER_CONNECTIONS](../../analysis-services/schema-rowsets/xml/discover-connections-rowset.md)|Fornece informações de uso de recurso e atividade sobre conexões abertas com o Analysis Services.|  
|[Conjunto de linhas DISCOVER_CSDL_METADATA](../../analysis-services/schema-rowsets/xml/discover-csdl-metadata-rowset.md)|Retorna informações sobre um modelo de tabela.<br /><br /> Requer a adição de SYSTEMRESTRICTSCHEMA e parâmetros adicionais.|  
|[Conjunto de linhas DISCOVER_DB_CONNECTIONS](../../analysis-services/schema-rowsets/xml/discover-db-connections-rowset.md)|Fornece informações de uso de recurso e atividade sobre conexões abertas do Analysis Services com fontes de dados externas, por exemplo, durante o processamento ou a importação.|  
|[Conjunto de linhas DISCOVER_DIMENSION_STAT](../../analysis-services/schema-rowsets/xml/discover-dimension-stat-rowset.md)|Retorna os atributos em uma dimensão ou colunas em uma tabela, dependendo do tipo de modelo.|  
|[Conjunto de linhas DISCOVER_ENUMERATORS](../../analysis-services/schema-rowsets/xml/discover-enumerators-rowset.md)|Retorna metadados sobre os enumeradores com suporte para uma fonte de dados específica.|  
|[Conjunto de linhas DISCOVER_INSTANCES](../../analysis-services/schema-rowsets/ole-db-olap/discover-instances-rowset.md)|Retorna informações sobre a instância especificada.<br /><br /> Requer a adição de SYSTEMRESTRICTSCHEMA e parâmetros adicionais.|  
|[Conjunto de linhas DISCOVER_JOBS](../../analysis-services/schema-rowsets/xml/discover-jobs-rowset.md)|Retorna informações sobre os trabalhos atuais.|  
|[Conjunto de linhas DISCOVER_KEYWORDS &#40;XMLA&#41;](../../analysis-services/schema-rowsets/xml/discover-keywords-rowset-xmla.md)|Retorna a lista de palavras-chave reservadas.|  
|[Conjunto de linhas DISCOVER_LITERALS](../../analysis-services/schema-rowsets/xml/discover-literals-rowset.md)|Retorna a lista de literais, incluindo tipos de dados e valores, com suporte do XMLA.|  
|[Conjunto de linhas DISCOVER_LOCKS](../../analysis-services/schema-rowsets/xml/discover-locks-rowset.md)|Retorna um instantâneo dos bloqueios usados em um determinado momento.|  
|[Conjunto de linhas DISCOVER_MEMORYGRANT](../../analysis-services/schema-rowsets/xml/discover-memorygrant-rowset.md)|Retorna informações sobre a memória alocada pelo Analysis Services na inicialização.|  
|[Conjunto de linhas DISCOVER_MEMORYUSAGE](../../analysis-services/schema-rowsets/xml/discover-memoryusage-rowset.md)|Mostra o uso de memória por objetos específicos.|  
|[Conjunto de linhas DISCOVER_OBJECT_ACTIVITY](../../analysis-services/schema-rowsets/xml/discover-object-activity-rowset.md)|Relata a atividade de objeto desde a última inicialização do serviço.|  
|[Conjunto de linhas DISCOVER_OBJECT_MEMORY_USAGE](../../analysis-services/schema-rowsets/xml/discover-object-memory-usage-rowset.md)|Relata o consumo de memória por objeto.|  
|[Conjunto de linhas DISCOVER_PARTITION_DIMENSION_STAT](../../analysis-services/schema-rowsets/xml/discover-partition-dimension-stat-rowset.md)|Fornece informações sobre os atributos em uma dimensão.<br /><br /> Requer a adição de SYSTEMRESTRICTSCHEMA e parâmetros adicionais.|  
|[Conjunto de linhas DISCOVER_PARTITION_STAT](../../analysis-services/schema-rowsets/xml/discover-partition-stat-rowset.md)|Fornece informações sobre as partições em uma dimensão, uma tabela ou um grupo de medidas.<br /><br /> Requer a adição de SYSTEMRESTRICTSCHEMA e parâmetros adicionais.|  
|[Conjunto de linhas DISCOVER_PERFORMANCE_COUNTERS](../../analysis-services/schema-rowsets/xml/discover-performance-counters-rowset.md)|Lista as colunas usadas em um contador de desempenho.<br /><br /> Requer a adição de SYSTEMRESTRICTSCHEMA e parâmetros adicionais.|  
|[Conjunto de linhas DISCOVER_PROPERTIES](../../analysis-services/schema-rowsets/xml/discover-properties-rowset.md)|Retorna informações sobre propriedades com suporte pelo XMLA para a fonte de dados especificada.|  
|[Conjunto de linhas DISCOVER_SCHEMA_ROWSETS](../../analysis-services/schema-rowsets/xml/discover-schema-rowsets-rowset.md)|Retorna os nomes, as restrições, a descrição e outras informações de todos os valores de enumeração com suporte do XMLA.|  
|[Conjunto de linhas DISCOVER_SESSIONS](../../analysis-services/schema-rowsets/xml/discover-sessions-rowset.md)|Relata as sessões ativas, incluindo o usuário e a duração da sessão.|  
|[Conjunto de linhas DISCOVER_STORAGE_TABLE_COLUMN_SEGMENTS](../../analysis-services/schema-rowsets/xml/discover-storage-table-column-segments-rowset.md)|Fornece informações em nível de coluna e segmento sobre tabelas de armazenamento usadas por um banco de dados do Analysis Services executado no modo de Tabela ou SharePoint.|  
|[Conjunto de linhas DISCOVER_STORAGE_TABLE_COLUMNS](../../analysis-services/schema-rowsets/xml/discover-storage-table-columns-rowset.md)|Permite ao cliente determinar a atribuição de colunas para tabelas de armazenamento usadas por um banco de dados do Analysis Services executado no modo de Tabela ou SharePoint.|  
|[Conjunto de linhas DISCOVER_STORAGE_TABLES](../../analysis-services/schema-rowsets/xml/discover-storage-tables-rowset.md)|Retorna informações sobre as tabelas usadas para armazenamento de modelos em um banco de dados modelo de Tabela.|  
|[Conjunto de linhas DISCOVER_TRACE_COLUMNS](../../analysis-services/schema-rowsets/xml/discover-trace-columns-rowset.md)|Retorna uma descrição XML das colunas disponíveis em um rastreamento.|  
|[Conjunto de linhas DISCOVER_TRACE_DEFINITION_PROVIDERINFO](../../analysis-services/schema-rowsets/xml/discover-trace-definition-providerinfo-rowset.md)|Retorna informações de nome e versão do provedor.|  
|[Conjunto de linhas DISCOVER_TRACE_EVENT_CATEGORIES](../../analysis-services/schema-rowsets/xml/discover-trace-event-categories-rowset.md)|Retorna uma lista de categorias disponíveis.|  
|[Conjunto de linhas DISCOVER_TRACES](../../analysis-services/schema-rowsets/xml/discover-traces-rowset.md)|Retorna uma lista de rastreamentos em execução ativa na conexão atual.|  
|[Conjunto de linhas DISCOVER_TRANSACTIONS](../../analysis-services/schema-rowsets/xml/discover-transactions-rowset.md)|Retorna uma lista de transações em execução ativa na conexão atual.|  
|[Conjunto de linhas DISCOVER_XEVENT_TRACE_DEFINITION](../Topic/DISCOVER_XEVENT_TRACE_DEFINITION%20Rowset.md)|Retorna uma lista de rastreamentos xevent em execução ativa na conexão atual.|  
|[Conjunto de linhas de DMSCHEMA_MINING_COLUMNS](../../analysis-services/schema-rowsets/data-mining/dmschema-mining-columns-rowset.md)|Lista as colunas individuais de todos os modelos de mineração disponíveis na conexão atual.|  
|[Conjunto de linhas DMSCHEMA_MINING_FUNCTIONS](../../analysis-services/schema-rowsets/data-mining/dmschema-mining-functions-rowset.md)|Retorna uma lista de funções com suporte dos algoritmos de mineração de dados no servidor.|  
|[Conjunto de linhas DMSCHEMA_MINING_MODEL_CONTENT](../../analysis-services/schema-rowsets/data-mining/dmschema-mining-model-content-rowset.md)|Retorna um conjunto de linhas que consiste em colunas que descrevem o modelo atual.|  
|[Conjunto de linhas DMSCHEMA_MINING_MODEL_CONTENT_PMML](../../analysis-services/schema-rowsets/data-mining/dmschema-mining-model-content-pmml-rowset.md)|Retorna um conjunto de linhas que consiste em colunas que descrevem o modelo atual no formato PMML.|  
|[Conjunto de linhas DMSCHEMA_MINING_MODEL_XML](../../analysis-services/schema-rowsets/data-mining/dmschema-mining-model-xml-rowset.md)|Retorna um conjunto de linhas que consiste em colunas que descrevem o modelo atual no formato PMML.|  
|[Conjunto de linhas DMSCHEMA_MINING_MODELS](../../analysis-services/schema-rowsets/data-mining/dmschema-mining-models-rowset.md)|Retorna uma lista dos modelos de mineração no banco de dados atual.|  
|[Conjunto de linhas DMSCHEMA_MINING_SERVICE_PARAMETERS](../../analysis-services/schema-rowsets/data-mining/dmschema-mining-service-parameters-rowset.md)|Retorna uma lista dos parâmetros para os algoritmos no servidor.|  
|[Conjunto de linhas DMSCHEMA_MINING_SERVICES](../../analysis-services/schema-rowsets/data-mining/dmschema-mining-services-rowset.md)|Fornece uma lista dos algoritmos de mineração de dados disponíveis no servidor.|  
|[Conjunto de linhas DMSCHEMA_MINING_STRUCTURE_COLUMNS](../../analysis-services/schema-rowsets/data-mining/dmschema-mining-structure-columns-rowset.md)|Retorna uma lista de todas as colunas de todos os modelos de mineração disponíveis na conexão atual.|  
|[Conjunto de linhas DMSCHEMA_MINING_STRUCTURES](../../analysis-services/schema-rowsets/data-mining/dmschema-mining-structures-rowset.md)|Lista as estruturas de mineração disponíveis na conexão atual.|  
|[Conjunto de linhas MDSCHEMA_CUBES](../../analysis-services/schema-rowsets/ole-db-olap/mdschema-cubes-rowset.md)|Retorna informações sobre os cubos definidos no banco de dados atual.|  
|[Conjunto de linhas MDSCHEMA_DIMENSIONS](../../analysis-services/schema-rowsets/ole-db-olap/mdschema-dimensions-rowset.md)|Retorna informações sobre as dimensões definidas no banco de dados atual.|  
|[Conjunto de linhas MDSCHEMA_FUNCTIONS](../../analysis-services/schema-rowsets/ole-db-olap/mdschema-functions-rowset.md)|Retorna uma lista das funções disponíveis para aplicativos cliente conectados ao banco de dados.|  
|[Conjunto de linhas MDSCHEMA_HIERARCHIES](../../analysis-services/schema-rowsets/ole-db-olap/mdschema-hierarchies-rowset.md)|Retorna informações sobre as hierarquias definidas no banco de dados atual.|  
|[Conjunto de linhas MDSCHEMA_INPUT_DATASOURCES](../../analysis-services/schema-rowsets/ole-db-olap/mdschema-input-datasources-rowset.md)|Retorna informações sobre os objetos de fonte de dados definidos no banco de dados atual.|  
|[Conjunto de linhas MDSCHEMA_KPIS](../../analysis-services/schema-rowsets/ole-db-olap/mdschema-kpis-rowset.md)|Retorna informações sobre os KPIs definidos no banco de dados atual.|  
|[Conjunto de linhas MDSCHEMA_LEVELS](../../analysis-services/schema-rowsets/ole-db-olap/mdschema-levels-rowset.md)|Retorna informações sobre os níveis nas hierarquias definidos no banco de dados atual.|  
|[Conjunto de linhas MDSCHEMA_MEASUREGROUP_DIMENSIONS](../../analysis-services/schema-rowsets/ole-db-olap/mdschema-measuregroup-dimensions-rowset.md)|Lista a dimensão dos grupos de medidas.|  
|[Conjunto de linhas MDSCHEMA_MEASURESGROUPS](../../analysis-services/schema-rowsets/ole-db-olap/mdschema-measuregroups-rowset.md)|Retorna uma lista dos grupos de medidas na conexão atual.|  
|[Conjunto de linhas MDSCHEMA_MEASURES](../../analysis-services/schema-rowsets/ole-db-olap/mdschema-measures-rowset.md)|Retorna uma lista de medidas na conexão atual.|  
|[Conjunto de linhas MDSCHEMA_MEMBERS](../../analysis-services/schema-rowsets/ole-db-olap/mdschema-members-rowset.md)|Retorna uma lista de todos os membros na conexão atual, organizada por banco de dados, cubo e dimensão.|  
|[Conjunto de linhas MDSCHEMA_PROPERTIES](../../analysis-services/schema-rowsets/ole-db-olap/mdschema-properties-rowset.md)|Retorna um nome totalmente qualificado de cada propriedade, junto com o tipo de propriedade, o tipo de dados e outros metadados.|  
|[Conjunto de linhas MDSCHEMA_SETS](../../analysis-services/schema-rowsets/ole-db-olap/mdschema-sets-rowset.md)|Retorna uma lista de conjuntos definidos na conexão atual.|  
  
## Consulte também  
 [Guia de operação do SQL Server 2008 R2 Analysis Services](http://go.microsoft.com/fwlink/?LinkID=225539&clcid=0x409)   
 [Novo System.Discover_Object_Activity](http://go.microsoft.com/fwlink/?linkid=221322)   
 [Nova função SYSTEMRESTRICTEDSCHEMA para conjuntos de linhas restritos e DMVs](http://go.microsoft.com/fwlink/?LinkId=231885)  
  
  