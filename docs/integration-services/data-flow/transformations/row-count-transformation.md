---
title: Transformação Contagem de Linhas | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.rowcounttrans.f1
helpviewer_keywords:
- updating variables
- Row Count transformation
- number of rows
- variables [Integration Services], updating
- counting rows
ms.assetid: b68293b9-a68c-40be-9d81-77342da1be29
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 4cd1b3a72a91eb3c2a2252eefcec6cf7416cae8f
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "71297865"
---
# <a name="row-count-transformation"></a>Transformação Contagem de Linhas

[!INCLUDE[ssis-appliesto](../../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  A transformação Contagem de Linhas conta as linhas quando passam por um fluxo de dados e armazena a contagem final em uma variável.  
  
 O pacote [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] pode usar contagens de linhas para atualizar as variáveis usadas em scripts, expressões e expressões de propriedade. Por exemplo, a variável que armazena a contagem de linhas pode atualizar o texto de mensagem em uma mensagem de email para incluir o número de linhas. A variável que a transformação Contagem de Linhas usa já deve existir e deve estar no escopo da tarefa de Fluxo de Dados ao qual esse fluxo com a transformação Contagem de Linhas pertence.  
  
 A transformação só armazena o valor da contagem de linhas na variável após a última linha ter passado pela transformação. Portanto, o valor da variável não é atualizado a tempo de usar o valor atualizado no fluxo de dados que contém a transformação Contagem de Linhas. Você pode usar a variável atualizada em um fluxo de dados separado.  
  
 Essa transformação tem uma entrada e uma saída. Não dá suporte a uma saída de erro.  
  
## <a name="configuration-of-the-row-count-transformation"></a>Configuração da transformação Contagem de Linhas  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../../includes/ssis-md.md)] ou programaticamente.  
  
 A caixa de diálogo **Editor Avançado** reflete as propriedades que podem ser definidas programaticamente. Para obter mais informações sobre as propriedades que podem ser definidas na caixa de diálogo **Editor Avançado** ou programaticamente, clique em um dos seguintes tópicos:  
  
-   [Propriedades comuns](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [Propriedades personalizadas de Transformação](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
## <a name="related-tasks"></a>Related Tasks  
 Para obter informações sobre como definir as propriedades desse componente, consulte [Definir as propriedades de um componente de fluxo de dados](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Variáveis do SSIS &#40;Integration Services&#41;](../../../integration-services/integration-services-ssis-variables.md)   
 [Fluxo de Dados](../../../integration-services/data-flow/data-flow.md)   
 [Transformações do Integration Services](../../../integration-services/data-flow/transformations/integration-services-transformations.md)  
  
  
