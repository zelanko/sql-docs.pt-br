---
title: "Editor de Origem SAP BW (página Gerenciador de Conexões) | Microsoft Docs"
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
- sql13.dts.designer.sapbwsource.connection.f1
ms.assetid: 2a6dc531-85ca-43c5-a65f-3ad3f7d537c4
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 0373c0142f2b466b12dd6c2ff1619f09b2b8b26f
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2018
---
# <a name="sap-bw-source-editor-connection-manager-page"></a>Editor de Origem SAP BW (página Gerenciador de Conexões)
  Use a página **Gerenciador de Conexões** da caixa de diálogo **Editor de Origem SAP BW** para selecionar o gerenciador de conexões SAP BW para a origem de SAP BW. Nesta página, você também seleciona o modo de execução e os parâmetros para extrair os dados do sistema SAP Netweaver BW.  
  
 Para saber mais sobre o componente de origem do SAP BW do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 para SAP BW, consulte [Origem SAP BW](../../integration-services/data-flow/sap-bw-source.md).  
  
> [!IMPORTANT]  
>  A documentação do Microsoft Connector 1.1 for SAP BW supõe familiaridade com o ambiente do SAP Netweaver BW. Para obter mais informações sobre o SAP Netweaver BW ou para obter informações sobre como configurar objetos e processos do SAP Netweaver BW, consulte sua documentação do SAP.  
  
> [!IMPORTANT]  
>  A extração de dados do SAP Netweaver BW exige licenciamento SAP adicional. Verifique esses requisitos com a SAP.  
  
 **Para abrir a página Gerenciador de Conexões**  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra o pacote [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que contém a origem SAP BW.  
  
2.  Na guia **Fluxo de Dados** , clique duas vezes na fonte SAP BW.  
  
3.  No **Editor de Origem SAP BW**, clique em **Gerenciador de Conexões** para abrir a página **Gerenciador de Conexões** do editor.  
  
## <a name="static-options"></a>Opções estáticas  
  
> [!NOTE]  
>  Se você não souber todos os valores necessários para configurar a origem, talvez precise perguntar ao administrador do SAP.  
  
 **Gerenciador de conexões SAP BW**  
 Selecione um gerenciador de conexões existente na lista ou crie uma nova conexão clicando em **Nova**.  
  
 **Nova**  
 Crie um novo gerenciador de conexões, usando a caixa de diálogo **Gerenciador de Conexões SAP BW** .  
  
 Para obter mais informações sobre essa caixa de diálogo, consulte [SAP BW Connection Manager Editor](../../integration-services/connection-manager/sap-bw-connection-manager-editor.md).  
  
 **Destino OHS**  
 Selecione o destino do OHS (Open Hub Service) a ser usado para extrair dados da origem.  
  
 **Modo de execução**  
 Especifique o método para extrair os dados da origem.  
  
|Opção|Description|  
|------------|-----------------|  
|**P - Disparar Cadeia de Processo**|Disparar uma cadeia de processo. Nesse caso, o pacote do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] inicia o processo de extração.|  
|**A - Aguardar Notificação**|Aguarde a notificação do sistema SAP Netweaver BW para iniciar a extração dos dados. Nesse caso, o sistema do SAP Netweaver BW inicia o processo de extração.|  
|**E - Extrair Somente**|Recupere os dados associados a uma ID de solicitação específica Nesse caso, o sistema SAP Netweaver BW já extraiu os dados em uma tabela interna e o pacote do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] apenas lê os dados.|  
  
 **Visualização**  
 Abra a caixa de diálogo **Visualizar** em que você pode visualizar os resultados. Para obter mais informações, consulte [Preview](../../integration-services/data-flow/preview.md).  
  
> [!IMPORTANT]  
>  A opção **Visualizar** , que está disponível na página **Gerenciador de Conexões** do editor de origem SAP BW, extrai dados de fato. Se você configurou o SAP Netweaver BW para extrair apenas os dados que foram alterados desde a extração anterior, selecionar **Visualizar** excluirá os dados visualizados da próxima extração.  
  
 Quando você clica em **Visualizar**, também abre a caixa de diálogo **Log de Solicitações** . Você pode usar essa caixa de diálogo para exibir os eventos que são registrados em log durante a solicitação que é feita no sistema SAP Netweaver BW para dados de exemplo. Para obter mais informações, consulte [Request Log](../../integration-services/data-flow/request-log.md).  
  
## <a name="execution-mode-dynamic-options"></a>Opções dinâmicas do modo de execução  
  
> [!NOTE]  
>  Se você não souber todos os valores necessários para configurar a origem, talvez precise perguntar ao administrador do SAP.  
  
### <a name="execution-mode--p---trigger-process-chain"></a>Modo de execução = P - Disparar Cadeia de Processo  
  
#### <a name="rfc-destination-options"></a>Opções de destino RFC  
 Você não precisa saber e inserir esses valores com antecedência. Use o botão **Pesquisar** para localizar e selecionar o destino RFC apropriado. Depois de selecionar um destino RFC, o componente insere os valores apropriados para essas opções.  
  
 **Host do gateway**  
 Digite o nome do servidor ou endereço IP do host do gateway. Em geral, o nome ou o endereço IP é o mesmo que o servidor de aplicativos do SAP.  
  
 **Serviço do gateway**  
 Digite o nome do serviço de gateway, no formato **sapgwNN**, em que **NN** é o número do sistema.  
  
 **ID do Programa**  
 Insira a ID do programa que está associada ao destino RFC.  
  
 **Pesquisar**  
 Pesquisar o destino RFC usando a caixa de diálogo **Pesquisar Destino RFC** . Para obter mais informações sobre essa caixa de diálogo, consulte [Look Up RFC Destination](../../integration-services/data-flow/look-up-rfc-destination.md).  
  
#### <a name="process-chain-options"></a>Opções da cadeia do processo  
 Você não precisa saber e inserir esses valores com antecedência. Use o botão **Pesquisar** para localizar e selecionar a cadeia de processo apropriada. Depois de selecionar uma cadeia de processo, o componente insere o valor apropriado para a opção.  
  
 **Cadeia de processo**  
 Digite o nome da cadeia de processo a ser disparada pela origem.  
  
 **Pesquisar**  
 Pesquisar a cadeia de processo usando a caixa de diálogo **Pesquisar Cadeia de Processo** . Para obter mais informações sobre essa caixa de diálogo, consulte [Look Up Process Chain](../../integration-services/data-flow/look-up-process-chain.md).  
  
### <a name="execution-mode--w---wait-for-notify"></a>Modo de execução = A - Aguardar Notificação  
  
#### <a name="rfc-destination-options"></a>Opções de destino RFC  
 Você não precisa saber e inserir esses valores com antecedência. Use o botão **Pesquisar** para localizar e selecionar o destino RFC apropriado. Depois de selecionar um destino RFC, o componente insere os valores apropriados para as opções.  
  
 **Host do gateway**  
 Digite o nome do servidor ou endereço IP do host do gateway. Em geral, o nome ou o endereço IP é o mesmo que o servidor de aplicativos do SAP.  
  
 **Serviço do gateway**  
 Digite o nome do serviço de gateway, no formato **sapgwNN**, em que **NN** é o número do sistema.  
  
 **ID do Programa**  
 Insira a ID do programa que está associada ao destino RFC.  
  
 **Pesquisar**  
 Pesquisar o destino RFC usando a caixa de diálogo **Pesquisar Destino RFC** . Para obter mais informações sobre essa caixa de diálogo, consulte [Look Up RFC Destination](../../integration-services/data-flow/look-up-rfc-destination.md).  
  
### <a name="execution-mode--e---extract-only"></a>Modo de execução = E - Extrair Somente  
 **Request ID**  
 Insira a ID de solicitação que está associada à extração.  
  
## <a name="see-also"></a>Consulte Também  
 [Editor de Origem SAP BW &#40;Página Colunas&#41;](../../integration-services/data-flow/sap-bw-source-editor-columns-page.md)   
 [Editor de Origem SAP BW &#40;Página Saída de Erro&#41;](../../integration-services/data-flow/sap-bw-source-editor-error-output-page.md)   
 [Editor de Origem SAP BW &#40;Página Avançado&#41;](../../integration-services/data-flow/sap-bw-source-editor-advanced-page.md)   
 [Ajuda F1 do Microsoft Connector para SAP BW](../../integration-services/microsoft-connector-for-sap-bw-f1-help.md)  
  
  
