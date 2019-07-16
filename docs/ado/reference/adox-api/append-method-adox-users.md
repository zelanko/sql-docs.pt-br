---
title: (Usuários do ADOX) do método append | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 99a21cd5dd32af9e84877865cfe7c0fc92f6c087
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67967220"
---
# <a name="append-method-adox-users"></a>Método Append (Usuários do ADOX)
Adiciona um novo [usuário](../../../ado/reference/adox-api/user-object-adox.md) do objeto para o [usuários](../../../ado/reference/adox-api/users-collection-adox.md) coleção.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Users.Append User[,Password]  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *Usuário*  
 Um **Variant** valor que contém o **usuário** objeto a ser acrescentado ou o nome do usuário para criar e anexar.  
  
 *Senha*  
 Opcional. Um **cadeia de caracteres** valor que contém a senha do usuário. O *senha* parâmetro corresponde ao valor especificado pela [ChangePassword](../../../ado/reference/adox-api/changepassword-method-adox.md) método de um **usuário** objeto.  
  
## <a name="remarks"></a>Comentários  
 O **os usuários** coleção de uma [catálogo](../../../ado/reference/adox-api/catalog-object-adox.md) representa usuários de todos os do catálogo. O **os usuários** coleção para uma [grupo](../../../ado/reference/adox-api/group-object-adox.md) representa apenas os usuários que têm uma associação no grupo específico.  
  
 Se o provedor não dá suporte para criar usuários, ocorrerá um erro.  
  
> [!NOTE]
>  Antes de acrescentar uma **usuário** do objeto para o **usuários** coleção de um **grupo** objeto, um **usuário** objeto com o mesmo [nome ](../../../ado/reference/adox-api/name-property-adox.md) como aquela a ser acrescentado já deve existir na **os usuários** coleção dos **catálogo**.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Coleção Users (ADOX)](../../../ado/reference/adox-api/users-collection-adox.md)  
  
## <a name="see-also"></a>Consulte também  
 [Groups e Users Append, ChangePassword exemplo dos métodos (VB)](../../../ado/reference/adox-api/groups-and-users-append-changepassword-methods-example-vb.md)   
 [Acrescentar o método (colunas do ADOX)](../../../ado/reference/adox-api/append-method-adox-columns.md)   
 [Acrescentar o método (grupos do ADOX)](../../../ado/reference/adox-api/append-method-adox-groups.md)   
 [Acrescentar o método (índices do ADOX)](../../../ado/reference/adox-api/append-method-adox-indexes.md)   
 [Acrescentar o método (chaves do ADOX)](../../../ado/reference/adox-api/append-method-adox-keys.md)   
 [Acrescentar o método (procedimentos do ADOX)](../../../ado/reference/adox-api/append-method-adox-procedures.md)   
 [Acrescentar o método (tabelas do ADOX)](../../../ado/reference/adox-api/append-method-adox-tables.md)   
 [Método Append (Exibições do ADOX)](../../../ado/reference/adox-api/append-method-adox-views.md)
