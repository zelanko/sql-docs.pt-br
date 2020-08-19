---
description: Tabela exclusiva, esquema exclusivo, propriedades de catálogo exclusivas – dinâmico (ADO)
title: Controlar alterações na tabela base do conjunto de registros (ADO) | Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 5c3f5bdb8a52f686ae336aa51986591788669979
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88441668"
---
# <a name="unique-table-unique-schema-unique-catalog-properties-dynamic-ado"></a>Tabela exclusiva, esquema exclusivo, propriedades de catálogo exclusivas – dinâmico (ADO)
Permite que você controle precisamente as modificações em uma tabela base específica em um [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md) que foi formado por uma operação de junção em várias tabelas base.  
  
-   **Tabela exclusiva** especifica o nome da tabela base na qual são permitidas atualizações, inserções e exclusões.  
  
-   **Esquema exclusivo** especifica o *esquema*ou o nome do proprietário da tabela.  
  
-   **Catálogo exclusivo** especifica o *Catálogo*ou o nome do banco de dados que contém a tabela.  
  
## <a name="settings-and-return-values"></a>Configurações e valores de retorno  
 Define ou retorna um valor de **cadeia de caracteres** que é o nome de uma tabela, um esquema ou um catálogo.  
  
## <a name="remarks"></a>Comentários  
 A tabela base desejada é identificada exclusivamente por seu catálogo, esquema e nomes de tabela. Quando a propriedade de **tabela exclusiva** é definida, os valores do **esquema exclusivo** ou propriedades de **catálogo exclusivo** são usados para localizar a tabela base. Ela é destinada, mas não é necessária, ou o **esquema exclusivo** e as propriedades de **catálogo exclusivo** devem ser definidos antes que a propriedade de **tabela exclusiva** seja definida.  
  
 A chave primária da **tabela exclusiva** é tratada como a chave primária do **conjunto de registros**inteiro. Essa é a chave usada para qualquer método que exija uma chave primária.  
  
 Enquanto a **tabela exclusiva** é definida, o método [delete](../../../ado/reference/ado-api/delete-method-ado-recordset.md) afeta apenas a tabela nomeada. Os métodos [AddNew](../../../ado/reference/ado-api/addnew-method-ado.md), [Ressync](../../../ado/reference/ado-api/resync-method.md), [Update](../../../ado/reference/ado-api/update-method.md)e [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md) afetam as tabelas base subjacentes apropriadas do **conjunto de registros**.  
  
 A **tabela exclusiva** deve ser especificada antes de fazer quaisquer ressincronizações personalizadas. Se a **tabela exclusiva** não tiver sido especificada, a propriedade de [comando Ressync](../../../ado/reference/ado-api/resync-command-property-dynamic-ado.md) não terá nenhum efeito.  
  
 Um erro de tempo de execução resultará se uma tabela base exclusiva não puder ser encontrada.  
  
 Essas propriedades dinâmicas são todas acrescentadas à coleção de [Propriedades](../../../ado/reference/ado-api/properties-collection-ado.md) do objeto **Recordset** quando a propriedade [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) é definida como **adUseClient**.  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
