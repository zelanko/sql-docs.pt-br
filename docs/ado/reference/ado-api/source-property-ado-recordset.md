---
title: Propriedade (conjunto de registros ADO) de origem | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 59a043b6258de83986e447c87209fa781a1ae352
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66711121"
---
# <a name="source-property-ado-recordset"></a>Propriedade Source (Conjunto de registros ADO)
Indica que a fonte de dados para um [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objeto.  
  
## <a name="settings-and-return-values"></a>As configurações e valores de retorno  
 Conjuntos de uma **cadeia de caracteres** valor ou [comando](../../../ado/reference/ado-api/command-object-ado.md) referência; do objeto retorna apenas um **cadeia de caracteres** valor que indica a origem do **Recordset**.  
  
## <a name="remarks"></a>Comentários  
 Use o **fonte** propriedade para especificar uma fonte de dados para um **conjunto de registros** objeto usando um dos seguintes: um **comando** objeto variável, uma instrução SQL, um procedimento armazenado, ou um nome de tabela.  
  
 Se você definir a **fonte** propriedade para um **comando** objeto, o [ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md) propriedade do **Recordset** objeto herdará o valor de **ActiveConnection** propriedade especificado **comando** objeto. No entanto, lendo a **fonte** propriedade não retorna um **comando** objeto; em vez disso, ele retorna o [CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md) propriedade do **comando** do objeto que você defina a **origem** propriedade.  
  
 Se o **fonte** é uma instrução SQL, um procedimento armazenado ou um nome de tabela, você pode otimizar o desempenho, passando a apropriado *opções* argumento com o [abrir](../../../ado/reference/ado-api/open-method-ado-recordset.md)chamada de método.  
  
 O **fonte** propriedade é leitura/gravação para fechado **conjunto de registros** objetos e somente leitura para abrir **Recordset** objetos.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo da propriedade Source (VB)](../../../ado/reference/ado-api/source-property-example-vb.md)   
 [Propriedade Source (Erro ADO)](../../../ado/reference/ado-api/source-property-ado-error.md)   
 [Propriedade Source (Registro ADO)](../../../ado/reference/ado-api/source-property-ado-record.md)
