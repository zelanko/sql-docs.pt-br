---
title: FieldAttributeEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- FieldAttributeEnum
helpviewer_keywords:
- FieldAttributeEnum enumeration [ADO]
ms.assetid: 6e34d886-005a-40dc-bd5c-6adcbf81e5cd
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: db3b72b7bdaf60febdeb41eb6f6e1e86c5064f63
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52507165"
---
# <a name="fieldattributeenum"></a>FieldAttributeEnum
Especifica um ou mais atributos de uma [campo](../../../ado/reference/ado-api/field-object.md) objeto.  
  
|Constante|Valor|Descrição|  
|--------------|-----------|-----------------|  
|**adFldCacheDeferred**|0x1000|Indica que o provedor armazena em cache valores de campo e que as leituras subsequentes são feitas do cache.|  
|**adFldFixed**|0x10|Indica que o campo contém dados de comprimento fixo.|  
|**adFldIsChapter**|0x2000|Indica que o campo contém um valor de capítulo, que especifica um conjunto de registros filho específicos relacionado a esse campo pai. Normalmente os campos de capítulo são usados com a formatação de dados ou filtros.|  
|**adFldIsCollection**|0x40000|Indica que o campo especifica que o recurso representado pelo registro é uma coleção de outros recursos, como uma pasta, em vez de um recurso simple, como um arquivo de texto.|  
|**adFldKeyColumn**|0x8000|Indica que o campo especifica todo ou parte de chave primária da coluna.|  
|**adFldIsDefaultStream**|0x20000|Indica que o campo contém o fluxo padrão para o recurso representado pelo registro. Por exemplo, o fluxo padrão pode ser o conteúdo HTML de uma pasta raiz em um site da Web, que é fornecido automaticamente quando a URL raiz é especificada.|  
|**adFldIsNullable**|0x20|Indica que o campo aceita valores nulos.|  
|**adFldIsRowURL**|0x10000|Indica que o campo contém a URL que nomeia o recurso do armazenamento de dados representado pelo registro.|  
|**adFldLong**|0x80|Indica que o campo é um campo binário longo. Também indica que você pode usar o [AppendChunk](../../../ado/reference/ado-api/appendchunk-method-ado.md) e [GetChunk](../../../ado/reference/ado-api/getchunk-method-ado.md) métodos.|  
|**adFldMayBeNull**|0x40|Indica que você pode ler valores nulos do campo.|  
|**adFldMayDefer**|0x2|Indica que o campo é adiada que é, os valores de campo não são recuperados da fonte de dados com o registro inteiro, mas somente quando você acessá-los explicitamente.|  
|**adFldNegativeScale**|0x4000|Indica que o campo representa um valor numérico de uma coluna que dá suporte a valores de escala negativos. A escala for especificada o [NumericScale](../../../ado/reference/ado-api/numericscale-property-ado.md) propriedade.|  
|**adFldRowID**|0x100|Indica que o campo contém um identificador de linha persistente que não pode ser gravado e não tem nenhum valor significativo, exceto para identificar a linha (por exemplo, um número de registros, identificador exclusivo e assim por diante).|  
|**adFldRowVersion**|0x200|Indica que o campo contém algum tipo de carimbo de data ou hora usado para acompanhar as atualizações.|  
|**adFldUnknownUpdatable**|0x8|Indica que o provedor não pode determinar se você pode escrever para o campo.|  
|**adFldUnspecified**|-1 0xFFFFFFFF|Indica que o provedor não especifica os atributos de campo.|  
|**adFldUpdatable**|0x4|Indica que você pode escrever para o campo.|  
  
## <a name="adowfc-equivalent"></a>Equivalente do ADO/WFC  
 Pacote: **com.ms.wfc.data**  
  
|Constante|  
|--------------|  
|AdoEnums.FieldAttribute.CACHEDEFERRED|  
|AdoEnums.FieldAttribute.FIXED|  
|AdoEnums.FieldAttribute.ISNULLABLE|  
|AdoEnums.FieldAttribute.LONG|  
|AdoEnums.FieldAttribute.MAYBENULL|  
|AdoEnums.FieldAttribute.MAYDEFER|  
|AdoEnums.FieldAttribute.NEGATIVESCALE|  
|AdoEnums.FieldAttribute.ROWID|  
|AdoEnums.FieldAttribute.ROWVERSION|  
|AdoEnums.FieldAttribute.UNKNOWNUPDATABLE|  
|AdoEnums.FieldAttribute.UNSPECIFIED|  
|AdoEnums.FieldAttribute.UPDATABLE|  
  
## <a name="applies-to"></a>Aplica-se a  
  
|||  
|-|-|  
|[Método Append (ADO)](../../../ado/reference/ado-api/append-method-ado.md)|[Propriedade Attributes (ADO)](../../../ado/reference/ado-api/attributes-property-ado.md)|
