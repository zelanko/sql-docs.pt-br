---
title: Bloquear elemento (XMLA) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: xmla
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: Lock Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#Lock
- microsoft.xml.analysis.lock
- http://schemas.microsoft.com/analysisservices/2003/engine#Lock
helpviewer_keywords: Lock command
ms.assetid: a819e805-4793-43bb-8af3-16a19f8bdab3
caps.latest.revision: "14"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 8e3a174682bd6e2c84f48dbf75462fadecf2a573
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="lock-element-xmla"></a>Elemento Lock (XMLA)
  Bloqueia um objeto especificado em um [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] instância.  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Command>  
   <Lock>  
      <ID>...</ID>  
      <Object>...</Object>  
      <Mode>...</Mode>  
   </Lock>  
</Command>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Nenhuma|  
|Valor padrão|Nenhuma|  
|Cardinalidade|0-n: Elemento opcional que pode ocorrer mais de uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[Comando](../../../analysis-services/xmla/xml-elements-properties/command-element-xmla.md)|  
|Elementos filho|[ID](../../../analysis-services/xmla/xml-elements-properties/id-element-xmla.md), [modo](../../../analysis-services/xmla/xml-elements-properties/mode-element-xmla.md), [objeto](../../../analysis-services/xmla/xml-elements-properties/object-element-xmla.md)|  
  
## <a name="remarks"></a>Comentários  
 O **bloqueio** comando bloqueia um objeto, para uso compartilhado ou exclusivo dentro do contexto da transação ativa no momento. Apenas administradores de banco de dados ou servidor podem emitir explicitamente um **bloqueio** comando. Um bloqueio em um objeto impede a confirmação de transações até que o bloqueio seja removido. O [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] oferece suporte a dois tipos de bloqueios, bloqueios compartilhados e bloqueios exclusivos. Para obter mais informações sobre os tipos de bloqueio suportados pelo [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)], consulte [elemento Mode &#40; XMLA &#41; ](../../../analysis-services/xmla/xml-elements-properties/mode-element-xmla.md).  
  
 O [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] permite apenas o bloqueio de bancos de dados. O **objeto** elemento deve conter uma referência de objeto para um [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] banco de dados. Se o **objeto** elemento não for especificado ou se o **objeto** elemento se refere a um objeto diferente de um banco de dados, ocorrerá um erro.  
  
 Outros comandos implicitamente problema um **bloqueio** comando um [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] banco de dados. Qualquer operação que leia dados ou metadados de um banco de dados, como qualquer **Discover** método ou um **Execute** método executando um **instrução** command, emite implicitamente um compartilhado bloqueio no banco de dados. Qualquer transação que confirme alterações em dados ou metadados para um objeto em um [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] banco de dados, como um **Execute** método executando um **Alter** command, emite implicitamente um bloqueio exclusivo no banco de dados.  
  
 Todos os bloqueios são mantidos no contexto da transação atual. Quando a transação atual é confirmada ou revertida, todos os bloqueios definidos dentro da transação são liberados automaticamente.  
  
## <a name="see-also"></a>Consulte também  
 [Desbloquear elemento &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-commands/unlock-element-xmla.md)   
 [Comandos &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-commands/xml-elements-commands.md)  
  
  
