---
title: Cmdlet New-PowerPivotSystemServiceInstance | Microsoft Docs
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
ms.assetid: 7ea94113-c0f1-4cca-9228-f1a034fba5db
caps.latest.revision: "10"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: f2e412047e4d859de637da933d2335232961ee13
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="new-powerpivotsystemserviceinstance-cmdlet"></a>Cmdlet New-PowerPivotSystemServiceInstance
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]Adiciona uma nova instância da [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] serviço do sistema para um servidor de aplicativos.  

>[!NOTE] 
>Este artigo pode conter informações desatualizadas e exemplos. Use o cmdlet Get-Help para a versão mais recente.
  
 **Aplica-se a:** SharePoint 2010 e SharePoint 2013.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
New-PowerPivotSystemServiceInstance [[-ParentService] <PowerPivotMidTierServicePipeBind>] [-SystemServiceInstanceName <string>] [-Provision] [<CommonParameters>]  
```  
  
## <a name="description"></a>Description  
 O cmdlet New-PowerPivotSystemServiceInstance provisiona um novo objeto PowerPivotSystemService no nível do farm após o uso da Instalação do SQL Server para instalar o [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint no servidor de aplicativos local. Somente é possível provisionar uma instância de serviço em cada servidor de aplicativos.  Se o serviço já foi provisionado, você não poderá executar esse cmdlet.  
  
## <a name="parameters"></a>Parâmetros  
  
### <a name="-parentservice-powerpivotmidtierservicepipebind"></a>-ParentService \<PowerPivotMidTierServicePipeBind >  
 Especifica o GUID do objeto pai do Serviço de Sistema [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] no farm. Nesta versão, apenas um objeto pai é permitido. Você pode usar Get-PowerPivotSystemService para retornar o objeto de serviço ou seu GUID.  
  
|||  
|-|-|  
|Obrigatório?|false|  
|Posição?|0|  
|Valor padrão||  
|Aceitar entrada de pipeline?|true|  
|Aceitar caracteres curinga?|false|  
  
### <a name="-systemserviceinstancename-string"></a>-SystemServiceInstanceName \<cadeia de caracteres >  
 Especifica um nome que identifica esse objeto.  
  
|||  
|-|-|  
|Obrigatório?|false|  
|Posição?|1|  
|Valor padrão||  
|Aceitar entrada de pipeline?|false|  
|Aceitar caracteres curinga?|false|  
  
### <a name="provision-switchparameter"></a>Provisionar [\<SwitchParameter >]  
 Torna o serviço disponível no SharePoint. Os valores válidos são $true ou $false.  
  
|||  
|-|-|  
|Obrigatório?|false|  
|Posição?|nomeado|  
|Valor padrão||  
|Aceitar entrada de pipeline?|false|  
|Aceitar caracteres curinga?|false|  
  
### <a name="commonparameters"></a>\<CommonParameters >  
 Este cmdlet oferece suporte aos parâmetros comuns: Verbose, Debug, ErrorAction, ErrorVariable, WarningAction, WarningVariable, OutBuffer e OutVariable. Para obter mais informações, consulte [About_CommonParameters](http://go.microsoft.com/fwlink/?linkID=227825).  
  
## <a name="inputs-and-outputs"></a>Entradas e saídas  
 O tipo de entrada é o tipo dos objetos que você pode transportar para o cmdlet. O tipo de retorno é o tipo dos objetos que o cmdlet retorna.  
  
|||  
|-|-|  
|Entradas|Nenhum.|  
|Saídas|Nenhum.|  
  
## <a name="example-1"></a>Exemplo 1  
  
```  
C:\PS>New-PowerPivotSystemServiceInstance -Provision:$true  
```  
  
 Este exemplo mostra o formulário mais comum do cmdlet. Ele registra o Serviço de Sistema [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] no servidor de aplicativos local com o farm.  
  
## <a name="example-2"></a>Exemplo 2  
  
```  
C:\PS>New-PowerPivotSystemServiceInstance -SystemServiceInstanceName "MyPSSInstance" -provision:$false  
```  
  
 Este exemplo denomina a instância do Serviço de Sistema [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , mas sem provisioná-la. Se você não fornecer um nome, o nome padrão Instância de Serviço de Sistema do SQL Server Analysis Services será usado. A criação de um nome personalizado para o serviço é opcional. Você poderá atribuir um nome ao serviço para oferecer suporte a cenários de teste ou se tiver uma ferramenta ou um script personalizado que provisione a instância em uma etapa posterior.  
  
  
