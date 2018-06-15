---
title: Caixa de diálogo Logon do Reporting Services (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.component: tools
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
f1_keywords:
- sql13.rtp.rptdesigner.reportservicelogin.f1
ms.assetid: 2037d797-0b61-44c7-931f-6c689c3fc733
caps.latest.revision: 31
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 8c8d8896b90ef86e34e83e9348bfbb4b9946dd26
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33030253"
---
# <a name="reporting-services-login-dialog-box-ssrs"></a>Caixa de diálogo Logon do Reporting Services (SSRS)
  Use a caixa de diálogo **Logon do Reporting Services** para fornecer credenciais para publicar relatórios no servidor de relatório.  
  
-   **Observação** Se esta for a primeira vez que você publica um relatório no servidor de relatório desde que você definiu a propriedade de implantação **TargetServerURL** para um projeto, verifique se o nome do servidor especificado é semelhante a **server** e não a **reports**. Por exemplo, `http://localhost/reportserver`e não a `http://localhost/reports`. Especificar o diretório `reports` no servidor local em vez do diretório `reportserver` indiretamente faz com que essa caixa de diálogo seja aberta. Para obter mais informações sobre como configurar **TargetServerURL**, consulte [Definir as propriedades da implantação &#40;Reporting Services&#41;](../../reporting-services/tools/set-deployment-properties-reporting-services.md).  
  
## <a name="options"></a>Opções  
 **Server**  
 Exibe o nome do servidor de relatório. Por exemplo, `http://localhost/reportserver`. Para servidores de relatório que usam uma porta diferente da porta 80 padrão, inclua o número da porta. Por exemplo, `http://localhost:81/reportserver`.  
  
 **User name**  
 Digite o nome de usuário para fazer logon no serviço Web.  
  
 **Senha**  
 Digite a senha para fazer logon no serviço Web.  
  
## <a name="see-also"></a>Consulte Também  
 [Conexões de dados, fontes de dados e cadeias de conexão &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)   
 [Especificar informações de credenciais e de conexão para fontes de dados de relatório](../../reporting-services/report-data/specify-credential-and-connection-information-for-report-data-sources.md)   
 [Ajuda F1 do Designer de Relatórios](../../reporting-services/tools/report-designer-f1-help.md)  
  
  
