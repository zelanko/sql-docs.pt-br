---
title: Cmdlet Invoke-ProcessPartition | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: 516fab44-734e-425b-9bd0-b4aee1fd338f
caps.latest.revision: "9"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: dc03c77ffd4fc5ad02d234fa5c1bdc456234779b
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/08/2017
---
# <a name="invoke-processpartition-cmdlet"></a>Cmdlet Invoke-ProcessPartition
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]Processe uma partição usando uma variável de tipo de processamento específica.  

>[!NOTE] 
>Este artigo pode conter informações desatualizadas e exemplos. Use o cmdlet Get-Help para a versão mais recente.
  
## <a name="syntax"></a>Sintaxe  
 `Invoke-ProcessPartition [-Name] <System.String> [-Database] <System.String> [-ProcessType] <Microsoft.AnalysisServices.ProcessType> [-CubeName] <System.String> [-MeasureGroupName] <System.String> [<CommonParameters>]`  
  
 `Invoke-ProcessPartition –DatabasePartition <Microsoft.AnalysisServices.Partition> [-ProcessType] <Microsoft.AnalysisServices.ProcessType> [<CommonParameters>]`  
  
## <a name="description"></a>Description  
 O cmdlet do Invoke-ProcessParition processa uma partição específica de um banco de dados do Analysis Services, para um determinado cubo e grupo de medidas. O valor ProcessType determina o escopo da operação. Ao processar uma partição, você deve especificar o tipo de processamento. Para obter mais informações, consulte [Opções e configurações de processamento &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/processing-options-and-settings-analysis-services.md).  
  
## <a name="parameters"></a>Parâmetros  
  
### <a name="-name-string"></a>-Nome \<cadeia de caracteres >  
 Especifica a partição a ser processada.  
  
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
  
### <a name="-cubename-string"></a>-Nome do cubo \<cadeia de caracteres >  
 Especifica o cubo ao qual o grupo de medidas pertence.  
  
|||  
|-|-|  
|Obrigatório?|true|  
|Posição?|2|  
|Valor padrão||  
|Aceitar entrada de pipeline?|false|  
|Aceitar caracteres curinga?|false|  
  
### <a name="-measuregroupname-string"></a>-MeasureGroupName \<cadeia de caracteres >  
 Especifica o grupo de medidas ao qual a partição pertence.  
  
|||  
|-|-|  
|Obrigatório?|true|  
|Posição?|2|  
|Valor padrão||  
|Aceitar entrada de pipeline?|false|  
|Aceitar caracteres curinga?|false|  
  
### <a name="-databasepartition-microsoftanalysisservicespartition"></a>-DatabasePartition \<AnalysisServices >  
 Especifica a partição a ser processada.  
  
|||  
|-|-|  
|Obrigatório?|true|  
|Posição?|2|  
|Valor padrão||  
|Aceitar entrada de pipeline?|false|  
|Aceitar caracteres curinga?|false|  
  
### <a name="-processtype-microsoftanalysisservicesprocesstype"></a>-ProcessType \<Microsoft.AnalysisServices.ProcessType >  
 Especifica o tipo de processo: ProcessFull, ProcessAdd, ProcessUpdate, ProcessIndexes, ProcessData, ProcessDefault, ProcessClear, ProcessStructure, ProcessCelarStructureOnly, ProcessScriptCache, ProcessRecalc.  
  
|||  
|-|-|  
|Obrigatório?|true|  
|Posição?|nomeado|  
|Valor padrão||  
|Aceitar entrada de pipeline?|false|  
|Aceitar caracteres curinga?|false|  
  
### <a name="commonparameters"></a>\<CommonParameters >  
 Este cmdlet oferece suporte aos parâmetros comuns: -Verbose, -Debug, -ErrorAction, -ErrorVariable, -OutBuffer e -OutVariable. Para obter mais informações, consulte [About_CommonParameters](http://go.microsoft.com/fwlink/?linkID=227825).  
  
## <a name="inputs-and-outputs"></a>Entradas e saídas  
 O tipo de entrada é o tipo dos objetos que você pode transportar para o cmdlet. O tipo de retorno é o tipo dos objetos que o cmdlet retorna.  
  
|||  
|-|-|  
|Entradas|Nenhum.|  
|Saídas|Nenhum.|  
  
## <a name="example-1"></a>Exemplo 1  
 `PS SQL SERVER:\sqlas\locahost\default\Databases\AWTEST\Cubes\Adventure Works\MeasureGroups\Sales Orders\Partitions\Total_Orders_2004 > Get-Item .| Invoke-ProcessPartition –ProcessType:ProcessDefault`  
  
 Este comando reside na identidade da partição a ser processada.  
  
## <a name="example-2"></a>Exemplo 2  
 `PS SQL SERVER:\sqlas\locahost\default\Databases\AWTEST\Cubes\Adventure Works\MeasureGroups> Invoke-ProcessPartition –Name “Total_Orders_2003” –MeasureGroupname “Sales Order” –CubeName “Adventure Works” –database “AWTEST” –ProcessType “ProcessFull”`  
  
 Este comando processa a partição Total_Orders_2003 no grupo de medidas Pedidos de Vendas do banco de dados AWTEST.  
  
  
  
