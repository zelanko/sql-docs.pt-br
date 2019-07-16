---
title: Propriedade ParentCatalog (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _User::get_ParentCatalog
- _Column::ParentCatalog
- _Table::put_ParentCatalog
- _Group::put_ParentCatalog
- _Column::get_ParentCatalog
- _Table::PutParentCatalog
- _Group::putref_ParentCatalog
- _Group::ParentCatalog
- _Column::PutParentCatalog
- _Column::put_ParentCatalog
- _Group::get_ParentCatalog
- _User::put_ParentCatalog
- _User::putref_ParentCatalog
- _Table::get_ParentCatalog
- _Group::PutParentCatalog
- _Table::ParentCatalog
- _Column::GetParentCatalog
- _Table::PutRefParentCatalog
- _User::GetParentCatalog
- _Table::GetParentCatalog
- _Table::putref_ParentCatalog
- _User::PutParentCatalog
- _User::ParentCatalog
- _User::PutRefParentCatalog
- _Group::GetParentCatalog
- _Group::PutRefParentCatalog
helpviewer_keywords:
- ParentCatalog property [ADOX]
ms.assetid: a0bb2ed8-d4cb-4f92-8de7-769bbe0e6273
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8bc9527109aaa4a3a8063b26a594c9bdb978dcf3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67965588"
---
# <a name="parentcatalog-property-adox"></a>Propriedade ParentCatalog (ADOX)
Especifica o catálogo do pai de um objeto de tabela, o usuário ou a coluna para fornecer acesso a propriedades específicas do provedor.  
  
## <a name="settings-and-return-values"></a>As configurações e valores de retorno  
 Define e retorna um [catálogo](../../../ado/reference/adox-api/catalog-object-adox.md) objeto. Definindo **ParentCatalog** para um aberto **catálogo** permite o acesso a propriedades específicas do provedor antes do acréscimo de uma tabela ou coluna para uma **catálogo** coleção.  
  
## <a name="remarks"></a>Comentários  
 Alguns provedores de dados permitem que os valores de propriedade específica do provedor a ser gravado apenas na criação: ou seja, quando uma tabela ou coluna é anexada ao seu **catálogo** coleção. Para acessar essas propriedades antes de anexar a esses objetos para um **catálogo**, especifique a **catálogo** no **ParentCatalog** propriedade primeiro.  
  
 Um erro ocorre quando a tabela ou coluna for acrescentada ao outro **catálogo** que o **ParentCatalog**.  
  
## <a name="applies-to"></a>Aplica-se a  
  
|||  
|-|-|  
|[Objeto Column (ADOX)](../../../ado/reference/adox-api/column-object-adox.md)|[Objeto Table (ADOX)](../../../ado/reference/adox-api/table-object-adox.md)|  
|[Objeto User (ADOX)](../../../ado/reference/adox-api/user-object-adox.md)||  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo da propriedade ParentCatalog (VB)](../../../ado/reference/adox-api/parentcatalog-property-example-vb.md)
