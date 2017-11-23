---
title: "Método ChangePassword (ADOX) | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology: drivers
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
helpviewer_keywords: ChangePassword method [ADOX]
ms.assetid: d187fbc6-5fac-4abb-803d-bf344dcf0302
caps.latest.revision: "12"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 33f2bfdc111277ef035aa8e3cde36f019a97f5b4
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
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
