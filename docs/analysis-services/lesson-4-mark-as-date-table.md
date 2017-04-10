---
title: "Li&#231;&#227;o 4: Marcar como Tabela de Data | Microsoft Docs"
ms.custom: ""
ms.date: "02/27/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "get-started-article"
applies_to: 
  - "SQL Server 2016"
ms.assetid: c32cc336-b7d8-4122-9d62-4936344d2315
caps.latest.revision: 18
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
---
# Li&#231;&#227;o 4: Marcar como Tabela de Data
Na Lição 2: Adicionar Dados, você importou uma tabela de dimensão chamada DimDate e a renomeou Date. Em seu modelo, essa tabela agora é chamada Date; ela também pode ser conhecida como uma *tabela Data*, pois contém dados de data e hora.  
  
Sempre que você usar funções de Inteligência de Dados Temporais em cálculos, como fará quando criar medidas mais adiante, especifique as propriedades da tabela de data, que inclui uma *tabela de Data* e uma *coluna de Data* de identificador exclusivo nessa tabela. Você pode criar relações válidas entre outras tabelas e a tabela de Data; necessário para cálculos que usam funções de inteligência de tempo DAX.  
  
Nesta lição, você aprenderá a marcar a tabela de Data importada e renomeada como a *tabela de Data* e a coluna de Data (na tabela de Data) como a *coluna de Data* (identificador exclusivo). O uso do nome Data pode ficar confuso, mas isso logo se esclarecerá.  
  
Tempo estimado para concluir esta lição: **3 minutos**  
  
## Pré-requisitos  
Este tópico faz parte de um tutorial de modelo de tabela, que deve ser concluído na ordem. Antes de executar as tarefas desta lição, você deverá ter concluído a lição anterior: [Lição 3: Renomear colunas](../analysis-services/lesson-3-rename-columns.md).  
  
### Para definir Marcar como Tabela de Data  
  
1.  No designer de modelos, clique na tabela **Data** (guia).  
  
2.  Selecione a coluna **Data** e, na janela **Propriedades**, em **Tipo de Dados**, verifique se a opção **Data** está selecionada.  
  
3.  Clique no menu **Tabela**, clique em **Data** e em **Marcar como Tabela de Data**.  
  
4.  Na caixa de diálogo **Marcar como Tabela de Data**, na caixa de listagem **Data**, selecione a coluna **Data** como o identificador exclusivo.  
  
## Próximas etapas  
Para continuar este tutorial, vá para a próxima lição: [Lição 5: Criar relações](../analysis-services/lesson-5-create-relationships.md).  
  
  
  
