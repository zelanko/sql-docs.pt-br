---
title: Elemento DTAInput (DTA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- XML
helpviewer_keywords:
- DTAInput element
ms.assetid: 40c19abf-ded5-43de-be96-5b43b1b81b03
caps.latest.revision: 13
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 7b414d14cf69815086973849d5e0f6b3badb6b3b
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36013478"
---
# <a name="dtainput-element-dta"></a>Elemento DTAInput (DTA)
  Contém a definição de entrada XML para o Orientador de Otimização do Mecanismo de Banco de Dados.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
<DTAXML>  
    <DTAInput>  
    ...code removed here...  
    </DTAInput>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Características|Description|  
|---------------------|-----------------|  
|**Comprimento e tipo de dados**|Nenhum.|  
|**Valor padrão**|Nenhum.|  
|**Ocorrência**|Opcional uma vez por elemento **DTAXML** .|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elementos|  
|------------------|--------------|  
|**Elemento pai**|[Elemento DTAXML &#40;DTA&#41;](dtaxml-element-dta.md)|  
|**Elementos filho**|[Elemento Server &#40;DTA&#41;](server-element-dta.md)<br /><br /> [Elemento de carga de trabalho &#40;DTA&#41;](workload-element-dta.md)<br /><br /> [Elemento TuningOptions &#40;DTA&#41;](tuningoptions-element-dta.md)<br /><br /> [Elemento de configuração &#40;DTA&#41;](configuration-element-dta.md)|  
  
## <a name="remarks"></a>Remarks  
 Esse elemento é a raiz da hierarquia de esquema de entrada do Orientador de Otimização do Mecanismo de Banco de Dados. Uma entrada para o Orientador de Otimização do Mecanismo de Banco de Dados pode consistir em argumentos que especificam os servidores cujo banco de dados serão ajustados, cargas de trabalho, opções de ajuste ou configuração especificada pelo usuário.  
  
## <a name="example"></a>Exemplo  
 Para obter um exemplo do elemento **DTAInput**, veja [Exemplo de arquivos de entrada XML simples &#40;DTA&#41;](simple-xml-input-file-sample-dta.md).  
  
## <a name="see-also"></a>Consulte também  
 [Referência do arquivo de entrada XML &#40;Orientador de Otimização do Mecanismo de Banco de Dados&#41;](xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  