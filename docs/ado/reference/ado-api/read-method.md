---
title: Método Read | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: reference
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
- Stream::raw_Read
- _Stream::Read
helpviewer_keywords:
- Read method [ADO]
ms.assetid: 838502de-80f1-4eeb-8838-dd3d9403e567
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 910d566d60afa2e255e05647e429af505bd5b4fe
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
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
  
## <a name="remarks"></a>Remarks  
 Se *NumBytes* é maior que o número de bytes restantes de **fluxo**, somente os bytes restantes são retornados. A leitura de dados não serão preenchidos de acordo com o comprimento especificado por *NumBytes*. Se não houver nenhum bytes para leitura, uma variante com um valor nulo será retornada. **Leitura** não pode ser usado para ler com versões anteriores.  
  
> [!NOTE]
>  *NumBytes* sempre mede bytes. Para texto **fluxo** objetos ([tipo](../../../ado/reference/ado-api/type-property-ado-stream.md) é **adTypeText**), use [ReadText](../../../ado/reference/ado-api/readtext-method.md).  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Stream (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>Consulte também  
 [Método ReadText](../../../ado/reference/ado-api/readtext-method.md)
