---
title: Comandos (XMLA) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- commands [XML for Analysis]
- XML for Analysis, commands
- XMLA, commands
ms.assetid: c8a93ea6-8eb5-4204-b037-69cb442a0082
caps.latest.revision: "14"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: c6a16dfc9dd0ff1c58edcc18c69c1d2f2709145a
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/08/2017
---
# <a name="xml-elements---commands"></a>Elementos XML - comandos
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]Esta seção de referência contém XML para elementos Analysis (XMLA) que podem ser usados dentro de **comando** elemento durante um **Execute** chamada de método.  
  
|Elemento|Description|  
|-------------|-----------------|  
|[Elemento Alter (XMLA)](../../../analysis-services/xmla/xml-elements-commands/alter-element-xmla.md)|Contém elementos do Analysis Services Scripting Language (ASSL) usados pelo [Execute](../../../analysis-services/xmla/xml-elements-methods-execute.md) método para alterar objetos em uma instância do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].|  
|[Elemento de backup](../../../analysis-services/xmla/xml-elements-commands/backup-element-xmla.md)|Faz backup de um [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] banco de dados para um arquivo de backup.|  
|[Elemento batch](../../../analysis-services/xmla/xml-elements-commands/batch-element-xmla.md)|Executa o XML de um ou mais comandos Analysis (XMLA) como uma operação em lote, em sequência ou em paralelo, em uma instância do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].|  
|[Elemento BeginTransaction](../../../analysis-services/xmla/xml-elements-commands/begintransaction-element-xmla.md)|Começa uma transação na sessão atual com uma instância do Analysis Services.|  
|[Elemento Cancel](../../../analysis-services/xmla/xml-elements-commands/cancel-element-xmla.md)|Cancela um comando atualmente em execução em uma instância do Analysis Services.|  
|[Elemento ClearCache](../../../analysis-services/xmla/xml-elements-commands/clearcache-element-xmla.md)|Desmarca o cache de memória para o objeto especificado em uma instância do Analysis Services.|  
|[Elemento CommitTransaction](../../../analysis-services/xmla/xml-elements-commands/committransaction-element-xmla.md)|Confirma uma transação na sessão atual com uma instância do Analysis Services.|  
|[Criar elemento](../../../analysis-services/xmla/xml-elements-commands/create-element-xmla.md)|Contém elementos do Analysis Services Scripting Language (ASSL) usados pelo [Execute](../../../analysis-services/xmla/xml-elements-methods-execute.md) método para criar objetos em uma instância do Analysis Services.|  
|[Elemento Delete](../../../analysis-services/xmla/xml-elements-commands/delete-element-xmla.md)|Exclui um objeto em uma instância do Analysis Services.|  
|[Elemento DesignAggregations](../../../analysis-services/xmla/xml-elements-commands/designaggregations-element-xmla.md)|Cria agregações para um design de agregação em uma instância do Analysis Services.|  
|[Elemento drop](../../../analysis-services/xmla/xml-elements-commands/drop-element-xmla.md)|Exclui membros de atributo de uma dimensão.|  
|[Elemento Insert](../../../analysis-services/xmla/xml-elements-commands/insert-element-xmla.md)|Insere membros de atributo em uma dimensão.|  
|[Elemento Lock](../../../analysis-services/xmla/xml-elements-commands/lock-element-xmla.md)|Bloqueia um objeto especificado em uma instância do Analysis Services.|  
|[Elemento MergePartitions](../../../analysis-services/xmla/xml-elements-commands/mergepartitions-element-xmla.md)|Intercala os dados de uma ou mais partições de origem em uma partição de destino e então exclui as partições de origem.|  
|[Elemento NotifyTableChange](../../../analysis-services/xmla/xml-elements-commands/notifytablechange-element-xmla.md)|Notifica uma instância do Analysis Services sobre a ocorrência de uma alteração nas tabelas em uma fonte de dados especificada.|  
|[Elemento Process](../../../analysis-services/xmla/xml-elements-commands/process-element-xmla.md)|Processa objetos em uma instância do Analysis Services.|  
|[Elemento Restore](../../../analysis-services/xmla/xml-elements-commands/restore-element-xmla.md)|Restaura um banco de dados do Analysis Services de um arquivo de backup.|  
|[Elemento RollbackTransaction](../../../analysis-services/xmla/xml-elements-commands/rollbacktransaction-element-xmla.md)|Reverte uma transação na sessão atual com uma instância do Analysis Services.|  
|[Elemento de instrução](../../../analysis-services/xmla/xml-elements-commands/statement-element-xmla.md)|Contém uma consulta ou instrução a ser enviada usando o [Execute](../../../analysis-services/xmla/xml-elements-methods-execute.md) método para uma instância do Analysis Services.|  
|[Elemento Subscribe](../../../analysis-services/xmla/xml-elements-commands/subscribe-element-xmla.md)|Assina um rastreamento e retorna um conjunto de linhas que contém os eventos de rastreamento de uma instância do Analysis Services.|  
|[Elemento Synchronize](../../../analysis-services/xmla/xml-elements-commands/synchronize-element-xmla.md)|Sincroniza um banco de dados do Analysis Services com outro banco de dados existente.|  
|[Elemento Unlock](../../../analysis-services/xmla/xml-elements-commands/unlock-element-xmla.md)|Desbloqueia um bloqueio especificado em uma instância do Analysis Services.|  
|[Elemento Update](../../../analysis-services/xmla/xml-elements-commands/update-element-xmla.md)|Atualiza membros de atributo em uma dimensão.|  
|[Elemento UpdateCells](../../../analysis-services/xmla/xml-elements-commands/updatecells-element-xmla.md)|Atualiza células em um cubo habilitado para gravação.|  
  
  
