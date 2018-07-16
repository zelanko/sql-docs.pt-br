---
title: Conformidade XML for Analysis (XMLA) | Microsoft Docs
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
helpviewer_keywords:
- compliance [XML for Analysis]
- XML for Analysis, compliance
- XMLA, extended functionality
- XML for Analysis, extended functionality
- XMLA, compliance
- extending XML for Analysis
ms.assetid: d987d320-5581-4454-ad45-68e3a22175b6
caps.latest.revision: 12
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: cc7a8da77b72f25a68764636fbe15bc2d9e4ae04
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37267082"
---
# <a name="xml-for-analysis-compliance-xmla"></a>Conformidade com XMLA (XML for Analysis)
  A especificação XML for Analysis 1.1 descreve um padrão aberto que aceita acesso a fontes de dados que residem na World Wide Web. Este tópico fornece detalhes sobre o nível de conformidade com a especificação XML for Analysis 1.1 que é compatível com [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
## <a name="compliant-items"></a>Itens de conformidade  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] está em conformidade com todos os itens obrigatórios listados na especificação XML for Analysis 1.1. Além disso, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] implementa o item opcional a seguir descrito na especificação XML for Analysis 1.1.  
  
|Item|Especificação|Implementação|  
|----------|-------------------|--------------------|  
|Suporte de sessão|Os elementos de cabeçalho SOAP estão listados na seção "Suporte para a capacidade de manutenção de status do processo em XML for Analysis" da especificação XML for Analysis 1.1.|Todos os elementos de cabeçalho SOAP listados têm suporte em [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], como descrito dentro da especificação.|  
  
## <a name="extensions"></a>Extensões  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] também estende a especificação XML for Analysis 1.1 para aceitar os recursos adicionais a seguir.  
  
|Item|Especificação|Implementação|  
|----------|-------------------|--------------------|  
|Negociação de protocolo|Nenhuma informações contida na especificação XML for Analysis 1.1 |[ProtocolCapabilities](xml-elements-headers/protocolcapabilities-element-xmla.md) elemento de cabeçalho adicionado pela [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para dar suporte à negociação de recursos de protocolo.|  
|Comandos do XMLA (XML for Analysis) aceitos pelo método Discover|Os comandos a seguir têm suporte na especificação XML for Analysis 1.1:<br /><br /> -   [Elemento Statement &#40;XMLA&#41;](xml-elements-commands/statement-element-xmla.md)|Os comandos a seguir têm suporte em [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]:<br /><br /> -   [Elemento ALTER &#40;XMLA&#41;](xml-elements-commands/alter-element-xmla.md)<br />-   [Elemento de backup &#40;XMLA&#41;](xml-elements-commands/backup-element-xmla.md)<br />-   [Elemento do lote &#40;XMLA&#41;](xml-elements-commands/batch-element-xmla.md)<br />-   [Elemento BeginTransaction &#40;XMLA&#41;](xml-elements-commands/begintransaction-element-xmla.md)<br />-   [Elemento Cancel &#40;XMLA&#41;](xml-elements-commands/cancel-element-xmla.md)<br />-   [Elemento ClearCache &#40;XMLA&#41;](xml-elements-commands/clearcache-element-xmla.md)<br />-   [Elemento CommitTransaction &#40;XMLA&#41;](xml-elements-commands/committransaction-element-xmla.md)<br />-   [Criar o elemento &#40;XMLA&#41;](xml-elements-commands/create-element-xmla.md)<br />-   [Excluir o elemento &#40;XMLA&#41;](xml-elements-commands/delete-element-xmla.md)<br />-   [Elemento DesignAggregations &#40;XMLA&#41;](xml-elements-commands/designaggregations-element-xmla.md)<br />-   [Elemento drop &#40;XMLA&#41;](xml-elements-commands/drop-element-xmla.md)<br />-   [Inserir o elemento &#40;XMLA&#41;](xml-elements-commands/insert-element-xmla.md)<br />-   [Bloquear elemento &#40;XMLA&#41;](xml-elements-commands/lock-element-xmla.md)<br />-   [Elemento MergePartitions &#40;XMLA&#41;](xml-elements-commands/mergepartitions-element-xmla.md)<br />-   [Elemento NotifyTableChange &#40;XMLA&#41;](xml-elements-commands/notifytablechange-element-xmla.md)<br />-   [Processar o elemento &#40;XMLA&#41;](xml-elements-commands/process-element-xmla.md)<br />-   [Restaurar o elemento &#40;XMLA&#41;](xml-elements-commands/restore-element-xmla.md)<br />-   [Elemento RollbackTransaction &#40;XMLA&#41;](xml-elements-commands/rollbacktransaction-element-xmla.md)<br />-Elemento SetPasswordEncryptionKey<br />-   [Elemento Statement &#40;XMLA&#41;](xml-elements-commands/statement-element-xmla.md)<br />-   [Inscrever-se o elemento &#40;XMLA&#41;](xml-elements-commands/subscribe-element-xmla.md)<br />-   [Elemento Synchronize &#40;XMLA&#41;](xml-elements-commands/synchronize-element-xmla.md)<br />-   [Desbloquear elemento &#40;XMLA&#41;](xml-elements-commands/unlock-element-xmla.md)<br />-   [Atualizar o elemento &#40;XMLA&#41;](xml-elements-commands/update-element-xmla.md)<br />-   [Elemento UpdateCells &#40;XMLA&#41;](xml-elements-commands/updatecells-element-xmla.md)|  
|Erros de coluna em conjuntos de linhas tabulares|Não listado na especificação XML for Analysis 1.1.|O [erro](xml-elements-properties/error-element-xmla.md) elemento é usado por [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para relatar erros para elementos de coluna contidos em um [linha](xml-elements-properties/error-element-xmla.md) elemento.|  
  
## <a name="see-also"></a>Consulte também  
 [XML for Analysis &#40;XMLA&#41; referência](xml-for-analysis-xmla-reference.md)  
  
  
