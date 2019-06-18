---
title: Elemento DTAInput (DTA) | Microsoft Docs
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
- DTAInput element
ms.assetid: 40c19abf-ded5-43de-be96-5b43b1b81b03
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d77f9a70ade63a2e8fdf1d063932b315d9f4656e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62650995"
---
# <a name="dtainput-element-dta"></a>Elemento DTAInput (DTA)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Contém a definição de entrada XML para o Orientador de Otimização do Mecanismo de Banco de Dados.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
<DTAXML>  
    <DTAInput>  
    ...code removed here...  
    </DTAInput>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Características|Descrição|  
|---------------------|-----------------|  
|**Comprimento e tipo de dados**|Nenhum.|  
|**Valor padrão**|Nenhum.|  
|**Ocorrência**|Opcional uma vez por elemento **DTAXML** .|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elementos|  
|------------------|--------------|  
|**Elemento pai**|[Elemento DTAXML &#40;DTA&#41;](../../tools/dta/dtaxml-element-dta.md)|  
|**Elementos filho**|[Elemento Server &#40;DTA&#41;](../../tools/dta/server-element-dta.md)<br /><br /> [Elemento Workload &#40;DTA&#41;](../../tools/dta/workload-element-dta.md)<br /><br /> [Elemento TuningOptions &#40;DTA&#41;](../../tools/dta/tuningoptions-element-dta.md)<br /><br /> [Elemento Configuration &#40;DTA&#41;](../../tools/dta/configuration-element-dta.md)|  
  
## <a name="remarks"></a>Remarks  
 Esse elemento é a raiz da hierarquia de esquema de entrada do Orientador de Otimização do Mecanismo de Banco de Dados. Uma entrada para o Orientador de Otimização do Mecanismo de Banco de Dados pode consistir em argumentos que especificam os servidores cujo banco de dados serão ajustados, cargas de trabalho, opções de ajuste ou configuração especificada pelo usuário.  
  
## <a name="example"></a>Exemplo  
 Para obter um exemplo do elemento **DTAInput**, veja [Exemplo de arquivos de entrada XML simples &#40;DTA&#41;](../../tools/dta/simple-xml-input-file-sample-dta.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Referência do arquivo de entrada XML &#40;Orientador de Otimização do Mecanismo de Banco de Dados&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
