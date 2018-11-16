---
title: Elemento DatabaseToConnect (DTA) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- DatabaseToConnect element
ms.assetid: 65153a66-3aee-4429-99b7-0816ac23c285
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f6c06339b7e38272e1a6923183f79869cbdd871c
ms.sourcegitcommit: 0f7cf9b7ab23df15624d27c129ab3a539e8b6457
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2018
ms.locfileid: "51291200"
---
# <a name="databasetoconnect-element-dta"></a>Elemento DatabaseToConnect (DTA)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Especifica o primeiro banco de dados que o Orientador de Otimização do Mecanismo de Banco de Dados conecta ao ajustar uma carga de trabalho.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
    <TuningOptions>  
...code removed here...  
      <DatabaseToConnect>...</DatabaseToConnect>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|**Comprimento e tipo de dados**|**string**, comprimento ilimitado.|  
|**Valor padrão**|Nenhum.|  
|**Ocorrência**|Opcional. Pode ser usado uma vez para cada elemento **TuningOptions** .|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elementos|  
|------------------|--------------|  
|**Elemento pai**|[Elemento TuningOptions &#40;DTA&#41;](../../tools/dta/tuningoptions-element-dta.md)|  
|**Elementos filho**|None|  
  
## <a name="remarks"></a>Remarks  
 Use o **DatabaseToConnect** para especificar o nome do primeiro banco de dados que o Orientador de Otimização do Mecanismo de Banco de Dados conectará quando iniciar a sessão de ajuste. Você pode especificar apenas um banco de dados com esse elemento. Se forem especificados vários nomes de banco de dados, o Orientador de Otimização do Mecanismo de Banco de Dados retornará um erro.  
  
## <a name="example"></a>Exemplo  
 Para obter um exemplo de uso, veja a [Amostra do arquivo de entrada XML com carga de trabalho embutida &#40;DTA&#41;](../../tools/dta/xml-input-file-sample-with-inline-workload-dta.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Referência do arquivo de entrada XML &#40;Orientador de Otimização do Mecanismo de Banco de Dados&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
