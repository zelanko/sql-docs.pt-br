---
title: Editor de Origem SAP BW (página Colunas) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: c2ec8bb7-be9b-4783-ad88-32512de784b0
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: f0031b874b2477bff53f8f0855b557a3188c3719
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62770885"
---
# <a name="sap-bw-source-editor-columns-page"></a>Editor de Origem de SAP BW (página Colunas)
  Use a página **Colunas** do **Editor de Origem SAP BW** para mapear uma coluna de saída em cada coluna externa (origem).  
  
 Para saber mais sobre o componente de origem do SAP BW do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 para SAP BW, consulte [Origem SAP BW](sap-bw-source.md).  
  
> [!IMPORTANT]  
>  A documentação do Microsoft Connector 1.1 for SAP BW supõe familiaridade com o ambiente do SAP Netweaver BW. Para obter mais informações sobre o SAP Netweaver BW ou para obter informações sobre como configurar objetos e processos do SAP Netweaver BW, consulte sua documentação do SAP.  
  
> [!IMPORTANT]  
>  A extração de dados do SAP Netweaver BW exige licenciamento SAP adicional. Verifique esses requisitos com a SAP.  
  
 **Para abrir a página Colunas**  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra o pacote [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que contém a origem SAP BW.  
  
2.  Na guia **Fluxo de Dados** , clique duas vezes na fonte SAP BW.  
  
3.  No **Editor de Origem SAP BW**, clique em **Colunas** para abrir a página **Colunas** do editor.  
  
## <a name="options"></a>Opções  
  
> [!NOTE]  
>  Se você não souber todos os valores necessários para configurar a origem, talvez precise perguntar ao administrador do SAP.  
  
 **Colunas Externas Disponíveis**  
 Exiba a lista de colunas externas disponíveis na fonte de dados, e selecione as colunas a serem incluídas no fluxo de dados.  
  
 Para incluir uma coluna no fluxo de dados, marque a caixa de seleção que corresponde a essa coluna. A ordem na qual você seleciona as caixas de seleção determina a ordem na qual as colunas serão geradas. Ou seja a primeira caixa de seleção que você selecionar será a primeira coluna gerada, a segunda caixa de seleção será a segunda e assim por diante.  
  
 **Coluna Externa**  
 Visualize as colunas externas (origem) selecionadas. As colunas selecionadas aparecem na ordem na que você verá suas colunas geradas correspondentes ao configurar os componentes downstream que consomem os dados dessa fonte.  
  
 Para alterar a ordem das colunas, na lista **Colunas Externas Disponíveis** , desmarque as caixas de seleção para todas as colunas. Em seguida, selecione as colunas na ordem que você quer que elas apareçam.  
  
 **Coluna de Saída**  
 Forneça um nome exclusivo para cada coluna de saída. O padrão é o nome da coluna externa (origem) selecionada. No entanto, você pode inserir qualquer nome descritivo exclusivo. [!INCLUDE[ssIS](../../includes/ssis-md.md)] exibirá os nomes de **Coluna de Saída** para as colunas ao configurar os componentes downstream que consomem os dados dessa fonte.  
  
## <a name="see-also"></a>Consulte também  
 [Editor de Origem SAP BW &#40;Página Gerenciador de Conexões&#41;](sap-bw-source-editor-connection-manager-page.md)   
 [Editor de Origem SAP BW &#40;Página Saída de Erro&#41;](sap-bw-source-editor-error-output-page.md)   
 [Editor de Origem SAP BW &#40;Página Avançado&#41;](sap-bw-source-editor-advanced-page.md)   
 [Ajuda F1 do Microsoft Connector 1.1 para SAP BW](../microsoft-connector-for-sap-bw-f1-help.md)  
  
  
