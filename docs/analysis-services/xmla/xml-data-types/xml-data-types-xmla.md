---
title: Tipos de dados XML (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- XML data types [XMLA]
- data types [XML for Analysis]
- XMLA, data types
- XML for Analysis, data types
ms.assetid: 979b5384-90d9-4e09-9286-1d1eafdc4864
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: f510e78d39ee1a61c17a9f79524a64befc0e127d
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="xml-data-types-xmla"></a>Tipos de dados XML (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  Além dos tipos primitivos e derivados padrão definidos pela recomendação XML 1.0, a especificação XML for Analysis (XMLA) 1.1 define tipos de dados adicionais para oferece suporte à representação de dados multidimensionais e tabulares.  
  
 O XMLA usa os tipos de dados listados na tabela a seguir.  
  
|Tipos de dados|Description|  
|----------------|-----------------|  
|Booliano|O tipo de dados **boolean** XML padrão.|  
|Decimal|O tipo de dados **decimal** XML padrão.|  
|[EmptyResult](../../../analysis-services/xmla/xml-data-types/emptyresult-data-type-xmla.md)|Um namespace no elemento **root** . Esse namespace é retornado quando um comando XMLA não retorna um resultado porque o comando XMLA não retorna um resultado ou porque ocorreu um erro no [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] instância ao executar o comando XMLA.|  
|[EnumString](../../../analysis-services/xmla/xml-data-types/enumstring-data-type-xmla.md)|Um conjunto de constantes de cadeia de caracteres nomeadas para um determinado enumerador.|  
|Integer|O tipo de dados **int** XML padrão.|  
|[MDDataSet](../../../analysis-services/xmla/xml-data-types/mddataset-data-type-xmla.md)|Dados multidimensionais retornados pelo *resultados* parâmetro o [Execute](../../../analysis-services/xmla/xml-elements-methods-execute.md) método.|  
|[Conjunto de resultados](../../../analysis-services/xmla/xml-data-types/resultset-data-type-xmla.md)|Um conjunto de resultados de XML autodescritivo retornado pelo método **Execute** .|  
|[Rowset](../../../analysis-services/xmla/xml-data-types/rowset-data-type-xmla.md)|Linhas de uma fonte de dados, estruturadas por um esquema XML inserido, retornado pelo [Discover](../../../analysis-services/xmla/xml-elements-methods-discover.md) método.|  
|Cadeia de caracteres|O tipo de dados **string** XML.|  
|UnsignedInt|O tipo de esquema **unsignedInt** XML.|  
  
 Para obter descrições completas dos tipos de dados de XML padrão, consulte a recomendação candidata do World Wide Web Consortium (WC3).  
  
## <a name="see-also"></a>Consulte também  
 [Elementos XML & #40; XMLA & #41;](http://msdn.microsoft.com/library/40ab2360-efb6-4ba6-bf23-e84964e51008)   
 [XML for Analysis & #40; XMLA & #41; Referência](../../../analysis-services/xmla/xml-for-analysis-xmla-reference.md)  
  
  
