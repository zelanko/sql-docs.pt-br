---
title: Propriedade ParentCatalog (ADOX) | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
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
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c255beddbc240f30f51642a0e8fe4fd785cf88bb
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/09/2018
---
# <a name="parentcatalog-property-adox"></a>Propriedade ParentCatalog (ADOX)
Especifica o catálogo do pai de um objeto de tabela, o usuário ou a coluna para fornecer acesso a propriedades específicas do provedor.  
  
## <a name="settings-and-return-values"></a>Configurações e valores de retorno  
 Define e retorna um [catálogo](../../../ado/reference/adox-api/catalog-object-adox.md) objeto. Configuração **ParentCatalog** para um abrir **catálogo** permite o acesso a propriedades específicas do provedor antes de anexar a uma tabela ou coluna para um **catálogo** coleção.  
  
## <a name="remarks"></a>Remarks  
 Alguns provedores de dados permitem que os valores de propriedade específica de provedor a ser gravada somente no momento da criação: ou seja, quando uma tabela ou coluna é acrescentada ao seu **catálogo** coleção. Para acessar essas propriedades antes de anexar esses objetos para um **catálogo**, especifique o **catálogo** no **ParentCatalog** propriedade primeiro.  
  
 Um erro ocorre quando a tabela ou coluna é anexada a outro **catálogo** que o **ParentCatalog**.  
  
## <a name="applies-to"></a>Aplica-se a  
  
|||  
|-|-|  
|[Objeto Column (ADOX)](../../../ado/reference/adox-api/column-object-adox.md)|[Objeto Table (ADOX)](../../../ado/reference/adox-api/table-object-adox.md)|  
|[Objeto User (ADOX)](../../../ado/reference/adox-api/user-object-adox.md)||  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo da propriedade ParentCatalog (VB)](../../../ado/reference/adox-api/parentcatalog-property-example-vb.md)
