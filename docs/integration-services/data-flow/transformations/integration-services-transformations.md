---
title: Transformações do Integration Services | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- transformations [Integration Services], listed
- transformations [Integration Services], types
- transformations [Integration Services]
- data flow [Integration Services], transformations
- business intelligence transformations [Integration Services]
- join transformations
- split transformations [Integration Services]
- custom transformations [Integration Services]
- row transformations [Integration Services]
- rowset transformations [Integration Services]
ms.assetid: c70c4f6e-82dd-4948-b923-fd5193f67f7e
author: chugugrace
ms.author: chugu
ms.openlocfilehash: ff200828c1204d15f648ec783fe720d86ac22dd1
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86919242"
---
# <a name="integration-services-transformations"></a>Transformações do Integration Services

[!INCLUDE[sqlserver-ssis](../../../includes/applies-to-version/sqlserver-ssis.md)]


  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] transformações são os componentes no fluxo de dados de um pacote que agregam, mesclam, distribuem e modificam dados. As transformações também podem executar operações de pesquisa e gerar conjuntos de dados de exemplo. Esta seção descreve as transformações que o [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] inclui e explica como elas funcionam.  
  
## <a name="business-intelligence-transformations"></a>Transformações de Business Intelligence  
 As transformações a seguir executam operações de business intelligence, como limpeza de dados, mineração de texto e execução de consultas de previsão de mineração de dados.  
  
|Transformação|DESCRIÇÃO|  
|--------------------|-----------------|  
|[Transformação Dimensão de Alteração Lenta](../../../integration-services/data-flow/transformations/slowly-changing-dimension-transformation.md)|A transformação que configura a atualização de uma dimensão variável lenta.|  
|[Transformação Agrupamento Difuso](../../../integration-services/data-flow/transformations/fuzzy-grouping-transformation.md)|A transformação que padroniza valores em dados de coluna.|  
|[Transformação Pesquisa Difusa](../../../integration-services/data-flow/transformations/fuzzy-lookup-transformation.md)|A transformação que pesquisa valores em uma tabela de referência usando uma correspondência difusa.|  
|[Transformação Extração de Termos](../../../integration-services/data-flow/transformations/term-extraction-transformation.md)|A transformação que extrai termos do texto.|  
|[Transformação Pesquisa de Termos](../../../integration-services/data-flow/transformations/term-lookup-transformation.md)|A transformação que pesquisa termos em uma tabela de referência e considera os termos extraídos do texto.|  
|[Transformação Consulta de Mineração de Dados](../../../integration-services/data-flow/transformations/data-mining-query-transformation.md)|A transformação que executa consultas de previsão de mineração de dados.|  
|[Transformação Limpeza DQS](../../../integration-services/data-flow/transformations/dqs-cleansing-transformation.md)|A transformação que corrige dados de uma fonte de dados conectada aplicando regras que foram criadas para a fonte de dados.|  
  
## <a name="row-transformations"></a>Transformações de linha  
 A coluna de atualização de transformações a seguir avalia e cria novas colunas. A transformação é aplicada a cada linha na entrada de transformação.  
  
|Transformação|DESCRIÇÃO|  
|--------------------|-----------------|  
|[Transformação Mapa de Caracteres](../../../integration-services/data-flow/transformations/character-map-transformation.md)|A transformação que se aplica às funções de cadeia para dados de caractere.|  
|[Transformação Copiar Coluna](../../../integration-services/data-flow/transformations/copy-column-transformation.md)|A transformação que adiciona cópias de colunas de entrada à saída de transformação.|  
|[Transformação Conversão de Dados](../../../integration-services/data-flow/transformations/data-conversion-transformation.md)|A transformação que converte o tipo de dados de uma coluna a um tipo de dados diferente.|  
|[Transformação Coluna Derivada](../../../integration-services/data-flow/transformations/derived-column-transformation.md)|A transformação que popula colunas com os resultados de expressões.|  
|[Transformação Exportar Coluna](../../../integration-services/data-flow/transformations/export-column-transformation.md)|A transformação que insere dados de um fluxo de dados em um arquivo.|  
|[Transformação Importar Coluna](../../../integration-services/data-flow/transformations/import-column-transformation.md)|A transformação que lê dados de um arquivo e os adiciona a um fluxo de dados.|  
|[Componente Script](../../../integration-services/data-flow/transformations/script-component.md)|A transformação que usa script para extrair, transformar ou carregar dados.|  
|[Transformação Comando OLE DB](../../../integration-services/data-flow/transformations/ole-db-command-transformation.md)|A transformação que executa comandos SQL para cada linha em um fluxo de dados.|  
  
## <a name="rowset-transformations"></a>Transformações de conjunto de linhas  
 As transformações a seguir criam novos conjuntos de linhas. O conjunto de linhas pode incluir valores agregados e classificados, conjuntos de linhas de exemplo, ou conjuntos de linhas dinâmicas e não dinâmicas.  
  
|Transformação|DESCRIÇÃO|  
|--------------------|-----------------|  
|[Transformação Agregação](../../../integration-services/data-flow/transformations/aggregate-transformation.md)|A transformação que executa agregações como AVERAGE, SUM e COUNT.|  
|[Transformação Classificação](../../../integration-services/data-flow/transformations/sort-transformation.md)|A transformação que classifica dados.|  
|[Transformação Amostragem Percentual](../../../integration-services/data-flow/transformations/percentage-sampling-transformation.md)|A transformação que cria um conjunto de dados de exemplo usando uma porcentagem para especificar o tamanho do exemplo.|  
|[Transformação Amostragem de Linhas](../../../integration-services/data-flow/transformations/row-sampling-transformation.md)|A transformação que cria um conjunto de dados de exemplo especificando o número de linhas no exemplo.|  
|[Transformação Dinâmica](../../../integration-services/data-flow/transformations/pivot-transformation.md)|A transformação que cria uma versão menos normalizada de uma tabela normalizada.|  
|[Transformação não dinâmica](../../../integration-services/data-flow/transformations/unpivot-transformation.md)|A transformação que cria uma versão mais normalizada de uma tabela não normalizada.|  
  
## <a name="split-and-join-transformations"></a>Transformações de divisão e junção  
 As seguintes transformações distribuem linhas para saídas diferentes, cria cópias de entradas de transformação, une várias entradas em uma saída e executa operações de pesquisa.  
  
|Transformação|DESCRIÇÃO|  
|--------------------|-----------------|  
|[Transformação Divisão Condicional](../../../integration-services/data-flow/transformations/conditional-split-transformation.md)|A transformação que roteia linhas de dados para saídas diferentes.|  
|[Transformação Multicast](../../../integration-services/data-flow/transformations/multicast-transformation.md)|A transformação que distribui conjuntos de dados para várias saídas.|  
|[Transformação Unir Tudo](../../../integration-services/data-flow/transformations/union-all-transformation.md)|A transformação que mescla vários conjuntos de dados.|  
|[Transformação Mesclagem](../../../integration-services/data-flow/transformations/merge-transformation.md)|A transformação que mescla dois conjuntos de dados classificados.|  
|[Transformação Junção de Mesclagem](../../../integration-services/data-flow/transformations/merge-join-transformation.md)|A transformação que une dois conjuntos de dados usando uma junção FULL, LEFT ou INNER.|  
|[Transformação Pesquisa](../../../integration-services/data-flow/transformations/lookup-transformation.md)|A transformação que pesquisa valores em uma tabela de referência usando uma correspondência exata.|  
|[Transformação Cache](../../../integration-services/data-flow/transformations/cache-transform.md)|A transformação que grava dados de uma fonte de dados conectada no fluxo de dados em um gerenciador de conexões de cache que salva os dados em um arquivo de cache. A transformação Pesquisa executa pesquisas nos dados no arquivo de cache.|  
|[Transformação Distribuidor de Dados Equilibrado](../../../integration-services/data-flow/transformations/balanced-data-distributor-transformation.md)|A transformação distribui uniformemente buffers de linhas de entrada em saídas em threads separados para melhorar o desempenho de pacotes SSIS que são executados em servidores com vários núcleos e vários processadores.|  
  
## <a name="auditing-transformations"></a>Transformações Auditoria  
 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] inclui as transformações a seguir para adicionar informações de auditoria e linhas de contagem.  
  
|Transformação|DESCRIÇÃO|  
|--------------------|-----------------|  
|[Transformação Auditoria](../../../integration-services/data-flow/transformations/audit-transformation.md)|A transformação que cria informações sobre o ambiente disponível para o fluxo de dados em um pacote.|  
|[Transformação Contagem de Linhas](../../../integration-services/data-flow/transformations/row-count-transformation.md)|A transformação que conta as linhas conforme se move por elas e armazena a contagem final em uma variável.|  
  
## <a name="custom-transformations"></a>Transformações personalizadas  
 Você também pode gravar transformações personalizadas. Para obter mais informações, consulte [Desenvolvendo um componente de transformação personalizado com saídas síncronas](../../../integration-services/extending-packages-custom-objects-data-flow-types/developing-a-custom-transformation-component-with-synchronous-outputs.md) e [Desenvolvendo um componente de transformação personalizado com saídas assíncronas](../../../integration-services/extending-packages-custom-objects-data-flow-types/developing-a-custom-transformation-component-with-asynchronous-outputs.md).  
  
  
