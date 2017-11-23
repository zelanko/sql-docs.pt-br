---
title: "Objeto de parâmetro | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords: Parameter
helpviewer_keywords: Parameter object [ADO]
ms.assetid: e010e794-7f0f-4026-8b5b-37328e437d63
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7916c054b41b63b358f8330ff1a21b05689f2920
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="parameter-object"></a>Objeto Parameter
Representa um parâmetro ou um argumento associado com um [comando](../../../ado/reference/ado-api/command-object-ado.md) objeto com base em um procedimento armazenado ou uma consulta parametrizada.  
  
## <a name="remarks"></a>Comentários  
 Muitos provedores de suportam a comandos com parâmetros. Estes são os comandos no qual a ação desejada é definida uma vez, mas variáveis (ou parâmetros) são usados para alterar alguns detalhes do comando. Por exemplo, uma instrução SQL SELECT pode usar um parâmetro para definir os critérios de correspondência de uma cláusula WHERE e outra para definir o nome de coluna para uma cláusula classificar por.  
  
 **Parâmetro** representar parâmetros associados a consultas parametrizadas ou os argumentos de entrada/saída e valores de retorno dos procedimentos armazenados. Dependendo da funcionalidade do provedor, algumas coleções, métodos ou propriedades de um **parâmetro** objeto pode não estar disponível.  
  
 Com as coleções, métodos e propriedades de um **parâmetro** do objeto, você pode fazer o seguinte:  
  
-   Definir ou retornar o nome de um parâmetro com o [nome](../../../ado/reference/ado-api/name-property-ado.md) propriedade.  
  
-   Definir ou retornar o valor de um parâmetro com o [valor](../../../ado/reference/ado-api/value-property-ado.md) propriedade. **Valor** é a propriedade padrão do **parâmetro** objeto.  
  
-   Definir ou retornar as características de parâmetro com o [atributos](../../../ado/reference/ado-api/attributes-property-ado.md), [direção](../../../ado/reference/ado-api/direction-property.md), [precisão](../../../ado/reference/ado-api/precision-property-ado.md), [NumericScale](../../../ado/reference/ado-api/numericscale-property-ado.md), [ Tamanho](../../../ado/reference/ado-api/size-property-ado-parameter.md), e [tipo](../../../ado/reference/ado-api/type-property-ado.md) propriedades.  
  
-   Passar dados binários longos ou de caractere para um parâmetro com o [AppendChunk](../../../ado/reference/ado-api/appendchunk-method-ado.md) método.  
  
-   Acessar atributos específicos do provedor usando o [propriedades](../../../ado/reference/ado-api/properties-collection-ado.md) coleção.  
  
 Se você souber os nomes e propriedades dos parâmetros associados com o procedimento armazenado ou uma consulta com parâmetros que você deseja chamar, você pode usar o [CreateParameter](../../../ado/reference/ado-api/createparameter-method-ado.md) método para criar **parâmetro** objetos com as configurações de propriedade apropriado e use o [Append](../../../ado/reference/ado-api/append-method-ado.md) método para adicioná-los para o [parâmetros](../../../ado/reference/ado-api/parameters-collection-ado.md) coleção. Isso permite definir e retornar valores de parâmetro sem a necessidade de chamar o [atualizar](../../../ado/reference/ado-api/refresh-method-ado.md) método no **parâmetros** coleção para recuperar as informações de parâmetro de provedor, uma potencialmente operação de uso intensivo de recursos.  
  
 O **parâmetro** o objeto não é seguro para script.  
  
 Esta seção contém o tópico a seguir.  
  
-   [Eventos, métodos e propriedades do objeto de parâmetro](../../../ado/reference/ado-api/parameter-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte também  
 [Objeto de comando (ADO)](../../../ado/reference/ado-api/command-object-ado.md)   
 [Método CreateParameter (ADO)](../../../ado/reference/ado-api/createparameter-method-ado.md)   
 [Coleção de parâmetros (ADO)](../../../ado/reference/ado-api/parameters-collection-ado.md)   
 [Coleção Properties (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
