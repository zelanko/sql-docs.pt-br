---
title: Transformações do Integration Services | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
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
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: b283f179a6d9ad79e90e4abdfc2e5af0c199d4dd
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62900255"
---
# <a name="integration-services-transformations"></a>Transformações do Integration Services
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] transformações são os componentes no fluxo de dados de um pacote que agregam, mesclam, distribuem e modificam dados. As transformações também podem executar operações de pesquisa e gerar conjuntos de dados de exemplo. Esta seção descreve as transformações que o [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] inclui e explica como elas funcionam.  
  
## <a name="business-intelligence-transformations"></a>Transformações de Business Intelligence  
 As transformações a seguir executam operações de business intelligence, como limpeza de dados, mineração de texto e execução de consultas de previsão de mineração de dados.  
  
|Transformation|Descrição|  
|--------------------|-----------------|  
|[Transformação Dimensão de Alteração Lenta](slowly-changing-dimension-transformation.md)|A transformação que configura a atualização de uma dimensão variável lenta.|  
|[Transformação Agrupamento Difuso](fuzzy-grouping-transformation.md)|A transformação que padroniza valores em dados de coluna.|  
|[Transformação Pesquisa Difusa](lookup-transformation.md)|A transformação que pesquisa valores em uma tabela de referência usando uma correspondência difusa.|  
|[Transformação Extração de Termos](term-extraction-transformation.md)|A transformação que extrai termos do texto.|  
|[Transformação Pesquisa de Termo](term-lookup-transformation.md)|A transformação que pesquisa termos em uma tabela de referência e considera os termos extraídos do texto.|  
|[Transformação Consulta de Mineração de Dados](data-mining-query-transformation.md)|A transformação que executa consultas de previsão de mineração de dados.|  
|[Transformação de Limpeza DQS](dqs-cleansing-transformation.md)|A transformação que corrige dados de uma fonte de dados conectada aplicando regras que foram criadas para a fonte de dados.|  
  
## <a name="row-transformations"></a>Transformações de linha  
 A coluna de atualização de transformações a seguir avalia e cria novas colunas. A transformação é aplicada a cada linha na entrada de transformação.  
  
|Transformation|Descrição|  
|--------------------|-----------------|  
|[Transformação Mapas de Caracteres](character-map-transformation.md)|A transformação que se aplica às funções de cadeia para dados de caractere.|  
|[Transformação Copiar Coluna](copy-column-transformation.md)|A transformação que adiciona cópias de colunas de entrada à saída de transformação.|  
|[Transformação Conversão de Dados](data-conversion-transformation.md)|A transformação que converte o tipo de dados de uma coluna a um tipo de dados diferente.|  
|[Transformação Coluna Derivada](derived-column-transformation.md)|A transformação que popula colunas com os resultados de expressões.|  
|[Transformação Exportar Colunas](export-column-transformation.md)|A transformação que insere dados de um fluxo de dados em um arquivo.|  
|[Transformação Importar Coluna](import-column-transformation.md)|A transformação que lê dados de um arquivo e os adiciona a um fluxo de dados.|  
|[Componente Script](script-component.md)|A transformação que usa script para extrair, transformar ou carregar dados.|  
|[Transformação Comando OLE DB](ole-db-command-transformation.md)|A transformação que executa comandos SQL para cada linha em um fluxo de dados.|  
  
## <a name="rowset-transformations"></a>Transformações de conjunto de linhas  
 As transformações a seguir criam novos conjuntos de linhas. O conjunto de linhas pode incluir valores agregados e classificados, conjuntos de linhas de exemplo, ou conjuntos de linhas dinâmicas e não dinâmicas.  
  
|Transformation|Descrição|  
|--------------------|-----------------|  
|[Transformação Agregação](aggregate-transformation.md)|A transformação que executa agregações como AVERAGE, SUM e COUNT.|  
|[Transformação Classificação](sort-transformation.md)|A transformação que classifica dados.|  
|[Transformação Amostragem Percentual](percentage-sampling-transformation.md)|A transformação que cria um conjunto de dados de exemplo usando uma porcentagem para especificar o tamanho do exemplo.|  
|[Transformação Amostragem de Linhas](row-sampling-transformation.md)|A transformação que cria um conjunto de dados de exemplo especificando o número de linhas no exemplo.|  
|[Transformação Dinâmica](pivot-transformation.md)|A transformação que cria uma versão menos normalizada de uma tabela normalizada.|  
|[Transformação não dinâmica](unpivot-transformation.md)|A transformação que cria uma versão mais normalizada de uma tabela não normalizada.|  
  
## <a name="split-and-join-transformations"></a>Transformações de divisão e junção  
 As seguintes transformações distribuem linhas para saídas diferentes, cria cópias de entradas de transformação, une várias entradas em uma saída e executa operações de pesquisa.  
  
|Transformation|Descrição|  
|--------------------|-----------------|  
|[Transformação Divisão Condicional](conditional-split-transformation.md)|A transformação que roteia linhas de dados para saídas diferentes.|  
|[Transformação Difusão Seletiva](multicast-transformation.md)|A transformação que distribui conjuntos de dados para várias saídas.|  
|[Transformação Unir Tudo](union-all-transformation.md)|A transformação que mescla vários conjuntos de dados.|  
|[Transformação Mesclar](merge-transformation.md)|A transformação que mescla dois conjuntos de dados classificados.|  
|[Transformação Junção de Mesclagem](merge-join-transformation.md)|A transformação que une dois conjuntos de dados usando uma junção FULL, LEFT ou INNER.|  
|[Transformação Pesquisa](lookup-transformation.md)|A transformação que pesquisa valores em uma tabela de referência usando uma correspondência exata.|  
|[Transformação Cache](cache-transform.md)|A transformação que grava dados de uma fonte de dados conectada no fluxo de dados em um gerenciador de conexões de cache que salva os dados em um arquivo de cache. A transformação Pesquisa executa pesquisas nos dados no arquivo de cache.|  
|[Transformação de BDD (Balanced Data Distributor)](balanced-data-distributor-transformation.md)|A transformação distribui uniformemente buffers de linhas de entrada em saídas em threads separados para melhorar o desempenho de pacotes SSIS que são executados em servidores com vários núcleos e vários processadores.|  
  
## <a name="auditing-transformations"></a>Transformações Auditoria  
 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] inclui as transformações a seguir para adicionar informações de auditoria e linhas de contagem.  
  
|Transformation|Descrição|  
|--------------------|-----------------|  
|[Transformação Auditoria](audit-transformation.md)|A transformação que cria informações sobre o ambiente disponível para o fluxo de dados em um pacote.|  
|[Transformação Contagem de Linhas](row-count-transformation.md)|A transformação que conta as linhas conforme se move por elas e armazena a contagem final em uma variável.|  
  
## <a name="custom-transformations"></a>Transformações personalizadas  
 Você também pode gravar transformações personalizadas. Para obter mais informações, consulte [Desenvolvendo um componente de transformação personalizado com saídas síncronas](../../extending-packages-custom-objects-data-flow-types/developing-a-custom-transformation-component-with-synchronous-outputs.md) e [Desenvolvendo um componente de transformação personalizado com saídas assíncronas](../../extending-packages-custom-objects-data-flow-types/developing-a-custom-transformation-component-with-asynchronous-outputs.md).  
  
  
