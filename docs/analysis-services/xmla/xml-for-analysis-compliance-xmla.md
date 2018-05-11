---
title: Conformidade XML for Analysis (XMLA) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: ad9117eaaed992d692e5dd7686b6cc6463a2c8e5
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="xml-for-analysis-compliance-xmla"></a>Conformidade com XMLA (XML for Analysis)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
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
|Comandos do XMLA (XML for Analysis) aceitos pelo método Discover|Os comandos a seguir têm suporte na especificação XML for Analysis 1.1:<br /><br /> [Elemento de instrução &#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/statement-element-xmla.md)|Os comandos a seguir têm suporte em [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]:<br /><br /> [Elemento ALTER &#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/alter-element-xmla.md)<br /><br /> [Elemento de backup &#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/backup-element-xmla.md)<br /><br /> [Elemento de lote &#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/batch-element-xmla.md)<br /><br /> [Elemento BeginTransaction &#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/begintransaction-element-xmla.md)<br /><br /> [Elemento Cancel &#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/cancel-element-xmla.md)<br /><br /> [Elemento ClearCache &#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/clearcache-element-xmla.md)<br /><br /> [Elemento CommitTransaction &#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/committransaction-element-xmla.md)<br /><br /> [Criar elemento &#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/create-element-xmla.md)<br /><br /> [Elemento Delete &#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/delete-element-xmla.md)<br /><br /> [Elemento DesignAggregations &#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/designaggregations-element-xmla.md)<br /><br /> [Elemento drop &#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/drop-element-xmla.md)<br /><br /> [Elemento Insert &#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/insert-element-xmla.md)<br /><br /> [Bloquear elemento &#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/lock-element-xmla.md)<br /><br /> [Elemento MergePartitions &#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/mergepartitions-element-xmla.md)<br /><br /> [Elemento NotifyTableChange &#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/notifytablechange-element-xmla.md)<br /><br /> [Processar o elemento &#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/process-element-xmla.md)<br /><br /> [Elemento Restore &#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/restore-element-xmla.md)<br /><br /> [Elemento RollbackTransaction &#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/rollbacktransaction-element-xmla.md)<br /><br /> [Elemento de instrução &#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/statement-element-xmla.md)<br /><br /> [Elemento Subscribe &#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/subscribe-element-xmla.md)<br /><br /> [Sincronizar o elemento & #40; XMLA & #41;](../../analysis-services/xmla/xml-elements-commands/synchronize-element-xmla.md)<br /><br /> [Elemento Unlock &#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/unlock-element-xmla.md)<br /><br /> [Elemento Update &#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/update-element-xmla.md)<br /><br /> [Elemento UpdateCells &#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/updatecells-element-xmla.md)|  
|Erros de coluna em conjuntos de linhas tabulares|Não listado na especificação XML for Analysis 1.1.|O [erro](../../analysis-services/xmla/xml-elements-properties/error-element-xmla.md) elemento é usado por [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para relatar erros para elementos de coluna contidos em um [linha](../../analysis-services/xmla/xml-elements-properties/error-element-xmla.md) elemento.|  
  
## <a name="see-also"></a>Consulte também  
 [XML for Analysis & #40; XMLA & #41; Referência](../../analysis-services/xmla/xml-for-analysis-xmla-reference.md)  
  
  
