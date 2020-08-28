---
description: Tabela exclusiva, esquema exclusivo, propriedades de catálogo exclusivas – dinâmico (ADO)
title: Controlar alterações na tabela base do conjunto de registros (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
ms.openlocfilehash: 50a17938a2e1cffd3cc0bf76d3cc3758358318d2
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88988157"
---
# <a name="unique-table-unique-schema-unique-catalog-properties-dynamic-ado"></a>Tabela exclusiva, esquema exclusivo, propriedades de catálogo exclusivas – dinâmico (ADO)
Permite que você controle precisamente as modificações em uma tabela base específica em um [conjunto de registros](./recordset-object-ado.md) que foi formado por uma operação de junção em várias tabelas base.  
  
-   **Tabela exclusiva** especifica o nome da tabela base na qual são permitidas atualizações, inserções e exclusões.  
  
-   **Esquema exclusivo** especifica o *esquema*ou o nome do proprietário da tabela.  
  
-   **Catálogo exclusivo** especifica o *Catálogo*ou o nome do banco de dados que contém a tabela.  
  
## <a name="settings-and-return-values"></a>Configurações e valores de retorno  
 Define ou retorna um valor de **cadeia de caracteres** que é o nome de uma tabela, um esquema ou um catálogo.  
  
## <a name="remarks"></a>Comentários  
 A tabela base desejada é identificada exclusivamente por seu catálogo, esquema e nomes de tabela. Quando a propriedade de **tabela exclusiva** é definida, os valores do **esquema exclusivo** ou propriedades de **catálogo exclusivo** são usados para localizar a tabela base. Ela é destinada, mas não é necessária, ou o **esquema exclusivo** e as propriedades de **catálogo exclusivo** devem ser definidos antes que a propriedade de **tabela exclusiva** seja definida.  
  
 A chave primária da **tabela exclusiva** é tratada como a chave primária do **conjunto de registros**inteiro. Essa é a chave usada para qualquer método que exija uma chave primária.  
  
 Enquanto a **tabela exclusiva** é definida, o método [delete](./delete-method-ado-recordset.md) afeta apenas a tabela nomeada. Os métodos [AddNew](./addnew-method-ado.md), [Ressync](./resync-method.md), [Update](./update-method.md)e [UpdateBatch](./updatebatch-method.md) afetam as tabelas base subjacentes apropriadas do **conjunto de registros**.  
  
 A **tabela exclusiva** deve ser especificada antes de fazer quaisquer ressincronizações personalizadas. Se a **tabela exclusiva** não tiver sido especificada, a propriedade de [comando Ressync](./resync-command-property-dynamic-ado.md) não terá nenhum efeito.  
  
 Um erro de tempo de execução resultará se uma tabela base exclusiva não puder ser encontrada.  
  
 Essas propriedades dinâmicas são todas acrescentadas à coleção de [Propriedades](./properties-collection-ado.md) do objeto **Recordset** quando a propriedade [CursorLocation](./cursorlocation-property-ado.md) é definida como **adUseClient**.  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto Recordset (ADO)](./recordset-object-ado.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Objeto Recordset (ADO)](./recordset-object-ado.md)