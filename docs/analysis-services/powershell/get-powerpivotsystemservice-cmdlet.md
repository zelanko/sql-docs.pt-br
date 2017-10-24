---
title: Cmdlet Get-PowerPivotSystemService | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: 33231250-3880-4d75-936b-d70662a01855
caps.latest.revision: 9
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 1b1878ab48daa6c13e633daa62deada76512d3bd
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="get-powerpivotsystemservice-cmdlet"></a>Cmdlet Get-PowerPivotSystemService

[!INCLUDE[ssas-appliesto-sqlas-all](../../includes/ssas-appliesto-sqlas-all.md)]

  Retorna as propriedades globais do objeto do Serviço de Sistema [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] em um farm. 

>[!NOTE] 
>Este artigo pode conter informações desatualizadas e exemplos. Use o cmdlet Get-Help para a versão mais recente.
  
 **Aplica-se a:** SharePoint 2010 e SharePoint 2013.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
Get-PowerPivotSystemService [-Identity <PowerPivotMidTierServicePipeBind>] [<CommonParameters>]  
```  
  
## <a name="description"></a>Description  
 O cmdlet Get-PowerPivotSystemService retorna as propriedades globais do objeto do Serviço de Sistema [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Há um objeto pai por farm, mas cada farm pode ter várias instâncias do Serviço de Sistema [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] executadas em servidores de aplicativo individuais no farm. O objeto pai mostra configurações no nível do servidor que não variam por instância. Se o farm incluir várias instalações do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint, uma lista delimitada por vírgulas das instâncias indicará quantas instâncias do Serviço de Sistema [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] estão no farm.  
  
## <a name="parameters"></a>Parâmetros  
  
### <a name="-identity-powerpivotmidtierservicepipebind"></a>-Identity \<PowerPivotMidTierServicePipeBind >  
 Especifica o objeto pai a ser obtido. O valor deve ser um GUID válido que identifica exclusivamente o objeto no farm.  
  
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
|Entradas|Nenhum.|  
|Saídas|Nenhum.|  
  
## <a name="example-1"></a>Exemplo 1  
  
```  
C:\PS>Get-PowerPivotSystemService  
```  
  
 Este exemplo retorna as propriedades globais do objeto pai, mostrando as propriedades que são compartilhadas por todas as instâncias do Serviço de Sistema [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] no farm.  
  
  

