---
description: SeekEnum
title: SeekEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- SeekEnum
helpviewer_keywords:
- SeekEnum enumeration [ADO]
ms.assetid: f0ec0c92-8253-47c6-9a14-e5dbccbad219
author: rothja
ms.author: jroth
ms.openlocfilehash: 345e6dff5c2bc372f06eb386a4546a61b9e5a1bb
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88989147"
---
# <a name="seekenum"></a>SeekEnum
Especifica o tipo de [busca](./seek-method.md) a ser executada.  
  
|Constante|Valor|Descrição|  
|--------------|-----------|-----------------|  
|**adSeekFirstEQ**|1|Busca a primeira chave igual a *keyValues*.|  
|**adSeekLastEQ**|2|Busca a última chave igual aos *valores*de tecla.|  
|**adSeekAfterEQ**|4|Busca uma chave igual a *keyvalores* ou apenas depois de onde a correspondência teria ocorrido.|  
|**adSeekAfter**|8|Busca uma chave logo após a ocorrência de uma correspondência com os *valores* de chaves.|  
|**adSeekBeforeEQ**|16|Busca uma chave igual a *keyValues*ou logo antes de onde essa correspondência teria ocorrido.|  
|**adSeekBefore**|32|Busca uma chave antes de onde houve uma correspondência com os *valores* .|  
  
## <a name="adowfc-equivalent"></a>Equivalente do ADO/WFC  
 Pacote: **com. ms. wfc. Data**  
  
|Constante|  
|--------------|  
|AdoEnums.Seek.FIRSTEQ|  
|AdoEnums.Seek.LASTEQ|  
|AdoEnums.Seek.AFTEREQ|  
|AdoEnums.Seek.AFTER|  
|AdoEnums.Seek.BEFOREEQ|  
|AdoEnums.Seek.BEFORE|  
  
## <a name="applies-to"></a>Aplica-se A  
 [Método Seek](./seek-method.md)