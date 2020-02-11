---
title: Editor de transformação pesquisa (página colunas) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.lookuptransformation.columns.f1
helpviewer_keywords:
- Lookup Transformation Editor
ms.assetid: 690ffef5-fd59-4e95-a27d-4fcf0d6b1c0b
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: e1a32dcbcee6704cb4fecef7b58cbff8354b910a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66057901"
---
# <a name="lookup-transformation-editor-columns-page"></a>Editor da Transformação Pesquisa (página Colunas)
  Use a página **Colunas** da caixa de diálogo **Editor da Transformação Pesquisa** para especificar a junção entre a tabela de origem e a tabela de referência, e para selecionar as colunas de pesquisa a partir da tabela de referência.  
  
 Para saber mais sobre a transformação Pesquisa, consulte [Lookup Transformation](data-flow/transformations/lookup-transformation.md).  
  
## <a name="options"></a>Opções  
 **Colunas de Entrada Disponíveis**  
 Exiba a lista das colunas de entrada disponíveis. As colunas de entrada são as colunas no fluxo de dados de uma origem conectada. As colunas de entrada e de pesquisa devem ter tipos de dados correspondentes.  
  
 Use uma operação arrastar e soltar para mapear as colunas de entrada disponíveis para as colunas de pesquisa.  
  
 Você também pode mapear as colunas de entrada para as colunas de pesquisa usando o teclado, destacando a coluna na tabela **Colunas de Entrada Disponíveis** , pressionando a tecla Aplicativo e clicando em **Editar Mapeamentos**.  
  
 **Colunas de pesquisa disponíveis**  
 Exiba a lista de colunas de pesquisa. As colunas de pesquisa são as colunas na tabela de referência que permitem pesquisar os valores que correspondem às colunas de entrada.  
  
 Use uma operação arrastar e soltar para mapear as colunas de pesquisa disponíveis para as colunas de entrada.  
  
 Use as caixas de seleção para selecionar as colunas de pesquisa na tabela de referência nas quais serão executadas as operações de pesquisa.  
  
 Você também pode mapear as colunas de pesquisa para as colunas de entrada usando o teclado, destacando a coluna na tabela **Colunas de Pesquisa Disponíveis** , pressionando a tecla Aplicativo e clicando em **Editar Mapeamentos**.  
  
 **coluna de pesquisa**  
 Exiba as colunas de pesquisa selecionadas. As escolhas são refletidas nas caixas de seleção da tabela **Colunas de Pesquisa Disponíveis** .  
  
 **Operação de pesquisa**  
 Selecione uma operação de pesquisa da lista a ser executada na coluna de pesquisa.  
  
 **Alias de Saída**  
 Digite um alias para a saída de cada coluna de pesquisa. O padrão é o nome da coluna de pesquisa; entretanto, é possível selecionar qualquer nome descritivo exclusivo.  
  
## <a name="see-also"></a>Consulte Também  
 [Editor de transformação pesquisa &#40;página Geral&#41;](general-page-of-integration-services-designers-options.md)   
 [Editor de transformação pesquisa &#40;página conexão&#41;](../../2014/integration-services/lookup-transformation-editor-connection-page.md)   
 [Editor de transformação pesquisa &#40;página avançado&#41;](../../2014/integration-services/lookup-transformation-editor-advanced-page.md)   
 [Editor de transformação pesquisa &#40;página saída de erro&#41;](../../2014/integration-services/lookup-transformation-editor-error-output-page.md)   
 [transformação Pesquisa Difusa](data-flow/transformations/fuzzy-lookup-transformation.md)  
  
  
