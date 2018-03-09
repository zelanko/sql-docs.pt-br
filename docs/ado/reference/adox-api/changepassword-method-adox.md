---
title: "Método ChangePassword (ADOX) | Microsoft Docs"
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
- _User25::raw_ChangePassword
- _User25::ChangePassword
helpviewer_keywords:
- ChangePassword method [ADOX]
ms.assetid: d187fbc6-5fac-4abb-803d-bf344dcf0302
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 76814245ef5e41e12774df25ea23283f98fd9100
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/09/2018
---
# <a name="changepassword-method-adox"></a>Método ChangePassword (ADOX)
Altera a senha de um [usuário](../../../ado/reference/adox-api/user-object-adox.md) conta.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
User.ChangePassword OldPassword, NewPassword  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *OldPassword*  
 Um **cadeia de caracteres** valor que especifica a senha do usuário existente. Se o usuário não tem uma senha, use uma cadeia de caracteres vazia ("") para *Senha_atual*.  
  
 *NewPassword*  
 Um **cadeia de caracteres** valor que especifica a nova senha.  
  
## <a name="remarks"></a>Remarks  
 Por motivos de segurança, especifique a senha antiga e a nova senha.  
  
 Um erro ocorrerá se o provedor não oferece suporte a administração das propriedades do objeto de confiança.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto User (ADOX)](../../../ado/reference/adox-api/user-object-adox.md)  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo dos métodos Groups e Users Append, ChangePassword (VB)](../../../ado/reference/adox-api/groups-and-users-append-changepassword-methods-example-vb.md)
