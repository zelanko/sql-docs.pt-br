---
description: Criar InfoPackage
title: Criar InfoPackage | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 9cd4a848-409f-4681-a390-1c49a2aadbd7
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 38c7183853dcac7043672d5e4a622362af08c10b
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96127279"
---
# <a name="create-infopackage"></a>Criar InfoPackage

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  Use a caixa de diálogo **Criar Novo InfoPackage** para criar um novo InfoPackage no sistema SAP Netweaver BW.  
  
 Você pode abrir a caixa de diálogo **Criar InfoPackage** da página **Gerenciador de Conexões** do **Editor de Destino SAP BW**. Para obter mais informações sobre o destino SAP BW, consulte [SAP BW Destination](../../integration-services/data-flow/sap-bw-destination.md).  
  
> [!IMPORTANT]  
>  A documentação do Microsoft Connector 1.1 for SAP BW supõe familiaridade com o ambiente do SAP Netweaver BW. Para obter mais informações sobre o SAP Netweaver BW ou para obter informações sobre como configurar objetos e processos do SAP Netweaver BW, consulte sua documentação do SAP.  
  
 **Para abrir a caixa de diálogo Criar InfoPackage**  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra o pacote [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que contém o destino SAP BW.  
  
2.  Na guia **Fluxo de Dados** , clique duas vezes no destino SAP BW.  
  
3.  No **Editor de Destino SAP BW**, clique em **Gerenciador de Conexões** para abrir a página **Gerenciador de Conexões** do editor.  
  
4.  Na página **Gerenciador de Conexões** , na caixa de grupo **Criar Objetos SAP BW** , selecione **InfoPackage** e clique em **Criar**.  
  
## <a name="options"></a>Opções  
 **InfoSource**  
 Digite o nome do InfoSource no qual o novo InfoPackage deve ser baseado.  
  
 **Descrição breve**  
 Digite uma descrição para o novo InfoPackage.  
  
 **Sistema de origem**  
 Selecione o sistema de dados com o qual o novo InfoPackage deve ser associado.  
  
 **Atributos**  
 Indica que o InfoPackage carregará dados de atributo.  
  
 **Textos**  
 Indica que o InfoPackage carregará dados de texto.  
  
 **Transação**  
 Indica que o InfoPackage carregará dados de transação.  
  
 **Salvar e Ativar**  
 Salvar e ativar o novo InfoPackage.  
  
## <a name="see-also"></a>Consulte Também  
 [Ajuda F1 do Microsoft Connector para SAP BW](../../integration-services/microsoft-connector-for-sap-bw-f1-help.md)  
  
  
