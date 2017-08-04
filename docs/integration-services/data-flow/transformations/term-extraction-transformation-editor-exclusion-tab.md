---
title: "Editor de transformação extração de termos (guia exclusão) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.termextraction.inclusionexclusion.f1
helpviewer_keywords:
- Term Extraction Transformation Editor
ms.assetid: 90110d95-fd97-4542-9cda-832c86606130
caps.latest.revision: 28
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 50d62aa983a1a5f12def175a375740155596fb65
ms.contentlocale: pt-br
ms.lasthandoff: 08/03/2017

---
# <a name="term-extraction-transformation-editor-exclusion-tab"></a>Editor de Transformação Extração de Termos (guia Exclusão)
  Use a guia **Exclusão** da caixa de diálogo do **Editor de Transformação Extração de Termos** para definir uma conexão com uma tabela de exclusão e especificar as colunas que contêm termos de exclusão.  
  
 Para saber mais sobre a transformação Extração de Termos, consulte [Term Extraction Transformation](../../../integration-services/data-flow/transformations/term-extraction-transformation.md).  
  
## <a name="options"></a>Opções  
 **Usar termos de exclusão**  
 Indique se devem ser excluídos termos específicos durante uma extração de termos especificando uma coluna que contém termos de exclusão. Você deve especificar as seguintes propriedades de origem caso opte por excluir termos.  
  
 **gerenciador de conexões OLE DB**  
 Selecione um gerenciador de conexões OLE DB existente ou crie uma nova conexão clicando em **Novo**.  
  
 **Novo**  
 Crie uma nova conexão com um banco de dados usando a caixa de diálogo **Configurar Gerenciador de Conexões OLE DB** .  
  
 **Tabela ou exibição**  
 Selecione a tabela ou exibição que contém os termos de exclusão.  
  
 **Coluna**  
 Selecione a coluna na tabela ou exibição que contém os termos de exclusão.  
  
 **Configurar Saída de Erro**  
 Use a caixa de diálogo [Configurar Saída de Erro](http://msdn.microsoft.com/library/5f8da390-fab5-44f8-b268-d8fa313ce4b9) para especificar tratamento de erro em linhas que causam erros.  
  
## <a name="see-also"></a>Consulte também  
 [Referência de mensagens e erros do Integration Services](../../../integration-services/integration-services-error-and-message-reference.md)   
 [Editor de transformação extração de termos &#40; Termo guia extração &#41;](../../../integration-services/data-flow/transformations/term-extraction-transformation-editor-term-extraction-tab.md)   
 [Editor de transformação extração de termos &#40; Guia Avançado &#41;](../../../integration-services/data-flow/transformations/term-extraction-transformation-editor-advanced-tab.md)   
 [Transformação de pesquisa de termo](../../../integration-services/data-flow/transformations/term-lookup-transformation.md)  
  
  
