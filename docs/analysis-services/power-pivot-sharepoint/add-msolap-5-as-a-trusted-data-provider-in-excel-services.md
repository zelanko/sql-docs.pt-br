---
title: "Adicionar MSOLAP. 5 como um provedor de dados confiável em serviços do Excel | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: c1f40fa4-de6d-41ee-8124-14b4d65988f5
caps.latest.revision: 6
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 9c1d5366817d19dea649b24ba17ea776a10fc7c5
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="add-msolap5-as-a-trusted-data-provider-in-excel-services"></a>Adicionar MSOLAP.5 como um provedor de dados confiável em Serviços do Excel
  MSOLAP.5 se refere ao provedor OLE DB do Analysis Services para SQL Server 2012. Os Serviços do Excel devem confiar neste provedor antes de fazer a solicitação de conexão que resulta na disponibilidade de dados do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] em um servidor.  
  
 Se você configurou o [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint usando a Ferramenta de Configuração do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , o MSOLAP.5 já poderá ser um provedor confiável porque a ferramenta inclui uma ação que atende a este requisito. No entanto, se você estiver usando o PowerShell, a Administração Central ou caso tenha excluído a ação do provedor confiável na ferramenta de configuração, o provedor deverá não existir e, nesse caso, você deverá adicioná-lo agora como parte da configuração do farm para o acesso a dados do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .  
  
 somente é necessário executar essa etapa uma vez para cada aplicativo de serviço de Serviços do Excel.  
  
 Cada servidor físico que manipula uma solicitação de dados do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , como um [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para o servidor SharePoint ou um servidor de Serviços do Excel, deve ter o provedor OLE DB instalado no computador. Uma instalação do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint sempre inclui o provedor OLE DB, mas se os Serviços do Excel estiverem sendo executados em um computador que não tenha o [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint, você deverá instalar o provedor manualmente. Para obter mais informações, consulte [Instalar o Provedor OLE DB do Analysis Services nos Servidores SharePoint](http://msdn.microsoft.com/en-us/2c62daf9-1f2d-4508-a497-af62360ee859).  
  
## <a name="add-a-trusted-provider-to-excel-services"></a>Adicionar um provedor confiável aos Serviços do Excel  
  
1.  Na Administração Central, clique em **Gerenciar aplicativos de serviço**e clique no aplicativo de serviço de Serviços do Excel.  
  
2.  Clique em **Provedores de Dados Confiáveis**.  
  
3.  Verifique se MSOLAP.5 aparece na lista. Dependendo do modo como você configurou o [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint, o MSOLAP.5 talvez já seja confiável.  
  
4.  Se esse item não estiver na lista, clique em **Adicionar Provedor de Dados Confiável**.  
  
5.  Na ID do Provedor, digite **MSOLAP.5**.  
  
6.  Em Tipo de Provedor, verifique se a opção OLE DB está selecionada.  
  
7.  Na Descrição do Provedor, digite **Microsoft OLE DB Provider for OLAP Services 11.0**.  
  
  

