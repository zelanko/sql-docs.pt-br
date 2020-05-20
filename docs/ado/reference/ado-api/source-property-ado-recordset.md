---
title: Propriedade Source (conjunto de registros ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::putref_Source
- Recordset15::Source
- Recordset15::PutSource
- Recordset15::get_Source
- Recordset15::GetSource
- Recordset15::PutRefSource
- Recordset15::put_Source
helpviewer_keywords:
- Source property [ADO Recordset]
ms.assetid: a05ba2c9-2821-4343-8607-4de9b764ec91
author: rothja
ms.author: jroth
ms.openlocfilehash: fc7d3336b9c346a070266b4ef1d104d0e32eb042
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82759802"
---
# <a name="source-property-ado-recordset"></a>Propriedade Source (Conjunto de registros ADO)
Indica a fonte de dados para um objeto [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) .  
  
## <a name="settings-and-return-values"></a>Configurações e valores de retorno  
 Define um valor de **cadeia de caracteres** ou uma referência de objeto de [comando](../../../ado/reference/ado-api/command-object-ado.md) ; retorna apenas um valor de **cadeia de caracteres** que indica a origem do **conjunto de registros**.  
  
## <a name="remarks"></a>Comentários  
 Use a propriedade **Source** para especificar uma fonte de dados para um objeto **Recordset** usando um dos seguintes: uma variável de objeto **Command** , uma instrução SQL, um procedimento armazenado ou um nome de tabela.  
  
 Se você definir a **Propriedade Source** como um objeto **Command** , a propriedade [ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md) do objeto **Recordset** herdará o valor da propriedade **ActiveConnection** para o objeto **Command** especificado. No entanto, a leitura da propriedade **Source** não retorna um objeto **Command** ; em vez disso, ele retorna a propriedade [CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md) do objeto **Command** para o qual você define a propriedade **Source** .  
  
 Se a propriedade **Source** for uma instrução SQL, um procedimento armazenado ou um nome de tabela, você poderá otimizar o desempenho passando o argumento *Options* apropriado com a chamada do método [Open](../../../ado/reference/ado-api/open-method-ado-recordset.md) .  
  
 A propriedade **Source** é leitura/gravação para objetos **Recordset** fechados e somente leitura para objetos Open **Recordset** .  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo da propriedade Source (VB)](../../../ado/reference/ado-api/source-property-example-vb.md)   
 [Propriedade Source (erro ADO)](../../../ado/reference/ado-api/source-property-ado-error.md)   
 [Propriedade Source (Registro ADO)](../../../ado/reference/ado-api/source-property-ado-record.md)
