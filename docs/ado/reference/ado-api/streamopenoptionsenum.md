---
description: StreamOpenOptionsEnum
title: StreamOpenOptionsEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- StreamOpenOptionsEnum
helpviewer_keywords:
- StreamOpenOptionsEnum enumeration [ADO]
ms.assetid: 85b6c57f-47ed-46ba-bd92-07882ae9e9d2
author: rothja
ms.author: jroth
ms.openlocfilehash: 8f3865a3b0e550e7e3fe4887fb948bca72eadf1b
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88988497"
---
# <a name="streamopenoptionsenum"></a>StreamOpenOptionsEnum
Especifica as opções para abrir um objeto de [fluxo](./stream-object-ado.md) . Os valores podem ser combinados com uma operação ou.  
  
|Constante|Valor|Descrição|  
|--------------|-----------|-----------------|  
|**adOpenStreamAsync**|1|Abre o objeto de **fluxo** no modo assíncrono.|  
|**adOpenStreamFromRecord**|4|Identifica o conteúdo do parâmetro de *origem* como um objeto de [registro](./record-object-ado.md) já aberto. O comportamento padrão é tratar a *origem* como uma URL que aponta diretamente para um nó em uma estrutura de árvore. O fluxo padrão associado a esse nó é aberto.|  
|**adOpenStreamUnspecified**|-1|Padrão. Especifica a abertura do objeto de **fluxo** com opções padrão.|  
  
## <a name="adowfc-equivalent"></a>Equivalente do ADO/WFC  
 Essas constantes não têm equivalentes ADO/WFC.  
  
## <a name="applies-to"></a>Aplica-se A  
 [Método Open (Fluxo do ADO)](./open-method-ado-stream.md)