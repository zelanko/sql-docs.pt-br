---
title: Criar InfoSource | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: e7db233b-5464-43de-9d26-6dd24c7ac1b7
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 7a81bf2cef2329853df05eda97e2ce53501369c8
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86923534"
---
# <a name="create-infosource"></a>Criar InfoSource

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  Use a caixa de diálogo **Criar InfoSource** para criar um novo InfoSource. Para criar o novo InfoSource, use a caixa de diálogo **Criar InfoSource para os Dados da Transação** ou **Criar InfoSource para Dados Mestres** .  
  
 Você pode abrir a caixa de diálogo **Criar InfoSource** da página **Gerenciador de Conexões** do **Editor de Destino SAP BW**. Para obter mais informações sobre o destino SAP BW, consulte [SAP BW Destination](../../integration-services/data-flow/sap-bw-destination.md).  
  
> [!IMPORTANT]  
>  A documentação do Microsoft Connector 1.1 for SAP BW supõe familiaridade com o ambiente do SAP Netweaver BW. Para obter mais informações sobre o SAP Netweaver BW ou para obter informações sobre como configurar objetos e processos do SAP Netweaver BW, consulte sua documentação do SAP.  
  
 **Para abrir a caixa de diálogo Criar InfoSource**  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra o pacote [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que contém o destino SAP BW.  
  
2.  Na guia **Fluxo de Dados** , clique duas vezes no destino SAP BW.  
  
3.  No **Editor de Destino SAP BW**, clique em **Gerenciador de Conexões** para abrir a página **Gerenciador de Conexões** do editor.  
  
4.  Na página **Gerenciador de Conexões** , na caixa de grupo **Criar Objetos SAP BW** , selecione **InfoSource**e clique em **Criar**.  
  
## <a name="options"></a>Opções  
 **Dados da transação**  
 Crie um novo InfoSource para os dados da transação.  
  
 Se você selecionar essa opção, a caixa de diálogo **Criar InfoSource para os Dados da Transação** será aberta. Você usa a caixa de diálogo **Criar InfoSource para os Dados da Transação** para criar o novo InfoSource. Para obter mais informações sobre essa caixa de diálogo, consulte [Criar InfoSource para os dados da transação](../../integration-services/data-flow/create-infosource-for-transaction-data.md).  
  
 **Dados mestres**  
 Crie um novo InfoSource para os dados mestres.  
  
 Se você selecionar essa opção, a caixa de diálogo **Criar InfoSource para os Dados Mestres** será aberta. Você usa a caixa de diálogo **Criar InfoSource para os Dados Mestres** para criar o novo InfoSource. Para obter mais informações sobre essa caixa de diálogo, consulte [Criar InfoSource para os dados mestres](../../integration-services/data-flow/create-infosource-for-master-data.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Ajuda F1 do Microsoft Connector para SAP BW](../../integration-services/microsoft-connector-for-sap-bw-f1-help.md)  
  
  
