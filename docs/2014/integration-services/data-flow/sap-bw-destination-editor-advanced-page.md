---
title: Editor de destino SAP BW (página Avançado) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
ms.assetid: 862957db-bbc6-4dda-bc0e-591457f1baa7
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 404fdbe10430e09ad2be96ec31b45c4bbf563260
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48159603"
---
# <a name="sap-bw-destination-editor-advanced-page"></a>Editor de Destino SAP BW (página Avançado)
  Use a página **Avançado** do **Editor de Destino SAP BW** para definir as configurações avançadas como o tamanho do pacote e informações de tempo limite.  
  
 Para saber mais sobre o destino SAP BW do Connector 1.1 do [!INCLUDE[msCoName](../../includes/msconame-md.md)] para SAP BW, consulte [Destino SAP BW](sap-bw-destination.md).  
  
> [!IMPORTANT]  
>  A documentação do Microsoft Connector 1.1 for SAP BW supõe familiaridade com o ambiente do SAP Netweaver BW. Para obter mais informações sobre o SAP Netweaver BW ou para obter informações sobre como configurar objetos e processos do SAP Netweaver BW, consulte sua documentação do SAP.  
  
 **Para abrir a página Avançado**  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra o pacote [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que contém o destino SAP BW.  
  
2.  Na guia **Fluxo de Dados** , clique duas vezes no destino SAP BW.  
  
3.  No **Editor de Destino SAP BW**, clique em **Avançado** para abrir a página **Avançada** do editor.  
  
## <a name="options"></a>Opções  
  
> [!NOTE]  
>  Se você não souber todos os valores necessários para configurar o destino, talvez precise perguntar ao administrador do SAP.  
  
 **Tamanho do pacote**  
 Especifique quantas linhas de dados serão transferidas de cada vez. O valor ideal para esse parâmetro depende do sistema SAP Netweaver BW e do processamento adicional dos dados que podem ocorrer. Normalmente, os valores entre 2000 e 20000 oferecem o melhor desempenho.  
  
 **Disparar cadeia de processo**  
 (Opcional) Especifique o nome de uma cadeia do processo a ser acionada depois que o carregamento dos dados for concluído.  
  
 **Tempo limite de espera pelo InfoPackage**  
 Especifique o número máximo de segundos que o destino deve aguardar o InfoPackage concluir.  
  
 **Aguardar a conclusão da transferência de dados**  
 Especifique se o destino deve aguardar até que o sistema SAP Netweaver BW termine de carregar os dados.  
  
 **Não Iniciar InfoPackage (aguardar apenas)**  
 Especifique que o destino não aciona um InfoPackage, mas apenas aguarda a notificação que o sistema SAP Netweaver BW iniciou o carregamento dos dados.  
  
## <a name="see-also"></a>Consulte também  
 [Editor de destino SAP BW &#40;página do Gerenciador de Conexão&#41;](sap-bw-destination-editor-connection-manager-page.md)   
 [Editor de destino SAP BW &#40;página mapeamentos&#41;](sap-bw-destination-editor-mappings-page.md)   
 [Editor de Destino SAP BW &#40;Página Saída de Erro&#41;](sap-bw-destination-editor-error-output-page.md)   
 [Ajuda F1 do Microsoft Connector 1.1 para SAP BW](../microsoft-connector-for-sap-bw-f1-help.md)  
  
  
