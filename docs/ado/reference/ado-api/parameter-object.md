---
title: Objeto de parâmetro | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Parameter
helpviewer_keywords:
- Parameter object [ADO]
ms.assetid: e010e794-7f0f-4026-8b5b-37328e437d63
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e4a39f93e6b98595270e46d5a6f9b54b35098cb1
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62710348"
---
# <a name="parameter-object"></a>Objeto Parameter
Representa um parâmetro ou um argumento associado a um [comando](../../../ado/reference/ado-api/command-object-ado.md) objeto com base em uma consulta parametrizada ou procedimento armazenado.  
  
## <a name="remarks"></a>Comentários  
 Muitos provedores dão suporte a comandos parametrizados. Estes são os comandos no qual a ação desejada é definida uma vez, mas as variáveis (ou parâmetros) são usados para alterar alguns detalhes do comando. Por exemplo, uma instrução SQL SELECT poderia usar um parâmetro para definir os critérios de correspondência de uma cláusula WHERE e outra para definir o nome de coluna para uma cláusula classificar por.  
  
 **Parâmetro** objetos representam parâmetros associados às consultas com parâmetros, ou os argumentos de entrada/saída e valores de retorno de procedimentos armazenados. Dependendo da funcionalidade do provedor, algumas coleções, métodos ou propriedades de um **parâmetro** objeto pode não estar disponível.  
  
 Com as coleções, métodos e propriedades de um **parâmetro** do objeto, você pode fazer o seguinte:  
  
-   Definir ou retornar o nome de um parâmetro com o [nome](../../../ado/reference/ado-api/name-property-ado.md) propriedade.  
  
-   Definir ou retornar o valor de um parâmetro com o [valor](../../../ado/reference/ado-api/value-property-ado.md) propriedade. **Valor** é a propriedade padrão de **parâmetro** objeto.  
  
-   Definir ou retornar as características de parâmetro com o [atributos](../../../ado/reference/ado-api/attributes-property-ado.md), [direção](../../../ado/reference/ado-api/direction-property.md), [precisão](../../../ado/reference/ado-api/precision-property-ado.md), [NumericScale](../../../ado/reference/ado-api/numericscale-property-ado.md), [ Tamanho](../../../ado/reference/ado-api/size-property-ado-parameter.md), e [tipo](../../../ado/reference/ado-api/type-property-ado.md) propriedades.  
  
-   Passar dados binários longos ou de caractere para um parâmetro com o [AppendChunk](../../../ado/reference/ado-api/appendchunk-method-ado.md) método.  
  
-   Acessar atributos específicos do provedor usando o [propriedades](../../../ado/reference/ado-api/properties-collection-ado.md) coleção.  
  
 Se você souber os nomes e as propriedades dos parâmetros associados com o procedimento armazenado ou uma consulta parametrizada que você deseja chamar, você pode usar o [CreateParameter](../../../ado/reference/ado-api/createparameter-method-ado.md) método criem **parâmetro** objetos com as configurações de propriedade apropriada e o uso de [Append](../../../ado/reference/ado-api/append-method-ado.md) método para adicioná-los para o [parâmetros](../../../ado/reference/ado-api/parameters-collection-ado.md) coleção. Isso lhe permite definir e retornar valores de parâmetro sem precisar telefonar para o [Refresh](../../../ado/reference/ado-api/refresh-method-ado.md) método na **parâmetros** coleção para recuperar as informações de parâmetro do provedor de um potencialmente operação de uso intensivo de recursos.  
  
 O **parâmetro** objeto não é seguro para script.  
  
 Esta seção contém o tópico a seguir.  
  
-   [Eventos, métodos e propriedades do objeto de parâmetro](../../../ado/reference/ado-api/parameter-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte também  
 [Objeto de comando (ADO)](../../../ado/reference/ado-api/command-object-ado.md)   
 [Método CreateParameter (ADO)](../../../ado/reference/ado-api/createparameter-method-ado.md)   
 [Coleção Parameters (ADO)](../../../ado/reference/ado-api/parameters-collection-ado.md)   
 [Coleção Properties (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
