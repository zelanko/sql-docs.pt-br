---
title: Editor de destino de processamento de partições (página Gerenciador de Conexão) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.partprocessingtransformation.connection.f1
helpviewer_keywords:
- Partition Processing Destination Editor
ms.assetid: 7add6f82-eed1-47fc-a5d7-7b91f3f24d34
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 2822193b536423e29f0d838ad64dda20664c7f8b
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48200956"
---
# <a name="partition-processing-destination-editor-connection-manager-page"></a>Editor de Destino de Processamento de Partições (página Gerenciador de Conexões)
  Use a página **Gerenciador de Conexões** da caixa de diálogo **Editor de Destino de Processamento de Partições** para especificar uma conexão a um projeto do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] ou a uma instância do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
 Para saber mais sobre o destino de Processamento de Partições, consulte [Partition Processing Destination](data-flow/partition-processing-destination.md).  
  
> [!NOTE]  
>  As tarefas descritas aqui não se aplicam a modelos de tabela do Analysis Services.  Você não pode mapear colunas de entrada para as colunas de partição em modelos de tabela. Você pode usar a tarefa Executar DDL do Analysis Services [Analysis Services Execute DDL Task](control-flow/analysis-services-execute-ddl-task.md) para processar a partição.  
  
## <a name="options"></a>Opções  
 **Connection manager**  
 Selecione um gerenciador de conexões existente na lista ou crie uma nova conexão clicando em **Nova**.  
  
 **Nova**  
 Crie uma nova conexão usando a caixa de diálogo **Adicionar Gerenciador de Conexões do Analysis Services** .  
  
 **Lista de partições disponíveis**  
 Selecione a partição a processar.  
  
 **Método de processamento**  
 Selecione o método de processamento. O valor padrão desta opção é **Completo**.  
  
|Valor|Description|  
|-----------|-----------------|  
|Adicionar (incremental)|Execute um processamento com incremento da partição.|  
|Completo|Execute um processamento completo da partição.|  
|Apenas dados|Execute um processamento de atualização da partição.|  
  
## <a name="see-also"></a>Consulte também  
 [Referência de mensagens e erros do Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Editor de destino de processamento de partições &#40;página mapeamentos&#41;](../../2014/integration-services/partition-processing-destination-editor-mappings-page.md)   
 [Editor de destino de processamento de partições &#40;página Avançado&#41;](../../2014/integration-services/partition-processing-destination-editor-advanced-page.md)  
  
  
