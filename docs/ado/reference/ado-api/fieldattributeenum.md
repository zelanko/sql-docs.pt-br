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
author: rothja
ms.author: jroth
ms.openlocfilehash: ca14531410942a77add7c6c99756b64bf99e785c
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82764517"
---
# <a name="fieldattributeenum"></a>FieldAttributeEnum
Especifica um ou mais atributos de um objeto de [campo](../../../ado/reference/ado-api/field-object.md) .  
  
|Constante|Valor|Descrição|  
|--------------|-----------|-----------------|  
|**adFldCacheDeferred**|0x1000|Indica que o provedor armazena em cache os valores de campo e que as leituras subsequentes são feitas a partir do cache.|  
|**adFldFixed**|0x10|Indica que o campo contém dados de comprimento fixo.|  
|**adFldIsChapter**|0x2000|Indica que o campo contém um valor de capítulo, que especifica um conjunto de registros filho específico relacionado a esse campo pai. Normalmente, os campos de capítulo são usados com formatação ou filtros de dados.|  
|**adFldIsCollection**|0x40000|Indica que o campo especifica que o recurso representado pelo registro é uma coleção de outros recursos, como uma pasta, em vez de um recurso simples, como um arquivo de texto.|  
|**adFldKeyColumn**|0x8000|Indica que o campo especifica toda ou parte da chave primária da coluna.|  
|**adFldIsDefaultStream**|0x20000|Indica que o campo contém o fluxo padrão para o recurso representado pelo registro. Por exemplo, o fluxo padrão pode ser o conteúdo HTML de uma pasta raiz em um site da Web, que é automaticamente servido quando a URL raiz é especificada.|  
|**adFldIsNullable**|0x20|Indica que o campo aceita valores nulos.|  
|**adFldIsRowURL**|0x10000|Indica que o campo contém a URL que nomeia o recurso do armazenamento de dados representado pelo registro.|  
|**adFldLong**|0x80|Indica que o campo é um campo binário longo. Também indica que você pode usar os métodos [AppendChunk](../../../ado/reference/ado-api/appendchunk-method-ado.md) e [GetChunk](../../../ado/reference/ado-api/getchunk-method-ado.md) .|  
|**adFldMayBeNull**|0x40|Indica que você pode ler valores nulos do campo.|  
|**adFldMayDefer**|0x2|Indica que o campo é adiado, ou seja, os valores de campo não são recuperados da fonte de dados com o registro inteiro, mas somente quando você os acessa explicitamente.|  
|**adFldNegativeScale**|0x4000|Indica que o campo representa um valor numérico de uma coluna que dá suporte a valores de escala negativos. A escala é especificada pela propriedade [NumericScale](../../../ado/reference/ado-api/numericscale-property-ado.md) .|  
|**adFldRowID**|0x100|Indica que o campo contém um identificador de linha persistente que não pode ser gravado e não tem nenhum valor significativo, exceto para identificar a linha (como um número de registro, identificador exclusivo e assim por diante).|  
|**adFldRowVersion**|0x200|Indica que o campo contém algum tipo de carimbo de data/hora usado para controlar atualizações.|  
|**adFldUnknownUpdatable**|0x8|Indica que o provedor não pode determinar se você pode gravar no campo.|  
|**adFldUnspecified**|-1 0xFFFFFFFF|Indica que o provedor não especifica os atributos do campo.|  
|**adFldUpdatable**|0x4|Indica que você pode gravar no campo.|  
  
## <a name="adowfc-equivalent"></a>Equivalente do ADO/WFC  
 Pacote: **com. ms. wfc. Data**  
  
|Constante|  
|--------------|  
|AdoEnums. Fieldattribute. CACHEDEFERRED|  
|AdoEnums. Fieldattribute. FIXED|  
|AdoEnums. Fieldattribute. IsNullable|  
|AdoEnums. Fieldattribute. LONG|  
|AdoEnums. Fieldattribute. MAYBENULL|  
|AdoEnums. Fieldattribute. MAYDEFER|  
|AdoEnums. Fieldattribute. NEGATIVESCALE|  
|AdoEnums. Fieldattribute. ROWID|  
|AdoEnums. Fieldattribute. CreateVersion|  
|AdoEnums. Fieldattribute. UNKNOWNUPDATABLE|  
|AdoEnums. Fieldattribute. não especificado|  
|AdoEnums. Fieldattribute. Updatable|  
  
## <a name="applies-to"></a>Aplica-se A  
  
|||  
|-|-|  
|[Método Append (ADO)](../../../ado/reference/ado-api/append-method-ado.md)|[Propriedade Attributes (ADO)](../../../ado/reference/ado-api/attributes-property-ado.md)|
