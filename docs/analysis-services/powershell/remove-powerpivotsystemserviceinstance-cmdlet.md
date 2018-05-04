---
title: Cmdlet Remove-PowerPivotSystemServiceInstance | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: ''
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: c3f6f960d0f2b39fa877203ede26f5e66b5c3c37
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="remove-powerpivotsystemserviceinstance-cmdlet"></a>Cmdlet Remove-PowerPivotSystemServiceInstance
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Remove uma instância do Serviço de Sistema do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] do farm.  

>[!NOTE] 
>Este artigo pode conter informações desatualizadas e exemplos. Use o cmdlet Get-Help para a versão mais recente.
  
 **Aplica-se a:** SharePoint 2010 e SharePoint 2013.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
Remove-PowerPivotSystemServiceInstance [-Confirm <switch>] [-DeleteLocal <switch>] [-Identity <PowerPivotMidTierServiceInstancePipeBind>] [<CommonParameters>]  
```  
  
## <a name="description"></a>Description  
 O cmdlet Remove-PowerPivotSystemServiceInstance remove informações de instância sobre o Serviço de Sistema do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] do farm. Ele não remove os arquivos de programa. Para remover permanentemente os arquivos de programa, você deve desinstalá-los.  
  
 Se você remover o Serviço de Sistema do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , não se esqueça de executar também Remove-PowerPivotEngineServiceInstance para remover a instância do Analysis Services associada, seguido de Remove-PowerPivotServiceApplication para excluir qualquer aplicativo PowerPivotservice. Os aplicativos de serviço não serão mais executados após a remoção dos serviços.  
  
 Para reverter essa alteração, você pode executar New-PowerPivotSystemServiceInstance -Provision:$true para habilitar novamente as informações de instância.  
  
## <a name="parameters"></a>Parâmetros  
  
### <a name="-identity-powerpivotmidtierserviceinstancepipebind"></a>-Identity \<PowerPivotMidTierServiceInstancePipeBind>  
 Especifica o GUID da instância do Serviço de Sistema do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] que você deseja remover. Há uma instância de serviço em cada servidor de aplicativo que tem uma instalação do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint.  
  
|||  
|-|-|  
|Obrigatório?|false|  
|Posição?|0|  
|Valor padrão||  
|Aceitar entrada de pipeline?|true|  
|Aceitar caracteres curinga?|false|  
  
### <a name="-deletelocal-switch"></a>-DeleteLocal \<alternar >  
 Exclui a instância do Serviço de Sistema do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] instalada no computador local, permitindo a você remover a instância sem ter que especificar uma identidade de objeto.  
  
|||  
|-|-|  
|Obrigatório?|false|  
|Posição?|nomeado|  
|Valor padrão||  
|Aceitar entrada de pipeline?|false|  
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
C:\PS>Remove-PowerPivotSystemServiceInstance -deletelocal  
```  
  
 Este exemplo mostra como remover a instância do Serviço de Sistema do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] executada no servidor de aplicativo local.  
  
## <a name="example-2"></a>Exemplo 2  
  
```  
C:\PS>Remove-PowerPivotSystemServiceInstance -identity 1234567-890a-bcde-fghijklmn  
```  
  
 Este exemplo mostra como excluir um Serviço de Sistema do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] específico com base em sua identidade.  
  
  
