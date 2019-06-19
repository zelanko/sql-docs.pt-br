---
title: Controle de alterações à tabela Base do conjunto de registros (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Unique Table property [ADO]
- Unique Schema property [ADO]
- Unique Catalog property [ADO]
ms.assetid: d0e775d8-e353-46a1-ad10-ed4cc240dfaa
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 9f653af8294002bf73b98bd4adc096fac8ba1658
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66710488"
---
# <a name="unique-table-unique-schema-unique-catalog-properties-dynamic-ado"></a>Tabela exclusiva, esquema exclusivo exclusiva catálogo propriedades dinâmica (ADO)
Permite que você de perto as modificações de controle para uma tabela base específica em um [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) que foi formada por uma operação de junção em várias tabelas base.  
  
-   **Tabela exclusiva** Especifica o nome da tabela base na qual as atualizações, inserções e exclusões são permitidas.  
  
-   **Esquema exclusivo** Especifica o *esquema*, ou o nome do proprietário da tabela.  
  
-   **Catálogo exclusivo** Especifica o *catálogo*, ou o nome do banco de dados que contém a tabela.  
  
## <a name="settings-and-return-values"></a>As configurações e valores de retorno  
 Define ou retorna um **cadeia de caracteres** valor que é o nome da tabela, esquema ou catálogo.  
  
## <a name="remarks"></a>Comentários  
 A tabela base desejada é identificada exclusivamente por seus nomes de tabela, esquema e catálogo. Quando o **tabela exclusiva** propriedade for definida, os valores da **esquema exclusivo** ou **catálogo exclusivo** propriedades são usadas para localizar a tabela base. É se destina, mas não obrigatório, que um ou ambos os **esquema exclusivo** e **catálogo exclusivo** propriedades ser definido antes do **tabela exclusiva** propriedade está definida.  
  
 A chave primária dos **tabela exclusiva** é tratado como a chave primária de toda a **conjunto de registros**. Esta é a chave que é usada para qualquer método que exigem uma chave primária.  
  
 Embora **tabela exclusiva** estiver definido, o [excluir](../../../ado/reference/ado-api/delete-method-ado-recordset.md) método afeta apenas a tabela nomeada. O [AddNew](../../../ado/reference/ado-api/addnew-method-ado.md), [ressincronizar](../../../ado/reference/ado-api/resync-method.md), [atualização](../../../ado/reference/ado-api/update-method.md), e [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md) métodos afetam quaisquer tabelas base subjacentes de apropriada da **Recordset**.  
  
 **Tabela exclusiva** deve ser especificado antes de fazer qualquer ressincronizações personalizadas. Se **tabela exclusiva** não foi especificado, o [comando ressincronizar](../../../ado/reference/ado-api/resync-command-property-dynamic-ado.md) propriedade não terá efeito.  
  
 Um erro de tempo de execução ocorre se uma tabela de base exclusiva não pode ser encontrada.  
  
 Essas propriedades dinâmicas são acrescentadas à **conjunto de registros** objeto [propriedades](../../../ado/reference/ado-api/properties-collection-ado.md) coleção quando o [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) propriedade é definida como  **adUseClient**.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Consulte também  
 [Objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
