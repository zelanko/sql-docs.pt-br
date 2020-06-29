---
title: Editor do Gerenciador de conexões MSMQ | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.msmqconnectionmanager.f1
helpviewer_keywords:
- MSMQ Connection Manager Editor
ms.assetid: ef842cb4-82da-4550-85fe-9bedbc1e77c7
author: chugugrace
ms.author: chugu
ms.openlocfilehash: d452aa1edc21af067f1deac0e4544b117cecf13b
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85440193"
---
# <a name="msmq-connection-manager-editor"></a>Editor do Gerenciador de Conexões MSMQ
  Use a caixa de diálogo **Gerenciador de Conexões MSMQ** para especificar o caminho do Serviço de Enfileiramento de Mensagens (também conhecido como MSMQ).  
  
 Para saber mais sobre o Gerenciador de Conexões MSMQ, consulte [Gerenciador de Conexões MSMQ](connection-manager/msmq-connection-manager.md).  
  
> [!NOTE]  
>  O gerenciador de conexões MSMQ aceita filas públicas e privadas locais e filas públicas remotas. Não dá suporte a filas privadas remotas. Para obter uma solução alternativa que usa a tarefa Script, consulte [Enviando a uma fila de mensagens particular remota com a tarefa Script](control-flow/script-task.md).  
  
## <a name="options"></a>Opções  
 **Nome**  
 Forneça um nome exclusivo para o gerenciador de conexões MSMQ no fluxo de trabalho. O nome fornecido será exibido no Designer do [!INCLUDE[ssIS](../includes/ssis-md.md)] .  
  
 **Descrição**  
 Descreva o gerenciador de conexões. Como prática recomendável, descreva o gerenciador de conexões em termos de objetivo, para tornar os pacotes autodocumentados e mais fáceis de manter.  
  
 **Caminho**  
 Digite o caminho completo da fila de mensagens. O formato do caminho depende do tipo de fila.  
  
|Tipo de fila|Exemplo de caminho|  
|----------------|-----------------|  
|Público|\<computer name>\\Nome da fila de<\>|  
|Particular|\<computer name>Nome da fila do \Bytes privados $ \\<\>|  
  
 Você pode usar um "." para representar o computador local.  
  
 **Teste**  
 Depois de configurar o Gerenciador de Conexões MSMQ, confirme se a conexão é viável clicando em **Testar**.  
  
## <a name="see-also"></a>Consulte Também  
 [Referência de mensagens e erros do Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)  
  
  
