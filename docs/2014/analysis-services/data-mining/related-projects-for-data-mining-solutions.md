---
title: Projetos relacionados para soluções de mineração de dados | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: dc26489a-4c27-4b89-8215-6d245427c350
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: af175693a93535b21b399cf4916ca4291fc94dfa
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66082985"
---
# <a name="related-projects-for-data-mining-solutions"></a>Projetos relacionados a soluções de mineração de dados
  O mínimo que é necessário para uma solução de mineração de dados é o projeto de mineração de dados que define fontes de dados, exibições da fonte de dados, estruturas de mineração e modelos de mineração. Porém, quando os modelos de mineração de dados são usados no processo diário de tomadas de decisão, é importante que a mineração de dados esteja integrada com outra parte de uma solução de análises preditiva, que pode incluir estes processos e componentes:  
  
-   Preparação e seleção de dados e variáveis. Inclui limpeza de dados, gerenciamento de metadados e integração de várias fontes de dados e a conversão, fusão e carregamento de dados em um data warehouse.  
  
-   Relatório de análise, apresentação de previsões, e auditoria/acompanhamento de atividades de mineração de dados.  
  
-   Usando modelos multidimensionais ou modelos de tabela para explorar resultados.  
  
-   Refinamento da solução de mineração de dados para dar suporte a novos dados ou alterações na infraestrutura de suporte dirigida pela análise atual.  
  
 Este tópico descreve os outros recursos do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] que geralmente fazem parte de uma solução de análises preditiva, para dar suporte aos processos de preparação de dados e mineração de dados, ou para dar suporte aos usuários fornecendo ferramentas para análise e ação.  
  
 [Serviços de Integração](#bkmk_SSIS)  
  
 [Reporting Services](#bkmk_SSRS)  
  
 [Serviço de qualidade de dados](#bkmk_DQSetc)  
  
 [Pesquisa de texto completo](#bkmk_FTSetc)  
  
 [Indexação semântica](#bkmk_SemSearch)  
  
##  <a name="bkmk_SSIS"></a>SQL Server Integration Services  
 
  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] fornece componentes e recursos que são necessários para a preparação de dados e o treinamento de fases de um projeto de mineração de dados. Embora você possa executar muitas limpezas de dados ou tarefas de preparação usando outras ferramentas, como scripts, o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] tem numerosas vantagens para a mineração de dados:  
  
-   Representa tarefas como parte de um fluxo de trabalho que pode ser repetido, automatizado, ramificado e estendido.  
  
-   Fornece amplo suporte para auditoria e vários modos de capturar erros e registrar eventos em log.  
  
     Além de capturar a linhagem de dados, você pode monitorar as alterações aos dados ao longo do pipeline de transformação de dados.  
  
     Você também pode integrar seus fluxos de trabalho de SSIS com os recursos que dão suporte à funcionalidade Change Data Capture no SQL Server.  
  
-   A mineração de dados pode ser incorporada no fluxo de trabalho do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , para separar dados de entrada inteligentemente em várias tabelas. Por exemplo, você pode usar uma consulta de previsão para dividir novos clientes em grupos diferentes para atingir em uma campanha de envio.  
  
 As listas a seguir fornecem links para os componentes do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que são usados amplamente no suporte à mineração de dados.  
  
 **Componentes de fluxo de controle**  
  
-   [Tarefa Executar DDL do Analysis Services](../../integration-services/control-flow/analysis-services-execute-ddl-task.md)  
  
-   [Tarefa Processamento do Analysis Services](../../integration-services/control-flow/analysis-services-processing-task.md)  
  
-   [Tarefa Controle de CDC](../../integration-services/control-flow/cdc-control-task.md)  
  
-   [Data Cleansing](../../data-quality-services/data-cleansing.md)  
  
-   [Data Mining Query Task](../../integration-services/control-flow/data-mining-query-task.md)  
  
-   [Tarefa Criação de Perfil de Dados](../../integration-services/control-flow/data-profiling-task.md)  
  
 **Componentes de fluxo de dados**  
  
-   [Componentes de fluxo CDC](../../integration-services/data-flow/cdc-flow-components.md)  
  
-   [Transformação Divisão Condicional](../../integration-services/data-flow/transformations/conditional-split-transformation.md)  
  
-   [transformação Conversão de Dados](../../integration-services/data-flow/transformations/data-conversion-transformation.md)  
  
-   [Destino de treinamento do modelo de mineração de dados](../../integration-services/data-flow/data-mining-model-training-destination.md)  
  
-   [Transformação Consulta de Mineração de Dados](../../integration-services/data-flow/transformations/data-mining-query-transformation.md)  
  
-   [Transformação Coluna Derivada](../../integration-services/data-flow/transformations/derived-column-transformation.md)  
  
-   [transformação Amostragem Percentual](../../integration-services/data-flow/transformations/percentage-sampling-transformation.md)  
  
-   [Transformação Extração de Termos](../../integration-services/data-flow/transformations/term-extraction-transformation.md)  
  
-   [transformação Pesquisa de Termos](../../integration-services/data-flow/transformations/lookup-transformation.md)  
  
##  <a name="bkmk_SSRS"></a>SQL Server Reporting Services  
 Embora o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] não seja visto normalmente como um componente crítico de soluções de mineração de dados, ele fornece os recursos a seguir que são úteis para a apresentação de soluções de mineração de dados.  
  
-   Integração de dados de várias origens em relatórios complexos. Crie consultas em relação ao conteúdo do modelo para analistas, e relatórios que mostram previsões e tendências para usuários finais.  
  
-   A capacidade de criar um relatório que permite que os usuários consultem diretamente um modelo de mineração existente.  
  
-   Integração com o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], para dar suporte ao detalhamento e à exploração de dimensões de mineração de dados, e cubos de mineração de dados criados de modelos OLAP.  
  
-   parametrização e formatação de recursos que estão disponíveis no [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
 Para obter informações sobre como usar o Reporting Services com consultas DMX como fonte de dados, consulte esses links:  
  
 [Recuperar dados de um modelo de mineração de dados &#40;DMX&#41; &#40;SSRS&#41;](../../reporting-services/report-data/retrieve-data-from-a-data-mining-model-dmx-ssrs.md)  
  
 [Interface de usuário do Designer de Consulta DMX do Analysis Services](../../reporting-services/report-data/analysis-services-dmx-query-designer-user-interface.md)  
  
 [Analysis Services tipo de conexão para o DMX &#40;SSRS&#41;](../../reporting-services/report-data/analysis-services-connection-type-for-dmx-ssrs.md)  
  
 Porém, não é necessário usar DMX como a fonte de dados. Os componentes do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] para mineração de dados também dão suporte a gravar os resultados de uma consulta de previsão em um banco de dados relacional. Se você tiver um fluxo de trabalho estabelecido para atualizar modelos usando o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], persistir previsões e outros resultados da consulta de mineração de dados para o SQL Server permitirá que você use o [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] para relatório, assim como outras ferramentas que não fazem interface com DMX.  
  
 Para obter mais informações sobre como usar o Reporting Services como a camada de apresentação para fontes de dados, consulte [Integrating Reporting Services into Applications](../../reporting-services/application-integration/integrating-reporting-services-into-applications.md).  
  
##  <a name="bkmk_DQSetc"></a>Data Quality Services  
 O DQS (Data Quality Services) é novidade no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Como os problemas de dados podem tornar a mineração de dados impossível, os mineradores de dados que executam análises repetidas ou que trabalham em organizações grandes com fontes de dados complexas podem descobrir que um projeto de dados bem planejado usando DQS é uma solução mais confiável para dar suporte à mineração de dados do que limpar dados ad hoc usando [!INCLUDE[tsql](../../includes/tsql-md.md)] ou outros scripts.  
  
 Os recursos de DQS a seguir devem ser considerados para preparação de dados e integridade de dados em uma solução de mineração de dados.  
  
 **Um processo de limpeza de dados assistido por computador que analisa dados de origem e propõe alterações.**  
 O DQS pode comparar dados de origem com dados de referência baseados em nuvem mantidos e garantidos por provedores de qualidade de dados.  
  
 O DQS também pode analisar dados de origem brutos e criar uma base de conhecimento usando os dados de usuário. Os dados processados são categorizados e então exibidos para o usuário para processamento posterior. O processo de limpeza é interativo, ou seja, o administrador de dados pode aprovar, rejeitar ou modificar os dados propostos pelo processo de limpeza de dados assistido por computador.  
  
 O resultado do processo é uma base de conhecimento que você pode melhorar continuamente ou reutilizar em várias fases do aprimoramento de dados.  
  
 Para obter mais informações, consulte [Data Cleansing](../../data-quality-services/data-cleansing.md).  
  
 **Um processo de correspondência assistido por computador que analisa dados de origem e propõe alterações.**  
 Para impedir a duplicação de dados, você pode realizar limpeza adicional da fonte de dados, para identificar correspondências exatas e aproximadas. Estes componentes permitem especificar as regras compatíveis e os limites aos quais aplicá-los.  
  
 Ao localizar correspondência de dados, você pode remover duplicatas que podem ser um problema para a mineração de dados. A eliminação de duplicação de dados não é automática; o administrador de dados ou profissional de TI deve verificar o conhecimento na base de conhecimento e as alterações a serem feitas nos dados.  
  
 Depois de criar o projeto de DQS inicial, você pode automatizar muitas das tarefas usando os componentes do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
 Para obter mais informações, consulte [Data Matching](../../data-quality-services/data-matching.md).  
  
 Ao executar atividades de limpeza e correspondência em um projeto de qualidade de dados, você pode obter estatísticas em tempo real e informações sobre os dados que estão sendo processados por DQS. A criação de perfil de dados ajuda a avaliar até que ponto a limpeza ou a correspondência de dados ajudaram a melhorar a qualidade dos dados, e entender as alterações que foram feitas. Para obter mais informações sobre criação de perfil de dados e notificações, consulte [Data Profiling and Notifications in DQS](../../data-quality-services/data-profiling-and-notifications-in-dqs.md).  
  
 **Uma base de dados de conhecimento que representa três tipos de conhecimento: conhecimento pronto para uso, conhecimento gerado pelo servidor DQS e conhecimento gerado pelo usuário.**  
 Depois de criar a base de conhecimento, você pode usá-la iterativamente para limpar e verificar outros dados.  
  
 Você pode importar novos dados nos dados da base de conhecimento de várias origens, sejam dados limpos conhecidos de provedores de referência ou dados brutos que são correspondentes a dados existentes na base de conhecimento.  
  
 Para obter informações detalhadas sobre a atividade de limpeza em um projeto de qualidade de dados, consulte Limpeza de Dados (DQS).  
  
 Você também pode aplicar o conhecimento na base de conhecimento a outras origens, para realizar limpeza de dados dentro de outros processos. Essa limpeza de dados pode ajudar a identificar erros de entrada de usuário, corrupção durante a transmissão ou armazenamento ou definições incompatíveis de dicionários de dados.  
  
 Para obter mais informações, consulte [DQS Knowledge Bases and Domains](../../data-quality-services/dqs-knowledge-bases-and-domains.md).  
  
##  <a name="bkmk_FTSetc"></a>Pesquisa de texto completo  
 A Pesquisa de Texto Completo no SQL Server permite que aplicativos e usuários executem consultas de texto completo em dados baseados em caracteres nas tabelas do SQL Server. Quando a pesquisa de texto completo está habilitada, você pode realizar pesquisas em dados de texto que são aprimorados por regras específicas de idioma sobre as várias formas de uma palavra ou frase. Você também pode configurar os critérios da pesquisa, como a distância entre vários termos e usar funções para restringir os resultados que são retornados em ordem de probabilidade.  
  
 Como as consultas de texto completo são um recurso fornecido pelo mecanismo de SQL Server, você pode criar consultas parametrizadas, gerar conjuntos de dados personalizados ou vetores de termos usando recursos de pesquisa de texto completo em uma fonte de dados de texto, e usar estas fontes em mineração de dados.  
  
 Para obter mais informações sobre como as consultas de texto completo interagem com o índice de texto completo, consulte [Consulta com pesquisa de texto completo](../../relational-databases/search/query-with-full-text-search.md).  
  
 Uma vantagem de usar os recursos de pesquisa de texto completo do SQL Server é que você pode aproveitar a inteligência linguística que está contida nos separadores de palavras e nos lematizadores enviados para todos os idiomas do SQL Server. Usando os separadores de palavras e lematizadores fornecidos, você pode garantir que as palavras sejam separadas usando os caracteres apropriados para cada idioma, e que não sejam negligenciados os sinônimos baseados em diacríticos ou variações ortográficas (como os vários formatos de números em japonês).  
  
 Além da inteligência linguística que governa os limites de palavras, os lematizadores para cada idioma podem reduzir variantes de uma palavra para um único termo, baseado no conhecimento das regras para conjugação e variação ortográfica naquele idioma. As regras para análise linguística diferem para cada idioma e são desenvolvidas com base em pesquisa extensa em corpus da vida real.  
  
 Para obter mais informações, veja [Configurar e gerenciar separadores de palavras e lematizadores para pesquisa](../../relational-databases/search/configure-and-manage-word-breakers-and-stemmers-for-search.md).  
  
 A versão de uma palavra que está armazenada depois que a indexação de texto completo seja um token em uma forma compactada. As consultas subsequentes para o índice de texto completo geram várias formas flexivas de uma palavra específica baseada nas regras desse idioma, para assegurar que todas as correspondências prováveis sejam feitas. Por exemplo, embora o token que é armazenado possa ser "Run", o mecanismo de consulta também procura os termos "Running", "Executed" e "Runner", pois eles são regularmente derivadas de morfológicas variações da palavra raiz "Run".  
  
 Você também pode criar e compilar um dicionário de sinônimos de usuário para armazenar sinônimos e habilitar melhores resultados de pesquisa ou categorização de termos. Ao desenvolver um dicionário de sinônimos personalizado para seus dados de texto completo, você pode efetivamente ampliar o escopo de consultas de texto completo baseadas nesses dados. Para obter mais informações, veja [Configurar e gerenciar arquivos de dicionário de sinônimos para pesquisa de texto completo](../../relational-databases/search/configure-and-manage-thesaurus-files-for-full-text-search.md).  
  
 Os requisitos para usar pesquisa de texto completo incluem o seguinte:  
  
-   O administrador de banco de dados deve criar um índice de texto completo na tabela.  
  
-   Só é permitido um índice de texto completo por tabela.  
  
-   Cada coluna que você indexa deve ter uma chave exclusiva.  
  
-   A indexação de texto completo tem suporte somente para colunas com esses tipos de dados: char, varchar, nchar, nvarchar, text, ntext, image, xml, varbinary e varbinary(max). Se a coluna for varbinary, varbinary(max), image ou xml, você deve especificar a extensão de arquivo do documento indexável (.doc, .pdf, .xls, e assim sucessivamente), em uma coluna de tipo separada.  
  
##  <a name="bkmk_SemSearch"></a>Indexação semântica  
 A pesquisa semântica é criada com os recursos de pesquisa de texto completo existentes no SQL Server, mas usa recursos e estatísticas adicionais para habilitar cenários como extração de palavra-chave automática e descoberta de documentos relacionados. Por exemplo, você pode usar pesquisa semântica para criar uma taxonomia de base para uma organização ou classificar um corpus de documentos. Ou você pode usar a combinação de termos extraídos e pontuações de similaridade de documentos em modelos de clustering ou de árvore de decisão.  
  
 Depois de habilitar a pesquisa semântica com êxito e de ter indexado suas colunas de dados, você pode usar as funções que são fornecidas nativamente com indexação semântica para fazer o seguinte:  
  
-   Retornar frases chave de palavra única com a sua contagem.  
  
-   Retornar documentos que contêm uma frase chave especificada.  
  
-   Retornar pontuações de similaridade e os termos que contribuem para a contagem.  
  
 Para obter mais informações, veja [Localizar frases-chave em documentos com a pesquisa semântica](../../relational-databases/search/find-key-phrases-in-documents-with-semantic-search.md) e [Localizar documentos semelhantes e relacionados com a pesquisa semântica](../../relational-databases/search/find-similar-and-related-documents-with-semantic-search.md).  
  
 Para obter mais informações sobre os objetos de banco de dados que dão suporte à indexação semântica, consulte [Habilitar a pesquisa semântica em tabelas e colunas](../../relational-databases/search/enable-semantic-search-on-tables-and-columns.md).  
  
 Os requisitos para usar pesquisa semântica incluem o seguinte:  
  
-   A pesquisa de texto completo também deve ser habilitada.  
  
-   A instalação dos componentes de pesquisa semântica também cria um banco de dados do sistema especial que não pode ser renomeado, alterado ou substituído.  
  
-   Os documentos que você indexa usando o serviço devem ser armazenados no SQL Server, em qualquer um dos objetos de banco de dados com suporte para indexação de texto completo, inclusive tabelas e exibições indexadas.  
  
-   Nem todos os idiomas de texto completo dão suporte à indexação semântica. Para ver uma lista dos idiomas com suporte, consulte [sys.fulltext_semantic_languages &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-semantic-languages-transact-sql).  
  
## <a name="see-also"></a>Consulte Também  
 [Soluções de modelo multidimensional &#40;SSAS&#41;](../multidimensional-models/multidimensional-model-solutions-ssas.md)   
 [Soluções de modelo de tabela &#40;SSAS de tabela&#41;](../tabular-model-solutions-ssas-tabular.md)  
  
  
