---
title: Pesquisar destino RFC | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: db9404d8-4c42-45e5-a100-c7a84b056109
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 4badd9c961f5a0d7ca2d3e32185a7ab742628d97
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62901775"
---
# <a name="look-up-rfc-destination"></a>Pesquisar destino RFC
  Use a caixa de diálogo **Pesquisar Destino RFC** para pesquisar um Destino RFC definido no sistema SAP Netweaver BW. Quando a lista de Destino RFC disponível é exibida, selecione o destino que você quer e o componente preencherá as opções associadas com os valores necessários.  
  
 A origem SAP BW e o destino SAP BW usam a caixa de diálogo **Pesquisar Destino RFC** . Para obter mais informações sobre esses componentes do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 para SAP BW, consulte [Fonte SAP BW](sap-bw-source.md) e [Destino SAP BW](sap-bw-destination.md).  
  
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
 Exiba o nome do serviço de gateway, no formato `sapgwNN`, em que `NN` é o número do sistema.  
  
 **ID do Programa**  
 Exiba a ID do programa que está associada ao destino RFC.  
  
## <a name="see-also"></a>Consulte também  
 [Editor de Origem SAP BW &#40;Página Gerenciador de Conexões&#41;](sap-bw-source-editor-connection-manager-page.md)   
 [Editor de Destino SAP BW &#40;Página Gerenciador de Conexões&#41;](sap-bw-destination-editor-connection-manager-page.md)   
 [Ajuda F1 do Microsoft Connector 1.1 para SAP BW](../microsoft-connector-for-sap-bw-f1-help.md)  
  
  
