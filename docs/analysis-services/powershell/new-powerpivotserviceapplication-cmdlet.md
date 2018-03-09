---
title: Cmdlet New-PowerPivotServiceApplication | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: 7bb2a2d2-04c8-43d4-a0fc-e8339ea22138
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 59b91b7bfc168b0722d5b8d37f74e521557c4416
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/15/2018
---
# <a name="new-powerpivotserviceapplication-cmdlet"></a>Cmdlet New-PowerPivotServiceApplication
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
Cria um novo aplicativo de serviço do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .  

>[!NOTE] 
>Este artigo pode conter informações desatualizadas e exemplos. Use o cmdlet Get-Help para a versão mais recente.
  
 **Aplica-se a:** SharePoint 2010 e SharePoint 2013.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
New-PowerPivotServiceApplication [-ServiceApplicationName] <string> [-DatabaseServerName] <string> [-DatabaseName] <string> [-AddToDefaultProxyGroup <switch>] [<CommonParameters>]  
```  
  
## <a name="description"></a>Description  
 O cmdlet New-PowerPivotServiceApplication cria um novo aplicativo de serviço do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] no farm. Você precisa definir pelo menos um aplicativo de serviço, e ele deve ser membro do grupo de serviço de proxy padrão. Opcionalmente, você poderá criar aplicativos de serviço adicionais se precisar variar propriedades ou parâmetros de configuração. É necessário atribuir associação a aplicativos de serviço adicionais para personalizar grupos de conexões de serviço. Apenas um aplicativo de serviço do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] pode ser membro do grupo proxy padrão.  
  
 Um novo aplicativo de serviço é criado usando uma configuração padrão. Para personalizar as propriedades de configuração, use o cmdlet Set-PowerPivotServiceApplication.  
  
## <a name="parameters"></a>Parâmetros  
  
### <a name="-serviceapplicationname-string"></a>-ServiceApplicationName \<string>  
 Define o nome para exibição do aplicativo de serviço.  
  
|||  
|-|-|  
|Obrigatório?|true|  
|Posição?|0|  
|Valor padrão||  
|Aceitar entrada de pipeline?|false|  
|Aceitar caracteres curinga?|false|  
  
### <a name="-databaseservername-string"></a>-DatabaseServerName \<string>  
 Especifica uma instância de mecanismo de banco de dados relacional do SQL Server que hospeda o banco de dados de aplicativo. Por padrão, você pode usar o servidor de banco de dados do farm ou pode escolher outro servidor de banco de dados no qual tenha direitos de criação de banco de dados.  
  
|||  
|-|-|  
|Obrigatório?|true|  
|Posição?|1|  
|Valor padrão||  
|Aceitar entrada de pipeline?|false|  
|Aceitar caracteres curinga?|false|  
  
### <a name="-databasename-string"></a>-DatabaseName \<cadeia de caracteres >  
 Especifica o nome de um banco de dados relacional do SQL Server que armazena dados de aplicativo. Não se esqueça de especificar um nome que corresponda ao aplicativo para que você possa identificar sua finalidade mais facilmente. Você pode criar um novo banco de dados ou especificar um banco de dados de aplicativo de serviço do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] existente para o novo aplicativo que está criando.  
  
|||  
|-|-|  
|Obrigatório?|true|  
|Posição?|2|  
|Valor padrão||  
|Aceitar entrada de pipeline?|false|  
|Aceitar caracteres curinga?|false|  
  
### <a name="-addtodefaultproxygroup-switch"></a>-AddToDefaultProxyGroup \<switch>  
 Cria uma conexão de serviço do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] no grupo de conexões de serviço padrão. Associações entre aplicativos Web e aplicativos de serviço são determinadas pela associação nesse grupo. Todos os aplicativos Web que assinam o grupo de conexões de serviço padrão podem usar o aplicativo de serviço do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] que você adiciona ao grupo. Embora você possa ter vários aplicativos de serviço do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] em um farm, somente um aplicativo de serviço pode ser membro do grupo de conexões do serviço padrão.  
  
 Se você já tiver um aplicativo de serviço do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] que seja membro do grupo proxy padrão, deverá definir AddToDefautlProxyGroup:$false para o novo aplicativo que está criando. Você precisará adicionar o novo aplicativo de serviço a um grupo de conexões de serviço personalizado.  Você pode usar cmdlets internos do SharePoint internos para esse propósito.  Get-SPServiceApplicationProxyGroup retorna a lista de grupos de conexões de serviço definidos no farm.  
  
|||  
|-|-|  
|Obrigatório?|false|  
|Posição?|nomeado|  
|Valor padrão||  
|Aceitar entrada de pipeline?|false|  
|Aceitar caracteres curinga?|false|  
  
### <a name="commonparameters"></a>\<CommonParameters>  
 Este cmdlet oferece suporte aos parâmetros comuns: Verbose, Debug, ErrorAction, ErrorVariable, WarningAction, WarningVariable, OutBuffer e OutVariable. Para obter mais informações, consulte [About_CommonParameters](http://go.microsoft.com/fwlink/?linkID=227825).  
  
## <a name="inputs-and-outputs"></a>Entradas e saídas  
 O tipo de entrada é o tipo dos objetos que você pode transportar para o cmdlet. O tipo de retorno é o tipo dos objetos que o cmdlet retorna.  
  
|||  
|-|-|  
|Entradas|Nenhuma.|  
|Saídas|Nenhuma.|  
  
## <a name="example-1"></a>Exemplo 1  
  
```  
C:\PS>New-PowerPivotServiceApplication -ServiceApplicationName "PowerPivot Service Application" -DatabaseServerName "AdvWorks-SRV01\PowerPivot" -DatabaseName "PowerPivotServiceApp1" -AddtoDefaultProxyGroup:$true  
```  
  
 Este exemplo cria um novo aplicativo de serviço. O banco de dados do aplicativo de serviço é criado em um servidor de banco de dados denominado AdvWorks-SRV01 que foi instalado como uma instância nomeada do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , uma configuração comum para várias instalações do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint. Você deve ter permissões de dbcreator na instância do SQL Server para criar o banco de dados. Você deve ser o db_owner no banco de dados de configuração do SharePoint. Como esse é o primeiro aplicativo de serviço do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] no farm, ele deve ser membro do grupo proxy padrão.  
  
  
