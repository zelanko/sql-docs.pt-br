---
title: Visualizar | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 551494c4-9e27-4592-9200-c6bf19e80c9a
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: b0b0f81c5de267d6e85525714d19999920ba9c71
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62770962"
---
# <a name="preview"></a>Visualizar
  Use a caixa de diálogo **Visualizar** para visualizar os dados que a origem do SAP BW extrairá.  
  
> [!IMPORTANT]  
>  A opção **Visualizar** , que está disponível na página **Gerenciador de Conexões** do **Editor de origem SAP BW**, extrai dados de fato. Se você configurou o SAP Netweaver BW para extrair apenas os dados que foram alterados desde a extração anterior, selecionar **Visualizar** excluirá os dados visualizados da próxima extração.  
  
 Para saber mais sobre o componente de origem do SAP BW do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 para SAP BW, consulte [Origem SAP BW](sap-bw-source.md).  
  
> [!IMPORTANT]  
>  A documentação do Microsoft Connector 1.1 for SAP BW supõe familiaridade com o ambiente do SAP Netweaver BW. Para obter mais informações sobre o SAP Netweaver BW ou para obter informações sobre como configurar objetos e processos do SAP Netweaver BW, consulte sua documentação do SAP.  
  
> [!IMPORTANT]  
>  A extração de dados do SAP Netweaver BW exige licenciamento SAP adicional. Verifique esses requisitos com a SAP.  
  
 **Para abrir a caixa de diálogo Visualizar**  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra o pacote [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que contém a origem SAP BW.  
  
2.  Na guia **Fluxo de Dados** , clique duas vezes na fonte SAP BW.  
  
3.  No **Editor de Origem SAP BW**, clique em **Gerenciador de Conexões** para abrir a página **Gerenciador de Conexões** do editor.  
  
4.  Configure a origem do SAP BW.  
  
5.  Depois de configurar a origem do SAP BW, na página **Gerenciador de Conexões** , clique em **Visualizar** para visualizar os dados na caixa de diálogo **Visualizar** .  
  
    > [!NOTE]  
    >  Clicar em **Visualizar** também abre a caixa de diálogo **Log de Solicitações** . Para obter mais informações sobre essa caixa de diálogo, consulte [Request Log](request-log.md).  
  
## <a name="options"></a>Opções  
 A caixa de diálogo **Visualizar** exibe as linhas que são solicitadas do sistema SAP Netweaver BW. As colunas que são exibidas são as colunas definidas nos dados da origem.  
  
 Não há nenhuma outra opção nesta caixa de diálogo.  
  
## <a name="see-also"></a>Consulte também  
 [Editor de Origem SAP BW &#40;Página Gerenciador de Conexões&#41;](sap-bw-source-editor-connection-manager-page.md)   
 [Ajuda F1 do Microsoft Connector 1.1 para SAP BW](../microsoft-connector-for-sap-bw-f1-help.md)  
  
  
