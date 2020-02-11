---
title: Método ChangePassword (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _User25::raw_ChangePassword
- _User25::ChangePassword
helpviewer_keywords:
- ChangePassword method [ADOX]
ms.assetid: d187fbc6-5fac-4abb-803d-bf344dcf0302
author: MightyPen
ms.author: genemi
ms.openlocfilehash: de8baf504a76407037322fd6b799f6d63584eae7
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67967030"
---
# <a name="changepassword-method-adox"></a>Método ChangePassword (ADOX)
Altera a senha de uma conta de [usuário](../../../ado/reference/adox-api/user-object-adox.md) .  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
User.ChangePassword OldPassword, NewPassword  
```  
  
#### <a name="parameters"></a>parâmetros  
 *OldPassword*  
 Um valor de **cadeia de caracteres** que especifica a senha existente do usuário. Se o usuário não tiver uma senha no momento, use uma cadeia de caracteres vazia ("") para *oldPassword*.  
  
 *NewPassword*  
 Um valor de **cadeia de caracteres** que especifica a nova senha.  
  
## <a name="remarks"></a>Comentários  
 Por motivos de segurança, a senha antiga deve ser especificada além da nova senha.  
  
 Ocorrerá um erro se o provedor não oferecer suporte à administração de propriedades de confiança.  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto User (ADOX)](../../../ado/reference/adox-api/user-object-adox.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo dos métodos Groups e Users Append, ChangePassword (VB)](../../../ado/reference/adox-api/groups-and-users-append-changepassword-methods-example-vb.md)
