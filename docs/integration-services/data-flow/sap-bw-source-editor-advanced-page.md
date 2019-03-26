---
title: Editor de Origem SAP BW (página Avançado) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.sapbwsource.advanced.f1
ms.assetid: 44f3c991-9e8f-4126-a9a2-2d9da779fb11
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 0df8d32e6d2af0ab67f1637b060d17421355499e
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/20/2019
ms.locfileid: "58280240"
---
# <a name="sap-bw-source-editor-advanced-page"></a>Editor de Origem de SAP BW (página Avançado)
  Use a página **Avançado** do **Editor de Fonte SAP BW** para especificar a regra de conversão de cadeia de caracteres e o período de tempo limite, e também para redefinir o status de uma ID de Solicitação específica.  
  
 Para saber mais sobre o componente de origem do SAP BW do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 para SAP BW, consulte [Origem SAP BW](../../integration-services/data-flow/sap-bw-source.md).  
  
> [!IMPORTANT]  
>  A documentação do Microsoft Connector 1.1 for SAP BW supõe familiaridade com o ambiente do SAP Netweaver BW. Para obter mais informações sobre o SAP Netweaver BW ou para obter informações sobre como configurar objetos e processos do SAP Netweaver BW, consulte sua documentação do SAP.  
  
> [!IMPORTANT]  
>  A extração de dados do SAP Netweaver BW exige licenciamento SAP adicional. Verifique esses requisitos com a SAP.  
  
 **Para abrir a página Gerenciador de Conexões**  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra o pacote [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que contém a origem SAP BW.  
  
2.  Na guia **Fluxo de Dados** , clique duas vezes na fonte SAP BW.  
  
3.  No **Editor de Origem SAP BW**, clique em **Avançado** para abrir a página **Avançada** do editor.  
  
## <a name="options"></a>Opções  
  
> [!NOTE]  
>  Se você não souber todos os valores necessários para configurar a origem, talvez precise perguntar ao administrador do SAP.  
  
 **Conversão da cadeia de caracteres**  
 Especifique a regra para aplicar à conversão de cadeia de caracteres.  
  
|Opção|Descrição|  
|------------|-----------------|  
|**Conversão automática de cadeia de caracteres**|Converta todas as cadeias de caracteres para **nvarchar** quando o sistema SAP Netweaver BW for um sistema Unicode. Caso contrário, converta todas as cadeias de caracteres para **varchar**.|  
|**Converter cadeias de caracteres em varchar**|Converta todas as cadeias de caracteres para **varchar**.|  
|**Converter cadeias de caracteres em nvarchar**|Converta todas as cadeias de caracteres para **nvarchar**.|  
  
 **Tempo Limite (segundos)**  
 Especifique o número máximo de segundos que a origem deve esperar.  
  
> [!NOTE]  
>  Esta opção só será válida se você tiver selecionado **A – Aguardar Notificação** como o valor de **Modo de Execução** na página do **Gerenciador de Conexões** do editor. Para obter mais informações, consulte [Editor de Origem SAP BW &#40;Página Gerenciador de Conexões&#41;](../../integration-services/data-flow/sap-bw-source-editor-connection-manager-page.md).  
  
 **Request ID**  
 Especifique a ID da Solicitação cujo status você quer redefinir para “V – Verde” quando clicar em **Redefinir**.  
  
 **Redefinir**  
 Permite redefinir o status da ID da solicitação para “V - Verde”, depois de ter solicitado a sua confirmação. Isso pode ser útil quando um problema tiver ocorrido e o sistema SAP Netweaver BW tiver marcado a solicitação com um status amarelo ou vermelho.  
  
## <a name="see-also"></a>Consulte Também  
 [Editor de Origem SAP BW &#40;Página Gerenciador de Conexões&#41;](../../integration-services/data-flow/sap-bw-source-editor-connection-manager-page.md)   
 [Editor de Origem SAP BW &#40;Página Colunas&#41;](../../integration-services/data-flow/sap-bw-source-editor-columns-page.md)   
 [Editor de Origem SAP BW &#40;Página Saída de Erro&#41;](../../integration-services/data-flow/sap-bw-source-editor-error-output-page.md)   
 [Ajuda F1 do Microsoft Connector para SAP BW](../../integration-services/microsoft-connector-for-sap-bw-f1-help.md)  
  
  
