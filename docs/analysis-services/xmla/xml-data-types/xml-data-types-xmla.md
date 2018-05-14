---
title: Tipos de dados XML (XMLA) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 07bb4d7212d586ed533afc129ac9e1643a7c7dc1
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
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
  
  
