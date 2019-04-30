---
title: Saltando para um registro | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- record jumping [ADO]
- jumping to record [ADO]
ms.assetid: 6caf6299-2eea-4d34-9b0e-b75aab07b740
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7185dca3db146e7c17f41cb0f0c5376274fe3634
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63161483"
---
# <a name="jumping-to-a-record"></a>Saltar para um registro
O [mova](../../../ado/reference/ado-api/move-method-ado.md) método permite que você mova para frente ou para trás na **conjunto de registros** um número especificado de registros usando a sintaxe a seguir:  
  
```  
oRs.Move NumRecords, Start  
```  
  
## <a name="remarks"></a>Comentários  
 O **mova** método tem suporte em todos os **Recordset** objetos.  
  
 Se o *NumRecords* argumento for maior que zero, a posição atual do registro move para frente (até o final do **Recordset**). Se *NumRecords* é menor que zero, a posição atual do registro move para trás (até o início de **Recordset**).  
  
 Se o **mova** chamada moveria a posição do registro atual para um ponto antes do primeiro registro, o ADO define o registro atual para a posição antes do primeiro registro na **conjunto de registros** (**BOF** está **verdadeiro**). Tentativa de mover quando com versões anteriores a **BOF** propriedade já está **verdadeiro** gera um erro.  
  
 Se o **mova** chamada moveria a posição do registro atual para um ponto após o último registro, o ADO define o registro atual para a posição após o último registro na **conjunto de registros** (**EOF** está **verdadeiro**). Tentativa de mover o encaminhamento quando o **EOF** propriedade já está **verdadeiro** gera um erro.  
  
 Chamar o **mova** método vazio **Recordset** objeto gera um erro.  
  
 Se você passar um indicador na *inicie* argumento, a movimentação é relativo ao registro com esse indicador, supondo que o **Recordset** objeto dá suporte a indicadores. Um indicador é obtido usando o [indicador](../../../ado/reference/ado-api/bookmark-property-ado.md) propriedade. Se não for especificado, a movimentação é relativo ao registro atual.  
  
 Se você estiver usando o **CacheSize** propriedade em cache localmente os registros do provedor, de passando um *NumRecords* argumento que move a posição atual do registro fora do grupo atual de registros armazenados em cache força o ADO para recuperar um novo grupo de registros, começando do registro de destino. O **CacheSize** propriedade determina o tamanho do grupo recém-recuperado e o registro de destino é o primeiro registro recuperado.
