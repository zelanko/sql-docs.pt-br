---
title: SaveOptionsEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- SaveOptionsEnum
helpviewer_keywords:
- SaveOptionsEnum enumeration [ADO]
ms.assetid: 59339100-6e29-48d1-aea3-6873796d186b
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5eb423643748725b1be3ac1c809e56efbee209d6
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/18/2018
---
# <a name="saveoptionsenum"></a>SaveOptionsEnum
Especifica se um arquivo deve ser criado ou substituído quando salvar uma [fluxo](../../../ado/reference/ado-api/stream-object-ado.md) objeto. Os valores podem ser **adSaveCreateNotExist** ou **adSaveCreateOverWrite**...  
  
|Constante|Value|Description|  
|--------------|-----------|-----------------|  
|**adSaveCreateNotExist**|1|Padrão. Cria um novo arquivo, se o arquivo especificado pelo *FileName* parâmetro já não existe.|  
|**adSaveCreateOverWrite**|2|Substitui o arquivo com os dados de atualmente aberto **fluxo** do objeto, se o arquivo especificado pelo *Filename* já existe um parâmetro. Se o arquivo especificado pelo *Filename* parâmetro não existe, um novo arquivo é criado.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC equivalente  
 Constantes não têm equivalentes do ADO/WFC.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Método SaveToFile](../../../ado/reference/ado-api/savetofile-method.md)
