---
title: Retornar resultados da tarefa Script | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
helpviewer_keywords:
- Script task [Integration Services], status information
- ExecutionValue property
- status information [Integration Services]
- TaskResult property
- SSIS Script task, status information
ms.assetid: ac06805b-c2db-44bd-af5c-5a0debe36dd7
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: cfc772b9809327e9b5383e81f489b5cf390f28ce
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47620554"
---
# <a name="returning-results-from-the-script-task"></a>Retornando resultados da tarefa Script
  A tarefa Script usa a propriedade <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.TaskResult%2A> e as propriedades <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.ExecutionValue%2A> opcionais para retornar informações de status para o tempo de execução do [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)], que poderá ser usado para determinar o caminho do fluxo de trabalho quando a tarefa Script for concluída.  
  
## <a name="taskresult"></a>TaskResult  
 A propriedade <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.TaskResult%2A> relata se a tarefa teve sucesso ou falhou. Por exemplo:  
  
 `Dts.TaskResult = ScriptResults.Success`  
  
## <a name="executionvalue"></a>ExecutionValue  
 A propriedade <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.ExecutionValue%2A> retorna opcionalmente um objeto definido pelo usuário, que quantifica ou fornece mais informações sobre o êxito ou falha da tarefa Script. Por exemplo, a tarefa de FTP usa a propriedade <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.ExecutionValue%2A> para retornar o número de arquivos transferidos. A tarefa Executar SQL retorna o número de linhas afetado pela tarefa. O <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.ExecutionValue%2A> também pode ser usado para determinar o caminho do fluxo de trabalho. Por exemplo:  
  
 `Dim rowsAffected as Integer`  
  
 `...`  
  
 `rowsAffected = 1000`  
  
 `Dts.ExecutionValue = rowsAffected`  
