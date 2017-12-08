---
title: Cmdlet Update-PowerPivotSystemService | Microsoft Docs
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
ms.assetid: a90f1158-68d3-4330-98c1-fb0f81e13328
caps.latest.revision: "8"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 92b1c88166578605f0060ac65278d13ab4c42864
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="update-powerpivotsystemservice-cmdlet"></a>Cmdlet Update-PowerPivotSystemService

[!INCLUDE[ssas-appliesto-sqlas-all](../../includes/ssas-appliesto-sqlas-all.md)]

  Atualiza o objeto pai do Serviço de Sistema do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] no farm.  

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
  
-   detalhado  
  
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
  
  
