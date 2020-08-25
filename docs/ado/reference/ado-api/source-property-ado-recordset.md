---
description: Propriedade Source (Conjunto de registros ADO)
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
ms.openlocfilehash: 29ce12027267918822ed49185f06ab28a6448190
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88777395"
---
# <a name="source-property-ado-recordset"></a>Propriedade Source (Conjunto de registros ADO)
Indica a fonte de dados para um objeto [Recordset](./recordset-object-ado.md) .  
  
## <a name="settings-and-return-values"></a>Configurações e valores de retorno  
 Define um valor de **cadeia de caracteres** ou uma referência de objeto de [comando](./command-object-ado.md) ; retorna apenas um valor de **cadeia de caracteres** que indica a origem do **conjunto de registros**.  
  
## <a name="remarks"></a>Comentários  
 Use a propriedade **Source** para especificar uma fonte de dados para um objeto **Recordset** usando um dos seguintes: uma variável de objeto **Command** , uma instrução SQL, um procedimento armazenado ou um nome de tabela.  
  
 Se você definir a **Propriedade Source** como um objeto **Command** , a propriedade [ActiveConnection](./activeconnection-property-ado.md) do objeto **Recordset** herdará o valor da propriedade **ActiveConnection** para o objeto **Command** especificado. No entanto, a leitura da propriedade **Source** não retorna um objeto **Command** ; em vez disso, ele retorna a propriedade [CommandText](./commandtext-property-ado.md) do objeto **Command** para o qual você define a propriedade **Source** .  
  
 Se a propriedade **Source** for uma instrução SQL, um procedimento armazenado ou um nome de tabela, você poderá otimizar o desempenho passando o argumento *Options* apropriado com a chamada do método [Open](./open-method-ado-recordset.md) .  
  
 A propriedade **Source** é leitura/gravação para objetos **Recordset** fechados e somente leitura para objetos Open **Recordset** .  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto Recordset (ADO)](./recordset-object-ado.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo da propriedade Source (VB)](./source-property-example-vb.md)   
 [Propriedade Source (erro ADO)](./source-property-ado-error.md)   
 [Propriedade Source (Registro ADO)](./source-property-ado-record.md)