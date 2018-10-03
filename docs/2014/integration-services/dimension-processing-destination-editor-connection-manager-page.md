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
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 1687baf77bcecedb61a3d1ecee3a9e3c9e155431
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48133726"
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
  
|Valor|Description|  
|-----------|-----------------|  
|**Adicionar (incremental)**|Execute um processamento com incremento da dimensão.|  
|**Completo**|Execute um processamento completo da dimensão.|  
|**Update (atualizar)**|Execute um processamento de atualização da dimensão.|  
  
## <a name="see-also"></a>Consulte também  
 [Referência de mensagens e erros do Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Editor de destino de processamento de dimensões &#40;página mapeamentos&#41;](../../2014/integration-services/dimension-processing-destination-editor-mappings-page.md)   
 [Editor de destino de processamento de dimensões &#40;página Avançado&#41;](../../2014/integration-services/dimension-processing-destination-editor-advanced-page.md)  
  
  
