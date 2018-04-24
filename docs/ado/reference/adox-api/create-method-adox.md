---
title: Criar método (ADOX) | Microsoft Docs
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
- _Catalog::raw_Create
- _Catalog::Create
helpviewer_keywords:
- Create method [ADOX]
ms.assetid: 64f5c21c-b581-42d8-bdc7-c4f1bebaf105
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c1c159f0e53c5c4b39d9c225dd7dfa8cee581445
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/18/2018
---
# <a name="create-method-adox"></a>Criar método (ADOX)
Cria um novo catálogo.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Catalog.Create ConnectString  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *ConnectString*  
 Um **cadeia de caracteres** valor usado para se conectar à fonte de dados.  
  
## <a name="remarks"></a>Remarks  
 O **criar** método cria e abre um novo ADO [Conexão](../../../ado/reference/ado-api/connection-object-ado.md) à fonte de dados especificado em *ConnectString*. Se for bem-sucedido, o novo **Conexão** objeto é atribuído para o [ActiveConnection](../../../ado/reference/adox-api/activeconnection-property-adox.md) propriedade.  
  
 Se o provedor não oferece suporte a criação de novos catálogos, ocorrerá um erro.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Catalog (ADOX)](../../../ado/reference/adox-api/catalog-object-adox.md)  
  
## <a name="see-also"></a>Consulte também  
 [Criar um exemplo de método (VB)](../../../ado/reference/adox-api/create-method-example-vb.md)   
 [Propriedade ActiveConnection (ADOX)](../../../ado/reference/adox-api/activeconnection-property-adox.md)
