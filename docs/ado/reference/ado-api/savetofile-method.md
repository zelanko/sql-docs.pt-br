---
title: Método SaveToFile | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Stream::raw_SaveToFile
- _Stream::SaveToFile
helpviewer_keywords:
- SaveToFile method [ADO]
ms.assetid: 8a8594f2-422b-4d2e-94f8-7fe337445900
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6afe36c7b3923c9ebf33fd615a1c21e34955e62d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63315216"
---
# <a name="savetofile-method"></a>Método SaveToFile
Salva o conteúdo binário de um [Stream](../../../ado/reference/ado-api/stream-object-ado.md) para um arquivo.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Stream.SaveToFile FileName, SaveOptions  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *FileName*  
 Um **cadeia de caracteres** valor que contém o nome totalmente qualificado do arquivo para o qual o conteúdo do **Stream** será salvo. Você pode salvar em qualquer local válido ou qualquer local que você tem acesso por meio de um valor UNC.  
  
 *SaveOptions*  
 Um [SaveOptionsEnum](../../../ado/reference/ado-api/saveoptionsenum.md) valor que especifica se um novo arquivo deve ser criado por **SaveToFile**, se ele ainda não existir. Valor padrão é **adSaveCreateNotExists**. Com essas opções, você pode especificar que um erro ocorre se o arquivo especificado não existe. Você também pode especificar que **SaveToFile** substitui o conteúdo atual de um arquivo existente.  
  
> [!NOTE]
>  Se você substituir um arquivo existente (quando **adSaveCreateOverwrite** é definido), **SaveToFile** trunca qualquer bytes do arquivo original existente que execute o novo [EOS](../../../ado/reference/ado-api/eos-property.md).  
  
## <a name="remarks"></a>Comentários  
 **SaveToFile** pode ser usado para copiar o conteúdo de um **Stream** objeto em um arquivo local. Não há nenhuma alteração no conteúdo ou propriedades do **Stream** objeto. O **Stream** objeto deve ser aberto antes de chamar **SaveToFile**.  
  
 Esse método não altera a associação do **Stream** objeto à sua fonte subjacente. O **Stream** objeto ainda será associado com a URL original ou **registro** que era sua fonte quando aberto.  
  
 Depois de um **SaveToFile** operação, a posição atual ([posição](../../../ado/reference/ado-api/position-property-ado.md)) no fluxo é definido para o início do fluxo (0).  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Stream (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>Consulte também  
 [Método Open (ADO Stream)](../../../ado/reference/ado-api/open-method-ado-stream.md)   
 [Método Save](../../../ado/reference/ado-api/save-method.md)
