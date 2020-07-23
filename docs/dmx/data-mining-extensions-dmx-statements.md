---
title: Referência de instrução DMX (Data Mining Extensions) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 1b8fe4c8a83eaf56aea70abc810e7dc45f35eebb
ms.sourcegitcommit: 205de8fa4845c491914902432791bddf11002945
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/23/2020
ms.locfileid: "86971764"
---
# <a name="data-mining-extensions-dmx-statements"></a>Instruções (DMX) de extensões de mineração de dados
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  Trabalhar com modelos de Data Mining no [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] envolve as seguintes tarefas principais:  
  
-   Criando estruturas de mineração e modelos de mineração  
  
-   Processando estruturas de mineração e modelos de mineração  
  
-   Excluindo ou descartando estruturas ou modelos de mineração  
  
-   Copiando modelos de mineração  
  
-   Pesquisando modelos de mineração  
  
-   Prevendo segundo modelos de mineração  
  
 Use as instruções DMX (Data Mining Extensions) para realizar todas essas tarefas de forma programada.  
  
 Criando estruturas de mineração e modelos de mineração  
 Use a instrução [criar estrutura de mineração &#40;&#41;DMX](../dmx/create-mining-structure-dmx.md) para adicionar uma nova estrutura de mineração a um banco de dados. Em seguida, você pode usar a instrução [ALTER MINING STRUCTURE &#40;DMX&#41;](../dmx/alter-mining-structure-dmx.md) para adicionar modelos de mineração à estrutura de mineração.  
  
 Use a instrução [criar modelo de mineração &#40;&#41;DMX](../dmx/create-mining-model-dmx.md) para criar um novo modelo de mineração e uma estrutura de mineração associada.  
  
 Processando estruturas de mineração e modelos de mineração  
 Use a instrução [INSERT INTO &#40;DMX&#41;](../dmx/insert-into-dmx.md) para processar uma estrutura de mineração e um modelo de mineração.  
  
 Excluindo ou descartando estruturas ou modelos de mineração  
 Use a instrução [DELETE &#40;DMX&#41;](../dmx/delete-dmx.md) para remover todos os dados treinados de um modelo de mineração ou estrutura de mineração. Use as instruções [&#40;dmx&#41;](../dmx/drop-mining-structure-dmx.md) ou drop de [modelo de mineração &#40;DMX&#41;](../dmx/drop-mining-model-dmx.md) para remover completamente uma estrutura de mineração ou modelo de mineração de um banco de dados.  
  
 Copiando modelos de mineração  
 Use a instrução [SELECT INTO &#40;DMX&#41;](../dmx/select-into-dmx.md) para copiar a estrutura de um modelo de mineração existente em um novo modelo de mineração e para treinar o novo modelo com os mesmos dados.  
  
 Pesquisando modelos de mineração  
 Use a instrução [SELECT &#40;DMX&#41;](../dmx/select-dmx.md) para procurar as informações que o algoritmo de Data Mining calcula e armazena no modelo de Data Mining durante o treinamento do modelo. Muito parecido com [!INCLUDE[tsql](../includes/tsql-md.md)] o, você pode usar várias cláusulas com a instrução SELECT para estender sua potência. Essas cláusulas incluem [DISTINCT de \<model> ](../dmx/select-distinct-from-model-dmx.md), [de \<model> . CASOS](../dmx/select-from-model-cases-dmx.md), [de \<model> . SAMPLE_CASES](../dmx/select-from-model-sample-cases-dmx.md), [de \<model> . CONTEÚDO](../dmx/select-from-model-content-dmx.md) e [de \<model> . DIMENSION_CONTENT](../dmx/select-from-model-dimension-content-dmx.md).  
  
 Prevendo segundo modelos de mineração  
 Use a cláusula de [junção de previsão](../dmx/select-from-model-prediction-join-dmx.md) da instrução SELECT para criar previsões baseadas em um modelo de mineração existente.  
  
 Você também pode importar e exportar modelos usando as instruções [import &#40;dmx&#41;](../dmx/import-dmx.md) e [exportar &#40;DMX&#41;](../dmx/export-dmx.md) .  
  
 Essas tarefas encaixam-se em duas categorias, instruções de definição de dados e instruções de manipulação de dados, descritas na tabela a seguir.  
  
|Tópico|Descrição|  
|-----------|-----------------|  
|[Instruções de definição de dados de extensões DMX &#40;extensões DMX&#41;](../dmx/dmx-statements-data-definition.md)|Parte da DLL (Data Definition Language). Usado definir um novo modelo de mineração (inclusive treinar) ou para descartar um modelo de mineração existente de um banco de dados.|  
|[&#40;instruções de manipulação de dados do DMX&#41; extensões do Data Mining](../dmx/dmx-statements-data-manipulation.md)|Parte da DML (Data Manipulation Language). Usado para trabalhar com modelos de mineração existentes, inclusive para pesquisar um modelo ou criar previsões.|  
  
## <a name="see-also"></a>Consulte Também  
 [Referência de função&#41; DMX &#40;extensões de mineração de dados](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Referência de operador de&#41; &#40;DMX de extensões de mineração de dados](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [&#40;as convenções de sintaxe de&#41; DMX de extensões de mineração de dados](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [As extensões de mineração de dados &#40;elementos de sintaxe DMX&#41;](../dmx/data-mining-extensions-dmx-syntax-elements.md)  
  
  
