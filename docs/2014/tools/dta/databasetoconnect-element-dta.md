---
title: Elemento DatabaseToConnect (DTA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
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
ms.openlocfilehash: 4fef2df598d96b33def41f27345f88226fd4c6b5
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63185418"
---
# <a name="databasetoconnect-element-dta"></a>Elemento DatabaseToConnect (DTA)
  Especifica o primeiro banco de dados que o Orientador de Otimização do Mecanismo de Banco de Dados conecta ao ajustar uma carga de trabalho.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
    <TuningOptions>  
...code removed here...  
      <DatabaseToConnect>...</DatabaseToConnect>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|DESCRIÇÃO|  
|--------------------|-----------------|  
|**Comprimento e tipo de dados**|
  `string`, comprimento ilimitado.|  
|**Valor padrão**|Nenhum.|  
|**Ocorrência**|Opcional. Pode ser usado uma vez para cada elemento `TuningOptions`.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elementos|  
|------------------|--------------|  
|**Elemento pai**|[Elemento TuningOptions &#40;DTA&#41;](tuningoptions-element-dta.md)|  
|**Elementos filho**|Nenhum|  
  
## <a name="remarks"></a>Comentários  
 Use o `DatabaseToConnect` para especificar o nome do primeiro banco de dados que o Orientador de Otimização do Mecanismo de Banco de Dados conectará quando iniciar a sessão de ajuste. Você pode especificar apenas um banco de dados com esse elemento. Se forem especificados vários nomes de banco de dados, o Orientador de Otimização do Mecanismo de Banco de Dados retornará um erro.  
  
## <a name="example"></a>Exemplo  
 Para obter um exemplo de uso, veja a [Amostra do arquivo de entrada XML com carga de trabalho embutida &#40;DTA&#41;](xml-input-file-sample-with-inline-workload-dta.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Referência do arquivo de entrada XML &#40;Orientador de Otimização do Mecanismo de Banco de Dados&#41;](xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
