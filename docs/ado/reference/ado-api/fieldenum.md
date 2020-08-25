---
description: FieldEnum
title: FieldEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- FieldEnum
helpviewer_keywords:
- FieldEnum enumeration [ADO]
ms.assetid: be4eda13-d4e4-4d6b-bb0d-3310b0a96fc2
author: rothja
ms.author: jroth
ms.openlocfilehash: cad540a13fbad480f795049df0d0150188df4283
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88775445"
---
# <a name="fieldenum"></a>FieldEnum
Especifica os campos especiais referenciados na coleção de [campos](./fields-collection-ado.md) de um objeto de [registro](./record-object-ado.md) .  
  
## <a name="remarks"></a>Comentários  
 Essas constantes fornecem um "atalho" para acessar campos especiais associados a um **registro**. Recupere o objeto [Field](./field-object.md) da coleção **Fields** e, em seguida, obtenha seu conteúdo com a propriedade [Value](./value-property-ado.md) do objeto **Field** .  
  
|Constante|Valor|Descrição|  
|--------------|-----------|-----------------|  
|**adDefaultStream**|-1|Faz referência ao campo que contém o objeto de [fluxo](./stream-object-ado.md) padrão associado a um **registro**.|  
|**adRecordURL**|-2|Faz referência ao campo que contém a cadeia de caracteres de URL absoluta para o **registro**atual.|