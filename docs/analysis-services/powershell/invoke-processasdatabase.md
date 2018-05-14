---
title: Chamar ProcessASDatabase | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: powershell
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 44a5654207e84f3488c66b3bc9cfab4778b51acb
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="invoke-processasdatabase"></a>ProcessASDatabase Invoke
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  Conduz a operação **Processo** em um **banco de dados** especificado com um **ProcessType** ou **RefreshType** específico dependendo do tipo de metadados subjacentes.  
  
 Use **ProcessType** para banco de dados com os metadados multidimensionais (isso inclui bancos de dados tabulares com compatibilidade nível 1050, 1100 ou 1103).  
  
 Use **RefreshType** para bancos de dados tabulares no nível de compatibilidade 1200 ou superior.  

>[!NOTE] 
>Este artigo pode conter informações desatualizadas e exemplos. Use o cmdlet Get-Help para a versão mais recente.
  
## <a name="syntax"></a>Sintaxe  
 `Invoke-ProcessASDatabase [-DatabaseName] <string> [-RefreshType] <RefreshType> {Full | ClearValues | Calculate |     DataOnly | Automatic | Add | Defragment} [-Server <string>] [-Credential <pscredential>] [-WhatIf] [-Confirm]     [<CommonParameters>]`  
  
 `Invoke-ProcessASDatabase [-DatabaseName] <string> [-ProcessType] <ProcessType> {ProcessFull | ProcessAdd |     ProcessUpdate | ProcessIndexes | ProcessData | ProcessDefault | ProcessClear | ProcessStructure |     ProcessClearStructureOnly | ProcessScriptCache | ProcessRecalc | ProcessDefrag} [-Server <string>] [-Credential     <pscredential>] [-WhatIf] [-Confirm]  [<CommonParameters>]`  
  
## <a name="description"></a>Description  
 O cmdlet **ProcessASDatabase Invoke** processa um banco de dados para o nível especificado. Por exemplo, para bancos de dados de Tabela no nível de compatibilidade 1200, a configuração de **RefreshType** como **completa** substitui os dados existentes por todos os novos dados.  
  
 O tipo de processamento (multidimensional) ou o tipo de atualização (tabular) são necessários e podem ser especificados antes ou após os parâmetros de banco de dados e servidor:  
  
-   Para multidimensional, consulte [Opções de processamento e configurações &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/processing-options-and-settings-analysis-services.md).  
  
-   Para tabela, consulte [Processar banco de dados, tabela ou partição &#40;Analysis Services&#41;](../../analysis-services/tabular-models/process-database-table-or-partition-analysis-services.md).  
  
## <a name="parameters"></a>Parâmetros  
  
### <a name="-databasename-string"></a>-DatabaseName \<cadeia de caracteres >  
 Especifica o banco de dados Multidimensional ou Tabular a ser processado.  
  
|||  
|-|-|  
|Obrigatório?|true|  
|Posição?|0|  
|Valor padrão||  
|Aceitar entrada de pipeline?|false|  
|Aceitar caracteres curinga?|false|  
  
### <a name="-servermicrosoftanalysissevicesserver"></a>-Server\<Microsoft.AnalysisSevices.Server>  
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
  
### <a name="-processtype-microsoftanalysisservicesprocesstype"></a>-ProcessType \<Microsoft.AnalysisServices.ProcessType >  
 Especifica o tipo de processo para um banco de dados Multidimensional ou Tabular nos níveis de compatibilidade 1050-1103. os valores válidos incluem ProcessFull, ProcessAdd, ProcessUpdate, ProcessIndexes, ProcessData, ProcessDefault, ProcessClear, ProcessStructure, ProcessCelarStructureOnly, ProcessScriptCache, ou ProcessRecalc. Consulte [Processando opções e configurações de &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/processing-options-and-settings-analysis-services.md) para obter descrições e orientação.  
  
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
  
## <a name="-whatif"></a>-Whatif  
 Inclua esse parâmetro para obter informações sobre o impacto da operação antes que ela seja executada.  
  
|||  
|-|-|  
|Obrigatório?|false|  
|Posição?|nomeado|  
|Valor padrão||  
|Aceitar entrada de pipeline?|false|  
|Aceitar caracteres curinga?|false|  
  
## <a name="-confirm"></a>-Confirm  
 Inclua esse parâmetro para confirmar interativamente a operação com uma resposta Sim ou não antes que ela seja executada.  
  
|||  
|-|-|  
|Obrigatório?|false|  
|Posição?||  
|Valor padrão||  
|Aceitar entrada de pipeline?||  
|Aceitar caracteres curinga?|false|  
  
## <a name="example-1-sqlas-provider"></a>Exemplo 1 (provedor SQLAS)  
 Este exemplo usa o provedor **SQLAS** para definir o contexto para a lista de bancos de dados em uma instância padrão.  Se você listar o conteúdo da pasta de bancos de dados, verá todos os bancos de dados junto com seu estado de processo e o modo de leitura-gravação.  
  
 Na pasta do banco de dados, é possível executar **Invoke-ProcessASDatabase** especificando apenas o nome do banco de dados.  
  
```  
PS > import-module SQLPS -DisableNameChecking  
PS  SQL Server > cd sqlas\ssas-srv-01\default\databases  
PS SQLSERVER:\sqlas\ssas-srv-01\default\databases> dir  
. . . .  
PS SQLSERVER:\sqlas\ssas-srv-01\default\databases> Invoke-ProcessASDatabase "adventureworks"  
  
```  
  
 Dependendo do tipo de banco de dados, você será solicitado a especificar um **RefreshType** ou um **ProcessType**.  
  
 A prova de processamento é a presença de um objeto de impacto na instrução return: Microsoft.AnalysisServices.Tabular.ObjectImpact.  
  
 Observe que, às vezes, as informações de estado do objeto são armazenadas em cache, portanto, se você listar o conteúdo de um diretório após o êxito do processamento, o estado do banco de dados reterá seu descritor “não processado” original. Isso é enganoso porque, uma vez que o objectimact é retornado, o banco de dados é processado.  
  
 Você pode confirmar que o processamento foi bem-sucedido examinando a página de propriedades de banco de dados no Management Studio, iniciando uma nova sessão ou retornando o estado de processamento de um objeto de banco de dados (por meio de [Microsoft.AnalysisServices.ProcessableMajorObject.LastProcessed](https://msdn.microsoft.com/library/microsoft.analysisservices.processablemajorobject.lastprocessed.aspx)).  
  
## <a name="example-2"></a>Exemplo 2  
 Este exemplo mostra a mesma operação usando apenas o cmdlet sem o provedor. Parâmetros adicionais são necessários para especificar o tipo de servidor e processo.  
  
```  
PS > import-module SQLPS -DisableNameChecking  
PS  SQL Server >  Invoke-ProcessASDatabase -databasename "AdventureWorks" -server '\\server-name\instancename' –ProcessType "ProcessFull"  
  
```  
  
  
  
