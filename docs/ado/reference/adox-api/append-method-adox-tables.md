---
description: Método Append (Tabelas do ADOX)
title: Método Append (tabelas ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Tables::Append
- Tables::raw_Append
helpviewer_keywords:
- Append method [ADOX]
ms.assetid: a362ed51-314c-4783-9598-538dbf755f3d
author: rothja
ms.author: jroth
ms.openlocfilehash: ffd2ef32cae3fafb7179568d1342606d32236657
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88985467"
---
# <a name="append-method-adox-tables"></a>Método Append (Tabelas do ADOX)
Adiciona um novo objeto [Table](./table-object-adox.md) à coleção [Tables](./tables-collection-adox.md) .  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Tables.Append Table  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *Table*  
 Um valor **Variant** que contém uma referência à **tabela** a ser acrescentada ou o nome da tabela a ser criada e acrescentada.  
  
## <a name="remarks"></a>Comentários  
 Ocorrerá um erro se o provedor não oferecer suporte à criação de tabelas.  
  
## <a name="applies-to"></a>Aplica-se A  
 [Coleção Tables (ADOX)](./tables-collection-adox.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo da propriedade Name e métodos de acréscimo de colunas e tabelas (VB)](./columns-and-tables-append-methods-name-property-example-vb.md)   
 [Exemplo da propriedade ParentCatalog (VB)](./parentcatalog-property-example-vb.md)   
 [Método Append (colunas ADOX)](./append-method-adox-columns.md)   
 [Método Append (grupos ADOX)](./append-method-adox-groups.md)   
 [Método Append (índices ADOX)](./append-method-adox-indexes.md)   
 [Método Append (chaves ADOX)](./append-method-adox-keys.md)   
 [Método Append (procedimentos do ADOX)](./append-method-adox-procedures.md)   
 [Método Append (usuários do ADOX)](./append-method-adox-users.md)   
 [Método Append (Exibições do ADOX)](./append-method-adox-views.md)