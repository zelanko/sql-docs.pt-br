---
title: Arquivo de elemento (DTA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- File element
ms.assetid: 73dce835-9a80-4aef-8e0f-9dcf07dd5b80
caps.latest.revision: 15
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 0cf6b51bf7f6d4f90a8a575326beb457e42e5d99
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37159757"
---
# <a name="file-element-dta"></a>Elemento de arquivo (DTA)
  Especifica o arquivo da carga de trabalho. A carga de trabalho é um conjunto de instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] executadas em um ou mais bancos de dados a serem ajustados. Os arquivos de carga de trabalho podem ser scripts [!INCLUDE[tsql](../../includes/tsql-md.md)] (.sql) ou arquivos de rastreamento (.trc). Para obter mais informações, consulte [Iniciar e usar o Orientador de Otimização do Mecanismo de Banco de Dados](../../relational-databases/performance/start-and-use-the-database-engine-tuning-advisor.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
<DTAInput>  
  <Server>...</Server>  
  <Workload>  
    <File>...</File>  
  </Workload>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|**Comprimento e tipo de dados**|Use o tipo de dados `string` para especificar o caminho de diretório para o arquivo de carga de trabalho. Por exemplo:<br /><br /> `<File>C:\Tuning\tun.sql</File>`<br /><br /> O limite de comprimento é aplicado pelo servidor.|  
|**Valor padrão**|Nenhum.|  
|**Ocorrência**|Exigido uma vez se não houver outro tipo de carga de trabalho especificada. É preciso especificar um elemento filho **EventString**, **File**ou **Database** para o pai **Workload** , mas só pode ser usado um tipo. Por exemplo, se uma carga de trabalho com o elemento **File** for especificada, não será possível especificar uma carga de trabalho com o elemento **Database** no mesmo arquivo de entrada XML.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elementos|  
|------------------|--------------|  
|**Elemento pai**|[Elemento de carga de trabalho &#40;DTA&#41;](workload-element-dta.md)|  
|**Elementos filho**|Nenhum.|  
  
## <a name="example"></a>Exemplo  
 Para obter um exemplo de uso desse elemento, veja [Exemplo de arquivos de entrada XML simples &#40;DTA&#41;](simple-xml-input-file-sample-dta.md).  
  
## <a name="see-also"></a>Consulte também  
 [Referência do arquivo de entrada XML &#40;Orientador de Otimização do Mecanismo de Banco de Dados&#41;](xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
