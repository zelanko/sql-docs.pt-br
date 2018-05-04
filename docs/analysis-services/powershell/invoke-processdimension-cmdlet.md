---
title: Cmdlet Invoke-ProcessDimension | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: ''
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f5cd3ad9f902aea9234046991ae9651702c5ee31
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="invoke-processdimension-cmdlet"></a>Cmdlet Invoke-ProcessDimension
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Processe uma dimensão usando uma variável de tipo de processamento específica.  

>[!NOTE] 
>Este artigo pode conter informações desatualizadas e exemplos. Use o cmdlet Get-Help para a versão mais recente.
  
## <a name="syntax"></a>Sintaxe  
 `Invoke-ProcessDimension [-Name] <System.String> [-Database] <System.String> [-ProcessType] <Microsoft.AnalysisServices.ProcessType> [<CommonParameters>]`  
  
 `Invoke-ProcessDimension –DatabaseDimension <Microsoft.AnalysisServices.Dimension> [-ProcessType] <Microsoft.AnalysisServices.ProcessType> [<CommonParameters>]`  
  
## <a name="description"></a>Description  
 O cmdlet Invoke-ProcessDimension processa a dimensão especificada. Especifique o tipo de processamento. Para obter mais informações sobre tipos de processamento de uma dimensão, consulte [Opções de processamento e configurações &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/processing-options-and-settings-analysis-services.md).  
  
## <a name="parameters"></a>Parâmetros  
  
### <a name="-name-string"></a>-Nome \<cadeia de caracteres >  
 Especifica a dimensão a ser processada.  
  
|||  
|-|-|  
|Obrigatório?|true|  
|Posição?|0|  
|Valor padrão||  
|Aceitar entrada de pipeline?|false|  
|Aceitar caracteres curinga?|false|  
  
### <a name="-database-string"></a>-Banco de dados \<cadeia de caracteres >  
 Especifica o banco de dados ao qual a dimensão pertence.  
  
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
  
### <a name="-databasedimension-microsoftanalysissevicesdimension"></a>-DatabaseDimension \<Microsoft.AnalysisSevices.Dimension >  
 Especifica um objeto Microsoft.AnalysisServices.Dimension a ser processado. Use este parâmetro se você desejar transmitir o nome da dimensão por pipeline.  
  
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
|Entradas|Microsoft.AnalysisSevices.Dimension|  
|Saídas|Nenhuma|  
  
## <a name="example-1"></a>Exemplo 1  
 `PS SQL SERVER:\sqlas\locahost\default\Databases\AWTEST\Dimensions\Account> Get-Item .| Invoke-ProcessDimension –ProcessType:ProcessDefault`  
  
 Este comando recupera o objeto de dimensão especificado através do pipeline e processa-o.  
  
## <a name="example-2"></a>Exemplo 2  
 `PS SQL SERVER:\sqlas\locahost\default\Databases\AWTEST\Dimensions > Invoke-ProcessDimension –Name “Customer” –Database “AWTEST” –ProcessType “ProcessDefault”`  
  
 Este comando identifica uma dimensão específica que será processada.  
  
> [!NOTE]  
>  Às vezes, uma dimensão processada com êxito aparece como 'não processada' quando você lista a pasta de dimensões na janela do PowerShell. Para certificar-se de que uma dimensão tenha sido de fato processada, verifique as propriedades de dimensão no SQL Server Management Studio.  
  
  
  
