---
title: 'Erro ao tentar estabelecer uma conexão com a fonte de dados externa. As seguintes conexões não foram atualizadas: dados PowerPivot | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 1b951da1-f62d-43d2-b40b-270a4a9ab92c
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c09c8984e964b4bdfa93b0fcebae2e613d484892
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66071949"
---
# <a name="an-error-occurred-during-an-attempt-to-establish-a-connection-to-the-external-data-source-the-following-connections-failed-to-refresh-powerpivot-data"></a>Erro ao tentar estabelecer uma conexão com a fonte de dados externa. As conexões a seguir não foram atualizadas: Dados PowerPivot
  Esse erro ocorrerá se você consultar dados PowerPivot em um servidor que não tenha o PowerPivot para SharePoint instalado. Isso também ocorrerá se o serviço do SQL Server Analysis Services (PowerPivot) for parado, ou se você estiver tentando exibir dados PowerPivot de uma versão anterior.  
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Aplica-se a|PowerPivot para SharePoint|  
|Versão do produto|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|  
|Causa|Falha na conexão de dados.|  
|Texto da mensagem|Erro ao tentar estabelecer uma conexão com a fonte de dados externa. As conexões a seguir não foram atualizadas: Dados PowerPivot|  
  
## <a name="explanation"></a>Explicação  
 Os Serviços do Excel retornam esse erro quando você consulta dados PowerPivot em uma pasta de trabalho do Excel que é publicada no SharePoint, e o ambiente do SharePoint não tem um servidor PowerPivot para SharePoint, ou se o serviço do SQL Server Analysis Services (PowerPivot) é interrompido.  
  
 O erro ocorre quando você segmenta ou filtra dados PowerPivot quando o mecanismo de consulta não está disponível.  
  
## <a name="user-action"></a>Ação do usuário  
 Instale o PowerPivot para SharePoint ou mova a pasta de trabalho PowerPivot para um ambiente do SharePoint que tenha o PowerPivot para SharePoint instalado. Para obter mais informações, consulte [PowerPivot for SharePoint 2010 Installation](../../sql-server/install/powerpivot-for-sharepoint-2010-installation.md).  
  
 Se o software estiver instalado, verifique se a instância do SQL Server Analysis Services (PowerPivot) está em execução. Selecione **Gerenciar serviços no servidor** na Administração Central. Além disso, verifique o aplicativo de console Serviços em Ferramentas Administrativas.  
  
 Para pastas de trabalho PowerPivot que foram criadas em uma versão do SQL Server 2008 R2 do PowerPivot para Excel, você deve instalar a versão do SQL Server 2008 R2 do provedor OLE DB do Analysis Services. Esse erro ocorrerá se você instalar o provedor, mas não registrar o arquivo Microsoft.AnalysisServices.ChannelTransport.dll. Para saber mais, veja [Instalar o provedor OLE DB do Analysis Services nos servidores do SharePoint](../../sql-server/install/install-the-analysis-services-ole-db-provider-on-sharepoint-servers.md).  
  
## <a name="see-also"></a>Consulte Também  
 [A conexão de dados usa a autenticação do Windows e as credenciais do usuário não puderam ser delegadas. Falha ao atualizar as seguintes conexões: dados PowerPivot](the-data-connection-user-could-not-be-delegated.md)  
  
  
