---
title: "Método Read | Microsoft Docs"
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
- Stream::raw_Read
- _Stream::Read
helpviewer_keywords: Read method [ADO]
ms.assetid: 838502de-80f1-4eeb-8838-dd3d9403e567
caps.latest.revision: "13"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 740be677f54f8d4b5d30902a792b58d4681df888
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="read-method"></a>Método Read
Lê um número especificado de bytes de um binário [fluxo](../../../ado/reference/ado-api/stream-object-ado.md) objeto.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Variant = Stream.Read ( NumBytes)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *NumBytes*  
 Opcional. Um **longo** valor que especifica o número de bytes a serem lidos do arquivo ou o [StreamReadEnum](../../../ado/reference/ado-api/streamreadenum.md) valor **adReadAll**, que é o padrão.  
  
## <a name="return-value"></a>Valor de retorno  
 O **leitura** método lê um número especificado de bytes ou o fluxo inteiro de um **fluxo** de objeto e retorna os dados resultantes como um **Variant**.  
  
## <a name="remarks"></a>Comentários  
 Se *NumBytes* é maior que o número de bytes restantes de **fluxo**, somente os bytes restantes são retornados. A leitura de dados não serão preenchidos de acordo com o comprimento especificado por *NumBytes*. Se não houver nenhum bytes para leitura, uma variante com um valor nulo será retornada. **Leitura** não pode ser usado para ler com versões anteriores.  
  
> [!NOTE]
>  *NumBytes* sempre mede bytes. Para texto **fluxo** objetos ([tipo](../../../ado/reference/ado-api/type-property-ado-stream.md) é **adTypeText**), use [ReadText](../../../ado/reference/ado-api/readtext-method.md).  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Stream (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>Consulte também  
 [Método ReadText](../../../ado/reference/ado-api/readtext-method.md)
