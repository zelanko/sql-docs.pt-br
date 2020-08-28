---
description: SaveOptionsEnum
title: SaveOptionsEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- SaveOptionsEnum
helpviewer_keywords:
- SaveOptionsEnum enumeration [ADO]
ms.assetid: 59339100-6e29-48d1-aea3-6873796d186b
author: rothja
ms.author: jroth
ms.openlocfilehash: 56e16ff6ca93dde78531394dc474a2e5cc817348
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88989307"
---
# <a name="saveoptionsenum"></a>SaveOptionsEnum
Especifica se um arquivo deve ser criado ou substituído ao salvar de um objeto de [fluxo](./stream-object-ado.md) . Os valores podem ser **adSaveCreateNotExist** ou **adSaveCreateOverWrite**..  
  
|Constante|Valor|Descrição|  
|--------------|-----------|-----------------|  
|**adSaveCreateNotExist**|1|Padrão. Cria um novo arquivo se o arquivo especificado pelo parâmetro *filename* ainda não existir.|  
|**adSaveCreateOverWrite**|2|Substitui o arquivo pelos dados do objeto de **fluxo** aberto no momento, se o arquivo especificado pelo parâmetro *filename* já existir. Se o arquivo especificado pelo parâmetro *filename* não existir, um novo arquivo será criado.|  
  
## <a name="adowfc-equivalent"></a>Equivalente do ADO/WFC  
 Essas constantes não têm equivalentes ADO/WFC.  
  
## <a name="applies-to"></a>Aplica-se A  
 [Método SaveToFile](./savetofile-method.md)