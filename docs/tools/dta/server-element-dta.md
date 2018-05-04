---
title: Elemento de servidor (DTA) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
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
- Server element
ms.assetid: 9fe0bfb4-3aa6-4eb2-a83e-c0d0e7d4e9f6
caps.latest.revision: 16
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 3bd0fb4b152c253cff5351138dccc41b397b6c2f
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MTE
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="server-element-dta"></a>Elemento de servidor (DTA)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
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
|**Ocorrência**|Necessário uma vez para cada elemento **DTAInput** .|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elementos|  
|------------------|--------------|  
|**Elemento pai**|[Elemento DTAInput &#40;DTA&#41;](../../tools/dta/dtainput-element-dta.md)|  
|**Elementos filho**|[Elemento Name para Server &#40;DTA&#41;](../../tools/dta/name-element-for-server-dta.md)<br /><br /> [Elemento Database para Server &#40;DTA&#41;](../../tools/dta/database-element-for-server-dta.md)|  
  
## <a name="remarks"></a>Remarks  
 Você pode especificar apenas um elemento **Server** para o elemento **DTAInput** . Esse elemento é chamado **ServerDetailsTypecomplexType** no esquema XML do DTA. Não confunda esse elemento **Server** com aquele que é o filho do elemento **Configuration**. Para obter mais informações, veja [Elemento Server para configuração &#40;DTA&#41;](../../tools/dta/server-element-for-configuration-dta.md).  
  
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
  
## <a name="see-also"></a>Consulte Também  
 [Referência do arquivo de entrada XML &#40;Orientador de Otimização do Mecanismo de Banco de Dados&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
