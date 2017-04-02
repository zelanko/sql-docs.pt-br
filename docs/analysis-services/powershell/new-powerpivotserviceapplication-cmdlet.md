---
title: "Cmdlet New-PowerPivotServiceApplication | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "reference"
ms.assetid: 7bb2a2d2-04c8-43d4-a0fc-e8339ea22138
caps.latest.revision: 10
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 10
---
# Cmdlet New-PowerPivotServiceApplication
  Cria um novo aplicativo de serviço do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .  
  
 **Aplica-se a:** SharePoint 2010 e SharePoint 2013.  
  
## Sintaxe  
  
```  
New-PowerPivotServiceApplication [-ServiceApplicationName] <string> [-DatabaseServerName] <string> [-DatabaseName] <string> [-AddToDefaultProxyGroup <switch>] [<CommonParameters>]  
```  
  
## Description  
 O cmdlet New-PowerPivotServiceApplication cria um novo aplicativo de serviço do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] no farm. Você precisa definir pelo menos um aplicativo de serviço, e ele deve ser membro do grupo de serviço de proxy padrão. Opcionalmente, você poderá criar aplicativos de serviço adicionais se precisar variar propriedades ou parâmetros de configuração. É necessário atribuir associação a aplicativos de serviço adicionais para personalizar grupos de conexões de serviço. Apenas um aplicativo de serviço do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] pode ser membro do grupo proxy padrão.  
  
 Um novo aplicativo de serviço é criado usando uma configuração padrão. Para personalizar as propriedades de configuração, use o cmdlet Set-PowerPivotServiceApplication.  
  
## Parâmetros  
  
### -ServiceApplicationName \<string>  
 Define o nome para exibição do aplicativo de serviço.  
  
|||  
|-|-|  
|Obrigatório?|true|  
|Posição?|0|  
|Valor padrão||  
|Aceitar entrada de pipeline?|false|  
|Aceitar caracteres curinga?|false|  
  
### -DatabaseServerName \<string>  
 Especifica uma instância de mecanismo de banco de dados relacional do SQL Server que hospeda o banco de dados de aplicativo. Por padrão, você pode usar o servidor de banco de dados do farm ou pode escolher outro servidor de banco de dados no qual tenha direitos de criação de banco de dados.  
  
|||  
|-|-|  
|Obrigatório?|true|  
|Posição?|1|  
|Valor padrão||  
|Aceitar entrada de pipeline?|false|  
|Aceitar caracteres curinga?|false|  
  
### -DatabaseName \<string>  
 Especifica o nome de um banco de dados relacional do SQL Server que armazena dados de aplicativo. Não se esqueça de especificar um nome que corresponda ao aplicativo para que você possa identificar sua finalidade mais facilmente. Você pode criar um novo banco de dados ou especificar um banco de dados de aplicativo de serviço do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] existente para o novo aplicativo que está criando.  
  
|||  
|-|-|  
|Obrigatório?|true|  
|Posição?|2|  
|Valor padrão||  
|Aceitar entrada de pipeline?|false|  
|Aceitar caracteres curinga?|false|  
  
### -AddToDefaultProxyGroup \<switch>  
 Cria uma conexão de serviço do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] no grupo de conexões de serviço padrão. Associações entre aplicativos Web e aplicativos de serviço são determinadas pela associação nesse grupo. Todos os aplicativos Web que assinam o grupo de conexões de serviço padrão podem usar o aplicativo de serviço do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] que você adiciona ao grupo. Embora você possa ter vários aplicativos de serviço do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] em um farm, somente um aplicativo de serviço pode ser membro do grupo de conexões do serviço padrão.  
  
 Se você já tiver um aplicativo de serviço do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] que seja membro do grupo proxy padrão, deverá definir AddToDefautlProxyGroup:$false para o novo aplicativo que está criando. Você precisará adicionar o novo aplicativo de serviço a um grupo de conexões de serviço personalizado.  Você pode usar cmdlets internos do SharePoint internos para esse propósito.  Get-SPServiceApplicationProxyGroup retorna a lista de grupos de conexões de serviço definidos no farm.  
  
|||  
|-|-|  
|Obrigatório?|false|  
|Posição?|nomeado|  
|Valor padrão||  
|Aceitar entrada de pipeline?|false|  
|Aceitar caracteres curinga?|false|  
  
### \<CommonParameters>  
 Este cmdlet oferece suporte aos parâmetros comuns: Verbose, Debug, ErrorAction, ErrorVariable, WarningAction, WarningVariable, OutBuffer e OutVariable. Para obter mais informações, consulte [About_CommonParameters](http://go.microsoft.com/fwlink/?linkID=227825).  
  
## Entradas e saídas  
 O tipo de entrada é o tipo dos objetos que você pode transportar para o cmdlet. O tipo de retorno é o tipo dos objetos que o cmdlet retorna.  
  
|||  
|-|-|  
|Entradas|Nenhum.|  
|Saídas|Nenhum.|  
  
## Exemplo 1  
  
```  
C:\PS>New-PowerPivotServiceApplication -ServiceApplicationName "PowerPivot Service Application" -DatabaseServerName "AdvWorks-SRV01\PowerPivot" -DatabaseName "PowerPivotServiceApp1" -AddtoDefaultProxyGroup:$true  
```  
  
 Este exemplo cria um novo aplicativo de serviço. O banco de dados do aplicativo de serviço é criado em um servidor de banco de dados denominado AdvWorks-SRV01 que foi instalado como uma instância nomeada do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)], uma configuração comum para várias instalações do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint. Você deve ter permissões de dbcreator na instância do SQL Server para criar o banco de dados. Você deve ser o db_owner no banco de dados de configuração do SharePoint. Como esse é o primeiro aplicativo de serviço do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] no farm, ele deve ser membro do grupo proxy padrão.  
  
  