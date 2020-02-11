---
title: Adicionar MSOLAP. 5 como um Provedor de Dados confiável nos serviços do Excel | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: c1f40fa4-de6d-41ee-8124-14b4d65988f5
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9095c1fa767e1854c300df1ad08bf5d1900af860
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66071933"
---
# <a name="add-msolap5-as-a-trusted-data-provider-in-excel-services"></a>Adicionar MSOLAP.5 como um provedor de dados confiável em Serviços do Excel
  MSOLAP.5 se refere ao provedor OLE DB do Analysis Services para SQL Server 2012. Os Serviços do Excel devem confiar neste provedor antes de fazer a solicitação de conexão que resulta na disponibilidade de dados PowerPivot em um servidor.  
  
 Se você configurou o PowerPivot para SharePoint usando a Ferramenta de Configuração do PowerPivot, o MSOLAP.5 já poderá ser um provedor de confiança porque a ferramenta inclui uma ação que atende a este requisito. No entanto, se você estiver usando o PowerShell, a Administração Central ou caso tenha excluído a ação do provedor confiável na ferramenta de configuração, o provedor deverá estar faltando e, nesse caso, você deverá adicioná-lo agora como parte da configuração do farm para o acesso a dados PowerPivot.  
  
 somente é necessário executar essa etapa uma vez para cada aplicativo de serviço de Serviços do Excel.  
  
 Todo servidor físico que manipula uma solicitação de dados PowerPivot, como um servidor PowerPivot para SharePoint ou um servidor de Serviços do Excel, deve ter o provedor OLE DB instalado no computador. Uma instalação do PowerPivot para SharePoint sempre inclui o provedor OLE DB, mas se os Serviços do Excel estiverem sendo executados em um computador que não tenha o PowerPivot para SharePoint, deverá instalar o provedor manualmente. Para obter mais informações, consulte [Instalar o Provedor OLE DB do Analysis Services nos Servidores SharePoint](../../sql-server/install/install-the-analysis-services-ole-db-provider-on-sharepoint-servers.md).  
  
## <a name="add-a-trusted-provider-to-excel-services"></a>Adicionar um provedor confiável aos Serviços do Excel  
  
1.  Na Administração Central, clique em **Gerenciar aplicativos de serviço**e clique no aplicativo de serviço de Serviços do Excel.  
  
2.  Clique em **Provedores de Dados Confiáveis**.  
  
3.  Verifique se MSOLAP.5 aparece na lista. Dependendo do modo como você configurou o PowerPivot para SharePoint, o MSOLAP.5 talvez já seja confiável.  
  
4.  Se esse item não estiver na lista, clique em **Adicionar Provedor de Dados Confiável**.  
  
5.  Na ID do Provedor, digite `MSOLAP.5`.  
  
6.  Em Tipo de Provedor, verifique se a opção OLE DB está selecionada.  
  
7.  Na Descrição do Provedor, digite **Microsoft OLE DB Provider for OLAP Services 11.0**.  
  
  
