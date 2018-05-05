---
title: DESCARTAR ESTRUTURA DE MINERAÇÃO (DMX) | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- DROP MINING STRUCTURE
- DROP_MINING_STRUCTURE
dev_langs:
- DMX
helpviewer_keywords:
- removing mining structures
- dropping mining structures
- DROP MINING STRUCTURE statement
- deleting mining structures
- mining structures [DMX], deleting
ms.assetid: 30df8c36-3a15-4d8c-98f3-0f8917be9fc8
caps.latest.revision: 15
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: 9d1317af40481261b60c375fb690260dd3173f6d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="drop-mining-structure-dmx"></a>DROP MINING STRUCTURE (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Ignora a estrutura de mineração especificada do banco de dados. Todos os modelos de mineração associados à estrutura são igualmente ignorados no banco de dados.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
DROP MINING STRUCTURE <structure>  
```  
  
## <a name="arguments"></a>Argumentos  
 *estrutura*  
 Identificador de estrutura.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir ignora a estrutura de mineração de Novo endereçamento do banco de dados.  
  
```  
DROP MINING STRUCTURE [New Mailing]  
```  
  
## <a name="see-also"></a>Consulte também  
 [Extensões de mineração de dados &#40;DMX&#41; instruções de definição de dados](../dmx/dmx-statements-data-definition.md)   
 [Extensões de mineração de dados &#40;DMX&#41; instruções de manipulação de dados](../dmx/dmx-statements-data-manipulation.md)   
 [Extensões de mineração de dados & #40; DMX & #41; Referência de instrução](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
