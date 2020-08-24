---
description: Método Close (ADO MD)
title: Método Close (ADO MD) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Close
- Cellset::Close
helpviewer_keywords:
- Close method [ADO MD]
ms.assetid: a3aa594d-f9d4-4654-8625-ec20153ff5d9
author: rothja
ms.author: jroth
ms.openlocfilehash: 666cf9afc4f6f5df5d3e950948e60bd644a45cdb
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88778265"
---
# <a name="close-method-ado-md"></a>Método Close (ADO MD)
Fecha um células aberto.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Cellset.Close  
```  
  
## <a name="remarks"></a>Comentários  
 Usar o **método Close** para fechar um [objeto células](./cellset-object-ado-md.md) liberará os dados associados, incluindo dados em qualquer [célula](./cell-object-ado-md.md), [eixo](./axis-object-ado-md.md), [posição](./position-object-ado-md.md)ou objetos de [membro](./member-object-ado-md.md) relacionados. Fechar um **células** não o Remove da memória; Você pode alterar suas configurações de propriedade e abri-las novamente mais tarde. Para eliminar completamente um objeto da memória, defina a variável de objeto como **Nothing**.  
  
 Posteriormente, você pode chamar o método [Open](./open-method-ado-md.md) para reabrir o **células** usando a mesma cadeia de caracteres de origem ou outra. Enquanto o objeto **células** é fechado, a recuperação de qualquer propriedade ou a chamada de qualquer método que referencie os dados subjacentes ou os metadados gera um erro.  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto Cellset (ADO MD)](./cellset-object-ado-md.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Objeto Axis (ADO MD)](./axis-object-ado-md.md)   
 [Objeto Cell (ADO MD)](./cell-object-ado-md.md)   
 [Objeto member (ADO MD)](./member-object-ado-md.md)   
 [Método Open (ADO MD)](./open-method-ado-md.md)   
 [Objeto Position (ADO MD)](./position-object-ado-md.md)   
 [Propriedade State (ADO MD)](./state-property-ado-md.md)