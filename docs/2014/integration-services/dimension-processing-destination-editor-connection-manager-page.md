---
title: Editor de destino de processamento de dimensões (página Gerenciador de Conexão) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.dimprocessingtransformation.connection.f1
helpviewer_keywords:
- Dimension Processing Destination Editor
ms.assetid: 44aab631-d62d-4895-8fc7-7f1f3b1b68ce
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: e48018f3bbc3f266a4e537f067b3fa9466dea275
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/22/2019
ms.locfileid: "58381945"
---
# <a name="dimension-processing-destination-editor-connection-manager-page"></a>Editor de Destino de Processamento de Dimensões (página Gerenciador de Conexões)
  Use a página **Gerenciador de Conexões** da caixa de diálogo **Editor de Destino de Processamento de Dimensões** para especificar uma conexão com um projeto do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] ou com uma instância do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
 Para saber mais sobre o destino de Processamento de Dimensões, consulte [Dimension Processing Destination](data-flow/dimension-processing-destination.md).  
  
## <a name="options"></a>Opções  
 **Connection manager**  
 Selecione um gerenciador de conexões existente na lista ou clique em **Novo** para criar um novo gerenciador de conexões.  
  
 **Nova**  
 Crie uma nova conexão usando a caixa de diálogo **Adicionar Gerenciador de Conexões do Analysis Services** .  
  
 **Lista de dimensões disponíveis**  
 Selecione a dimensão a processar.  
  
 **Método de processamento**  
 Selecione o método de processamento a aplicar à dimensão selecionada na lista. O valor padrão desta opção é **Completo**.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**Adicionar (incremental)**|Execute um processamento com incremento da dimensão.|  
|**Completo**|Execute um processamento completo da dimensão.|  
|**Update (atualizar)**|Execute um processamento de atualização da dimensão.|  
  
## <a name="see-also"></a>Consulte também  
 [Referência de mensagens e erros do Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Editor de Destino de Processamento de Dimensões &#40;página Mapeamentos&#41;](../../2014/integration-services/dimension-processing-destination-editor-mappings-page.md)   
 [Editor de Destino de Processamento de Dimensões &#40;Página Avançado&#41;](../../2014/integration-services/dimension-processing-destination-editor-advanced-page.md)  
  
  
