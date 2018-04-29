---
title: Log de solicitações | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: data-flow
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 165d3833-0493-490c-9f63-8a134a7fafb8
caps.latest.revision: 10
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1e2d3ea8253e3bc999168d5890fe3de23e34eaaa
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
---
# <a name="request-log"></a>Log de solicitações
  Use a caixa de diálogo **Log de Solicitações** para exibir os eventos que são registrados em log durante a solicitação que é feita no sistema SAP Netweaver BW para dados de exemplo. Essas informações podem ser úteis se você precisar solucionar problemas da configuração da origem do SAP BW.  
  
 Para saber mais sobre o componente de origem do SAP BW do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 para SAP BW, consulte [Origem SAP BW](../../integration-services/data-flow/sap-bw-source.md).  
  
> [!IMPORTANT]  
>  A documentação do Microsoft Connector 1.1 for SAP BW supõe familiaridade com o ambiente do SAP Netweaver BW. Para obter mais informações sobre o SAP Netweaver BW ou para obter informações sobre como configurar objetos e processos do SAP Netweaver BW, consulte sua documentação do SAP.  
  
> [!IMPORTANT]  
>  A extração de dados do SAP Netweaver BW exige licenciamento SAP adicional. Verifique esses requisitos com a SAP.  
  
 **Para abrir a caixa de diálogo Log de Solicitações**  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra o pacote [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que contém a origem SAP BW.  
  
2.  Na guia **Fluxo de Dados** , clique duas vezes na fonte SAP BW.  
  
3.  No **Editor de Origem SAP BW**, clique em **Gerenciador de Conexões** para abrir a página **Gerenciador de Conexões** do editor.  
  
4.  Depois de configurar a origem do SAP BW, clique em **Visualizar** para visualizar os eventos na caixa de diálogo **Log de Solicitações** .  
  
    > [!NOTE]  
    >  Clicar em **Visualizar** também abre a caixa de diálogo **Visualizar** . Para obter mais informações sobre essa caixa de diálogo, consulte [Preview](../../integration-services/data-flow/preview.md).  
  
## <a name="options"></a>Opções  
 **Time**  
 Exibe a hora em que o evento foi registrado em log.  
  
 **Tipo**  
 Exibe o tipo do evento que foi registrado em log. A tabela seguinte lista os possíveis tipos de evento.  
  
|Valor|Description|  
|-----------|-----------------|  
|P|Mensagem de êxito.|  
|E|Mensagem de erro|  
|L|Mensagem de aviso.|  
|I|Mensagem informativa.|  
|Um|A operação foi anulada.|  
  
 **Mensagem**  
 Exibe o texto da mensagem associada ao evento de log.  
  
## <a name="see-also"></a>Consulte Também  
 [Editor de Origem SAP BW &#40;Página Gerenciador de Conexões&#41;](../../integration-services/data-flow/sap-bw-source-editor-connection-manager-page.md)   
 [Ajuda F1 do Microsoft Connector para SAP BW](../../integration-services/microsoft-connector-for-sap-bw-f1-help.md)  
  
  
