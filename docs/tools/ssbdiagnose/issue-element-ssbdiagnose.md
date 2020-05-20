---
title: Elemento Issue
description: No SQL Server, o elemento Issue relata um problema encontrado pelo utilitário ssbdiagnose. O arquivo de saída XML tem um elemento Issue por problema reportado.
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: tools-other
ms.topic: conceptual
helpviewer_keywords:
- issue element
- XML output file format [ssbdiagnose], issue element
- ssbdiagnose
ms.assetid: 2246a886-686b-44ca-9771-b155cedad8be
author: markingmyname
ms.author: maghan
ms.manager: jroth
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 03/01/2017
ms.openlocfilehash: 0f0d339322dea349f7769ae32d7380f70c922539
ms.sourcegitcommit: b8933ce09d0e631d1183a84d2c2ad3dfd0602180
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/13/2020
ms.locfileid: "83150573"
---
# <a name="issue-element-ssbdiagnose"></a>Elemento Issue (ssbdiagnose)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

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
  
|Atributo|Descrição|  
|---------------|-----------------|  
|**tipo**|Identifica qual categoria de problema o elemento Issue está reportando:<br /><br /> **"Diagnóstico"** reporta um problema de configuração encontrado durante a análise da configuração de um [!INCLUDE[ssSB](../../includes/sssb-md.md)] .<br /><br /> **"Problema"** reporta um problema que impediu o **ssbdiagnose** de concluir sua análise. Corrija o problema e execute o **ssbdiagnose**novamente.<br /><br /> **"Evento"** reporta um evento [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] encontrado quando você executa uma verificação de **-RUNTIME** . Os eventos só serão reportados se **-SHOWEVENTS** for especificado.|  
|**code**|Identifica o número de erro da mensagem.|  
|**server**|Identifica a instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] na qual o problema foi encontrado. Se o problema estava em uma instância padrão, o atributo de servidor só terá o nome do computador. Se o problema estava em uma instância nomeada, o atributo de servidor estará no formato NomedoComputador\NomedaInstância.|  
|**database**|Identifica o nome do banco de dados no qual o problema foi encontrado.|  
|**object**|Identifica o nome do objeto no qual o problema foi encontrado. Se o problema ocorreu em um nível de instância ou banco de dados, o atributo de objeto repetirá o nome da instância ou do banco de dados.|  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|**Comprimento e tipo de dados**|**string**, tamanho é ilimitado.|  
|**Valor**|Retorna o texto da mensagem de erro.|  
|**Ocorrência**|Uma vez por erro reportado.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elementos|  
|------------------|--------------|  
|**Elemento pai**|[Elemento DiagnosticInformation &#40;ssbdiagnose&#41;](../../tools/ssbdiagnose/diagnosticinformation-element-ssbdiagnose.md)|  
|**Elementos filho**|Nenhum|  
  
## <a name="example"></a>Exemplo  
 Este elemento reporta um erro 1102 para um banco de dados que não tenha uma chave mestra e o erro foi encontrado durante a análise de uma configuração do [!INCLUDE[ssSB](../../includes/sssb-md.md)] .  
  
```  
<Issue type="Diagnosis" code="1102" server="TestComputer" database="TargetDB" object="TargetDB">The master key was not found</diagnostic>  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Utilitário ssbdiagnose &#40;Service Broker&#41;](../../tools/ssbdiagnose/ssbdiagnose-utility-service-broker.md)  
  
  
