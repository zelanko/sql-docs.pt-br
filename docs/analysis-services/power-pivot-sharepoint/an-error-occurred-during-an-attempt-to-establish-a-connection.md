---
title: Ocorreu um erro durante uma tentativa de estabelecer uma conexão | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ppvt-sharepoint
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 28d5bd077da96e3dd6f8a48004c3a5df1b681f61
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/11/2018
ms.locfileid: "53215735"
---
# <a name="an-error-occurred-during-an-attempt-to-establish-a-connection"></a>Ocorreu um erro durante uma tentativa de estabelecer uma conexão
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Esse erro ocorrerá se você consultar dados do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] em um servidor que não tenha o [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint instalado. Isso também ocorre se o SQL Server Analysis Services ( [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]) serviço for interrompido, ou se você estiver tentando exibir [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] dados de uma versão anterior.  
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Aplica-se a|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint|  
|Versão do Produto|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|  
|Causa|Falha na conexão de dados.|  
|Texto da mensagem|Erro ao tentar estabelecer uma conexão com a fonte de dados externa. As conexões a seguir não foram atualizadas: [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] Dados|  
  
## <a name="explanation"></a>Explicação  
 Os serviços do Excel retornam este erro ao consultar [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] dados em uma pasta de trabalho do Excel que é publicada no SharePoint e o ambiente do SharePoint não tem um [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] do servidor SharePoint ou do SQL Server Analysis Services ( [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]) serviço está parado.  
  
 O erro ocorre quando você segmenta ou filtra dados do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] quando o mecanismo de consulta não está disponível.  
  
## <a name="user-action"></a>Ação do usuário  
 Instale o [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint ou mova a pasta de trabalho do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para um ambiente do SharePoint que tenha o [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint instalado. Para saber mais, confira [Instalação do Power Pivot para SharePoint 2010](http://msdn.microsoft.com/8d47dde7-c941-4280-a934-e2fe3f9a938f).  
  
 Se o software estiver instalado, verifique se que o SQL Server Analysis Services ( [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]) instância está em execução. Selecione **Gerenciar serviços no servidor** na Administração Central. Além disso, verifique o aplicativo de console Serviços em Ferramentas Administrativas.  
  
 Para pastas de trabalho do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] que foram criadas em uma versão do SQL Server 2008 R2 do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para Excel, você deve instalar a versão do SQL Server 2008 R2 do provedor OLE DB do Analysis Services. Esse erro ocorrerá se você instalar o provedor, mas não registrar o arquivo Microsoft.AnalysisServices.ChannelTransport.dll. Para saber mais, veja [Instalar o provedor OLE DB do Analysis Services nos servidores do SharePoint](http://msdn.microsoft.com/2c62daf9-1f2d-4508-a497-af62360ee859).  
  
## <a name="see-also"></a>Consulte também  
 [A conexão de dados usa a Autenticação do Windows e não foi possível delegar as credenciais de usuário. As conexões a seguir não foram atualizadas: Dados do Power Pivot](../../analysis-services/power-pivot-sharepoint/the-data-connection-user-could-not-be-delegated.md)  
  
  
