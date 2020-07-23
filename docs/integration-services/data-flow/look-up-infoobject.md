---
title: Pesquisar InfoObject | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: e7f4c132-a5ec-49d8-a964-45775432731f
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 5fc863ce6460977b2eb91c53531983a0dde92668
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86916493"
---
# <a name="look-up-infoobject"></a>Pesquisar InfoObject

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  Use a caixa de diálogo **Pesquisar InfoObject** para pesquisar um InfoObject definido no sistema SAP Netweaver BW. Quando a lista de InfoObjects disponível é exibida, selecione o InfoObject que você quer e o destino do SAP BW preencherá as opções associadas com os valores necessários.  
  
 O destino SAP BW do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 para SAP BW usa a caixa de diálogo **Pesquisar InfoObject** . Para obter mais informações sobre o destino SAP BW, consulte [SAP BW Destination](../../integration-services/data-flow/sap-bw-destination.md).  
  
> [!IMPORTANT]  
>  A documentação do Microsoft Connector 1.1 for SAP BW supõe familiaridade com o ambiente do SAP Netweaver BW. Para obter mais informações sobre o SAP Netweaver BW ou para obter informações sobre como configurar objetos e processos do SAP Netweaver BW, consulte sua documentação do SAP.  
  
 **Para abrir a caixa de diálogo Pesquisar InfoObject**  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra o pacote [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que contém o destino SAP BW.  
  
2.  Na guia **Fluxo de Dados** , clique duas vezes no destino SAP BW.  
  
3.  No **Editor de Destino SAP BW**, clique em **Gerenciador de Conexões** para abrir a página **Gerenciador de Conexões** do editor.  
  
4.  Na página **Gerenciador de Conexões** , na caixa do grupo **Criar Objetos SAP BW** , selecione uma destas opções:  
  
    1.  Selecione **InfoCube**. Em seguida, clique em **Criar**. Na caixa de diálogo **Criar InfoCube para os Dados da Transação** , clique em **Pesquisar** na coluna **IObject** para uma das linhas na lista. Cada linha representa uma coluna no fluxo de dados do pacote.  
  
    2.  Selecione **InfoSource**. Em seguida, clique em **Criar**. Na caixa de diálogo **Criar InfoSource** , selecione **Dados da Transação**. Na caixa de diálogo **Criar InfoSource para os Dados da Transação** , clique em **Pesquisar** na coluna **IObject** para uma das linhas na lista. Cada linha representa uma coluna no fluxo de dados do pacote.  
  
    3.  Selecione **InfoSource**. Em seguida, clique em **Criar**. Na caixa de diálogo **Criar InfoSource** , selecione **Dados mestres**. Na caixa de diálogo **Criar InfoSource para Dados Mestres** , clique em **Pesquisar**.  
  
 Você também pode abrir a caixa de diálogo **Pesquisar InfoObject** clicando em **Adicionar** na seção **Atributos** da caixa de diálogo **Criar Novo InfoObject** .  
  
## <a name="lookup-options"></a>Opções de pesquisa  
 Nas caixas de texto do campo de pesquisa, você pode filtrar os resultados usando o caractere curinga asterisco (*) ou usando uma cadeia de caracteres parcial em combinação com o caractere curinga asterisco. No entanto, se você deixar um campo de pesquisa vazio, o processo de pesquisa corresponderá apenas a cadeias de caracteres vazias nesse campo.  
  
 **Características**  
 Pesquisar InfoObjects que representam as características.  
  
 **Unidades**  
 Pesquisar InfoObjects que representam as unidades.  
  
 **Valores-chave**  
 Pesquisar InfoObjects que representam as imagens chave.  
  
 **Características de hora**  
 Pesquisar InfoObjects que representam as características de hora.  
  
 **Nome**  
 Digite o nome do InfoObject que você deseja pesquisar ou um nome parcial com o caractere curinga asterisco (*). Ou use o caractere curinga asterisco sozinho para incluir todos os InfoObjects.  
  
 **Descrição**  
 Insira a descrição ou uma descrição parcial com o caractere curinga asterisco (*). Ou use o caractere curinga asterisco sozinho para incluir todos os InfoObjects independentemente da descrição.  
  
 **Pesquisar**  
 Pesquisar InfoObjects compatíveis que sejam definidos no sistema SAP Netweaver BW.  
  
## <a name="lookup-results"></a>Resultados da pesquisa  
 Depois que você clicar no botão Pesquisar, uma lista de InfoObjects no sistema SAP Netweaver BW é exibido em uma tabela com os seguintes cabeçalhos de coluna.  
  
 **InfoObject**  
 Exibe o nome do InfoObject que está definido no sistema SAP Netweaver BW.  
  
 **Texto (curto)**  
 Exibe o texto curto associado ao InfoObject.  
  
 Quando a lista de InfoObjects disponível é exibida, selecione o InfoObject que você quer e o destino preencherá as opções associadas com os valores necessários.  
  
## <a name="see-also"></a>Consulte Também  
 [Criar InfoCube para os Dados da Transação](../../integration-services/data-flow/create-infocube-for-transaction-data.md)   
 [Criar InfoSource](../../integration-services/data-flow/create-infosource.md)   
 [Criar InfoSource para os dados da transação](../../integration-services/data-flow/create-infosource-for-transaction-data.md)   
 [Criar InfoSource para dados mestre](../../integration-services/data-flow/create-infosource-for-master-data.md)   
 [Criar novo InfoObject](../../integration-services/data-flow/create-new-infoobject.md)   
 [Editor de Destino SAP BW &#40;Página Gerenciador de Conexões&#41;](../../integration-services/data-flow/sap-bw-destination-editor-connection-manager-page.md)   
 [Ajuda F1 do Microsoft Connector para SAP BW](../../integration-services/microsoft-connector-for-sap-bw-f1-help.md)  
  
  
