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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: aafcab3ad379dc25a2681a5d4f0d3f5e8d6eab5c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67966675"
---
# <a name="create-method-adox"></a>Método Create (ADOX)
Cria um novo catálogo.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Catalog.Create ConnectString  
```  
  
#### <a name="parameters"></a>parâmetros  
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
