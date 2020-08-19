---
description: Namespaces
title: Namespaces | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- namespaces in ADO
ms.assetid: efff5569-db52-451d-a039-2e74870534da
author: rothja
ms.author: jroth
ms.openlocfilehash: a4ab26dd8f767315a3392a2434689561fdb391d6
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88453138"
---
# <a name="namespaces"></a>Namespaces
O formato de persistência XML no ADO usa os quatro namespaces a seguir.  
  
## <a name="remarks"></a>Comentários  
 O formato de persistência XML no ADO usa os quatro namespaces a seguir.  
  
|Prefixo|Descrição|  
|------------|-----------------|  
|s|Refere-se ao namespace "XML-Data" que contém os elementos e atributos que definem o esquema do conjunto de registros atual.|  
|DT|Refere-se à especificação de definições de tipo de dados.|  
|rs|Refere-se ao namespace que contém elementos e atributos específicos para propriedades e atributos do conjunto de registros ADO.|  
|z|Refere-se ao esquema do conjunto de linhas atual.|  
  
 Um cliente não deve adicionar suas próprias marcas a esses namespaces, conforme definido pela especificação. Por exemplo, um cliente não deve definir um namespace como "urn: schemas-microsoft-com: Rowset" e, em seguida, escrever algo como "RS: MyOwnTag". Para saber mais sobre namespaces, consulte a [recomendação namespaces do W3C em XML](http://www.w3.org/TR/REC-xml-names/).  
  
> [!IMPORTANT]
>  A ID da marca do esquema deve ser "RowsetSchema" e o namespace usado para fazer referência ao esquema do conjunto de linhas atual deve apontar para "#RowsetSchema".  
  
 Observe que o prefixo do namespace – a parte entre os dois-pontos e o sinal de igualdade é arbitrário.  
  
```  
xmlns:rs="urn:schemas-microsoft-com:rowset"  
```  
  
 O usuário pode definir isso como qualquer nome, desde que esse nome seja usado consistentemente em todo o documento XML. O ADO sempre grava "s", "RS", "DT" e "z", mas esses nomes de prefixo não são embutidos em código no componente de carregamento.  
  
## <a name="see-also"></a>Consulte Também  
 [Persistência de registros em formato XML](../../../ado/guide/data/persisting-records-in-xml-format.md)
