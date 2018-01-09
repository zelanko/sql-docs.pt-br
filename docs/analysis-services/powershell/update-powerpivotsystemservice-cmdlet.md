---
title: Cmdlet Update-PowerPivotSystemService | Microsoft Docs
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
ms.assetid: a90f1158-68d3-4330-98c1-fb0f81e13328
caps.latest.revision: "8"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 045979085e6d8e1622fef2a961f6c9fdb21d772a
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="update-powerpivotsystemservice-cmdlet"></a>Cmdlet Update-PowerPivotSystemService
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]Atualiza o objeto pai do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] serviço do sistema no farm.  

>[!NOTE] 
>Este artigo pode conter informações desatualizadas e exemplos. Use o cmdlet Get-Help para a versão mais recente.
  
 **Aplica-se a:** SharePoint 2010 e SharePoint 2013.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
Update-PowerPivotSystemService [-Confirm <switch>] [<CommonParameters>]  
```  
  
## <a name="description"></a>Description  
 O cmdlet **Update-PowerPivotSystemService** executa uma série de ações de atualização no objeto pai do Serviço de Sistema do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , nas instâncias e nos aplicativos de serviço do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] no farm. Todos os serviços da camada intermediária e aplicativos em uma implantação do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint devem ser executados no mesmo nível funcional. Este cmdlet executa as ações de atualização em todos esses objetos.  
  
 Execute esse cmdlet após a execução da Instalação do SQL Server para instalar uma versão mais nova do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint ou se você tiver aplicado uma atualização cumulativa no servidor. Para verificar se a atualização é necessária, execute `Get-PowerPivotSystemService` para analisar a propriedade **NeedsUpgrade** . Se **NeedsUpgrade** for true, você deverá executar o cmdlet para atualizar os objetos da camada intermediária do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] no farm.  
  
 Como uma implantação do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint inclui serviços de dados da camada intermediária e de back-end, você deve executar **Update-PowerPivotEngineService** sempre que executar **Update-PowerPivotSystemService** para assegurar que ambas as camadas tenham a mesma versão no farm.  
  
 Não é possível reverter a atualização para a versão anterior. Se você reverter para uma versão anterior, remova o [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] do seu farm do SharePoint e reinstale o software. Para verificar se a operação de atualização foi bem-sucedida, execute `Get-PowerPivotSystemService` para analisar as propriedades globais das informações de versão e para verificar se **NeedsUpgrade** não está mais definida como true.  
  
## <a name="parameters"></a>Parâmetros  
  
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
 Este cmdlet oferece suporte aos seguintes parâmetros:  
  
-   Detalhado  
  
-   Depurador  
  
-   ErrorAction  
  
-   ErrorVariable  
  
-   WarningAction  
  
-   WarningVariable  
  
-   OutBuffer  
  
-   OutVariable  
  
 Para obter mais informações, consulte [About_CommonParameters](http://go.microsoft.com/fwlink/?linkID=227825).  
  
## <a name="inputs-and-outputs"></a>Entradas e saídas  
 O tipo de entrada é o tipo dos objetos que você pode transportar para o cmdlet. O tipo de retorno é o tipo dos objetos que o cmdlet retorna.  
  
|||  
|-|-|  
|Entradas|Nenhum.|  
|Saídas|Nenhum.|  
  
  
