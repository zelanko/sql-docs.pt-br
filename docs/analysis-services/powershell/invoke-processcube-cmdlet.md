---
title: Cmdlet Invoke-ProcessCube | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: ''
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 02be0d6d491bf05e13b534c76b19a3eadb1074b3
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="invoke-processcube-cmdlet"></a>Cmdlet ProcessCube
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  Processe um cubo usando uma variável de tipo de processamento específica.  
  
>[!NOTE] 
>Este artigo pode conter informações desatualizadas e exemplos. Use o cmdlet Get-Help para a versão mais recente.
  
## <a name="syntax"></a>Sintaxe  
 `Invoke-ProcessCube [-Name] <System.String> [-Database] <System.String> [-ProcessType] <Microsoft.AnalysisServices.ProcessType> [<CommonParameters>]`  
  
 `Invoke-ProcessCube –DatabaseCube <Microsoft.AnalysisServices.Cube> [-ProcessType] <Microsoft.AnalysisServices.ProcessType> [<CommonParameters>]`  
  
## <a name="description"></a>Description  
 O cmdlet Invoke-ProcessCube processa um cubo ao nível que você especificar. Por exemplo, ProcessFull substitui os dados existentes por todos os novos dados. Ao processar um cubo, você deve especificar o tipo de processamento. Para obter mais informações, consulte [Opções e configurações de processamento &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/processing-options-and-settings-analysis-services.md).  
  
## <a name="parameters"></a>Parâmetros  
  
### <a name="-name-string"></a>-Nome \<cadeia de caracteres >  
 Especifica o cubo a ser processado.  
  
|||  
|-|-|  
|Obrigatório?|true|  
|Posição?|0|  
|Valor padrão||  
|Aceitar entrada de pipeline?|false|  
|Aceitar caracteres curinga?|false|  
  
### <a name="-database-string"></a>-Banco de dados \<cadeia de caracteres >  
 Especifica o banco de dados ao qual o cubo pertence.  
  
|||  
|-|-|  
|Obrigatório?|true|  
|Posição?|1|  
|Valor padrão||  
|Aceitar entrada de pipeline?|false|  
|Aceitar caracteres curinga?|false|  
  
### <a name="-processtype-microsoftanalysisservicesprocesstype"></a>-ProcessType \<Microsoft.AnalysisServices.ProcessType >  
 Especifica o tipo de processo: ProcessFull, ProcessAdd, ProcessUpdate, ProcessIndexes, ProcessData, ProcessDefault, ProcessClear, ProcessStructure, ProcessCelarStructureOnly, ProcessScriptCache, ProcessRecalc.  
  
|||  
|-|-|  
|Obrigatório?|true|  
|Posição?|2|  
|Valor padrão||  
|Aceitar entrada de pipeline?|false|  
|Aceitar caracteres curinga?|false|  
  
### <a name="-databasecube-microsoftanalysissevicescube"></a>-DatabaseCube \<Microsoft.AnalysisSevices.Cube >  
 Especifica um objeto Microsoft.AnalysisServices.Cube a ser processado. Use este parâmetro se você desejar transmitir o nome do cubo por pipeline.  
  
|||  
|-|-|  
|Obrigatório?|true|  
|Posição?|nomeado|  
|Valor padrão||  
|Aceitar entrada de pipeline?|True (ByPropertyName)|  
|Aceitar caracteres curinga?|false|  
  
### <a name="commonparameters"></a>\<CommonParameters >  
 Este cmdlet oferece suporte aos parâmetros comuns: -Verbose, -Debug, -ErrorAction, -ErrorVariable, -OutBuffer e -OutVariable. Para obter mais informações, consulte [About_CommonParameters](http://go.microsoft.com/fwlink/?linkID=227825).  
  
## <a name="inputs-and-outputs"></a>Entradas e saídas  
 O tipo de entrada é o tipo dos objetos que você pode transportar para o cmdlet. O tipo de retorno é o tipo dos objetos que o cmdlet retorna.  
  
|||  
|-|-|  
|Entradas|Nenhuma|  
|Saídas|Nenhuma|  
  
## <a name="example-1"></a>Exemplo 1  
 `PS SQL SERVER:\sqlas\locahost\default\Databases\AWTEST\Cubes\Adventure Works > Get-Item .| Invoke-ProcessCube–ProcessType:ProcessDefault`  
  
 Este comando reside na identidade do cubo ser processado.  
  
## <a name="example-2"></a>Exemplo 2  
 `PS SQL SERVER:\sqlas\locahost\default > Invoke-ProcessCube “Adventure Works” –database AWTEST –ProcessType:ProcessDefault`  
  
 Este comando processa o cubo Adventure Works no banco de dados AWTEST.   
  
  
