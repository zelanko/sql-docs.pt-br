---
title: Método Append (tabelas ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8c16ac4d18806b670c8b3e27dc09c9019d7ecdeb
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67967241"
---
# <a name="append-method-adox-tables"></a>Método Append (Tabelas do ADOX)
Adiciona um novo objeto [Table](../../../ado/reference/adox-api/table-object-adox.md) à coleção [Tables](../../../ado/reference/adox-api/tables-collection-adox.md) .  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Tables.Append Table  
```  
  
#### <a name="parameters"></a>parâmetros  
 *Table*  
 Um valor **Variant** que contém uma referência à **tabela** a ser acrescentada ou o nome da tabela a ser criada e acrescentada.  
  
## <a name="remarks"></a>Comentários  
 Ocorrerá um erro se o provedor não oferecer suporte à criação de tabelas.  
  
## <a name="applies-to"></a>Aplica-se A  
 [Coleção Tables (ADOX)](../../../ado/reference/adox-api/tables-collection-adox.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo da propriedade Name e métodos de acréscimo de colunas e tabelas (VB)](../../../ado/reference/adox-api/columns-and-tables-append-methods-name-property-example-vb.md)   
 [Exemplo da propriedade ParentCatalog (VB)](../../../ado/reference/adox-api/parentcatalog-property-example-vb.md)   
 [Método Append (colunas ADOX)](../../../ado/reference/adox-api/append-method-adox-columns.md)   
 [Método Append (grupos ADOX)](../../../ado/reference/adox-api/append-method-adox-groups.md)   
 [Método Append (índices ADOX)](../../../ado/reference/adox-api/append-method-adox-indexes.md)   
 [Método Append (chaves ADOX)](../../../ado/reference/adox-api/append-method-adox-keys.md)   
 [Método Append (procedimentos do ADOX)](../../../ado/reference/adox-api/append-method-adox-procedures.md)   
 [Método Append (usuários do ADOX)](../../../ado/reference/adox-api/append-method-adox-users.md)   
 [Método Append (Exibições do ADOX)](../../../ado/reference/adox-api/append-method-adox-views.md)
