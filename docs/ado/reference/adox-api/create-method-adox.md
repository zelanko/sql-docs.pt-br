---
description: Método Create (ADOX)
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
ms.openlocfilehash: b5add8972d95413841a6c9c45de2dcc26d8cbb24
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88770835"
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
 O método **Create** cria e abre uma nova [conexão](../ado-api/connection-object-ado.md) ADO com a fonte de dados especificada em *ConnectString*. Se for bem-sucedido, o novo objeto de **conexão** será atribuído à propriedade [ActiveConnection](./activeconnection-property-adox.md) .  
  
 Ocorrerá um erro se o provedor não oferecer suporte à criação de novos catálogos.  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto Catalog (ADOX)](./catalog-object-adox.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo do método Create (VB)](./create-method-example-vb.md)   
 [Propriedade ActiveConnection (ADOX)](./activeconnection-property-adox.md)