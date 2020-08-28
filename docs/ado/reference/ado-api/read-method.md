---
description: Método Read
title: Método Read | Microsoft Docs
ms.prod: sql
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Stream::raw_Read
- _Stream::Read
helpviewer_keywords:
- Read method [ADO]
ms.assetid: 838502de-80f1-4eeb-8838-dd3d9403e567
author: rothja
ms.author: jroth
ms.openlocfilehash: 6d4b0ab7c3cc77c1f83eac4c3a30e9f637d950ba
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88989897"
---
# <a name="read-method"></a>Método Read
Lê um número especificado de bytes de um objeto de [fluxo](./stream-object-ado.md) binário.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Variant = Stream.Read ( NumBytes)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *NumBytes*  
 Opcional. Um valor **longo** que especifica o número de bytes a serem lidos do arquivo ou o valor de [StreamReadEnum](./streamreadenum.md) **adReadAll**, que é o padrão.  
  
## <a name="return-value"></a>Valor de retorno  
 O método **Read** lê um número especificado de bytes ou o fluxo inteiro de um objeto de **fluxo** e retorna os dados resultantes como uma **variante**.  
  
## <a name="remarks"></a>Comentários  
 Se *NumBytes* for maior que o número de bytes restante no **fluxo**, somente os bytes restantes serão retornados. A leitura de dados não é preenchida para corresponder ao comprimento especificado por *NumBytes*. Se não houver nenhum byte restante para leitura, será retornada uma variante com um valor nulo. A **leitura** não pode ser usada para ler versões anteriores.  
  
> [!NOTE]
>  *NumBytes* sempre mede bytes. Para objetos de **fluxo** de texto (o[tipo](./type-property-ado-stream.md) é **adTypeText**), use [ReadText](./readtext-method.md).  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto Stream (ADO)](./stream-object-ado.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Método ReadText](./readtext-method.md)