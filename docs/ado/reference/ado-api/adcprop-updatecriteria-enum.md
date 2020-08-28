---
description: ADCPROP_UPDATECRITERIA_ENUM
title: ADCPROP_UPDATECRITERIA_ENUM | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ADCPROP_UPDATECRITERIA_ENUM
helpviewer_keywords:
- ADCPROP_UPDATECRITERIA_ENUM [ADO]
ms.assetid: 33fd7b65-2ec8-4f62-91a7-630b5dab1aa2
author: rothja
ms.author: jroth
ms.openlocfilehash: 3711266f3658fe2366caa56c6afba07d6b63c4c9
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88976807"
---
# <a name="adcprop_updatecriteria_enum"></a>ADCPROP_UPDATECRITERIA_ENUM
Especifica quais campos podem ser usados para detectar conflitos durante uma atualização otimista de uma linha da fonte de dados com um objeto [Recordset](./recordset-object-ado.md) .  
  
 Use essas constantes com a propriedade dinâmica "**Atualizar critérios**" do **conjunto de registros** , que é referenciada no índice de [propriedades dinâmicas do ADO](./ado-dynamic-property-index.md) e documentada no [serviço de cursor da Microsoft para obter OLE DB](../../guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md) documentação.  
  
|Constante|Valor|Descrição|  
|--------------|-----------|-----------------|  
|**adCriteriaAllCols**|1|Detecta conflitos se qualquer coluna da linha de fonte de dados tiver sido alterada.|  
|**adCriteriaKey**|0|Detecta conflitos se a coluna de chave da linha de fonte de dados foi alterada, o que significa que a linha foi excluída.|  
|**adCriteriaTimeStamp**|3|Detecta conflitos se o carimbo de data/hora da linha da fonte de dados foi alterado, o que significa que a linha foi acessada depois que o **conjunto de registros** foi obtido.|  
|**adCriteriaUpdCols**|2|Detecta conflitos se qualquer uma das colunas da linha de fonte de dados que correspondem aos campos atualizados do **conjunto de registros** tiver sido alterada.|  
  
## <a name="adowfc-equivalent"></a>Equivalente do ADO/WFC  
 Pacote: **com. ms. wfc. Data**  
  
|Constante|  
|--------------|  
|AdoEnums.AdcPropUpdateCriteria.ALLCOLS|  
|AdoEnums.AdcPropUpdateCriteria.KEY|  
|AdoEnums.AdcPropUpdateCriteria.TIMESTAMP|  
|AdoEnums.AdcPropUpdateCriteria.UPDCOLS|