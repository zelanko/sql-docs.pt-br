---
title: Criar InfoCube para os dados da transação | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 673cea01-a260-4fce-a1a0-f73839289805
caps.latest.revision: 9
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: e002bdd169d03e0db1cd972ac6e1c52adc19946c
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36131037"
---
# <a name="create-infocube-for-transaction-data"></a>Criar InfoCube para os dados da transação
  Use a caixa de diálogo **Criar InfoCube para os Dados da Transação** para criar um novo InfoCube para dados de transação no sistema SAP Netweaver BW.  
  
 Você pode abrir a caixa de diálogo **Criar InfoCube para os Dados da Transação** da página **Gerenciador de Conexões** do **Editor de Destino SAP BW**. Para obter mais informações sobre o destino SAP BW, consulte [SAP BW Destination](sap-bw-destination.md).  
  
> [!IMPORTANT]  
>  A documentação do Microsoft Connector 1.1 for SAP BW supõe familiaridade com o ambiente do SAP Netweaver BW. Para obter mais informações sobre o SAP Netweaver BW ou para obter informações sobre como configurar objetos e processos do SAP Netweaver BW, consulte sua documentação do SAP.  
  
 **Para abrir a caixa de diálogo Criar InfoCube para os Dados da Transação**  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra o pacote [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que contém o destino SAP BW.  
  
2.  Na guia **Fluxo de Dados** , clique duas vezes no destino SAP BW.  
  
3.  No **Editor de Destino SAP BW**, clique em **Gerenciador de Conexões** para abrir a página **Gerenciador de Conexões** do editor.  
  
4.  Na página **Gerenciador de Conexões** , na caixa de grupo **Criar Objetos SAP BW** , selecione **InfoCube**e clique em **Criar**.  
  
## <a name="general-options"></a>Opções gerais  
 **Nome do InfoCube**  
 Digite um nome para o novo InfoCube.  
  
 **Descrição longa**  
 Digite uma descrição para o novo InfoCube.  
  
 **Salvar e ativar**  
 Salvar e ativar o novo InfoCube.  
  
## <a name="infocube-transfer-structure-options"></a>Opções da estrutura de transferência do InfoCube  
 A seção da estrutura de transferência do InfoCube permite associar colunas de fluxo de dados a InfoObjects.  
  
 **PipelineElement**  
 Exibe a coluna na saída do fluxo de dados que está conectado ao destino SAP BW.  
  
 **PipelineDataType**  
 Exibe o tipo de dados da coluna de fluxo de dados.  
  
 **InfoObject**  
 Exibe o nome do InfoObject associado à coluna de fluxo de dados.  
  
 **Tipo**  
 Exibe o tipo do InfoObject associado à coluna de fluxo de dados. A tabela a seguir lista os valores possíveis do tipo.  
  
|Valor|Description|  
|-----------|-----------------|  
|CHA|Características|  
|UNI|Unidades|  
|KYF|Valores-chave|  
|TIM|Características de hora|  
  
 **Iobject - Pesquisa**  
 Associar um InfoObject existente à coluna de fluxo de dados para a linha atual. Para fazer essa associação, clique em **Pesquisar**e use a caixa de diálogo **Pesquisar InfoObject** para selecionar o InfoObject existente. Para obter mais informações sobre essa caixa de diálogo, consulte [Look Up InfoObject](look-up-infoobject.md).  
  
 Depois de selecionar um InfoObject existente, o componente preenche as colunas **InfoObject** e **Tipo** com os valores selecionados.  
  
 **Iobject - Novo**  
 Crie um novo InfoObject e associe esse novo InfoObject à coluna de fluxo de dados na linha atual. Para criar o novo InfoObject, clique em **Novo**e use a caixa de diálogo **Criar Novo InfoObject** para criar o InfoObject. Para obter mais informações sobre essa caixa de diálogo, consulte [Create New InfoObject](create-new-infoobject.md).  
  
 Depois de criar um novo InfoObject, o componente preenche as colunas **InfoObject** e **Tipo** com os novos valores.  
  
 **Iobject - Remover**  
 Remover a associação entre o InfoObject e a coluna de fluxo de dados para a linha atual. Para remover essa associação, clique em **Remover**.  
  
## <a name="see-also"></a>Consulte também  
 [Ajuda F1 do Microsoft Connector 1.1 para SAP BW](../microsoft-connector-for-sap-bw-f1-help.md)  
  
  