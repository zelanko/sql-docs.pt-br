---
title: "Método SaveToFile | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- _Stream::raw_SaveToFile
- _Stream::SaveToFile
helpviewer_keywords:
- SaveToFile method [ADO]
ms.assetid: 8a8594f2-422b-4d2e-94f8-7fe337445900
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 64fa2093400ac9c003397659be3d9d6f4251eee2
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/09/2018
---
# <a name="savetofile-method"></a>Método SaveToFile
Salva o conteúdo binário de um [fluxo](../../../ado/reference/ado-api/stream-object-ado.md) para um arquivo.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Stream.SaveToFile FileName, SaveOptions  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *FileName*  
 Um **cadeia de caracteres** valor que contém o nome totalmente qualificado do arquivo para o qual o conteúdo do **fluxo** será salvo. Você pode salvar em qualquer local válido ou qualquer local que você tem acesso a por meio de um valor UNC.  
  
 *SaveOptions*  
 Um [SaveOptionsEnum](../../../ado/reference/ado-api/saveoptionsenum.md) valor que especifica se um novo arquivo deve ser criado por **SaveToFile**, se ele ainda não existir. Valor padrão é **adSaveCreateNotExists**. Com essas opções, você pode especificar que um erro ocorrerá se o arquivo especificado não existe. Você também pode especificar que **SaveToFile** substitui o conteúdo atual de um arquivo existente.  
  
> [!NOTE]
>  Se você substituir um arquivo existente (quando **adSaveCreateOverwrite** é definido), **SaveToFile** trunca qualquer bytes do arquivo original existente que execute o novo [EOS](../../../ado/reference/ado-api/eos-property.md).  
  
## <a name="remarks"></a>Remarks  
 **SaveToFile** pode ser usado para copiar o conteúdo de um **fluxo** objeto para um arquivo local. Não há nenhuma alteração no conteúdo ou propriedades do **fluxo** objeto. O **fluxo** objeto deve ser aberto antes de chamar **SaveToFile**.  
  
 Este método não altera a associação do **fluxo** objeto de fonte de dados subjacente. O **fluxo** objeto ainda será associado com a URL original ou **registro** que foi sua origem quando aberto.  
  
 Após um **SaveToFile** operação, a posição atual ([posição](../../../ado/reference/ado-api/position-property-ado.md)) no fluxo é definido para o início do fluxo (0).  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Stream (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>Consulte também  
 [Método Open (fluxo de ADO)](../../../ado/reference/ado-api/open-method-ado-stream.md)   
 [Método Save](../../../ado/reference/ado-api/save-method.md)
