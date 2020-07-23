---
title: Criar InfoSource para os dados da transação | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: ab5f23e2-cd4e-4507-83d9-ac5ef721c171
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 28c3d7da3777f20957d0bdd4cf0881453af2cc00
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86923970"
---
# <a name="create-infosource-for-transaction-data"></a>Criar InfoSource para os dados da transação

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  Use a caixa de diálogo **Criar InfoSource para os Dados da Transação** para criar um novo InfoSource para dados de transação no sistema SAP Netweaver BW.  
  
 Você pode abrir a caixa de diálogo **Criar InfoSource para os Dados da Transação** da página **Gerenciador de Conexões** do **Editor de Destino SAP BW**. Para obter mais informações sobre o destino SAP BW, consulte [SAP BW Destination](../../integration-services/data-flow/sap-bw-destination.md).  
  
> [!IMPORTANT]  
>  A documentação do Microsoft Connector 1.1 for SAP BW supõe familiaridade com o ambiente do SAP Netweaver BW. Para obter mais informações sobre o SAP Netweaver BW ou para obter informações sobre como configurar objetos e processos do SAP Netweaver BW, consulte sua documentação do SAP.  
  
 **Para abrir a caixa de diálogo Criar InfoSource para os Dados da Transação**  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra o pacote [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que contém o destino SAP BW.  
  
2.  Na guia **Fluxo de Dados** , clique duas vezes no destino SAP BW.  
  
3.  No **Editor de Destino SAP BW**, clique em **Gerenciador de Conexões** para abrir a página **Gerenciador de Conexões** do editor.  
  
4.  Na página **Gerenciador de Conexões** , na caixa de grupo **Criar Objetos SAP BW** , selecione **InfoSource**e clique em **Criar**.  
  
5.  Na caixa de diálogo **Criar InfoSource** , selecione **Dados da Transação**e clique em **OK**.  
  
## <a name="general-options"></a>Opções gerais  
 **Nome do InfoSource**  
 Digite um nome para o novo InfoSource.  
  
 **Descrição breve**  
 Insira uma descrição curta para o novo InfoSource.  
  
 **Descrição longa**  
 Insira uma descrição longa para o novo InfoSource.  
  
 **Sistema de origem**  
 Selecione o sistema de origem associado ao InfoSource.  
  
 **Salvar e Ativar**  
 Salvar e ativar o novo InfoSource.  
  
## <a name="infosource-transfer-structure-options"></a>Opções da estrutura de transferência do InfoSource  
 A estrutura de transferência do InfoSource permite associar colunas de fluxo de dados a InfoSources.  
  
 **PipelineElement**  
 Exibe a coluna na saída do fluxo de dados que está conectado ao destino SAP BW.  
  
 **PipelineDataType**  
 Exibe o tipo de dados [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] da coluna de fluxo de dados.  
  
 **Iobject - Pesquisa**  
 Associar um InfoObject existente à coluna de fluxo de dados na linha atual. Para fazer essa associação, clique em **Pesquisar** e use a caixa de diálogo **Pesquisar InfoObject** para selecionar o InfoObject existente. Para obter mais informações sobre essa caixa de diálogo, consulte [Look Up InfoObject](../../integration-services/data-flow/look-up-infoobject.md).  
  
 Depois de selecionar um InfoObject existente, o componente preenche as colunas **InfoObject** e **Tipo** com os valores selecionados.  
  
 **Iobject - Novo**  
 Crie um novo InfoObject e associe esse novo InfoObject à coluna de fluxo de dados na linha atual. Para criar o novo InfoObject, clique em **Novo**e use a caixa de diálogo **Criar Novo InfoObject** para criar o InfoObject. Para obter mais informações sobre essa caixa de diálogo, consulte [Create New InfoObject](../../integration-services/data-flow/create-new-infoobject.md).  
  
 Depois de criar um novo InfoObject, o componente preenche as colunas **InfoObject** e **Tipo** com os novos valores.  
  
 **Iobject - Remover**  
 Remover a associação entre o InfoObject e a coluna de fluxo de dados para a linha atual. Para remover essa associação, clique em **Remover**.  
  
 **InfoObject**  
 Exibe o nome do InfoObject associado à coluna de fluxo de dados.  
  
 **Tipo**  
 Exibe o tipo do InfoObject associado à coluna de fluxo de dados. A tabela a seguir lista os valores possíveis do tipo.  
  
|Valor|DESCRIÇÃO|  
|-----------|-----------------|  
|CHA|Características|  
|UNI|Unidades|  
|KYF|Valores-chave|  
|TIM|Características de hora|  
  
 **Campo unidade**  
 Especifique as unidades que o InfoObject usará.  
  
## <a name="see-also"></a>Consulte Também  
 [Criar InfoSource](../../integration-services/data-flow/create-infosource.md)   
 [Ajuda F1 do Microsoft Connector para SAP BW](../../integration-services/microsoft-connector-for-sap-bw-f1-help.md)  
  
  
