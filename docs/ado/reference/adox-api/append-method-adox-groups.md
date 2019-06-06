---
title: (Grupos do ADOX) do método append | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Groups::raw_Append
- Groups::Append
helpviewer_keywords:
- Append method [ADOX]
ms.assetid: 56b94fc6-7ef0-4e4a-82a3-033b94c46036
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: b6b9740b58ef53fd4fcc2becda50f73609a1bf5c
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66708358"
---
# <a name="append-method-adox-groups"></a>Método Append (Grupos do ADOX)
Adiciona um novo [grupo](../../../ado/reference/adox-api/group-object-adox.md) do objeto para o [grupos](../../../ado/reference/adox-api/groups-collection-adox.md) coleção.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Groups.Append Group  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *Agrupar*  
 O **grupo** objeto a ser acrescentado ou o nome do grupo para criar e anexar.  
  
## <a name="remarks"></a>Comentários  
 O **grupos** coleção de uma [catálogo](../../../ado/reference/adox-api/catalog-object-adox.md) representa todas as contas de grupo do catálogo. O **grupos** coleção para uma [usuário](../../../ado/reference/adox-api/user-object-adox.md) representa somente o grupo ao qual o usuário pertence.  
  
 Se o provedor não dá suporte a criação de grupos, ocorrerá um erro.  
  
> [!NOTE]
>  Antes de acrescentar uma **grupo** do objeto para o **grupos** coleção de um **usuário** objeto, um **grupo** objeto com o mesmo [ Nome da](../../../ado/reference/adox-api/name-property-adox.md) como aquela a ser acrescentado já deve existir na **grupos** coleção da **catálogo**.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Coleção Groups (ADOX)](../../../ado/reference/adox-api/groups-collection-adox.md)  
  
## <a name="see-also"></a>Consulte também  
 [Groups e Users Append, ChangePassword exemplo dos métodos (VB)](../../../ado/reference/adox-api/groups-and-users-append-changepassword-methods-example-vb.md)   
 [Acrescentar o método (colunas do ADOX)](../../../ado/reference/adox-api/append-method-adox-columns.md)   
 [Acrescentar o método (índices do ADOX)](../../../ado/reference/adox-api/append-method-adox-indexes.md)   
 [Acrescentar o método (chaves do ADOX)](../../../ado/reference/adox-api/append-method-adox-keys.md)   
 [Acrescentar o método (procedimentos do ADOX)](../../../ado/reference/adox-api/append-method-adox-procedures.md)   
 [Acrescentar o método (tabelas do ADOX)](../../../ado/reference/adox-api/append-method-adox-tables.md)   
 [Acrescentar o método (usuários do ADOX)](../../../ado/reference/adox-api/append-method-adox-users.md)   
 [Método Append (Exibições do ADOX)](../../../ado/reference/adox-api/append-method-adox-views.md)
