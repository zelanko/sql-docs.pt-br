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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67965588"
---
# <a name="parentcatalog-property-adox"></a>Propriedade ParentCatalog (ADOX)
Especifica o catálogo pai de uma tabela, um usuário ou um objeto de coluna para fornecer acesso às propriedades específicas do provedor.  
  
## <a name="settings-and-return-values"></a>Configurações e valores de retorno  
 Define e retorna um objeto de [Catálogo](../../../ado/reference/adox-api/catalog-object-adox.md) . A definição de **ParentCatalog** para um **Catálogo** aberto permite o acesso a propriedades específicas do provedor antes de acrescentar uma tabela ou coluna a uma coleção de **catálogos** .  
  
## <a name="remarks"></a>Comentários  
 Alguns provedores de dados permitem que os valores de propriedade específicos do provedor sejam gravados somente na criação: ou seja, quando uma tabela ou coluna é anexada à sua coleção de **Catálogo** . Para acessar essas propriedades antes de acrescentar esses objetos a um **Catálogo**, especifique primeiro o **Catálogo** na propriedade **ParentCatalog** .  
  
 Um erro ocorre quando a tabela ou coluna é anexada a um **Catálogo** diferente do **ParentCatalog**.  
  
## <a name="applies-to"></a>Aplica-se A  
  
|||  
|-|-|  
|[Objeto Column (ADOX)](../../../ado/reference/adox-api/column-object-adox.md)|[Objeto Table (ADOX)](../../../ado/reference/adox-api/table-object-adox.md)|  
|[Objeto User (ADOX)](../../../ado/reference/adox-api/user-object-adox.md)||  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo da propriedade ParentCatalog (VB)](../../../ado/reference/adox-api/parentcatalog-property-example-vb.md)
