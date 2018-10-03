---
title: Elemento BeginTransaction (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- BeginTransaction Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#BeginTransaction
- microsoft.xml.analysis.begintransaction
- http://schemas.microsoft.com/analysisservices/2003/engine#BeginTransaction
helpviewer_keywords:
- BeginTransaction command
ms.assetid: fca122fc-b57c-4ba6-849b-ca8c93cf64e9
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 5e8b1954836a7c5b079d629602d03ba4b45d8620
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48083458"
---
# <a name="begintransaction-element-xmla"></a>Elemento BeginTransaction (XMLA)
  Começa uma transação na sessão atual com uma instância do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Command>  
   <BeginTransaction />  
</Command>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|None|  
|Valor padrão|None|  
|Cardinalidade|0-n: Elemento opcional que pode ocorrer mais de uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[Comando](../xml-elements-properties/command-element-xmla.md)|  
|Elementos filho|None|  
  
## <a name="remarks"></a>Comentários  
 O comando `BeginTransaction` inicia uma transação ativa na sessão atual. Se uma transação ativa já existir, a instância do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] aumentará a contagem de referência de transações para a sessão atual. Se não existir, a instância iniciará uma nova transação e definirá a contagem de referência de sessão atual como 1. Se uma transação ativa for explicitamente especificada usando o comando `BeginTransaction`, todos os comandos subsequentes serão executados na transação especificada explicitamente.  
  
 Quando a sessão atual for encerrada e a contagem de referência de transações for maior que zero, todas as transações ativas serão revertidas.  
  
 Se não houver nenhuma transação ativa especificada explicitamente na sessão atual, cada comando emitido na sessão atual será executando em uma transação definida implicitamente. A transação implícita é confirmada se o comando tiver sucesso ou revertida se o comando falhar.  
  
## <a name="see-also"></a>Consulte também  
 [Elemento Cancel &#40;XMLA&#41;](cancel-element-xmla.md)   
 [Elemento CommitTransaction &#40;XMLA&#41;](committransaction-element-xmla.md)   
 [Elemento RollbackTransaction &#40;XMLA&#41;](rollbacktransaction-element-xmla.md)   
 [Comandos &#40;XMLA&#41;](xml-elements-commands.md)  
  
  
