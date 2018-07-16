---
title: Elemento DTAXML (DTA) | Microsoft Docs
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
- DTAXML element
ms.assetid: 3d9942ed-8a27-40db-a7c9-808984d914a2
caps.latest.revision: 18
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d460721fd138c0629322687b1160b8c75cdd0cfa
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37177133"
---
# <a name="dtaxml-element-dta"></a>Elemento DTAXML (DTA)
  O elemento raiz de um arquivo de entrada ou saída XML do Orientador de Otimização do Mecanismo de Banco de Dados, **DTAXML** , contém todos os elementos que descrevem a entrada e a saída de ajuste geradas pelo Orientador.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
<DTAXML   
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"   
    xmlns="http://schemas.microsoft.com/sqlserver/2004/07/dta">  
    ...code removed here...  
</DTAXML>  
```  
  
## <a name="element-attributes"></a>Atributos do elemento  
  
|attribute|Description|  
|---------------|-----------------|  
|`xmlns:xsi`|Obrigatórios. Identifica o namespace da instância do esquema XML. Os atributos deste espaço para namespace são usados como referência ao esquema que é utilizado para validar o arquivo XML do Orientador de Otimização do Mecanismo de Banco de Dados.<br /><br /> Valor obrigatório: [http://www.w3.org/2001/XMLSchema-instance](http://www.w3.org/2001/XMLSchema-instance)|  
|`xmlns`|Obrigatórios. Identifica o namespace do Orientador de Otimização do Mecanismo de Banco de Dados.<br /><br /> Se você editar o arquivo XML do Orientador de Otimização do Mecanismo de Banco de Dados usando o editor de XML no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], esse valor será usado pela Ajuda de F1 e pela Ajuda Dinâmica para localizar possíveis tópicos de referência nos Manuais Online do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .<br /><br /> Valor obrigatório:<br /><br /> do[Esquema XML do Orientador de Otimização do Mecanismo de Banco de Dados](http://go.microsoft.com/fwlink/?LinkId=43100) |  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|**Comprimento e tipo de dados**|Nenhum.|  
|**Valor padrão**|Nenhum.|  
|**Ocorrência**|Obrigatória uma vez por arquivo XML DTA.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elementos|  
|------------------|--------------|  
|**Elemento pai**|Nenhum|  
|**Elementos filho**|[Elemento DTAInput &#40;DTA&#41;](dtainput-element-dta.md)<br /><br /> `DTAOutput` Elemento (consulte [esquema XML do Orientador de otimização de mecanismo de banco de dados](http://schemas.microsoft.com/sqlserver/) para obter informações)|  
  
## <a name="remarks"></a>Remarks  
 Para obter mais informações sobre namespaces XML, consulte [Namespaces em um documento XML](http://go.microsoft.com/fwlink/?LinkId=7341) na Biblioteca MSDN do [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
## <a name="example"></a>Exemplo  
 Para obter exemplos de elementos **DTAXML** típicos, consulte [Exemplos de arquivo de entrada XML &#40;DTA&#41;](xml-input-file-samples-dta.md).  
  
## <a name="see-also"></a>Consulte também  
 [Referência do arquivo de entrada XML &#40;orientador de otimização do mecanismo de banco de dados&#41;](xml-input-file-reference-database-engine-tuning-advisor.md)   
 [Iniciar e usar o Orientador de Otimização do Mecanismo de Banco de Dados](../../relational-databases/performance/start-and-use-the-database-engine-tuning-advisor.md)  
  
  
