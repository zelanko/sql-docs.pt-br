---
title: Transformação Contagem de Linhas | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.rowcounttrans.f1
helpviewer_keywords:
- updating variables
- Row Count transformation
- number of rows
- variables [Integration Services], updating
- counting rows
ms.assetid: b68293b9-a68c-40be-9d81-77342da1be29
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: d991ee94e04be0ea72450b8e3e4649c339d1c2a4
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62900199"
---
# <a name="row-count-transformation"></a>Transformação Contagem de Linhas
  A transformação Contagem de Linhas conta as linhas quando passam por um fluxo de dados e armazena a contagem final em uma variável.  
  
 Um pacote do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] pode usar contagens de linhas para atualizar as variáveis usadas em scripts, expressões e expressões de propriedade. Por exemplo, a variável que armazena a contagem de linhas pode atualizar o texto de mensagem em uma mensagem de email para incluir o número de linhas. A variável que a transformação Contagem de Linhas usa já deve existir e deve estar no escopo da tarefa de Fluxo de Dados ao qual esse fluxo com a transformação Contagem de Linhas pertence.  
  
 A transformação só armazena o valor da contagem de linhas na variável após a última linha ter passado pela transformação. Portanto, o valor da variável não é atualizado a tempo de usar o valor atualizado no fluxo de dados que contém a transformação Contagem de Linhas. Você pode usar a variável atualizada em um fluxo de dados separado.  
  
 Essa transformação tem uma entrada e uma saída. Não dá suporte a uma saída de erro.  
  
## <a name="configuration-of-the-row-count-transformation"></a>Configuração da transformação Contagem de Linhas  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../../includes/ssis-md.md)] ou programaticamente.  
  
 A caixa de diálogo **Editor Avançado** reflete as propriedades que podem ser definidas programaticamente. Para obter mais informações sobre as propriedades que podem ser definidas na caixa de diálogo **Editor Avançado** ou programaticamente, clique em um dos seguintes tópicos:  
  
-   [Propriedades comuns](../../common-properties.md)  
  
-   [Propriedades personalizadas da transformação](transformation-custom-properties.md)  
  
## <a name="related-tasks"></a>Related Tasks  
 Para obter informações sobre como definir as propriedades desse componente, consulte [Definir as propriedades de um componente de fluxo de dados](../set-the-properties-of-a-data-flow-component.md).  
  
## <a name="see-also"></a>Consulte também  
 [Variáveis do SSIS &#40;Integration Services&#41;](../../integration-services-ssis-variables.md)   
 [Fluxo de Dados](../data-flow.md)   
 [Transformações do Integration Services](integration-services-transformations.md)  
  
  
