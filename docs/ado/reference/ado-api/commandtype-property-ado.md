---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0cd6d06a50047f431700af9418a504faa4bd6957
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67919691"
---
# <a name="commandtype-property-ado"></a>Propriedade CommandType (ADO)
Indica o tipo de um objeto de [comando](../../../ado/reference/ado-api/command-object-ado.md) .  
  
## <a name="settings-and-return-values"></a>Configurações e valores de retorno  
 Define ou retorna um ou mais valores de [CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md) .  
  
> [!NOTE]
>  Não use os valores **CommandTypeEnum** de **adCmdFile** ou **adCmdTableDirect** com **CommandType**. Esses valores só podem ser usados como opções com os métodos [Open](../../../ado/reference/ado-api/open-method-ado-recordset.md) e [Requery](../../../ado/reference/ado-api/requery-method.md) de um [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md).  
  
## <a name="remarks"></a>Comentários  
 Use a propriedade **CommandType** para otimizar a avaliação da propriedade [CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md) .  
  
 Se o valor da propriedade **CommandType** for definido como o valor padrão, **adCmdUnknown**, você poderá ter um desempenho reduzido porque o ADO deve fazer chamadas para o provedor para determinar se a propriedade **CommandText** é uma instrução SQL, um procedimento armazenado ou um nome de tabela. Se você souber o tipo de comando que está usando, definir a propriedade **CommandType** instruirá o ADO a ir diretamente para o código relevante. Se a propriedade **CommandType** não corresponder ao tipo de comando na propriedade **CommandText** , ocorrerá um erro quando você chamar o método [Execute](../../../ado/reference/ado-api/execute-method-ado-command.md) .  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto Command (ADO)](../../../ado/reference/ado-api/command-object-ado.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo das propriedades ActiveConnection, CommandText, CommandTimeout, CommandType, size e Direction (VB)](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vb.md)   
 [Exemplo das propriedades ActiveConnection, CommandText, CommandTimeout, CommandType, size e Direction (VC + +)](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vc.md)   
 [Exemplo das propriedades ActiveConnection, CommandText, CommandTimeout, CommandType, size e Direction (JScript)](../../../ado/reference/ado-api/activeconnection-commandtext-timeout-type-size-example-jscript.md)
