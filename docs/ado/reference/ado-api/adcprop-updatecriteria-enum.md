---
title: ADCPROP_UPDATECRITERIA_ENUM | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 12d960e8fcd5e1f27ea8198ce52e080f6fddf7c2
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67921414"
---
# <a name="adcprop_updatecriteria_enum"></a>ADCPROP_UPDATECRITERIA_ENUM
Especifica quais campos podem ser usados para detectar conflitos durante uma atualização otimista de uma linha da fonte de dados com um objeto [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) .  
  
 Use essas constantes com a propriedade dinâmica "**Atualizar critérios**" do **conjunto de registros** , que é referenciada no índice de [propriedades dinâmicas do ADO](../../../ado/reference/ado-api/ado-dynamic-property-index.md) e documentada no [serviço de cursor da Microsoft para obter OLE DB](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md) documentação.  
  
|Constante|Valor|DESCRIÇÃO|  
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
