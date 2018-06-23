---
title: Elemento Issue (ssbdiagnose) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- issue element
- XML output file format [ssbdiagnose], issue element
- ssbdiagnose
ms.assetid: 2246a886-686b-44ca-9771-b155cedad8be
caps.latest.revision: 17
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: adff003b1d6b98d7778311b84aca4666dd802d27
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36118240"
---
# <a name="issue-element-ssbdiagnose"></a>Elemento Issue (ssbdiagnose)
  Reporta um problema que foi encontrado pelo utilitário **ssbdiagnose** . O arquivo de saída XML de **ssbdiagnose** tem um elemento Issue por problema reportado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
<Issue  
    type="..."   
    code="..."   
    server="..."   
    database="..."   
    object="...">   
    ...   
</Issue>  
```  
  
## <a name="element-attributes"></a>Atributos do elemento  
  
|attribute|Description|  
|---------------|-----------------|  
|`type`|Identifica qual categoria de problema o elemento Issue está reportando:<br /><br /> **"Diagnóstico"** reporta um problema de configuração encontrado durante a análise da configuração de um [!INCLUDE[ssSB](../../includes/sssb-md.md)] .<br /><br /> **"Problema"** reporta um problema que impediu o **ssbdiagnose** de concluir sua análise. Corrija o problema e execute o **ssbdiagnose**novamente.<br /><br /> **"Evento"** reporta um evento [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] encontrado quando você executa uma verificação de **-RUNTIME** . Os eventos só serão reportados se **-SHOWEVENTS** for especificado.|  
|`code`|Identifica o número de erro da mensagem.|  
|`server`|Identifica a instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] na qual o problema foi encontrado. Se o problema estava em uma instância padrão, o atributo de servidor só terá o nome do computador. Se o problema estava em uma instância nomeada, o atributo de servidor estará no formato NomedoComputador\NomedaInstância.|  
|`database`|Identifica o nome do banco de dados no qual o problema foi encontrado.|  
|`object`|Identifica o nome do objeto no qual o problema foi encontrado. Se o problema ocorreu em um nível de instância ou banco de dados, o atributo de objeto repetirá o nome da instância ou do banco de dados.|  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|**Comprimento e tipo de dados**|`string`, tamanho é ilimitado.|  
|**Value**|Retorna o texto da mensagem de erro.|  
|**Ocorrência**|Uma vez por erro reportado.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elementos|  
|------------------|--------------|  
|**Elemento pai**|[Elemento DiagnosticInformation &#40;ssbdiagnose&#41;](diagnosticinformation-element-ssbdiagnose.md)|  
|**Elementos filho**|Nenhum|  
  
## <a name="example"></a>Exemplo  
 Este elemento reporta um erro 1102 para um banco de dados que não tenha uma chave mestra e o erro foi encontrado durante a análise de uma configuração do [!INCLUDE[ssSB](../../includes/sssb-md.md)] .  
  
```  
<Issue type="Diagnosis" code="1102" server="TestComputer" database="TargetDB" object="TargetDB">The master key was not found</diagnostic>  
```  
  
## <a name="see-also"></a>Consulte também  
 [Utilitário ssbdiagnose &#40;Service Broker&#41;](ssbdiagnose-utility-service-broker.md)  
  
  