---
title: Cmdlet Invoke-ProcessTable | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: 865e6d06-b99a-41f3-9d6f-c3c97b529b23
caps.latest.revision: "9"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 01d14a3ee7db466f184cb99fbb271520ab448244
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/08/2017
---
# <a name="invoke-processtable-cmdlet"></a>Cmdlet Invoke-ProcessTable
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]Conduz a **processo** operação em um **tabela** com um determinado **RefreshType**.  

>[!NOTE] 
>Este artigo pode conter informações desatualizadas e exemplos. Use o cmdlet Get-Help para a versão mais recente.
  
## <a name="syntax"></a>Sintaxe  
 `Invoke-ProcessTable [-DatabaseName] <string> [-TableName] <string> [-RefreshType] <RefreshType> {Full |     ClearValues | Calculate | DataOnly | Automatic | Add | Defragment} [-Server <string>] [-Credential <pscredential>     [-WhatIf] [-Confirm]  [<CommonParameters>]`  
  
 `Invoke-ProcessTable -RefreshType <RefreshType> {Full | ClearValues | Calculate | DataOnly | Automatic | Add |     Defragment} -Table <Table> [-Server <string>] [-Credential <pscredential>] [-WhatIf] [-Confirm]     [<CommonParameters>]`  
  
## <a name="parameters"></a>Parâmetros  
  
### <a name="-tablename-string"></a>-TableName \<cadeia de caracteres >  
 Nome da tabela à qual pertence a partição a ser processada.  
  
|||  
|-|-|  
|Obrigatório?|true|  
|Posição?|0|  
|Valor padrão||  
|Aceitar entrada de pipeline?|false|  
|Aceitar caracteres curinga?|false|  
  
### <a name="-databasename-string"></a>-DatabaseName \<cadeia de caracteres >  
 Especifica o banco de dados ao qual a tabela pertence.  
  
|||  
|-|-|  
|Obrigatório?|true|  
|Posição?|0|  
|Valor padrão||  
|Aceitar entrada de pipeline?|false|  
|Aceitar caracteres curinga?|false|  
  
### <a name="-servermicrosoftanalysissevicesserver"></a>-Servidor\<Microsoft.AnalysisSevices.Server >  
 Opcionalmente, especifica a instância do servidor a ser conectado, se você não estiver usando o diretório do provedor **SQLAS** para contexto.  
  
|||  
|-|-|  
|Obrigatório?|false|  
|Posição?|nomeado|  
|Valor padrão||  
|Aceitar entrada de pipeline?|false|  
|Aceitar caracteres curinga?|false|  
  
### <a name="-refreshtype-microsoftanalysisservicesrefreshtype"></a>-RefreshType \<Microsoft.AnalysisServices.RefreshType >  
 Especifica o tipo de processo para um banco de dados Tabular.  Os valores válidos são Full, ClearValues, Calculate, DataOnly, Automatic, Add e Defragment. Consulte [Processar banco de dados, tabela ou partição &#40;Analysis Services&#41;](../../analysis-services/tabular-models/process-database-table-or-partition-analysis-services.md) para obter descrições e orientações.  
  
|||  
|-|-|  
|Obrigatório?|true|  
|Posição?|1|  
|Valor padrão||  
|Aceitar entrada de pipeline?|false|  
|Aceitar caracteres curinga?|false|  
  
### <a name="-credential"></a>-Credential  
 Se esse parâmetro for especificado, o nome de usuário e a senha serão usados para conexão com a instância do Analysis Server. Se nenhuma credencial for especifica, a conta padrão do Windows do usuário que executa o script será assumida.  
  
|||  
|-|-|  
|Obrigatório?|false|  
|Posição?|nomeado|  
|Valor padrão||  
|Aceitar entrada de pipeline?|false|  
|Aceitar caracteres curinga?|false|  
  
### <a name="-whatif"></a>-Whatif  
 Inclua esse parâmetro para obter informações sobre o impacto da operação antes que ela seja executada.  
  
|||  
|-|-|  
|Obrigatório?|false|  
|Posição?|nomeado|  
|Valor padrão||  
|Aceitar entrada de pipeline?|false|  
|Aceitar caracteres curinga?|false|  
  
### <a name="-confirm"></a>-Confirm  
 Inclua esse parâmetro para confirmar interativamente a operação com uma resposta Sim ou não antes que ela seja executada.  
  
|||  
|-|-|  
|Obrigatório?|false|  
|Posição?||  
|Valor padrão||  
|Aceitar entrada de pipeline?||  
|Aceitar caracteres curinga?|false|  
  
## <a name="example-1"></a>Exemplo 1  
 `PS SQLSERVER:\SQLAS\MachineName\Instance\Databases\DB1\> Invoke-ProcessTable -TableName "myTable" -Database "DB1"  -RefreshType "Full"`  
  
 Este comando é redirecionado na identidade da tabela para ser processado.  
  
## <a name="example-2"></a>Exemplo 2  
 `PS SQLSERVER:\SQLAS\MachineName\Instance\Databases\DB1\> Invoke-ProcessTable -TableName "myTable" -Database "DB1"  -RefreshType [Microsoft.AnalysisServices.Tabular.RefreshType]::Full`  
  
 Este comando processa uma tabela de metadados tabulares usando um tipo de atualização do **enum** .  
  
  
