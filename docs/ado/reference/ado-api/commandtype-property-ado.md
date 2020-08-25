---
description: Propriedade CommandType (ADO)
title: Propriedade CommandType (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Command15::CommandType
helpviewer_keywords:
- CommandType property [ADO]
ms.assetid: ca44809c-8647-48b6-a7fb-0be70a02f53e
author: rothja
ms.author: jroth
ms.openlocfilehash: 0216a04051ee45cf92d5451396c8012dbd47fe7b
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88776085"
---
# <a name="commandtype-property-ado"></a>Propriedade CommandType (ADO)
Indica o tipo de um objeto de [comando](./command-object-ado.md) .  
  
## <a name="settings-and-return-values"></a>Configurações e valores de retorno  
 Define ou retorna um ou mais valores de [CommandTypeEnum](./commandtypeenum.md) .  
  
> [!NOTE]
>  Não use os valores **CommandTypeEnum** de **adCmdFile** ou **adCmdTableDirect** com **CommandType**. Esses valores só podem ser usados como opções com os métodos [Open](./open-method-ado-recordset.md) e [Requery](./requery-method.md) de um [conjunto de registros](./recordset-object-ado.md).  
  
## <a name="remarks"></a>Comentários  
 Use a propriedade **CommandType** para otimizar a avaliação da propriedade [CommandText](./commandtext-property-ado.md) .  
  
 Se o valor da propriedade **CommandType** for definido como o valor padrão, **adCmdUnknown**, você poderá ter um desempenho reduzido porque o ADO deve fazer chamadas para o provedor para determinar se a propriedade **CommandText** é uma instrução SQL, um procedimento armazenado ou um nome de tabela. Se você souber o tipo de comando que está usando, definir a propriedade **CommandType** instruirá o ADO a ir diretamente para o código relevante. Se a propriedade **CommandType** não corresponder ao tipo de comando na propriedade **CommandText** , ocorrerá um erro quando você chamar o método [Execute](./execute-method-ado-command.md) .  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto Command (ADO)](./command-object-ado.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo das propriedades ActiveConnection, CommandText, CommandTimeout, CommandType, size e Direction (VB)](./activeconnection-commandtext-commandtimeout-commandtype-size-example-vb.md)   
 [Exemplo das propriedades ActiveConnection, CommandText, CommandTimeout, CommandType, size e Direction (VC + +)](./activeconnection-commandtext-commandtimeout-commandtype-size-example-vc.md)   
 [Exemplo das propriedades ActiveConnection, CommandText, CommandTimeout, CommandType, size e Direction (JScript)](./activeconnection-commandtext-timeout-type-size-example-jscript.md)