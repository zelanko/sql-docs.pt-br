---
title: Consultando os conjuntos de linhas do esquema de mineração de dados (Analysis Services-Mineração de dados) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- schema rowsets [Analysis Services], data mining
- data mining [Analysis Services], queries
- mining model content
- data mining [Analysis Services], schema rowsets
- schema rowsets [Analysis Services], retrieving
- data mining [Analysis Services], troubleshooting
ms.assetid: 442d8c29-07c7-45de-9a15-d556059f68d7
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 30a4a503b16693a3774aa7f68771fb0f9dd70810
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66084904"
---
# <a name="querying-the-data-mining-schema-rowsets-analysis-services---data-mining"></a>Consultando os conjuntos de linhas de esquema de mineração de dados (Analysis Services - Mineração de Dados)
  No [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], muitos dos conjuntos de linhas de esquema de mineração de dados OLE DB existentes foram expostos como um conjunto de tabelas do sistema que pode ser consultado usando as instruções DMX (Data Mining Extensions). Ao criar consultas no conjunto de linhas de esquema de mineração de dados, é possível identificar os serviços disponíveis, obter atualizações sobre o status de seus modelos e estruturas e localizar detalhes sobre o conteúdo ou os parâmetros do modelo. Para obter uma descrição dos conjuntos de linhas de esquema de mineração de dados, consulte [Data Mining Schema Rowsets](../../relational-databases/native-client-ole-db-rowsets/rowsets.md).  
  
> [!NOTE]  
>  Você também pode consultar os conjuntos de linhas de esquema de mineração de dados usando o XMLA. Para obter mais informações sobre como fazer isso no SQL Server Management Studio, consulte [Criar uma consulta de mineração de dados usando o XMLA](create-a-data-mining-query-by-using-xmla.md).  
  
## <a name="list-of-data-mining-schema-rowsets"></a>Lista de conjuntos de linhas de esquema de mineração de dados  
 A tabela a seguir lista os conjuntos de linhas de esquema de mineração de dados que podem ser úteis para consultas e monitoramentos.  
  
|Nome do conjunto de linhas|Descrição|  
|-----------------|-----------------|  
|DMSCHEMA_MINING_MODELS|Lista todos os modelos de mineração no contexto atual.<br /><br /> As informações incluem a data de criação, os parâmetros usados para criar o modelo e o tamanho do treinamento definido.|  
|DMSCHEMA_MINING_COLUMNS|Lista todas as colunas usadas nos modelos de mineração no contexto atual.<br /><br /> As informações incluem o mapeamento para a coluna de origem de estrutura de mineração, o tipo de dados, a precisão e as funções de previsão que podem ser usadas com a coluna.|  
|DMSCHEMA_MINING_STRUCTURES|Lista toda a estrutura de mineração no contexto atual.<br /><br /> As informações incluem se a estrutura é populada, a data em que a estrutura foi processada e a definição do conjunto de dados validado para a estrutura, se houver.|  
|DMSCHEMA_MINING_STRUCTURE_COLUMNS|Lista todas as colunas usadas nas estruturas de mineração no contexto atual.<br /><br /> As informações incluem o tipo de conteúdo e de dados, a nulidade e se a coluna contém dados de tabela aninhados.|  
|DMSCHEMA_MINING_SERVICES|Lista todos os serviços de mineração, ou algoritmos, disponíveis no servidor especificado.<br /><br /> As informações incluem os sinalizadores de modelagem com suporte, os tipos de entrada e os tipos de fonte de dados com suporte.|  
|DMSCHEMA_MINING_SERVICE_PARAMETERS|Lista todos os parâmetros para os serviços de mineração disponíveis na instância atual.<br /><br /> As informações incluem o tipo de dados para cada parâmetro, os valores padrão e os limites superiores e inferiores.|  
|DMSCHEMA_MODEL_CONTENT|Retorna o conteúdo do modelo, caso o modelo tenha sido processado.<br /><br /> Para obter mais informações, consulte [Conteúdo do modelo de mineração &#40;Analysis Services – Mineração de dados&#41;](mining-model-content-analysis-services-data-mining.md).|  
|DBSCHEMA_CATALOGS|Lista todos os bancos de dados (catálogos) na instância atual do Analysis Services.|  
|MDSCHEMA_INPUT_DATASOURCES|Lista todas as fontes de dados na instância atual do Analysis Services.|  
  
> [!NOTE]  
>  A lista na tabela não é abrangente; ela mostra apenas os conjuntos de linhas que podem ser interessantes para solucionar os problemas.  
  
## <a name="examples"></a>Exemplos  
 A seção a seguir fornece alguns exemplos de consultas nos conjuntos de linhas de esquema de mineração de dados.  
  
### <a name="example-1-list-data-mining-services"></a>Exemplo 1: lista de serviços de mineração de dados  
 A consulta a seguir retorna uma lista dos serviços de mineração disponíveis no servidor atual, indicando que os algoritmos estão habilitados. As colunas fornecidas para cada serviço de mineração incluem os sinalizadores de modelagem e os tipos de conteúdo que podem ser usados em cada algoritmo, o GUID para cada serviço e todos os limites de previsão que podem ter sido adicionados a cada serviço.  
  
```  
SELECT *  
FROM $system.DMSCHEMA_MINING_SERVICES  
```  
  
### <a name="example-2-list-mining-model-parameters"></a>Exemplo 2: lista de parâmetros de modelo de mineração  
 O exemplo a seguir retorna os parâmetros usados para criar um modelo de mineração específico:  
  
```  
SELECT MINING_PARAMETERS   
FROM $system.DMSCHEMA_MINING_MODELS  
WHERE MODEL_NAME = 'TM Clustering'  
```  
  
### <a name="example-3-list-all-rowsets"></a>Exemplo 3: lista de todos os conjuntos de linhas  
 O exemplo a seguir retorna uma lista abrangente dos conjuntos de linhas disponíveis no servidor atual:  
  
```  
SELECT *   
FROM $system.DBSCHEMA_TABLES  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Conceitos da solução de problemas (Analysis Services - Mineração de Dados)](https://msdn.microsoft.com/library/cc645881.aspx)  
  
  
