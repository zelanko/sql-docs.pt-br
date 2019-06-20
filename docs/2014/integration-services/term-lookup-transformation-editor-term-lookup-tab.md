---
title: Editor de transformação de pesquisa de termos (guia pesquisa de termos) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.termlookup.termlookup.f1
helpviewer_keywords:
- Term Lookup Transformation Editor
ms.assetid: 245d3466-d51f-4073-978a-694a8d9dfaec
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 2939d160773d60944a2e8a786e5495cea366edb1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66055127"
---
# <a name="term-lookup-transformation-editor-term-lookup-tab"></a>Editor de Transformação Pesquisa de Termos (guia Pesquisa de Termos)
  Use a guia **Pesquisa de Termos** na caixa de diálogo **Editor de Transformação Pesquisa de Termos** para mapear uma coluna de entrada para uma coluna de pesquisa em uma tabela de referência e fornecer um alias para cada coluna de saída.  
  
 Para saber mais sobre a transformação Pesquisa de Termos, consulte [Term Lookup Transformation](data-flow/transformations/lookup-transformation.md).  
  
## <a name="options"></a>Opções  
 **Colunas de Entrada Disponíveis**  
 Usando as caixas de seleção, selecione colunas de entrada para passar para a saída inalteradas. Arraste uma coluna de entrada para a lista **Colunas de Referência Disponíveis** para mapeá-la para uma coluna de pesquisa na tabela de referência. As colunas de entrada e de pesquisa devem ter tipos de dados correspondentes e que tenham suporte no DT_NTEXT ou DT_WSTR. Selecione uma linha de mapeamento e clique com o botão direito do mouse para editar os mapeamentos na caixa de diálogo [Criar Relações](data-flow/transformations/create-relationships.md) .  
  
 **Colunas de Referência Disponíveis**  
 Exiba as colunas disponíveis na tabela de referência. Escolha a coluna que contém a lista de termos a corresponder.  
  
 **Coluna de Passagem**  
 Selecione na lista de colunas de entrada disponíveis. As seleções se refletem naquelas da caixa de seleção da tabela **Colunas de Entrada Disponíveis** .  
  
 **Alias de Coluna de Saída**  
 Digite um alias para cada coluna de saída. O padrão é o nome da coluna; no entanto, é possível escolher qualquer nome descritivo exclusivo.  
  
 **Configurar Saída de Erro**  
 Use a caixa de diálogo [Configurar Saída de Erro](../../2014/integration-services/configure-error-output.md) para especificar as opções de tratamento de erro em linhas que causam erros.  
  
## <a name="see-also"></a>Consulte também  
 [Referência de mensagens e erros do Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Editor de Transformação Pesquisa de Termos &#40;Guia Tabela de Referência&#41;](../../2014/integration-services/term-lookup-transformation-editor-reference-table-tab.md)   
 [Editor de Transformação Pesquisa de Termos &#40;Guia Avançado&#41;](../../2014/integration-services/term-lookup-transformation-editor-advanced-tab.md)   
 [Transformação Extração de Termos](data-flow/transformations/term-extraction-transformation.md)  
  
  
