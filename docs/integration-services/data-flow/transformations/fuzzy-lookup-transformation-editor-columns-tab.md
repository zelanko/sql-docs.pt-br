---
title: "Editor de Transforma&#231;&#227;o Pesquisa Difusa (guia Colunas) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.fuzzylookuptransformation.columns.f1"
helpviewer_keywords: 
  - "Editor de Transformação Pesquisa Difusa"
ms.assetid: aaf45327-79e9-4760-9b4d-546ace91b5b4
caps.latest.revision: 26
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 26
---
# Editor de Transforma&#231;&#227;o Pesquisa Difusa (guia Colunas)
  Use a guia **Colunas** da caixa de diálogo **Editor de Transformação Pesquisa Difusa** para definir propriedades das colunas de entrada e saída.  
  
 Para saber mais sobre a transformação Pesquisa Difusa, consulte [Fuzzy Lookup Transformation](../../../integration-services/data-flow/transformations/fuzzy-lookup-transformation.md).  
  
## Opções  
 **Colunas de Entrada Disponíveis**  
 Arraste colunas de entrada para conectá-las com colunas de pesquisa disponíveis. Essas colunas devem ter tipos de dados correspondentes com suporte. Selecione uma linha de mapeamento e clique com o botão direito do mouse para editar os mapeamentos na caixa de diálogo [Criar Relações](../../../integration-services/data-flow/transformations/create-relationships.md).  
  
 **Nome**  
 Exiba os nomes das colunas de entrada disponíveis.  
  
 **Passagem**  
 Especifique se as colunas de entrada devem ser incluídas na saída da transformação.  
  
 **Colunas de Pesquisa Disponíveis**  
 Use as caixas de seleção para selecionar colunas nas quais executar operações de pesquisa difusa.  
  
 **coluna de pesquisa**  
 Selecione colunas de pesquisa na lista de colunas da tabela de referência disponíveis. Suas seleções se refletem nas da caixa de seleção da tabela **Colunas de Pesquisa Disponíveis** . Selecionar uma coluna na tabela **Colunas de Pesquisa Disponíveis** cria uma coluna de saída que contém o valor da coluna da tabela de referência para cada linha correspondente retornada.  
  
 **Alias de Saída**  
 Digite um alias para a saída de cada coluna de pesquisa. O padrão é o nome da coluna de pesquisa com um valor de índice numérico anexado; contudo, é possível escolher qualquer nome descritivo exclusivo.  
  
## Consulte também  
 [Referência de mensagens e erros do Integration Services](../../../integration-services/integration-services-error-and-message-reference.md)   
 [Editor de Transformação Pesquisa Difusa &#40;Guia Tabela de Referência&#41;](../../../integration-services/data-flow/transformations/fuzzy-lookup-transformation-editor-reference-table-tab.md)   
 [Editor de Transformação Pesquisa Difusa &#40;Guia Avançado&#41;](../../../integration-services/data-flow/transformations/fuzzy-lookup-transformation-editor-advanced-tab.md)  
  
  