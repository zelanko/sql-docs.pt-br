---
title: "Referência Data Mining Extensions (DMX) instrução | Microsoft Docs"
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- DMX
helpviewer_keywords:
- Data Mining Extensions [Analysis Services], statements
- DMX [Analysis Services], statements
- statements [DMX], reference
- mining models [Analysis Services], training
- mining structures [DMX]
- mining models [Analysis Services], options
- mining structures [DMX], options
ms.assetid: 9cfa1db4-0f21-4fa3-8158-f94c48987e1b
caps.latest.revision: 31
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: e7c9740eebec925bc2b25c6437f488f898288a1e
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="data-mining-extensions-dmx-statements"></a>Instruções Data Mining Extensions (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Trabalhando com dados de modelos de mineração em [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] envolve as seguintes tarefas principais:  
  
-   Criando estruturas de mineração e modelos de mineração  
  
-   Processando estruturas de mineração e modelos de mineração  
  
-   Excluindo ou descartando estruturas ou modelos de mineração  
  
-   Copiando modelos de mineração  
  
-   Pesquisando modelos de mineração  
  
-   Prevendo segundo modelos de mineração  
  
 Use as instruções DMX (Data Mining Extensions) para realizar todas essas tarefas de forma programada.  
  
 Criando estruturas de mineração e modelos de mineração  
 Use o [criar estrutura de MINERAÇÃO &#40; DMX &#41;](../dmx/create-mining-structure-dmx.md) instrução para adicionar uma nova estrutura de mineração para um banco de dados. Você pode usar o [ALTER MINING STRUCTURE &#40; DMX &#41;](../dmx/alter-mining-structure-dmx.md) instrução para adicionar modelos de mineração à estrutura de mineração.  
  
 Use o [criar modelo de MINERAÇÃO &#40; DMX &#41;](../dmx/create-mining-model-dmx.md) instrução para criar uma nova estrutura de mineração associada e modelo de mineração.  
  
 Processando estruturas de mineração e modelos de mineração  
 Use o [INSERT INTO &#40; DMX &#41;](../dmx/insert-into-dmx.md) instrução para processar uma estrutura de mineração e um modelo de mineração.  
  
 Excluindo ou descartando estruturas ou modelos de mineração  
 Use o [Excluir &#40; DMX &#41;](../dmx/delete-dmx.md) instrução para remover todos os dados treinados de um modelo de mineração ou estrutura de mineração. Use o [DROP MINING STRUCTURE &#40; DMX &#41;](../dmx/drop-mining-structure-dmx.md) ou [DROP MINING MODEL &#40; DMX &#41;](../dmx/drop-mining-model-dmx.md) instruções para remover completamente uma estrutura de mineração ou modelo de mineração de um banco de dados.  
  
 Copiando modelos de mineração  
 Use o [SELECT INTO &#40; DMX &#41;](../dmx/select-into-dmx.md) instrução para copiar a estrutura de um modelo de mineração existente em um novo modelo de mineração e para treinar o novo modelo com os mesmos dados.  
  
 Pesquisando modelos de mineração  
 Use o [SELECT &#40; DMX &#41;](../dmx/select-dmx.md) instrução para pesquisar as informações que o algoritmo de mineração de dados calcula e armazena no modelo de mineração de dados durante o treinamento do modelo. Semelhantemente ao [!INCLUDE[tsql](../includes/tsql-md.md)], você pode usar várias cláusulas com a instrução SELECT, para estender a sua capacidade. Essas cláusulas incluem [DISTINTOS de \<modelo >](../dmx/select-distinct-from-model-dmx.md), [FROM \<modelo >. CASOS](../dmx/select-from-model-cases-dmx.md), [FROM \<modelo >. SAMPLE_CASES](../dmx/select-from-model-sample-cases-dmx.md), [FROM \<modelo >. CONTEÚDO](../dmx/select-from-model-content-dmx.md) e [FROM \<modelo >. DIMENSION_CONTENT](../dmx/select-from-model-dimension-content-dmx.md).  
  
 Prevendo segundo modelos de mineração  
 Use o [PREDICTION JOIN](../dmx/select-from-model-prediction-join-dmx.md) cláusula da instrução SELECT para criar previsões com base em um modelo de mineração existente.  
  
 Você também pode importar e exportar modelos usando o [Importar &#40; DMX &#41;](../dmx/import-dmx.md) e [exportar &#40; DMX &#41;](../dmx/export-dmx.md) instruções.  
  
 Essas tarefas encaixam-se em duas categorias, instruções de definição de dados e instruções de manipulação de dados, descritas na tabela a seguir.  
  
|Tópico|Description|  
|-----------|-----------------|  
|[Extensões de mineração de dados &#40; DMX &#41; Instruções de definição de dados](../dmx/dmx-statements-data-definition.md)|Parte da DLL (Data Definition Language). Usado definir um novo modelo de mineração (inclusive treinar) ou para descartar um modelo de mineração existente de um banco de dados.|  
|[Extensões de mineração de dados &#40; DMX &#41; Instruções de manipulação de dados](../dmx/dmx-statements-data-manipulation.md)|Parte da DML (Data Manipulation Language). Usado para trabalhar com modelos de mineração existentes, inclusive para pesquisar um modelo ou criar previsões.|  
  
## <a name="see-also"></a>Consulte também  
 [Extensões de mineração de dados &#40; DMX &#41; Referência de função](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Extensões de mineração de dados &#40; DMX &#41; Referência de operador](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Extensões de mineração de dados &#40; DMX &#41; Convenções de sintaxe](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [Extensões de mineração de dados &#40; DMX &#41; Elementos de sintaxe](../dmx/data-mining-extensions-dmx-syntax-elements.md)  
  
  

