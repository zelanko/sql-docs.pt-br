---
title: Caixa de diálogo Logon do Reporting Services (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.rtp.rptdesigner.reportservicelogin.f1
ms.assetid: 2037d797-0b61-44c7-931f-6c689c3fc733
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 232ee51614a668b07263c3e3a4182f23652135bf
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66099865"
---
# <a name="reporting-services-login-dialog-box-ssrs"></a>Caixa de diálogo Logon do Reporting Services (SSRS)
  Use a caixa de diálogo **Logon do Reporting Services** para fornecer credenciais para publicar relatórios no servidor de relatório.  
  
-   **Observação** Se esta for a primeira vez que você publicou um relatório em um servidor de relatório desde que definiu a propriedade de implantação **TargetServerURL** para um projeto, verifique se o nome do servidor especificado é `http://localhost/reportserver`semelhante a, `http://localhost/reports`e não. Especificar o diretório `reports` no servidor local em vez do diretório `reportserver` indiretamente faz com que essa caixa de diálogo seja aberta. Para obter mais informações sobre como configurar **TargetServerURL**, consulte [Definir as propriedades da implantação &#40;Reporting Services&#41;](set-deployment-properties-reporting-services.md).  
  
## <a name="options"></a>Opções  
 **Servidor**  
 Exibe o nome do servidor de relatório. Por exemplo, `http://localhost/reportserver`. Para servidores de relatório que usam uma porta diferente da porta 80 padrão, inclua o número da porta. Por exemplo, `http://localhost:81/reportserver`.  
  
 **Nome de usuário**  
 Digite o nome de usuário para fazer logon no serviço Web.  
  
 **Senha**  
 Digite a senha para fazer logon no serviço Web.  
  
## <a name="see-also"></a>Consulte Também  
 [Conexões de dados, fontes de dados e cadeias de conexão no Reporting Services](../data-connections-data-sources-and-connection-strings-in-reporting-services.md)   
 [Especificar informações de credenciais e de conexão para fontes de dados de relatório](../report-data/specify-credential-and-connection-information-for-report-data-sources.md) [Report Designer ajuda F1](report-designer-f1-help.md)  
  
  
