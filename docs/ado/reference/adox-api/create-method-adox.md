---
title: Método Create (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Catalog::raw_Create
- _Catalog::Create
helpviewer_keywords:
- Create method [ADOX]
ms.assetid: 64f5c21c-b581-42d8-bdc7-c4f1bebaf105
author: rothja
ms.author: jroth
ms.openlocfilehash: 15ea5cf8b565a943f4905a890cb08ba0afed202f
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82759262"
---
# <a name="create-method-adox"></a>Método Create (ADOX)
Cria um novo catálogo.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Catalog.Create ConnectString  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *ConnectString*  
 Um valor de **cadeia de caracteres** usado para se conectar à fonte de dados.  
  
## <a name="remarks"></a>Comentários  
 O método **Create** cria e abre uma nova [conexão](../../../ado/reference/ado-api/connection-object-ado.md) ADO com a fonte de dados especificada em *ConnectString*. Se for bem-sucedido, o novo objeto de **conexão** será atribuído à propriedade [ActiveConnection](../../../ado/reference/adox-api/activeconnection-property-adox.md) .  
  
 Ocorrerá um erro se o provedor não oferecer suporte à criação de novos catálogos.  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto Catalog (ADOX)](../../../ado/reference/adox-api/catalog-object-adox.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo do método Create (VB)](../../../ado/reference/adox-api/create-method-example-vb.md)   
 [Propriedade ActiveConnection (ADOX)](../../../ado/reference/adox-api/activeconnection-property-adox.md)
