---
title: Elemento Member (XMLA) | Microsoft Docs
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
api_name:
- Member Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#Member
- microsoft.xml.analysis.member
- http://schemas.microsoft.com/analysisservices/2003/engine#Member
helpviewer_keywords:
- Member element
ms.assetid: 5cc33a1f-192e-4821-a4ef-9a5f2bb7a9f0
caps.latest.revision: 11
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 318a54528ed5f9d22f0925ff10e0596413e47043
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37217926"
---
# <a name="member-element-xmla"></a>Elemento Member (XMLA)
  Representa um único membro em um elemento pai [Members](members-element-xmla.md) ou [Tuple](tuple-element-xmla.md) .  
  
## <a name="syntax"></a>Sintaxe  
  
```xml  
  
<Members>  
   ...  
   <Member>  
      <UName>...</UName>  
      <Caption>...</Caption>  
      <LName>...</LName>  
      <LNum>...</LNum>  
      <DisplayInfo>...</DisplayInfo>  
   </Member>  
   ...  
</Members>  
<!-- or -->  
<Tuple>  
   ...  
   <Member Hierarchy="string">  
      <UName>...</UName>  
      <Caption>...</Caption>  
      <LName>...</LName>  
      <LNum>...</LNum>  
      <DisplayInfo>...</DisplayInfo>  
   </Member>  
   ...  
</Tuple>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Nenhum|  
|Valor padrão|Nenhum|  
|Cardinalidade|0-n: Elemento opcional que pode ocorrer mais de uma vez.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elemento|  
|------------------|-------------|  
|Elementos pai|[Members](members-element-xmla.md), [Tuple](tuple-element-xmla.md)|  
|Elementos filho|[Caption](caption-element-xmla.md), [DisplayInfo](displayinfo-element-xmla.md), [LName](name-element-xmla.md), [LNum](lnum-element-xmla.md), [UName](uname-element-xmla.md)|  
  
## <a name="attributes"></a>Atributos  
  
|attribute|Description|  
|---------------|-----------------|  
|Hierarquia|Atributo `String` obrigatório (somente para elementos pai `Tuple`). O nome da hierarquia à qual o membro representado pelo elemento `Member` pertence.|  
  
## <a name="remarks"></a>Remarks  
 O elemento `Member` contém as informações necessárias para identificar e exibir um membro em uma determinada hierarquia. Para elementos pai `Members`, a hierarquia já é especificada pelo atributo `Hierarchy` do elemento pai. Para elementos pai `Tuple`, a hierarquia é especificada usando o atributo `Hierarchy` do elemento `Member`.  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades &#40;XMLA&#41;](xml-elements-properties.md)  
  
  
