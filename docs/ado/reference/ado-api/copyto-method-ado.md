---
title: Método CopyTo (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Stream::raw_CopyTo
- _Stream::CopyTo
helpviewer_keywords:
- CopyTo method [ADO]
ms.assetid: b4aa5714-916b-48b8-8b09-cc2708379602
author: rothja
ms.author: jroth
ms.openlocfilehash: d8b34e47948cbc0742b0b7b0a4f413d56e4086cf
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82760242"
---
# <a name="copyto-method-ado"></a>Método CopyTo (ADO)
Copia o número especificado de caracteres ou bytes (dependendo do [tipo](../../../ado/reference/ado-api/type-property-ado-stream.md)) no [fluxo](../../../ado/reference/ado-api/stream-object-ado.md) para outro objeto de **fluxo** .  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Stream.CopyTo DestStream, NumChars  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *DestStream*  
 Um valor de variável de objeto que contém uma referência a um objeto de **fluxo** aberto. O **fluxo** atual é copiado para o **fluxo** de destino especificado por *DestStream*. O **fluxo** de destino já deve estar aberto. Caso contrário, ocorrerá um erro em tempo de execução.  
  
> [!NOTE]
>  O parâmetro *DestStream* não pode ser um proxy de objeto de **fluxo** porque isso requer acesso a uma interface privada no objeto de **fluxo** que não pode ser remoto para o cliente.  
  
 *NumChars*  
 Opcional. Um valor **inteiro** que especifica o número de bytes ou caracteres a serem copiados da posição atual no **fluxo** de origem para o **fluxo**de destino. O valor padrão é-1, que especifica que todos os caracteres ou bytes são copiados da posição atual para [EOS](../../../ado/reference/ado-api/eos-property.md).  
  
## <a name="remarks"></a>Comentários  
 Esse método copia o número especificado de caracteres ou bytes, começando da posição atual especificada pela propriedade [Position](../../../ado/reference/ado-api/position-property-ado.md) . Se o número especificado for maior do que o número disponível de bytes até **EOS**, somente os caracteres ou bytes da posição atual para **EOS** serão copiados. Se o valor de *NUMCHARS* for-1, ou omitido, todos os caracteres ou bytes iniciados a partir da posição atual serão copiados.  
  
 Se houver caracteres ou bytes existentes no fluxo de destino, todo o conteúdo além do ponto em que a cópia termina e não será truncado. A **posição** se torna o byte imediatamente após o último byte copiado. Se você quiser truncar esses bytes, chame [SetEOS](../../../ado/reference/ado-api/seteos-method.md).  
  
 **CopyTo** deve ser usado para copiar dados para um **fluxo** de destino do mesmo tipo que o **fluxo** de origem (suas configurações de propriedade de **tipo** são **adTypeText** ou ambos **adTypeBinary**). Para objetos de **fluxo** de texto, você pode alterar a configuração da propriedade [charset](../../../ado/reference/ado-api/charset-property-ado.md) do **fluxo** de destino para traduzir de um conjunto de caracteres para outro. Além disso, objetos de **fluxo** de texto podem ser copiados com êxito em objetos de **fluxo** binários, mas objetos de **fluxo** binários não podem ser copiados em objetos de **fluxo** de texto.  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto Stream (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)
