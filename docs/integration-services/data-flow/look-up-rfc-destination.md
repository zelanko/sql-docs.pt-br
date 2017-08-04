---
title: Pesquisar destino RFC | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: db9404d8-4c42-45e5-a100-c7a84b056109
caps.latest.revision: 10
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 3c9db6a056a69d502b4a93b9575cb565da798adf
ms.contentlocale: pt-br
ms.lasthandoff: 08/03/2017

---
# <a name="look-up-rfc-destination"></a>Pesquisar destino RFC
  Use a caixa de diálogo **Pesquisar Destino RFC** para pesquisar um Destino RFC definido no sistema SAP Netweaver BW. Quando a lista de Destino RFC disponível é exibida, selecione o destino que você quer e o componente preencherá as opções associadas com os valores necessários.  
  
 A origem SAP BW e o destino SAP BW usam a caixa de diálogo **Pesquisar Destino RFC** . Para obter mais informações sobre esses componentes do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 para SAP BW, consulte [Fonte SAP BW](../../integration-services/data-flow/sap-bw-source.md) e [Destino SAP BW](../../integration-services/data-flow/sap-bw-destination.md).  
  
> [!IMPORTANT]  
>  A documentação do Microsoft Connector 1.1 for SAP BW supõe familiaridade com o ambiente do SAP Netweaver BW. Para obter mais informações sobre o SAP Netweaver BW ou para obter informações sobre como configurar objetos e processos do SAP Netweaver BW, consulte sua documentação do SAP.  
  
 **Para abrir a caixa de diálogo Pesquisar Destino RFC**  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra o pacote [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que contém a origem ou destino SAP BW.  
  
2.  Na guia **Fluxo de Dados** , clique duas vezes na origem ou destino SAP BW.  
  
3.  No **Editor de Origem SAP BW** ou **Editor de Destino SAP BW**, clique em **Gerenciador de Conexões** para abrir a página **Gerenciador de Conexões** do editor.  
  
4.  Na página **Gerenciador de Conexões** , na caixa de grupo **Destino RFC** , clique em **Pesquisar** para exibir a caixa de diálogo **Pesquisar Destino RFC** .  
  
     No **Editor de Origem SAP BW**, a caixa de grupo **Destino RFC** aparecerá apenas se o valor do **Modo de Execução** for **P - Disparar Cadeia de Processo** ou **A - Aguardar Notificação**.  
  
## <a name="options"></a>Opções  
 **Destino**  
 Exibe o nome do destino RFC que está definido no sistema SAP Netweaver BW.  
  
 **Host do Gateway**  
 Exiba o nome do servidor ou endereço IP do host do gateway. Em geral, o nome ou o endereço IP é o mesmo que o servidor de aplicativos do SAP.  
  
 **Serviço de gateway**  
 Exiba o nome do serviço de gateway, no formato **sapgwNN**, em que **NN** é o número do sistema.  
  
 **ID do Programa**  
 Exiba a ID do programa que está associada ao destino RFC.  
  
## <a name="see-also"></a>Consulte também  
 [Editor de origem do SAP BW &#40; Página Gerenciador de Conexão &#41;](../../integration-services/data-flow/sap-bw-source-editor-connection-manager-page.md)   
 [Editor de destino do SAP BW &#40; Página Gerenciador de Conexão &#41;](../../integration-services/data-flow/sap-bw-destination-editor-connection-manager-page.md)   
 [Ajuda F1 do Microsoft Connector for SAP BW](../../integration-services/microsoft-connector-for-sap-bw-f1-help.md)  
  
  
