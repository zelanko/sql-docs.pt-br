---
title: Conformidade XML for Analysis (XMLA) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- compliance [XML for Analysis]
- XML for Analysis, compliance
- XMLA, extended functionality
- XML for Analysis, extended functionality
- XMLA, compliance
- extending XML for Analysis
ms.assetid: d987d320-5581-4454-ad45-68e3a22175b6
caps.latest.revision: 15
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 5657f57d1f7eee76efb51da0c4bd3ff278aa47ac
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="xml-for-analysis-compliance-xmla"></a>Conformidade com XMLA (XML for Analysis)
  A especificação XML for Analysis 1.1 descreve um padrão aberto que aceita acesso a fontes de dados que residem na World Wide Web. Este tópico fornece detalhes sobre o nível de conformidade com a especificação XML for Analysis 1.1 que é suportada por [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
## <a name="compliant-items"></a>Itens de conformidade  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] está em conformidade com todos os itens obrigatórios listados na especificação XML for Analysis 1.1. Além disso, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] implementa o item opcional a seguir descrito na especificação XML for Analysis 1.1.  
  
|Item|Especificação|Implementação|  
|----------|-------------------|--------------------|  
|Suporte de sessão|Os elementos de cabeçalho SOAP estão listados na seção "Suporte para a capacidade de manutenção de status do processo em XML for Analysis" da especificação XML for Analysis 1.1.|Todos os elementos de cabeçalho SOAP listados têm suporte em [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], como descrito dentro da especificação.|  
  
## <a name="extensions"></a>Extensões  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] também estende a especificação XML for Analysis 1.1 para aceitar os recursos adicionais a seguir.  
  
|Item|Especificação|Implementação|  
|----------|-------------------|--------------------|  
|Negociação de protocolo|Nenhuma informações contida na especificação XML for Analysis 1.1 |Elemento de cabeçalho ProtocolCapabilities adicionado por [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para dar suporte a negociação de recursos de protocolo.|  
|Comandos do XMLA (XML for Analysis) aceitos pelo método Discover|Os comandos a seguir têm suporte na especificação XML for Analysis 1.1:<br /><br /> [Elemento de instrução &#40; XMLA &#41;](../../analysis-services/xmla/xml-elements-commands/statement-element-xmla.md)|Os comandos a seguir têm suporte em [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]:<br /><br /> [Alterar o elemento &#40; XMLA &#41;](../../analysis-services/xmla/xml-elements-commands/alter-element-xmla.md)<br /><br /> [Elemento de backup &#40; XMLA &#41;](../../analysis-services/xmla/xml-elements-commands/backup-element-xmla.md)<br /><br /> [Elemento batch &#40; XMLA &#41;](../../analysis-services/xmla/xml-elements-commands/batch-element-xmla.md)<br /><br /> [Elemento BeginTransaction &#40; XMLA &#41;](../../analysis-services/xmla/xml-elements-commands/begintransaction-element-xmla.md)<br /><br /> [Cancelar o elemento &#40; XMLA &#41;](../../analysis-services/xmla/xml-elements-commands/cancel-element-xmla.md)<br /><br /> [Elemento ClearCache &#40; XMLA &#41;](../../analysis-services/xmla/xml-elements-commands/clearcache-element-xmla.md)<br /><br /> [Elemento CommitTransaction &#40; XMLA &#41;](../../analysis-services/xmla/xml-elements-commands/committransaction-element-xmla.md)<br /><br /> [Criar elemento &#40; XMLA &#41;](../../analysis-services/xmla/xml-elements-commands/create-element-xmla.md)<br /><br /> [Excluir o elemento &#40; XMLA &#41;](../../analysis-services/xmla/xml-elements-commands/delete-element-xmla.md)<br /><br /> [Elemento DesignAggregations &#40; XMLA &#41;](../../analysis-services/xmla/xml-elements-commands/designaggregations-element-xmla.md)<br /><br /> [Remover elemento &#40; XMLA &#41;](../../analysis-services/xmla/xml-elements-commands/drop-element-xmla.md)<br /><br /> [Inserir o elemento &#40; XMLA &#41;](../../analysis-services/xmla/xml-elements-commands/insert-element-xmla.md)<br /><br /> [Elemento lock &#40; XMLA &#41;](../../analysis-services/xmla/xml-elements-commands/lock-element-xmla.md)<br /><br /> [Elemento MergePartitions &#40; XMLA &#41;](../../analysis-services/xmla/xml-elements-commands/mergepartitions-element-xmla.md)<br /><br /> [Elemento NotifyTableChange &#40; XMLA &#41;](../../analysis-services/xmla/xml-elements-commands/notifytablechange-element-xmla.md)<br /><br /> [Elemento Process &#40; XMLA &#41;](../../analysis-services/xmla/xml-elements-commands/process-element-xmla.md)<br /><br /> [Restaurar o elemento &#40; XMLA &#41;](../../analysis-services/xmla/xml-elements-commands/restore-element-xmla.md)<br /><br /> [Elemento RollbackTransaction &#40; XMLA &#41;](../../analysis-services/xmla/xml-elements-commands/rollbacktransaction-element-xmla.md)<br /><br /> [Elemento de instrução &#40; XMLA &#41;](../../analysis-services/xmla/xml-elements-commands/statement-element-xmla.md)<br /><br /> [Inscrever-se o elemento &#40; XMLA &#41;](../../analysis-services/xmla/xml-elements-commands/subscribe-element-xmla.md)<br /><br /> [Sincronizar o elemento &#40; XMLA &#41;](../../analysis-services/xmla/xml-elements-commands/synchronize-element-xmla.md)<br /><br /> [Desbloquear elemento &#40; XMLA &#41;](../../analysis-services/xmla/xml-elements-commands/unlock-element-xmla.md)<br /><br /> [Atualizar o elemento &#40; XMLA &#41;](../../analysis-services/xmla/xml-elements-commands/update-element-xmla.md)<br /><br /> [Elemento UpdateCells &#40; XMLA &#41;](../../analysis-services/xmla/xml-elements-commands/updatecells-element-xmla.md)|  
|Erros de coluna em conjuntos de linhas tabulares|Não listado na especificação XML for Analysis 1.1.|O [erro](../../analysis-services/xmla/xml-elements-properties/error-element-xmla.md) elemento é usado por [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para relatar erros para elementos de coluna contidos em um [linha](../../analysis-services/xmla/xml-elements-properties/error-element-xmla.md) elemento.|  
  
## <a name="see-also"></a>Consulte também  
 [Referência de XML for Analysis &#40;XMLA&#41;](../../analysis-services/xmla/xml-for-analysis-xmla-reference.md)  
  
  
