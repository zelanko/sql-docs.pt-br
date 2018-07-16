---
title: Tipos de dados XML (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
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
- XML data types [XMLA]
- data types [XML for Analysis]
- XMLA, data types
- XML for Analysis, data types
ms.assetid: 979b5384-90d9-4e09-9286-1d1eafdc4864
caps.latest.revision: 35
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9ccba3c69101362d1a384320808a30066ae572b3
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37297086"
---
# <a name="xml-data-types-xmla"></a>Tipos de dados XML (XMLA)
  Além dos tipos primitivos e derivados padrão definidos pela recomendação XML 1.0, a especificação XML for Analysis (XMLA) 1.1 define tipos de dados adicionais para oferece suporte à representação de dados multidimensionais e tabulares.  
  
 O XMLA usa os tipos de dados listados na tabela a seguir.  
  
|Tipos de dados|Description|  
|----------------|-----------------|  
|Booliano|O tipo de dados `boolean` XML padrão.|  
|Decimal|O tipo de dados `decimal` XML padrão.|  
|[EmptyResult](emptyresult-data-type-xmla.md)|Um namespace no elemento `root`. Esse namespace é retornado quando um comando XMLA não retorna um resultado porque o comando XMLA não retorna um resultado ou porque ocorreu um erro na [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] instância ao executar o comando XMLA.|  
|[EnumString](enumstring-data-type-xmla.md)|Um conjunto de constantes de cadeia de caracteres nomeadas para um determinado enumerador.|  
|Integer|O tipo de dados `int` XML padrão.|  
|[MDDataSet](mddataset-data-type-xmla.md)|Dados multidimensionais retornados pelo *resultado* parâmetro do [Execute](../xml-elements-methods-execute.md) método.|  
|[Conjunto de resultados](resultset-data-type-xmla.md)|Um conjunto de resultados de XML autodescritivo retornado pelo método `Execute`.|  
|[Rowset](rowset-data-type-xmla.md)|Linhas de uma fonte de dados, estruturadas por um esquema XML inserido, retornado pelo [Discover](../xml-elements-methods-discover.md) método.|  
|Cadeia de caracteres|O tipo de dados `string` XML.|  
|UnsignedInt|O tipo de esquema `unsignedInt` XML.|  
  
 Para obter descrições completas dos tipos de dados de XML padrão, consulte a recomendação candidata do World Wide Web Consortium (WC3).  
  
## <a name="see-also"></a>Consulte também  
 [Elementos XML &#40;XMLA&#41;](../../dev-guide/xml-elements-xmla.md)   
 [XML for Analysis &#40;XMLA&#41; referência](../xml-for-analysis-xmla-reference.md)  
  
  
