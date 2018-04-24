---
title: Método (usuários ADOX) append | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Users::raw_Append
- Users::Append
helpviewer_keywords:
- Append method [ADOX]
ms.assetid: b80bc5d5-78ca-4f75-956b-2ac658029cc7
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 267dbd8bc1eb05a1d0f56c9078c5f5518d1e38d7
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/18/2018
---
# <a name="append-method-adox-users"></a>Acrescente o método (ADOX usuários)
Adiciona um novo [usuário](../../../ado/reference/adox-api/user-object-adox.md) o objeto para o [usuários](../../../ado/reference/adox-api/users-collection-adox.md) coleção.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Users.Append User[,Password]  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *Usuário*  
 Um **Variant** valor que contém o **usuário** objeto a ser acrescentado ou o nome do usuário para criar e anexar.  
  
 *Senha*  
 Opcional. Um **cadeia de caracteres** valor que contém a senha do usuário. O *senha* parâmetro corresponde ao valor especificado pelo [ChangePassword](../../../ado/reference/adox-api/changepassword-method-adox.md) método de um **usuário** objeto.  
  
## <a name="remarks"></a>Remarks  
 O **usuários** coleção de um [catálogo](../../../ado/reference/adox-api/catalog-object-adox.md) representa usuários todos do catálogo. O **usuários** coleção para um [grupo](../../../ado/reference/adox-api/group-object-adox.md) representa apenas os usuários que têm uma associação no grupo específico.  
  
 Se o provedor não oferece suporte para criar usuários, ocorrerá um erro.  
  
> [!NOTE]
>  Antes de anexar um **usuário** o objeto para o **usuários** coleção de um **grupo** objeto, um **usuário** objeto com o mesmo [nome ](../../../ado/reference/adox-api/name-property-adox.md) como um a ser acrescentada já deve existir no **usuários** coleção do **catálogo**.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Coleção Users (ADOX)](../../../ado/reference/adox-api/users-collection-adox.md)  
  
## <a name="see-also"></a>Consulte também  
 [Adicionar usuários e grupos, exemplo dos métodos ChangePassword (VB)](../../../ado/reference/adox-api/groups-and-users-append-changepassword-methods-example-vb.md)   
 [Acrescente o método (ADOX colunas)](../../../ado/reference/adox-api/append-method-adox-columns.md)   
 [(Grupos de ADOX) do método append](../../../ado/reference/adox-api/append-method-adox-groups.md)   
 [Método (ADOX índices) append](../../../ado/reference/adox-api/append-method-adox-indexes.md)   
 [(ADOX chaves) do método append](../../../ado/reference/adox-api/append-method-adox-keys.md)   
 [Acrescente o método (ADOX procedimentos)](../../../ado/reference/adox-api/append-method-adox-procedures.md)   
 [(Tabelas ADOX) do método append](../../../ado/reference/adox-api/append-method-adox-tables.md)   
 [Método Append (Exibições do ADOX)](../../../ado/reference/adox-api/append-method-adox-views.md)
