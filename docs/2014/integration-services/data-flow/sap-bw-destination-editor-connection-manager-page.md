---
title: Editor de destino SAP BW (página Gerenciador de Conexões) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 04ae38f8-5287-45a3-826a-8aac5dd15a91
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: e4d8da5c0b352964fe9017be902557e29e1e2ed3
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52781418"
---
# <a name="sap-bw-destination-editor-connection-manager-page"></a>Editor de Destino SAP BW (página Gerenciador de Conexões)
  Use a página **Gerenciador de Conexões** da caixa de diálogo **Editor de Destino SAP BW** para selecionar o gerenciador de conexões do SAP BW que o destino de SAP BW usará. Nesta página, você também seleciona os parâmetros para carregar os dados no sistema SAP Netweaver BW.  
  
 Para saber mais sobre o destino SAP BW do Connector 1.1 do [!INCLUDE[msCoName](../../includes/msconame-md.md)] para SAP BW, consulte [Destino SAP BW](sap-bw-destination.md).  
  
> [!IMPORTANT]  
>  A documentação do Microsoft Connector 1.1 for SAP BW supõe familiaridade com o ambiente do SAP Netweaver BW. Para obter mais informações sobre o SAP Netweaver BW ou para obter informações sobre como configurar objetos e processos do SAP Netweaver BW, consulte sua documentação do SAP.  
  
 **Para abrir a página Gerenciador de Conexões**  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra o pacote [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que contém o destino SAP BW.  
  
2.  Na guia **Fluxo de Dados** , clique duas vezes no destino SAP BW.  
  
3.  No **Editor de Destino SAP BW**, clique em **Gerenciador de Conexões** para abrir a página **Gerenciador de Conexões** do editor.  
  
## <a name="options"></a>Opções  
  
> [!NOTE]  
>  Se você não souber todos os valores necessários para configurar o destino, talvez precise perguntar ao administrador do SAP.  
  
 **Gerenciador de conexões SAP BW**  
 Selecione um gerenciador de conexões existente na lista ou crie uma nova conexão clicando em **Nova**.  
  
 **Nova**  
 Crie um novo gerenciador de conexões, usando a caixa de diálogo **Gerenciador de Conexões SAP BW** .  
  
 **Testar carga**  
 Execute um teste do processo de carga que usa as configurações selecionadas e não carrega nenhuma linha.  
  
### <a name="infopackageinfosource-options"></a>Opções do InfoPackage/InfoSource  
 Você não precisa saber e inserir esses valores com antecedência. Use o botão **Pesquisar** para localizar e selecionar o InfoPackage apropriado. Depois de selecionar um InfoPackage, o componente insere os valores apropriados para essas opções.  
  
 **InfoPackage**  
 Digite o nome do InfoPackage.  
  
 **InfoSource**  
 Digite o nome do InfoSource.  
  
 **Tipo**  
 Digite o caractere único que identifica o tipo do InfoSource. A tabela a seguir lista os valores aceitáveis de caractere único.  
  
|Value|Descrição|  
|-----------|-----------------|  
|**D**|Dados da transação|  
|**M**|Dados mestres|  
|**T**|Textos|  
|**H**|Dados da hierarquia|  
  
 **Sistema lógico**  
 Insira o nome do sistema lógico que está associado ao InfoPackage.  
  
 **Pesquisar**  
 Pesquisar o InfoPackage usando a caixa de diálogo **Pesquisar InfoPackage** . Para obter mais informações sobre essa caixa de diálogo, consulte [Look Up InfoPackage](look-up-infopackage.md).  
  
### <a name="rfc-destination-options"></a>Opções de destino RFC  
 Você não precisa saber e inserir esses valores com antecedência. Use o botão **Pesquisar** para localizar e selecionar o destino RFC apropriado. Depois de selecionar um destino RFC, o componente insere os valores apropriados para essas opções.  
  
 **Host do gateway**  
 Digite o nome do servidor ou endereço IP do host do gateway. Em geral, o nome ou o endereço IP é o mesmo que o servidor de aplicativos do SAP.  
  
 **Serviço do gateway**  
 Digite o nome do serviço de gateway, no formato `sapgwNN`, em que `NN` é o número do sistema.  
  
 **ID do Programa**  
 Insira a ID do programa que está associada ao destino RFC.  
  
 **Pesquisar**  
 Pesquisar o destino RFC usando a caixa de diálogo **Pesquisar Destino RFC** . Para obter mais informações sobre essa caixa de diálogo, consulte [Look Up RFC Destination](look-up-rfc-destination.md).  
  
### <a name="create-sap-bw-objects-options"></a>Criar opções de objetos SAP BW  
 **Selecionar tipo de objeto**  
 Selecione o tipo de objeto SAP Netweaver BW que deseja criar. Você pode selecionar um dos seguintes tipos:  
  
-   InfoObject  
  
-   InfoCube  
  
-   InfoSource  
  
-   InfoPackage  
  
 **Criar**  
 Crie o tipo selecionado de objeto do SAP Netweaver BW.  
  
|Tipo de objeto|Resultado|  
|-----------------|------------|  
|**InfoObject**|Crie um novo InfoObject usando a caixa de diálogo **Criar Novo InfoObject** . Para obter mais informações sobre essa caixa de diálogo, consulte [Create New InfoObject](create-new-infoobject.md).|  
|**InfoCube**|Crie um novo InfoCube usando a caixa de diálogo **Criar InfoCube para os Dados da Transação** . Para obter mais informações sobre essa caixa de diálogo, consulte [Create InfoCube for Transaction Data](create-infocube-for-transaction-data.md).|  
|**InfoSource**|Crie um novo InfoSource usando a caixa de diálogo **Criar InfoSource** e, em seguida, **Criar InfoSource para os Dados da Transação** ou **Criar InfoSource para Dados Mestres** . Para obter mais informações sobre essas caixas de diálogo, consulte [Create InfoSource](create-infosource.md), [Create InfoSource for Transaction Data](create-infosource-for-transaction-data.md) e [Create InfoSource for Master Data](create-infosource-for-master-data.md).|  
|**InfoPackage**|Crie um novo InfoPackage usando a caixa de diálogo **Criar InfoPackage** . Para obter mais informações sobre essa caixa de diálogo, consulte [Create InfoPackage](create-infopackage.md).|  
  
## <a name="see-also"></a>Consulte também  
 [Editor de Destino SAP BW &#40;Página Mapeamentos&#41;](sap-bw-destination-editor-mappings-page.md)   
 [Editor de Destino SAP BW &#40;Página Saída de Erro&#41;](sap-bw-destination-editor-error-output-page.md)   
 [Editor de Destino SAP BW &#40;Página Avançado&#41;](sap-bw-destination-editor-advanced-page.md)   
 [Ajuda F1 do Microsoft Connector 1.1 para SAP BW](../microsoft-connector-for-sap-bw-f1-help.md)  
  
  
