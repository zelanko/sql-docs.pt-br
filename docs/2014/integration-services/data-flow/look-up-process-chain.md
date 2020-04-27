---
title: Pesquisar cadeia de processo | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: f6303ea4-fbbf-4cba-bc60-828df62be8c2
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 01c30422e6f0a1beb65c5f72259fce2aa8f80806
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62771126"
---
# <a name="look-up-process-chain"></a>Pesquisar cadeia de processo
  Use a caixa de diálogo **Pesquisar Cadeia de Processo** para pesquisar uma cadeia de processo definida no sistema SAP Netweaver BW. Quando a lista de cadeias de processo disponível é exibida, selecione a cadeia que você quer e a origem preencherá as opções associadas com os valores necessários.  
  
 A origem SAP BW do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 para SAP BW usa a caixa de diálogo **Pesquisar Cadeia de Processo** . Para saber mais sobre a origem de SAP BW, consulte [SAP BW Source](sap-bw-source.md).  
  
> [!IMPORTANT]  
>  A documentação do Microsoft Connector 1.1 for SAP BW supõe familiaridade com o ambiente do SAP Netweaver BW. Para obter mais informações sobre o SAP Netweaver BW ou para obter informações sobre como configurar objetos e processos do SAP Netweaver BW, consulte sua documentação do SAP.  
  
 **Para abrir a caixa de diálogo Pesquisar Cadeia de Processo**  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra o pacote [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que contém a origem SAP BW.  
  
2.  Na guia **Fluxo de Dados** , clique duas vezes na fonte SAP BW.  
  
3.  No **Editor de Origem SAP BW**, clique em **Gerenciador de Conexões** para abrir a página **Gerenciador de Conexões** do editor.  
  
4.  Na caixa de grupo **Cadeia de processo** , clique em **Pesquisar** para exibir a caixa de diálogo **Pesquisar Cadeia de Processo** .  
  
     A caixa de grupo **Cadeia de processo** aparecerá apenas se o valor de **Modo de Execução** for **P – Disparar Cadeia de Processo**.  
  
## <a name="lookup-options"></a>Opções de pesquisa  
 Nos campos de pesquisa, você pode filtrar os resultados usando o caractere curinga asterisco (*) ou usando uma cadeia de caracteres parcial em combinação com o caractere curinga asterisco. No entanto, se você deixar um campo de pesquisa vazio, a operação de pesquisa corresponderá apenas a cadeias de caracteres vazias nesse campo.  
  
 **Cadeia de processo**  
 Digite o nome da cadeia de processo que você deseja pesquisar ou insira um nome parcial com o caractere curinga asterisco (*). Ou use o caractere curinga asterisco sozinho para incluir todas as cadeias de processo.  
  
 **Pesquisar**  
 Pesquisar cadeias de processo compatíveis que sejam definidos no sistema SAP Netweaver BW.  
  
## <a name="lookup-results"></a>Resultados da pesquisa  
 Depois que você clicar no botão Pesquisar, uma lista de cadeias de processo no sistema SAP Netweaver BW é exibido em uma tabela com os seguintes cabeçalhos de coluna.  
  
 **Cadeia de processo**  
 Exibe o nome da cadeia de processo que está definida no sistema SAP Netweaver BW.  
  
 **Descrição**  
 Exibe a descrição da cadeia de processo.  
  
 Quando a lista de cadeias de processo disponível é exibida, selecione a cadeia que você quer e a origem preencherá as opções associadas com os valores necessários.  
  
## <a name="see-also"></a>Consulte Também  
 [Editor de Origem SAP BW &#40;Página Gerenciador de Conexões&#41;](sap-bw-source-editor-connection-manager-page.md)   
 [Ajuda F1 do Microsoft Connector 1.1 for SAP BW](../microsoft-connector-for-sap-bw-f1-help.md)  
  
  
