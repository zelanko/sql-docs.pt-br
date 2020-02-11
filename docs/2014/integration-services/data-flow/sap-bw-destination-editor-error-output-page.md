---
title: Editor de destino de SAP BW (página Saída de Erro) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: a543d811-0bd2-4890-a0d3-f5fdcd4524b8
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 196d7f2bb3a227bd29ccc6fd5d427a59070d525a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62770912"
---
# <a name="sap-bw-destination-editor-error-output-page"></a>Editor de Destino de SAP BW (página Saída de Erro)
  Use a página **Saída de Erro** do **Editor de Destino SAP BW** para especificar opções de tratamento de erro.  
  
 Para saber mais sobre o destino SAP BW do Connector 1.1 do [!INCLUDE[msCoName](../../includes/msconame-md.md)] para SAP BW, consulte [Destino SAP BW](sap-bw-destination.md).  
  
> [!IMPORTANT]  
>  A documentação do Microsoft Connector 1.1 for SAP BW supõe familiaridade com o ambiente do SAP Netweaver BW. Para obter mais informações sobre o SAP Netweaver BW ou para obter informações sobre como configurar objetos e processos do SAP Netweaver BW, consulte sua documentação do SAP.  
  
 **Para abrir a página Saída de Erro**  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra o pacote [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que contém o destino SAP BW.  
  
2.  Na guia **Fluxo de Dados** , clique duas vezes no destino SAP BW.  
  
3.  No **Editor de Destino SAP BW**, clique em **Saída do Erro** para abrir a página **Saída do Erro** do editor.  
  
## <a name="options"></a>Opções  
  
> [!NOTE]  
>  Se você não souber todos os valores necessários para configurar o destino, talvez precise perguntar ao administrador do SAP.  
  
 **Entrada ou Saída**  
 Visualize o nome da entrada.  
  
 **Coluna**  
 Esta opção não é usada.  
  
 **Erro**  
 Especifique o que o destino deve fazer quando ocorrer um erro: ignorar a falha, redirecionar a linha ou falhar o componente.  
  
 **Truncation**  
 Esta opção não é usada.  
  
 **Descrição**  
 Visualize a descrição da operação.  
  
 **Definir este valor para células selecionadas**  
 Especifique o que o destino deve fazer a todas as células selecionadas quando ocorre um erro ou um truncamento: ignorar a falha, redirecionar a linha ou causar a falha no componente.  
  
 **Aplicar**  
 Aplique a opção de tratamento de erros às células selecionadas.  
  
## <a name="see-also"></a>Consulte Também  
 [Editor de Destino SAP BW &#40;Página Gerenciador de Conexões&#41;](sap-bw-destination-editor-connection-manager-page.md)   
 [Editor de Destino SAP BW &#40;Página Mapeamentos&#41;](sap-bw-destination-editor-mappings-page.md)   
 [Editor de Destino SAP BW &#40;Página Avançado&#41;](sap-bw-destination-editor-advanced-page.md)   
 [Ajuda F1 do Microsoft Connector 1.1 for SAP BW](../microsoft-connector-for-sap-bw-f1-help.md)  
  
  
