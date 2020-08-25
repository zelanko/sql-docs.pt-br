---
description: Objeto Parameter
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
author: rothja
ms.author: jroth
ms.openlocfilehash: eac5abf388644cff05c4a3a81955f025c65dd7aa
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88773405"
---
# <a name="parameter-object"></a>Objeto Parameter
Representa um parâmetro ou argumento associado a um objeto de [comando](./command-object-ado.md) com base em uma consulta parametrizada ou em um procedimento armazenado.  
  
## <a name="remarks"></a>Comentários  
 Muitos provedores oferecem suporte a comandos com parâmetros. Esses são comandos nos quais a ação desejada é definida uma vez, mas variáveis (ou parâmetros) são usadas para alterar alguns detalhes do comando. Por exemplo, uma instrução SQL SELECT poderia usar um parâmetro para definir os critérios de correspondência de uma cláusula WHERE e outra para definir o nome da coluna para uma cláusula SORT BY.  
  
 Os objetos de **parâmetro** representam parâmetros associados a consultas parametrizadas ou os argumentos in/out e os valores de retorno de procedimentos armazenados. Dependendo da funcionalidade do provedor, algumas coleções, métodos ou propriedades de um objeto de **parâmetro** podem não estar disponíveis.  
  
 Com as coleções, métodos e propriedades de um objeto de **parâmetro** , você pode fazer o seguinte:  
  
-   Defina ou retorne o nome de um parâmetro com a propriedade [Name](./name-property-ado.md) .  
  
-   Defina ou retorne o valor de um parâmetro com a propriedade [Value](./value-property-ado.md) . **Value** é a propriedade padrão do objeto **Parameter** .  
  
-   Defina ou retorne características de parâmetro com os [atributos](./attributes-property-ado.md), [direção](./direction-property.md), [precisão](./precision-property-ado.md), [NumericScale](./numericscale-property-ado.md), [tamanho](./size-property-ado-parameter.md)e propriedades de [tipo](./type-property-ado.md) .  
  
-   Passe dados binários longos ou de caractere para um parâmetro com o método [AppendChunk](./appendchunk-method-ado.md) .  
  
-   Acesse atributos específicos do provedor usando a coleção de [Propriedades](./properties-collection-ado.md) .  
  
 Se você souber os nomes e as propriedades dos parâmetros associados ao procedimento armazenado ou à consulta parametrizada que deseja chamar, poderá usar o método [CreateParameter](./createparameter-method-ado.md) para criar objetos de **parâmetro** com as configurações de propriedade apropriadas e usar o método [Append](./append-method-ado.md) para adicioná-los à coleção de [parâmetros](./parameters-collection-ado.md) . Isso permite que você defina e retorne valores de parâmetro sem precisar chamar o método de [atualização](./refresh-method-ado.md) na coleção de **parâmetros** para recuperar as informações de parâmetro do provedor, uma operação potencialmente intensiva de recursos.  
  
 O objeto de **parâmetro** não é seguro para scripts.  
  
 Esta seção contém o tópico a seguir.  
  
-   [Propriedades, métodos e eventos do objeto Parameter](./parameter-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Objeto Command (ADO)](./command-object-ado.md)   
 [Método CreateParameter (ADO)](./createparameter-method-ado.md)   
 [Coleção Parameters (ADO)](./parameters-collection-ado.md)   
 [Coleção Properties (ADO)](./properties-collection-ado.md)