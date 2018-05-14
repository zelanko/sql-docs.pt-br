---
title: Cmdlet Get-PowerPivotSystemServiceInstance | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: powershell
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: cb07d3ee84f8a43e15732f3aafc1a4c7cef83fbf
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="get-powerpivotsystemserviceinstance-cmdlet"></a>Cmdlet Get-PowerPivotSystemServiceInstance
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Retorna uma ou mais instâncias do Serviço de Sistema [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] em execução em servidores de aplicativos no farm.  

>[!NOTE] 
>Este artigo pode conter informações desatualizadas e exemplos. Use o cmdlet Get-Help para a versão mais recente.
  
 **Aplica-se a:** SharePoint 2010 e SharePoint 2013.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
Get-PowerPivotSystemServiceInstance [-Identity <PowerPivotMidTierServiceInstancePipeBind>] [<CommonParameters>]  
```  
  
## <a name="description"></a>Description  
 O cmdlet Get-PowerPivotSystemServiceInstance retorna as propriedades de uma ou mais instâncias do Serviço de Sistema [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] em execução no farm. O cmdlet relata o tipo de aplicativo, o status (online ou offline) e a identidade. Para exibir propriedades adicionais de uma instância específica, adicione o parâmetro Identity e a opção format-list ao cmdlet.  
  
## <a name="parameters"></a>Parâmetros  
  
### <a name="-identity-powerpivotmidtierserviceinstancepipebind"></a>-Identity \<PowerPivotMidTierServiceInstancePipeBind>  
 Especifica a instância de serviço a ser obtida. O valor deve ser um GUID válido que identifica exclusivamente o objeto no farm.  
  
|||  
|-|-|  
|Obrigatório?|false|  
|Posição?|0|  
|Valor padrão||  
|Aceitar entrada de pipeline?|true|  
|Aceitar caracteres curinga?|false|  
  
### <a name="commonparameters"></a>\<CommonParameters >  
 Este cmdlet oferece suporte aos parâmetros comuns: Verbose, Debug, ErrorAction, ErrorVariable, WarningAction, WarningVariable, OutBuffer e OutVariable. Para obter mais informações, consulte [about_CommonParameters](http://go.microsoft.com/fwlink/?linkID=227825)  
  
## <a name="inputs-and-outputs"></a>Entradas e saídas  
 O tipo de entrada é o tipo dos objetos que você pode transportar para o cmdlet. O tipo de retorno é o tipo dos objetos que o cmdlet retorna.  
  
|||  
|-|-|  
|Entradas|Nenhuma.|  
|Saídas|Nenhuma.|  
  
## <a name="example-1"></a>Exemplo 1  
  
```  
C:\PS>Get-PowerPivotSystemServiceInstance -Identity 1234567-890a-bcde-fghijklm | format-list| format-list  
```  
  
 Este exemplo retorna propriedades adicionais da instância especificada, incluindo o nome do servidor, a versão e o status de atualização.  
  
  
