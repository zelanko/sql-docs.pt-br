---
title: Adicionar MSOLAP.5 como um provedor de dados confiável nos serviços do Excel | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ppvt-sharepoint
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: d7576aadda3739709acdffcb1b2419c20d39ed4e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "68164453"
---
# <a name="add-msolap5-as-a-trusted-data-provider-in-excel-services"></a>Adicionar MSOLAP.5 como um provedor de dados confiável em Serviços do Excel
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  MSOLAP.5 se refere ao provedor OLE DB do Analysis Services para SQL Server 2012. Os Serviços do Excel devem confiar neste provedor antes de fazer a solicitação de conexão que resulta na disponibilidade de dados do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] em um servidor.  
  
 Se você configurou o [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint usando a Ferramenta de Configuração do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , o MSOLAP.5 já poderá ser um provedor confiável porque a ferramenta inclui uma ação que atende a este requisito. No entanto, se você estiver usando o PowerShell, a Administração Central ou caso tenha excluído a ação do provedor confiável na ferramenta de configuração, o provedor deverá não existir e, nesse caso, você deverá adicioná-lo agora como parte da configuração do farm para o acesso a dados do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .  
  
 somente é necessário executar essa etapa uma vez para cada aplicativo de serviço de Serviços do Excel.  
  
 Cada servidor físico que manipula uma solicitação de dados do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , como um [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para o servidor SharePoint ou um servidor de Serviços do Excel, deve ter o provedor OLE DB instalado no computador. Uma instalação do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint sempre inclui o provedor OLE DB, mas se os Serviços do Excel estiverem sendo executados em um computador que não tenha o [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint, você deverá instalar o provedor manualmente. Para obter mais informações, consulte [Instalar o Provedor OLE DB do Analysis Services nos Servidores SharePoint](http://msdn.microsoft.com/2c62daf9-1f2d-4508-a497-af62360ee859).  
  
## <a name="add-a-trusted-provider-to-excel-services"></a>Adicionar um provedor confiável aos Serviços do Excel  
  
1.  Na Administração Central, clique em **Gerenciar aplicativos de serviço**e clique no aplicativo de serviço de Serviços do Excel.  
  
2.  Clique em **Provedores de Dados Confiáveis**.  
  
3.  Verifique se MSOLAP.5 aparece na lista. Dependendo do modo como você configurou o [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint, o MSOLAP.5 talvez já seja confiável.  
  
4.  Se esse item não estiver na lista, clique em **Adicionar Provedor de Dados Confiável**.  
  
5.  Na ID do Provedor, digite **MSOLAP.5**.  
  
6.  Em Tipo de Provedor, verifique se a opção OLE DB está selecionada.  
  
7.  Na Descrição do Provedor, digite **Microsoft OLE DB Provider for OLAP Services 11.0**.  
  
  
