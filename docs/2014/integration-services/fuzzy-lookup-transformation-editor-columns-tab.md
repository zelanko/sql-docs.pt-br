---
title: Editor de transformação pesquisa difusa (guia colunas) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.fuzzylookuptransformation.columns.f1
helpviewer_keywords:
- Fuzzy Lookup Transformation Editor
ms.assetid: aaf45327-79e9-4760-9b4d-546ace91b5b4
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 74182d9ca6f1a1c7bf2657d5c296c98fe52516a2
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85425213"
---
# <a name="fuzzy-lookup-transformation-editor-columns-tab"></a>Editor de Transformação Pesquisa Difusa (guia Colunas)
  Use a guia **Colunas** da caixa de diálogo **Editor de Transformação Pesquisa Difusa** para definir propriedades das colunas de entrada e saída.  
  
 Para saber mais sobre a transformação Pesquisa Difusa, consulte [Fuzzy Lookup Transformation](data-flow/transformations/lookup-transformation.md).  
  
## <a name="options"></a>Opções  
 **Colunas de Entrada Disponíveis**  
 Arraste colunas de entrada para conectá-las com colunas de pesquisa disponíveis. Essas colunas devem ter tipos de dados correspondentes com suporte. Selecione uma linha de mapeamento e clique com o botão direito do mouse para editar os mapeamentos na caixa de diálogo [Criar Relações](data-flow/transformations/create-relationships.md) .  
  
 **Nome**  
 Exiba os nomes das colunas de entrada disponíveis.  
  
 **Passagem**  
 Especifique se as colunas de entrada devem ser incluídas na saída da transformação.  
  
 **Colunas de Pesquisa Disponíveis**  
 Use as caixas de seleção para selecionar colunas nas quais executar operações de pesquisa difusa.  
  
 **coluna de pesquisa**  
 Selecione colunas de pesquisa na lista de colunas da tabela de referência disponíveis. Suas seleções se refletem nas da caixa de seleção da tabela **Colunas de Pesquisa Disponíveis** . Selecionar uma coluna na tabela **Colunas de Pesquisa Disponíveis** cria uma coluna de saída que contém o valor da coluna da tabela de referência para cada linha correspondente retornada.  
  
 **Alias de saída**  
 Digite um alias para a saída de cada coluna de pesquisa. O padrão é o nome da coluna de pesquisa com um valor de índice numérico anexado; contudo, é possível escolher qualquer nome descritivo exclusivo.  
  
## <a name="see-also"></a>Consulte Também  
 [Integration Services referência de erro e mensagem](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Editor de transformação pesquisa difusa &#40;guia tabela de referência&#41;](../../2014/integration-services/fuzzy-lookup-transformation-editor-reference-table-tab.md)   
 [Editor de Transformação Pesquisa Difusa &#40;Guia Avançado&#41;](../../2014/integration-services/fuzzy-lookup-transformation-editor-advanced-tab.md)  
  
  
