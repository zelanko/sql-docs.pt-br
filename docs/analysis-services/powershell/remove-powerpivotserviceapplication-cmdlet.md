---
title: Cmdlet Remove-PowerPivotServiceApplication | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: powershell
ms.reviewer: 
ms.suite: sql
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: 2742b2a3-927c-4e7c-bd7d-43c072fa01ab
caps.latest.revision: "11"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 1333667175ea137687188c97e3664450586cc21e
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="remove-powerpivotserviceapplication-cmdlet"></a>Cmdlet Remove-PowerPivotServiceApplication

[!INCLUDE[ssas-appliesto-sqlas-all](../../includes/ssas-appliesto-sqlas-all.md)]

  Exclui um aplicativo de serviço [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .  

>[!NOTE] 
>Este artigo pode conter informações desatualizadas e exemplos. Use o cmdlet Get-Help para a versão mais recente.
  
 **Aplica-se a:** SharePoint 2010 e SharePoint 2013.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
Remove-PowerPivotServiceApplication [-Identity <SPGeminiServiceApplicationPipeBind>] [-DeleteAll <switch>] [-RemoveData <switch>] [-Confirm <switch>] [<CommonParameters>]  
```  
  
## <a name="description"></a>Description  
 O cmdlet Remove-PowerPivotServiceApplication exclui um aplicativo de serviço [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] do farm. Use DeleteAll para excluir todos os aplicativos de serviço de uma vez ou use o parâmetro Identity para remover uma única instância. Para obter informações de instância, execute Get-PowerPivotServiceApplication para retornar todas as instâncias no farm.  
  
 Use o parâmetro RemoveData para remover bancos de dados de aplicativo de serviço e arquivos armazenados em cache, se desejar. [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] permanecem nas bibliotecas de conteúdo, mas não estão mais funcionais após a remoção do aplicativo de serviço.  
  
## <a name="parameters"></a>Parâmetros  
  
### <a name="-identity-spgeminiserviceapplicationpipebind"></a>-Identity \<SPGeminiServiceApplicationPipeBind >  
 Especifica o GUID de um único aplicativo de serviço [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] no farm. Você deverá especificar o GUID se quiser remover apenas um aplicativo, deixando outros aplicativos de serviço inalterados.  
  
|||  
|-|-|  
|Obrigatório?|false|  
|Posição?|0|  
|Valor padrão||  
|Aceitar entrada de pipeline?|true|  
|Aceitar caracteres curinga?|false|  
  
### <a name="-confirm-switch"></a>-Confirme \<alternar >  
 Solicita sua confirmação antes de executar o comando. Este valor é habilitado por padrão. Para ignorar a resposta de confirmação em um comando, especifique Confirm:$false no comando.  
  
|||  
|-|-|  
|Obrigatório?|false|  
|Posição?|nomeado|  
|Valor padrão||  
|Aceitar entrada de pipeline?|false|  
|Aceitar caracteres curinga?|false|  
  
### <a name="-deleteall-switch"></a>-DeleteAll \<alternar >  
 Exclui todos os aplicativos de serviço [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , mas não exclui o banco de dados de aplicativo de serviço, nem os objetos de instância de serviço no farm. [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] e Serviço de Mecanismo do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] permanecem instanciados, mas inutilizáveis, após a remoção dos aplicativos de serviço.  
  
|||  
|-|-|  
|Obrigatório?|false|  
|Posição?|nomeado|  
|Valor padrão||  
|Aceitar entrada de pipeline?|false|  
|Aceitar caracteres curinga?|false|  
  
### <a name="-removedata-switch"></a>-RemoveData \<alternar >  
 Remove o banco de dados de aplicativo de serviço que contém agendamentos de atualizações de dados, dados de uso de pasta de trabalho, mapas de instância usados para rastrear quais bancos de dados estão carregados e outros dados internos.  
  
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
C:\PS>Remove-PowerPivotServiceApplication -identity 12345678-90ab-cdef-ghijklmnop  
```  
  
 Este exemplo exclui um único aplicativo de serviço [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , mas não remove seu banco de dados ou cache. Se você não especificar uma identidade, receberá uma solicitação para fornecer uma.  
  
## <a name="example-2"></a>Exemplo 2  
  
```  
C:\PS>Remove-PowerPivotServiceApplication -DeleteAll  
```  
  
 Este exemplo exclui todos os aplicativos de serviço [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] no farm. Os bancos de dados e o cache não são excluídos.  
  
## <a name="example-3"></a>Exemplo 3  
  
```  
CC:\PS>Remove-PowerPivotServiceApplication -identity 12345678-90ab-cdef-ghijklmnop -RemoveData  
```  
  
 Este exemplo exclui um único aplicativo de serviço [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] e seu banco de dados e arquivos de cache.  
  
  
