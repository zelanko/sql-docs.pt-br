---
description: Método ChangePassword (ADOX)
title: Método ChangePassword (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
author: rothja
ms.author: jroth
ms.openlocfilehash: e51037f9838e9aef279351c822e6c35ffb25f0fb
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88985197"
---
# <a name="changepassword-method-adox"></a>Método ChangePassword (ADOX)
Altera a senha de uma conta de [usuário](./user-object-adox.md) .  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
User.ChangePassword OldPassword, NewPassword  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *OldPassword*  
 Um valor de **cadeia de caracteres** que especifica a senha existente do usuário. Se o usuário não tiver uma senha no momento, use uma cadeia de caracteres vazia ("") para *oldPassword*.  
  
 *NewPassword*  
 Um valor de **cadeia de caracteres** que especifica a nova senha.  
  
## <a name="remarks"></a>Comentários  
 Por motivos de segurança, a senha antiga deve ser especificada além da nova senha.  
  
 Ocorrerá um erro se o provedor não oferecer suporte à administração de propriedades de confiança.  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto User (ADOX)](./user-object-adox.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo dos métodos Groups e Users Append, ChangePassword (VB)](./groups-and-users-append-changepassword-methods-example-vb.md)