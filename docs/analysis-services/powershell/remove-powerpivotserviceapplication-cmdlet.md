---
title: Cmdlet Remove-PowerPivotServiceApplication | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: powershell
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 30b7826bf0239ed59b0b94ce624ab1eb212a34fc
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="remove-powerpivotserviceapplication-cmdlet"></a>Cmdlet Remove-PowerPivotServiceApplication
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
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
|Entradas|Nenhuma.|  
|Saídas|Nenhuma.|  
  
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
  
  
