---
title: Criar InfoSource para dados mestre | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: b52a9a89-8380-4a02-8a83-dcfb46ae860e
caps.latest.revision: 9
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: d3eaf1b67e763b48067cbca3314788ac216ab0ab
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36130808"
---
# <a name="create-infosource-for-master-data"></a>Criar InfoSource para Dados Mestres
  Use a caixa de diálogo **Criar InfoSource para os Dados Mestres** para criar um novo InfoSource para dados mestres no sistema SAP Netweaver BW.  
  
 Você pode abrir a caixa de diálogo **Criar InfoSource para os Dados Mestres** da página **Gerenciador de Conexões** do **Editor de Destino SAP BW**. Para obter mais informações sobre o destino SAP BW, consulte [SAP BW Destination](sap-bw-destination.md).  
  
> [!IMPORTANT]  
>  A documentação do Microsoft Connector 1.1 for SAP BW supõe familiaridade com o ambiente do SAP Netweaver BW. Para obter mais informações sobre o SAP Netweaver BW ou para obter informações sobre como configurar objetos e processos do SAP Netweaver BW, consulte sua documentação do SAP.  
  
 **Para abrir a caixa de diálogo Criar InfoSource para os Dados Mestres**  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra o pacote [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que contém o destino SAP BW.  
  
2.  Na guia **Fluxo de Dados** , clique duas vezes no destino SAP BW.  
  
3.  No **Editor de Destino SAP BW**, clique em **Gerenciador de Conexões** para abrir a página **Gerenciador de Conexões** do editor.  
  
4.  Na página **Gerenciador de Conexões** , na caixa de grupo **Criar Objetos SAP BW** , selecione **InfoSource**e clique em **Criar**.  
  
5.  Na caixa de diálogo **Criar InfoSource** , selecione **Dados Mestres**e clique em **OK**.  
  
## <a name="options"></a>Opções  
 **Nome do InfoObject**  
 Digite o nome do InfoObject no qual o novo InfoSource deve ser baseado.  
  
 **Pesquisar**  
 Pesquisar InfoObject. Essa opção abre a caixa de diálogo **Pesquisar InfoObject** na qual é possível selecionar o InfoObject. Para obter mais informações sobre essa caixa de diálogo, consulte [Look Up InfoObject](look-up-infoobject.md).  
  
 Depois de selecionar um InfoObject, o componente preenche a caixa de texto **Nome do InfoObject** com o nome do InfoObject selecionado.  
  
 **Nova**  
 Criar um novo InfoObject. Essa opção abre a caixa de diálogo **Criar Novo InfoObject** na qual é possível criar o novo InfoObject. Para obter mais informações sobre essa caixa de diálogo, consulte [Create New InfoObject](create-new-infoobject.md).  
  
 Depois de criar um InfoObject, o componente preenche a caixa de texto **Nome do InfoObject** com o nome do novo InfoObject.  
  
 **Descrição breve**  
 Insira uma descrição curta para o novo InfoSource.  
  
 **Descrição longa**  
 Insira uma descrição longa para o novo InfoSource.  
  
 **Sistema de origem**  
 Selecione o sistema de origem a ser associado ao novo InfoSource.  
  
 **Aplicativo**  
 Insira o nome do aplicativo cliente a ser associado ao novo InfoSource.  
  
 **Atributos**  
 Indica que os dados mestres consistem em atributos.  
  
 **Textos**  
 Indica que os dados mestres consistem em atributos.  
  
 **Salvar e Ativar**  
 Salvar e ativar o novo InfoSource.  
  
## <a name="see-also"></a>Consulte também  
 [Criar InfoSource](create-infosource.md)   
 [Ajuda F1 do Microsoft Connector 1.1 para SAP BW](../microsoft-connector-for-sap-bw-f1-help.md)  
  
  