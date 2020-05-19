---
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
ms.openlocfilehash: 3423d215fa4a52286509769bb2ac0b75d2283a02
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82755838"
---
# <a name="saveoptionsenum"></a>SaveOptionsEnum
Especifica se um arquivo deve ser criado ou substituído ao salvar de um objeto de [fluxo](../../../ado/reference/ado-api/stream-object-ado.md) . Os valores podem ser **adSaveCreateNotExist** ou **adSaveCreateOverWrite**..  
  
|Constante|Valor|Descrição|  
|--------------|-----------|-----------------|  
|**adSaveCreateNotExist**|1|Padrão. Cria um novo arquivo se o arquivo especificado pelo parâmetro *filename* ainda não existir.|  
|**adSaveCreateOverWrite**|2|Substitui o arquivo pelos dados do objeto de **fluxo** aberto no momento, se o arquivo especificado pelo parâmetro *filename* já existir. Se o arquivo especificado pelo parâmetro *filename* não existir, um novo arquivo será criado.|  
  
## <a name="adowfc-equivalent"></a>Equivalente do ADO/WFC  
 Essas constantes não têm equivalentes ADO/WFC.  
  
## <a name="applies-to"></a>Aplica-se A  
 [Método SaveToFile](../../../ado/reference/ado-api/savetofile-method.md)
