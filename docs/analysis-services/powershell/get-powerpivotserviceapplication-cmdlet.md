---
title: Cmdlet Get-PowerPivotServiceApplication | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: powershell
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 2a5ccd05b8c5e947972218a22c0abbc358731ee5
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="get-powerpivotserviceapplication-cmdlet"></a>Cmdlet Get-PowerPivotServiceApplication
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Retorna um ou mais aplicativos de serviço [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .  

>[!NOTE] 
>Este artigo pode conter informações desatualizadas e exemplos. Use o cmdlet Get-Help para a versão mais recente.
  
 **Aplica-se a:** SharePoint 2010 e SharePoint 2013.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
Get-PowerPivotServiceApplication [[-Identity] <SPGeminiServiceApplicationPipeBind>] [<CommonParameters>]  
```  
  
## <a name="description"></a>Description  
 O cmdlet Get-PowerPivotServiceApplication retorna o aplicativo de serviço especificado pelo parâmetro Identity. Se nenhum parâmetro for especificado, o cmdlet retornará todos os aplicativos de serviço [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] no farm. Cada aplicativo é identificado por seu nome para exibição, tipo de aplicativo e GUID. Para exibir as propriedades adicionais de um aplicativo de serviço [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , adicione a opção format-list ao cmdlet.  
  
## <a name="parameters"></a>Parâmetros  
  
### <a name="-identity-spgeminiserviceapplicationpipebind"></a>-Identity \<SPGeminiServiceApplicationPipeBind >  
 Especifica o aplicativo de serviço a ser obtido. O valor deve ser um GUID válido que identifica exclusivamente o objeto no farm.  
  
|||  
|-|-|  
|Obrigatório?|false|  
|Posição?|0|  
|Valor padrão||  
|Aceitar entrada de pipeline?|true|  
|Aceitar caracteres curinga?|false|  
  
### <a name="commonparameters"></a>\<CommonParameters >  
 Este cmdlet oferece suporte aos parâmetros comuns: Verbose, Debug, ErrorAction, ErrorVariable, WarningAction, WarningVariable, OutBuffer e OutVariable. Para obter mais informações, consulte [About_CommonParameters](http://go.microsoft.com/fwlink/?linkID=227825).  
  
## <a name="inputs-and-outputs"></a>Entradas e saídas  
 O tipo de entrada é o tipo dos objetos que você pode transportar para o cmdlet. O tipo de retorno é o tipo dos objetos que o cmdlet retorna.  
  
|||  
|-|-|  
|Entradas|Nenhuma.|  
|Saídas|Nenhuma.|  
  
## <a name="example-1"></a>Exemplo 1  
  
```  
C:\PS>Get-PowerPivotServiceApplication  
```  
  
 Este exemplo retorna um ou mais aplicativos de serviço no farm.  
  
## <a name="example-2"></a>Exemplo 2  
  
```  
C:\PS>Get-PowerPivotServiceApplication | format-list  
```  
  
 Este exemplo retorna todas as propriedades de um aplicativo de serviço [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .  
  
## <a name="example-3"></a>Exemplo 3  
  
```  
C:\PS>get-PowerPivotServiceApplication -Identity 1234567-890a-bcde-fghijklm  
```  
  
 Este exemplo retorna um único aplicativo de serviço, ao mesmo tempo em que mostra o nome para exibição, o tipo de aplicativo e o GUID do aplicativo. Se o nome para exibição for longo, ele será truncado. Use a opção format-list para exibir o nome completo.  
  
  
