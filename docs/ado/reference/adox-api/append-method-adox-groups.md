---
title: Método Append (grupos ADOX) | Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 3896de6c921f85d4b3e5a2194b1baa2fe511f22b
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82764047"
---
# <a name="append-method-adox-groups"></a>Método Append (Grupos do ADOX)
Adiciona um novo objeto de [grupo](../../../ado/reference/adox-api/group-object-adox.md) à coleção de [grupos](../../../ado/reference/adox-api/groups-collection-adox.md) .  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Groups.Append Group  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *Group*  
 O objeto de **grupo** a ser anexado ou o nome do grupo a ser criado e acrescentado.  
  
## <a name="remarks"></a>Comentários  
 A coleção de **grupos** de um [Catálogo](../../../ado/reference/adox-api/catalog-object-adox.md) representa todas as contas de grupo do catálogo. A coleção de **grupos** de um [usuário](../../../ado/reference/adox-api/user-object-adox.md) representa apenas o grupo ao qual o usuário pertence.  
  
 Ocorrerá um erro se o provedor não oferecer suporte à criação de grupos.  
  
> [!NOTE]
>  Antes de acrescentar um objeto de **grupo** à coleção de **grupos** de um objeto de **usuário** , um objeto de **grupo** com o mesmo [nome](../../../ado/reference/adox-api/name-property-adox.md) que aquele a ser anexado já deve existir na coleção de **grupos** do **Catálogo**.  
  
## <a name="applies-to"></a>Aplica-se A  
 [Coleção Groups (ADOX)](../../../ado/reference/adox-api/groups-collection-adox.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo dos métodos Groups e Users Append, ChangePassword (VB)](../../../ado/reference/adox-api/groups-and-users-append-changepassword-methods-example-vb.md)   
 [Método Append (colunas ADOX)](../../../ado/reference/adox-api/append-method-adox-columns.md)   
 [Método Append (índices ADOX)](../../../ado/reference/adox-api/append-method-adox-indexes.md)   
 [Método Append (chaves ADOX)](../../../ado/reference/adox-api/append-method-adox-keys.md)   
 [Método Append (procedimentos do ADOX)](../../../ado/reference/adox-api/append-method-adox-procedures.md)   
 [Método Append (tabelas ADOX)](../../../ado/reference/adox-api/append-method-adox-tables.md)   
 [Método Append (usuários do ADOX)](../../../ado/reference/adox-api/append-method-adox-users.md)   
 [Método Append (Exibições do ADOX)](../../../ado/reference/adox-api/append-method-adox-views.md)
