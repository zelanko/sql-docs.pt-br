---
title: Arquivo de elemento (DTA) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.component: dta
ms.reviewer: ''
ms.suite: sql
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
ms.openlocfilehash: ce2d29b97757b054cd66a245644f37122d355d26
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MTE
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="file-element-dta"></a>Elemento de arquivo (DTA)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Especifica o arquivo da carga de trabalho. A carga de trabalho é um conjunto de instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] executadas em um ou mais bancos de dados a serem ajustados. Os arquivos de carga de trabalho podem ser scripts [!INCLUDE[tsql](../../includes/tsql-md.md)] (.sql) ou arquivos de rastreamento (.trc). Para obter mais informações, veja[Iniciar e usar o Orientador de Otimização do Mecanismo de Banco de Dados](../../relational-databases/performance/start-and-use-the-database-engine-tuning-advisor.md).  
  
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
|**Comprimento e tipo de dados**|Use o tipo de dados **string** para especificar o caminho de diretório para o arquivo de carga de trabalho. Por exemplo:<br /><br /> `<File>C:\Tuning\tun.sql</File>`<br /><br /> Observe que o limite de comprimento é aplicado pelo servidor.|  
|**Valor padrão**|Nenhum.|  
|**Ocorrência**|Exigido uma vez se não houver outro tipo de carga de trabalho especificada. É preciso especificar um elemento filho **EventString**, **File**ou **Database** para o pai **Workload** , mas só pode ser usado um tipo. Por exemplo, se uma carga de trabalho com o elemento **File** for especificada, não será possível especificar uma carga de trabalho com o elemento **Database** no mesmo arquivo de entrada XML.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elementos|  
|------------------|--------------|  
|**Elemento pai**|[Elemento Workload &#40;DTA&#41;](../../tools/dta/workload-element-dta.md)|  
|**Elementos filho**|Nenhum.|  
  
## <a name="example"></a>Exemplo  
 Para obter um exemplo de uso desse elemento, veja [Exemplo de arquivos de entrada XML simples &#40;DTA&#41;](../../tools/dta/simple-xml-input-file-sample-dta.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Referência do arquivo de entrada XML &#40;Orientador de Otimização do Mecanismo de Banco de Dados&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
