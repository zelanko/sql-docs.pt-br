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
author: markingmyname
ms.author: maghan
ms.openlocfilehash: e37bef50b77ded9d41fde856cbe4beebdf05cb9f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68119790"
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
  
  
