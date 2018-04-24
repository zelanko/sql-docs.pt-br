---
title: Método (ADOX grupos) append | Microsoft Docs
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
- Groups::raw_Append
- Groups::Append
helpviewer_keywords:
- Append method [ADOX]
ms.assetid: 56b94fc6-7ef0-4e4a-82a3-033b94c46036
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 70fad30091c3f17162998ead00ce8b5de24ad680
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/18/2018
---
# <a name="append-method-adox-groups"></a>(Grupos de ADOX) do método append
Adiciona um novo [grupo](../../../ado/reference/adox-api/group-object-adox.md) o objeto para o [grupos](../../../ado/reference/adox-api/groups-collection-adox.md) coleção.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Groups.Append Group  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *Agrupar*  
 O **grupo** objeto a ser acrescentado ou o nome do grupo para criar e anexar.  
  
## <a name="remarks"></a>Remarks  
 O **grupos** coleção de um [catálogo](../../../ado/reference/adox-api/catalog-object-adox.md) representa todas as contas de grupo do catálogo. O **grupos** coleção para um [usuário](../../../ado/reference/adox-api/user-object-adox.md) representa apenas o grupo ao qual o usuário pertence.  
  
 Um erro ocorrerá se o provedor não oferece suporte a criação de grupos.  
  
> [!NOTE]
>  Antes de anexar um **grupo** o objeto para o **grupos** coleção de um **usuário** objeto, um **grupo** objeto com o mesmo [ Nome](../../../ado/reference/adox-api/name-property-adox.md) como um a ser acrescentada já deve existir no **grupos** coleção do **catálogo**.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Coleção Groups (ADOX)](../../../ado/reference/adox-api/groups-collection-adox.md)  
  
## <a name="see-also"></a>Consulte também  
 [Adicionar usuários e grupos, exemplo dos métodos ChangePassword (VB)](../../../ado/reference/adox-api/groups-and-users-append-changepassword-methods-example-vb.md)   
 [Acrescente o método (ADOX colunas)](../../../ado/reference/adox-api/append-method-adox-columns.md)   
 [Método (ADOX índices) append](../../../ado/reference/adox-api/append-method-adox-indexes.md)   
 [(ADOX chaves) do método append](../../../ado/reference/adox-api/append-method-adox-keys.md)   
 [Acrescente o método (ADOX procedimentos)](../../../ado/reference/adox-api/append-method-adox-procedures.md)   
 [(Tabelas ADOX) do método append](../../../ado/reference/adox-api/append-method-adox-tables.md)   
 [Acrescente o método (ADOX usuários)](../../../ado/reference/adox-api/append-method-adox-users.md)   
 [Método Append (Exibições do ADOX)](../../../ado/reference/adox-api/append-method-adox-views.md)
