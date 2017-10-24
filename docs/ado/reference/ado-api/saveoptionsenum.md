---
title: SaveOptionsEnum | Microsoft Docs
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- SaveOptionsEnum
helpviewer_keywords:
- SaveOptionsEnum enumeration [ADO]
ms.assetid: 59339100-6e29-48d1-aea3-6873796d186b
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 97f3d76d9fed33de5ba79d84a062891316c70ae0
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="saveoptionsenum"></a>SaveOptionsEnum
Especifica se um arquivo deve ser criado ou substituído quando salvar uma [fluxo](../../../ado/reference/ado-api/stream-object-ado.md) objeto. Os valores podem ser **adSaveCreateNotExist** ou **adSaveCreateOverWrite**...  
  
|Constante|Valor|Description|  
|--------------|-----------|-----------------|  
|**adSaveCreateNotExist**|1|Padrão. Cria um novo arquivo, se o arquivo especificado pelo *FileName* parâmetro já não existe.|  
|**adSaveCreateOverWrite**|2|Substitui o arquivo com os dados de atualmente aberto **fluxo** do objeto, se o arquivo especificado pelo *Filename* já existe um parâmetro. Se o arquivo especificado pelo *Filename* parâmetro não existe, um novo arquivo é criado.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC equivalente  
 Constantes não têm equivalentes do ADO/WFC.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Método SaveToFile](../../../ado/reference/ado-api/savetofile-method.md)

