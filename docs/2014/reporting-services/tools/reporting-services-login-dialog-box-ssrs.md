---
title: Caixa de diálogo Logon do Reporting Services (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.rtp.rptdesigner.reportservicelogin.f1
ms.assetid: 2037d797-0b61-44c7-931f-6c689c3fc733
caps.latest.revision: 29
author: markingmyname
ms.author: maghan
manager: mblythe
ms.openlocfilehash: e4a3feeca737e1d4db6627af5ece9fa9d36c6b7b
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36115638"
---
# <a name="reporting-services-login-dialog-box-ssrs"></a>Caixa de diálogo Logon do Reporting Services (SSRS)
  Use a caixa de diálogo **Logon do Reporting Services** para fornecer credenciais para publicar relatórios no servidor de relatório.  
  
-   **Observação** Se esta for a primeira vez que você publica um relatório no servidor de relatório desde que você definiu a propriedade de implantação **TargetServerURL** para um projeto, verifique se o nome do servidor especificado é semelhante a `http://localhost/reportserver`e não a `http://localhost/reports`. Especificar o diretório `reports` no servidor local em vez do diretório `reportserver` indiretamente faz com que essa caixa de diálogo seja aberta. Para obter mais informações sobre como configurar **TargetServerURL**, consulte [Definir as propriedades da implantação &#40;Reporting Services&#41;](set-deployment-properties-reporting-services.md).  
  
## <a name="options"></a>Opções  
 **Server**  
 Exibe o nome do servidor de relatório. Por exemplo, `http://localhost/reportserver`. Para servidores de relatório que usam uma porta diferente da porta 80 padrão, inclua o número da porta. Por exemplo, `http://localhost:81/reportserver`.  
  
 **Nome de usuário**  
 Digite o nome de usuário para fazer logon no serviço Web.  
  
 **Senha**  
 Digite a senha para fazer logon no serviço Web.  
  
## <a name="see-also"></a>Consulte também  
 [Conexões de dados, fontes de dados e cadeias de caracteres de Conexão no Reporting Services](../data-connections-data-sources-and-connection-strings-in-reporting-services.md)   
 [Especificar informações de Conexão para fontes de dados de relatório e credenciais](../report-data/specify-credential-and-connection-information-for-report-data-sources.md) [Ajuda F1 do Designer de relatórios](report-designer-f1-help.md)  
  
  