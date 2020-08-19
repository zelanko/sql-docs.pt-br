---
description: Método Append (Usuários do ADOX)
title: Método Append (usuários ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Users::raw_Append
- Users::Append
helpviewer_keywords:
- Append method [ADOX]
ms.assetid: b80bc5d5-78ca-4f75-956b-2ac658029cc7
author: rothja
ms.author: jroth
ms.openlocfilehash: e774ab590e3f405cab157293405eba5e575ecb52
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88440458"
---
# <a name="append-method-adox-users"></a>Método Append (Usuários do ADOX)
Adiciona um novo objeto de [usuário](../../../ado/reference/adox-api/user-object-adox.md) à coleção [usuários](../../../ado/reference/adox-api/users-collection-adox.md) .  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Users.Append User[,Password]  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *Usuário*  
 Um valor **Variant** que contém o objeto de **usuário** a ser anexado ou o nome do usuário a ser criado e acrescentado.  
  
 *Senha*  
 Opcional. Um valor de **cadeia de caracteres** que contém a senha para o usuário. O parâmetro de *senha* corresponde ao valor especificado pelo método [ChangePassword](../../../ado/reference/adox-api/changepassword-method-adox.md) de um objeto de **usuário** .  
  
## <a name="remarks"></a>Comentários  
 A coleção de **usuários** de um [Catálogo](../../../ado/reference/adox-api/catalog-object-adox.md) representa todos os usuários do catálogo. A coleção de **usuários** para um [grupo](../../../ado/reference/adox-api/group-object-adox.md) representa apenas os usuários que têm uma associação no grupo específico.  
  
 Ocorrerá um erro se o provedor não oferecer suporte à criação de usuários.  
  
> [!NOTE]
>  Antes de acrescentar um objeto de **usuário** à coleção de **usuários** de um objeto de **grupo** , um objeto de **usuário** com o mesmo [nome](../../../ado/reference/adox-api/name-property-adox.md) que aquele a ser anexado já deve existir na coleção de **usuários** do **Catálogo**.  
  
## <a name="applies-to"></a>Aplica-se A  
 [Coleção Users (ADOX)](../../../ado/reference/adox-api/users-collection-adox.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo dos métodos Groups e Users Append, ChangePassword (VB)](../../../ado/reference/adox-api/groups-and-users-append-changepassword-methods-example-vb.md)   
 [Método Append (colunas ADOX)](../../../ado/reference/adox-api/append-method-adox-columns.md)   
 [Método Append (grupos ADOX)](../../../ado/reference/adox-api/append-method-adox-groups.md)   
 [Método Append (índices ADOX)](../../../ado/reference/adox-api/append-method-adox-indexes.md)   
 [Método Append (chaves ADOX)](../../../ado/reference/adox-api/append-method-adox-keys.md)   
 [Método Append (procedimentos do ADOX)](../../../ado/reference/adox-api/append-method-adox-procedures.md)   
 [Método Append (tabelas ADOX)](../../../ado/reference/adox-api/append-method-adox-tables.md)   
 [Método Append (Exibições do ADOX)](../../../ado/reference/adox-api/append-method-adox-views.md)
