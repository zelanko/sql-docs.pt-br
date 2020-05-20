---
title: Elemento Nome do servidor (DTA)
description: No utilitário dta, o elemento Name de Server contém o nome do servidor no qual residem os bancos de dados que você deseja ajustar.
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- Name element
ms.assetid: 4c94754d-6d62-4357-8ce7-f107ebf90c71
author: markingmyname
ms.author: maghan
ms.manager: jroth
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 03/01/2017
ms.openlocfilehash: 4efa5cd3285a9247c9319db789e4c17d66cacb29
ms.sourcegitcommit: b8933ce09d0e631d1183a84d2c2ad3dfd0602180
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/13/2020
ms.locfileid: "83151224"
---
# <a name="name-element-for-server-dta"></a>Elemento Nome do servidor (DTA)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Contém o nome do servidor em que residem os bancos de dados que você deseja ajustar.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
...code removed here...  
<Server>  
    <Name>...</Name>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|**Comprimento e tipo de dados**|**string**, entre 1 e 255 caracteres.|  
|**Valor padrão**|Nenhum.|  
|**Ocorrência**|Exigido uma vez por elemento de **Servidor** .|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elementos|  
|------------------|--------------|  
|**Elemento pai**|[Elemento Server &#40;DTA&#41;](../../tools/dta/server-element-dta.md)|  
|**Elementos filho**|Nenhum.|  
  
## <a name="example"></a>Exemplo  
 Para obter um exemplo de como esse elemento **Name** é usado, consulte [Elemento Server &#40;DTA&#41;](../../tools/dta/server-element-dta.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Referência do arquivo de entrada XML &#40;Orientador de Otimização do Mecanismo de Banco de Dados&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
