---
title: Fonte de propriedade (conjunto de registros ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
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
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3ea11a8615db1802712b591b6fa38b54fc6e59e0
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/18/2018
---
# <a name="source-property-ado-recordset"></a>Propriedade Source (conjunto de registros ADO)
Indica a fonte de dados para um [registros](../../../ado/reference/ado-api/recordset-object-ado.md) objeto.  
  
## <a name="settings-and-return-values"></a>Configurações e valores de retorno  
 Define um **cadeia de caracteres** valor ou [comando](../../../ado/reference/ado-api/command-object-ado.md) objeto referência; retorna apenas um **cadeia de caracteres** valor que indica a fonte do **Recordset**.  
  
## <a name="remarks"></a>Remarks  
 Use o **fonte** propriedade para especificar uma fonte de dados para um **registros** objeto usando um dos seguintes: um **comando** objeto variável, uma instrução SQL, um procedimento armazenado, ou um nome de tabela.  
  
 Se você definir o **fonte** propriedade para um **comando** objeto, o [ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md) propriedade do **registros** objeto herdará o valor de **ActiveConnection** propriedade especificado **comando** objeto. No entanto, ler o **fonte** propriedade não retorna um **comando** objeto; em vez disso, ele retorna o [CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md) propriedade o **comando** do objeto que você definir o **fonte** propriedade.  
  
 Se o **fonte** é um nome de tabela, um procedimento armazenado ou uma instrução SQL, você pode otimizar o desempenho, passando apropriada *opções* argumento com o [abrir](../../../ado/reference/ado-api/open-method-ado-recordset.md)chamada de método.  
  
 O **fonte** propriedade é leitura/gravação para fechado **registros** objetos e somente leitura para abrir **registros** objetos.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo da propriedade Source (VB)](../../../ado/reference/ado-api/source-property-example-vb.md)   
 [Propriedade Source (erro de ADO)](../../../ado/reference/ado-api/source-property-ado-error.md)   
 [Propriedade Source (Registro ADO)](../../../ado/reference/ado-api/source-property-ado-record.md)
