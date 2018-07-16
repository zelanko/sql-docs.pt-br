---
title: Elemento de servidor (DTA) | Microsoft Docs
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
- Server element
ms.assetid: 9fe0bfb4-3aa6-4eb2-a83e-c0d0e7d4e9f6
caps.latest.revision: 16
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: c152b69c2d19be43c833e2f6418225f233e46074
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37236036"
---
# <a name="server-element-dta"></a>Elemento de servidor (DTA)
  Contém a informações de identificação do servidor no qual residem os bancos de dados a serem ajustados.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
<DTAInput>  
    <Server>  
    ...code removed here...  
    </Server>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|**Comprimento e tipo de dados**|Nenhum.|  
|**Valor padrão**|Nenhum.|  
|**Ocorrência**|Obrigatório uma vez por `DTAInput` elemento.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elementos|  
|------------------|--------------|  
|**Elemento pai**|[Elemento DTAInput &#40;DTA&#41;](dtainput-element-dta.md)|  
|**Elementos filho**|[Nome de elemento para o servidor &#40;DTA&#41;](name-element-for-server-dta.md)<br /><br /> [Elemento Database para servidor &#40;DTA&#41;](database-element-for-server-dta.md)|  
  
## <a name="remarks"></a>Remarks  
 Você pode especificar apenas um `Server` elemento para o `DTAInput` elemento. Esse elemento é chamado **ServerDetailsTypecomplexType** no esquema XML do DTA. Não confunda esse `Server` elemento com aquele que é o filho do `Configuration` elemento. Para obter mais informações, veja [Elemento Server para configuração &#40;DTA&#41;](server-element-for-configuration-dta.md).  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir mostra como especificar a tabela **Sales.SalesPerson** no banco de dados **AdventureWorks** no SERVER001:  
  
```xml  
<Server>  
  <Name>SERVER001</Name>  
  <Database>  
    <Name>AdventureWorks</Name>  
    <Schema>  
      <Name>Sales</Name>  
      <Table>  
        <Name>SalesPerson</Name>  
      </Table>  
    </Schema>  
  </Database>  
</Server  
```  
  
## <a name="see-also"></a>Consulte também  
 [Referência do arquivo de entrada XML &#40;Orientador de Otimização do Mecanismo de Banco de Dados&#41;](xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
