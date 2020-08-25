---
description: SaveOptionsEnum
title: SaveOptionsEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
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
ms.openlocfilehash: edac11f61b003307703ec13daed8022b8af31bae
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88777555"
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