---
title: Comandos (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
topic_type:
- apiref
- apinav
helpviewer_keywords:
- commands [XML for Analysis]
- XML for Analysis, commands
- XMLA, commands
ms.assetid: c8a93ea6-8eb5-4204-b037-69cb442a0082
caps.latest.revision: 14
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: bbfb56cc1ee12acd511c344ba3e1940fd5d56b32
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36010097"
---
# <a name="commands-xmla"></a>Commands (XMLA)
  Essa seção de referência contém elementos XMLA (XML for Analysis) que podem ser utilizados com o elemento `Command` durante uma chamada de método `Execute`.  
  
|Elemento|Description|  
|-------------|-----------------|  
|[Elemento Alter (XMLA)](alter-element-xmla.md)|Contém elementos do Analysis Services Scripting Language (ASSL) usados pelo [Execute](../xml-elements-methods-execute.md) método para alterar objetos em uma instância do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].|  
|[Elemento Backup](backup-element-xmla.md)|Faz backup de um [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] banco de dados para um arquivo de backup.|  
|[Elemento Batch](batch-element-xmla.md)|Executa o XML de um ou mais comandos Analysis (XMLA) como uma operação em lote, em sequência ou em paralelo, em uma instância do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].|  
|[Elemento BeginTransaction](begintransaction-element-xmla.md)|Começa uma transação na sessão atual com uma instância do Analysis Services.|  
|[Elemento Cancel](cancel-element-xmla.md)|Cancela um comando atualmente em execução em uma instância do Analysis Services.|  
|[Elemento ClearCache](clearcache-element-xmla.md)|Desmarca o cache de memória para o objeto especificado em uma instância do Analysis Services.|  
|[Elemento CommitTransaction](committransaction-element-xmla.md)|Confirma uma transação na sessão atual com uma instância do Analysis Services.|  
|[Elemento Create](create-element-xmla.md)|Contém elementos do Analysis Services Scripting Language (ASSL) usados pelo [Execute](../xml-elements-methods-execute.md) método para criar objetos em uma instância do Analysis Services.|  
|[Elemento Delete](delete-element-xmla.md)|Exclui um objeto em uma instância do Analysis Services.|  
|[Elemento DesignAggregations](designaggregations-element-xmla.md)|Cria agregações para um design de agregação em uma instância do Analysis Services.|  
|[Elemento Drop](drop-element-xmla.md)|Exclui membros de atributo de uma dimensão.|  
|[Elemento Insert](insert-element-xmla.md)|Insere membros de atributo em uma dimensão.|  
|[Elemento Lock](lock-element-xmla.md)|Bloqueia um objeto especificado em uma instância do Analysis Services.|  
|[Elemento MergePartitions](mergepartitions-element-xmla.md)|Intercala os dados de uma ou mais partições de origem em uma partição de destino e então exclui as partições de origem.|  
|[Elemento NotifyTableChange](notifytablechange-element-xmla.md)|Notifica uma instância do Analysis Services sobre a ocorrência de uma alteração nas tabelas em uma fonte de dados especificada.|  
|[Elemento Process](process-element-xmla.md)|Processa objetos em uma instância do Analysis Services.|  
|[Elemento Restore](restore-element-xmla.md)|Restaura um banco de dados do Analysis Services de um arquivo de backup.|  
|[Elemento RollbackTransaction](rollbacktransaction-element-xmla.md)|Reverte uma transação na sessão atual com uma instância do Analysis Services.|  
|[Elemento Statement](statement-element-xmla.md)|Contém uma consulta ou instrução a ser enviada usando o [Execute](../xml-elements-methods-execute.md) método para uma instância do Analysis Services.|  
|[Elemento Subscribe](subscribe-element-xmla.md)|Assina um rastreamento e retorna um conjunto de linhas que contém os eventos de rastreamento de uma instância do Analysis Services.|  
|[Elemento Synchronize](synchronize-element-xmla.md)|Sincroniza um banco de dados do Analysis Services com outro banco de dados existente.|  
|[Elemento Unlock](unlock-element-xmla.md)|Desbloqueia um bloqueio especificado em uma instância do Analysis Services.|  
|[Elemento Update](../xml-elements-commands/update-element-xmla.md)|Atualiza membros de atributo em uma dimensão.|  
|[Elemento UpdateCells](updatecells-element-xmla.md)|Atualiza células em um cubo habilitado para gravação.|  
  
  