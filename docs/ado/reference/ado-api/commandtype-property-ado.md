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
manager: craigg
ms.openlocfilehash: 6612a90b94f10bdd08441d7814a7137121659045
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47658414"
---
# <a name="commandtype-property-ado"></a>Propriedade CommandType (ADO)
Indica o tipo de um [comando](../../../ado/reference/ado-api/command-object-ado.md) objeto.  
  
## <a name="settings-and-return-values"></a>As configurações e valores de retorno  
 Define ou retorna um ou mais [CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md) valores.  
  
> [!NOTE]
>  Não use o **CommandTypeEnum** valores de **adCmdFile** ou **adCmdTableDirect** com **CommandType**. Esses valores só podem ser usados como opções com o [aberto](../../../ado/reference/ado-api/open-method-ado-recordset.md) e [Requery](../../../ado/reference/ado-api/requery-method.md) métodos de um [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md).  
  
## <a name="remarks"></a>Comentários  
 Use o **CommandType** propriedade para otimizar a avaliação da [CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md) propriedade.  
  
 Se o **CommandType** o valor da propriedade é definido como o valor padrão, **adCmdUnknown**, você pode enfrentar desempenho diminuído porque ADO deve fazer chamadas para o provedor para determinar se o  **CommandText** propriedade é uma instrução SQL, um procedimento armazenado ou um nome de tabela. Se você souber que tipo de comando que você está usando, definindo o **CommandType** propriedade instrui o ADO para ir diretamente para o código relevante. Se o **CommandType** propriedade não coincide com o tipo de comando na **CommandText** propriedade, um erro ocorre quando você chama o [Execute](../../../ado/reference/ado-api/execute-method-ado-command.md) método.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Command (ADO)](../../../ado/reference/ado-api/command-object-ado.md)  
  
## <a name="see-also"></a>Consulte também  
 [ActiveConnection, CommandText, CommandTimeout, CommandType, tamanho e exemplo de propriedades de direção (VB)](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vb.md)   
 [ActiveConnection, CommandText, CommandTimeout, CommandType, tamanho e exemplo de propriedades de direção (VC + +)](../../../ado/reference/ado-api/activeconnection-commandtext-commandtimeout-commandtype-size-example-vc.md)   
 [ActiveConnection, CommandText, CommandTimeout, CommandType, tamanho e exemplo de propriedades de direção (JScript)](../../../ado/reference/ado-api/activeconnection-commandtext-timeout-type-size-example-jscript.md)
