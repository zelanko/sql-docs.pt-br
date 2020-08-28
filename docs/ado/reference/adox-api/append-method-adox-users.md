---
description: Método Append (Usuários do ADOX)
title: Método Append (usuários ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
ms.openlocfilehash: 14b0c573b3ccf8a03b1c2f6513cdac67303fb4bf
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88985427"
---
# <a name="append-method-adox-users"></a>Método Append (Usuários do ADOX)
Adiciona um novo objeto de [usuário](./user-object-adox.md) à coleção [usuários](./users-collection-adox.md) .  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Users.Append User[,Password]  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *Usuário*  
 Um valor **Variant** que contém o objeto de **usuário** a ser anexado ou o nome do usuário a ser criado e acrescentado.  
  
 *Senha*  
 Opcional. Um valor de **cadeia de caracteres** que contém a senha para o usuário. O parâmetro de *senha* corresponde ao valor especificado pelo método [ChangePassword](./changepassword-method-adox.md) de um objeto de **usuário** .  
  
## <a name="remarks"></a>Comentários  
 A coleção de **usuários** de um [Catálogo](./catalog-object-adox.md) representa todos os usuários do catálogo. A coleção de **usuários** para um [grupo](./group-object-adox.md) representa apenas os usuários que têm uma associação no grupo específico.  
  
 Ocorrerá um erro se o provedor não oferecer suporte à criação de usuários.  
  
> [!NOTE]
>  Antes de acrescentar um objeto de **usuário** à coleção de **usuários** de um objeto de **grupo** , um objeto de **usuário** com o mesmo [nome](./name-property-adox.md) que aquele a ser anexado já deve existir na coleção de **usuários** do **Catálogo**.  
  
## <a name="applies-to"></a>Aplica-se A  
 [Coleção Users (ADOX)](./users-collection-adox.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo dos métodos Groups e Users Append, ChangePassword (VB)](./groups-and-users-append-changepassword-methods-example-vb.md)   
 [Método Append (colunas ADOX)](./append-method-adox-columns.md)   
 [Método Append (grupos ADOX)](./append-method-adox-groups.md)   
 [Método Append (índices ADOX)](./append-method-adox-indexes.md)   
 [Método Append (chaves ADOX)](./append-method-adox-keys.md)   
 [Método Append (procedimentos do ADOX)](./append-method-adox-procedures.md)   
 [Método Append (tabelas ADOX)](./append-method-adox-tables.md)   
 [Método Append (Exibições do ADOX)](./append-method-adox-views.md)