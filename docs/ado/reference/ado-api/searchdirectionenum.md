---
description: SearchDirectionEnum
title: SearchDirectionEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- SearchDirectionEnum
helpviewer_keywords:
- SearchDirectionEnum enumeration [ADO]
ms.assetid: 81272ae3-2165-4f4e-adfe-9ede0368cb17
author: rothja
ms.author: jroth
ms.openlocfilehash: dc30978b5ce157aa103e41f2b68dd8b36864f25a
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88989219"
---
# <a name="searchdirectionenum"></a>SearchDirectionEnum
Especifica a direção de uma pesquisa de registro em um [conjunto de registros](./recordset-object-ado.md).  
  
|Constante|Valor|Descrição|  
|--------------|-----------|-----------------|  
|**adSearchBackward**|-1|Pesquisa retroativamente, parando no início do **conjunto de registros**. Se uma correspondência não for encontrada, o ponteiro de registro será posicionado em [BOF](./bof-eof-properties-ado.md).|  
|**adSearchForward**|1|Pesquisa para frente, parando no final do **conjunto de registros**. Se uma correspondência não for encontrada, o ponteiro de registro será posicionado em [EOF](./bof-eof-properties-ado.md).|  
  
## <a name="adowfc-equivalent"></a>Equivalente do ADO/WFC  
 Pacote: **com. ms. wfc. Data**  
  
|Constante|  
|--------------|  
|AdoEnums.SearchDirection.BACKWARD|  
|AdoEnums.SearchDirection.FORWARD|  
  
## <a name="applies-to"></a>Aplica-se A  
 [Método Find (ADO)](./find-method-ado.md)