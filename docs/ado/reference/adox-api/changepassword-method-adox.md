---
title: "Método ChangePassword (ADOX) | Microsoft Docs"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- _User25::raw_ChangePassword
- _User25::ChangePassword
helpviewer_keywords:
- ChangePassword method [ADOX]
ms.assetid: d187fbc6-5fac-4abb-803d-bf344dcf0302
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 18dd53bc701cf6a4b77c8e77f5b1851aff57f2ba
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="changepassword-method-adox"></a>Método ChangePassword (ADOX)
Altera a senha de um [usuário](../../../ado/reference/adox-api/user-object-adox.md) conta.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
User.ChangePassword OldPassword, NewPassword  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *Senha_atual*  
 Um **cadeia de caracteres** valor que especifica a senha do usuário existente. Se o usuário não tem uma senha, use uma cadeia de caracteres vazia ("") para *Senha_atual*.  
  
 *NewPassword*  
 Um **cadeia de caracteres** valor que especifica a nova senha.  
  
## <a name="remarks"></a>Comentários  
 Por motivos de segurança, especifique a senha antiga e a nova senha.  
  
 Um erro ocorrerá se o provedor não oferece suporte a administração das propriedades do objeto de confiança.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto User (ADOX)](../../../ado/reference/adox-api/user-object-adox.md)  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo dos métodos Groups e Users Append, ChangePassword (VB)](../../../ado/reference/adox-api/groups-and-users-append-changepassword-methods-example-vb.md)
