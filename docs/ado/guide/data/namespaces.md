---
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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 0e04ffd13183462b0d2a5e68ebc177b8b342b570
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66701857"
---
# <a name="namespaces"></a>Namespaces
O formato de persistência XML no ADO usa os seguintes namespaces de quatro.  
  
## <a name="remarks"></a>Comentários  
 O formato de persistência XML no ADO usa os seguintes namespaces de quatro.  
  
|Prefixo|Descrição|  
|------------|-----------------|  
|s|Refere-se ao namespace "XML-Data", que contém os elementos e atributos que definem o esquema do conjunto de registros atual.|  
|dt|Refere-se a especificação de definições de tipo de dados.|  
|rs|Refere-se aos elementos de recipiente de namespace e atributos específicos para as propriedades do conjunto de registros ADO e atributos.|  
|z|Refere-se ao esquema do conjunto de linhas atual.|  
  
 Um cliente não deve adicionar suas próprias marcas para esses namespaces, conforme definido pela especificação. Por exemplo, um cliente não deve definir um namespace como "urn: schemas-microsoft-com:rowset" e, em seguida, escrever algo como "rs: MyOwnTag." Para obter mais informações sobre namespaces, consulte a [Namespaces W3C na recomendação XML](http://www.w3.org/TR/REC-xml-names/).  
  
> [!IMPORTANT]
>  A ID para a marca de esquema deve ser "RowsetSchema", e o namespace usado para consultar o esquema do conjunto de linhas atual deve apontar para "#RowsetSchema".  
  
 Observe que o prefixo do namespace - a parte entre os dois-pontos e o sinal de igual - é arbitrário.  
  
```  
xmlns:rs="urn:schemas-microsoft-com:rowset"  
```  
  
 O usuário pode definir isso para ser qualquer nome desde que esse nome é usado de forma consistente em todo o documento XML. ADO sempre grava "s," "rs", "dt," e "z", mas esses nomes de prefixo não são embutidos em código no componente de carregamento.  
  
## <a name="see-also"></a>Consulte também  
 [Persistência de registros em formato XML](../../../ado/guide/data/persisting-records-in-xml-format.md)
