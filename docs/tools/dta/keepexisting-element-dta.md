---
title: Elemento KeepExisting (DTA)
description: No utilitário dta, o elemento KeepExisting especifica estruturas de design físico que Orientador de Otimização do Mecanismo de Banco de Dados retém quando gera recomendações.
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- KeepExisting element
ms.assetid: e67aae61-d06d-4a03-85ba-6516c3502dce
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 03/01/2017
ms.openlocfilehash: 9a9b112adc2f91dd6bdf68655148ba74c4204b8d
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85643845"
---
# <a name="keepexisting-element-dta"></a>Elemento KeepExisting (DTA)

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

Especifica as estruturas físicas de design (índices, exibições indexadas ou particionamento) que o Orientador de Otimização do Mecanismo de Banco de Dados deve reter ao gerar sua recomendação.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
<DTAInput>  
...code removed...  
    <TuningOptions>  
      <KeepExisting>...</KeepExisting>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|**Comprimento e tipo de dados**|**string**, o limite de tamanho é imposto pelo servidor.|  
|**Valores permitidos**|**NONE**<br /> Não existe nenhuma estrutura.<br /><br /> **ALL**<br /> Todas as estruturas existentes.<br /><br /> **ALIGNED**<br /> Todas as estruturas alinhadas por partição.<br /><br /> **CL_IDX**<br /> Todos os índices clusterizados em tabelas<br /><br /> **IDX**<br /> Todos os índices clusterizados e não cluster em tabelas<br /><br /> Use apenas um desses valores com este elemento.|  
|**Valor padrão**|Nenhum.|  
|**Ocorrência**|Opcional. Pode-se usar apenas uma vez para cada elemento de **TuningOptions** .|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elementos|  
|------------------|--------------|  
|**Elemento pai**|[Elemento TuningOptions &#40;DTA&#41;](../../tools/dta/tuningoptions-element-dta.md)|  
|**Elementos filho**|Nenhum.|  
  
## <a name="example"></a>Exemplo  
 Para obter um exemplo de uso desse elemento, veja [Exemplo de arquivos de entrada XML simples &#40;DTA&#41;](../../tools/dta/simple-xml-input-file-sample-dta.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Referência do arquivo de entrada XML &#40;Orientador de Otimização do Mecanismo de Banco de Dados&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
