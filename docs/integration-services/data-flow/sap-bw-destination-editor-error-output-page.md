---
title: "Editor de destino do SAP BW (página saída de erro) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: data-flow
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.sapbwdestination.erroroutput.f1
ms.assetid: a543d811-0bd2-4890-a0d3-f5fdcd4524b8
caps.latest.revision: 10
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: f1b243b6fae68be78e20bbb87a18c16cb78d24f7
ms.contentlocale: pt-br
ms.lasthandoff: 08/03/2017

---
# <a name="sap-bw-destination-editor-error-output-page"></a>Editor de Destino de SAP BW (página Saída de Erro)
  Use a página **Saída de Erro** do **Editor de Destino SAP BW** para especificar opções de tratamento de erro.  
  
 Para saber mais sobre o destino SAP BW do Connector 1.1 do [!INCLUDE[msCoName](../../includes/msconame-md.md)] para SAP BW, consulte [Destino SAP BW](../../integration-services/data-flow/sap-bw-destination.md).  
  
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
  
 **Description**  
 Visualize a descrição da operação.  
  
 **Definir este valor para células selecionadas**  
 Especifique o que o destino deve fazer a todas as células selecionadas quando ocorre um erro ou um truncamento: ignorar a falha, redirecionar a linha ou causar a falha no componente.  
  
 **Aplicar**  
 Aplique a opção de tratamento de erros às células selecionadas.  
  
## <a name="see-also"></a>Consulte também  
 [Editor de destino do SAP BW &#40; Página Gerenciador de Conexão &#41;](../../integration-services/data-flow/sap-bw-destination-editor-connection-manager-page.md)   
 [Editor de destino do SAP BW &#40; Página mapeamentos &#41;](../../integration-services/data-flow/sap-bw-destination-editor-mappings-page.md)   
 [Editor de destino do SAP BW &#40; Página Avançado &#41;](../../integration-services/data-flow/sap-bw-destination-editor-advanced-page.md)   
 [Ajuda F1 do Microsoft Connector for SAP BW](../../integration-services/microsoft-connector-for-sap-bw-f1-help.md)  
  
  

