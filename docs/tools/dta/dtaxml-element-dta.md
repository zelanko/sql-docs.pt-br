---
title: Elemento DTAXML (DTA)
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- DTAXML element
ms.assetid: 3d9942ed-8a27-40db-a7c9-808984d914a2
author: markingmyname
ms.author: maghan
ms.manager: jroth
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.openlocfilehash: aeb5bfc3544d5de783a40fcfe8692a466fee6b40
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "75307729"
---
# <a name="dtaxml-element-dta"></a>Elemento DTAXML (DTA)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

O elemento raiz de um arquivo de entrada ou saída XML do Orientador de Otimização do Mecanismo de Banco de Dados, **DTAXML** , contém todos os elementos que descrevem a entrada e a saída de ajuste geradas pelo Orientador.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
<DTAXML   
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"   
    xmlns="https://schemas.microsoft.com/sqlserver/2004/07/dta">  
    ...code removed here...  
</DTAXML>  
```  
  
## <a name="element-attributes"></a>Atributos do elemento  
  
|Atributo|DESCRIÇÃO|  
|---------------|-----------------|  
|**xmlns:xsi**|Obrigatórios. Identifica o namespace da instância do esquema XML. Os atributos deste espaço para namespace são usados como referência ao esquema que é utilizado para validar o arquivo XML do Orientador de Otimização do Mecanismo de Banco de Dados.<br /><br /> Valor obrigatório: [http://www.w3.org/2001/XMLSchema-instance](http://www.w3.org/2001/XMLSchema-instance)|  
|**xmlns**|Obrigatórios. Identifica o namespace do Orientador de Otimização do Mecanismo de Banco de Dados.<br /><br /> Se você editar o arquivo XML do Orientador de Otimização do Mecanismo de Banco de Dados usando o editor de XML no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], esse valor será usado pela Ajuda de F1 e pela Ajuda Dinâmica para localizar possíveis tópicos de referência nos Manuais Online do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .<br /><br /> Valor obrigatório:<br /><br /> do[Esquema XML do Orientador de Otimização do Mecanismo de Banco de Dados](https://go.microsoft.com/fwlink/?LinkId=43100)|  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|DESCRIÇÃO|  
|--------------------|-----------------|  
|**Comprimento e tipo de dados**|Nenhum.|  
|**Valor padrão**|Nenhum.|  
|**Ocorrência**|Obrigatória uma vez por arquivo XML DTA.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elementos|  
|------------------|--------------|  
|**Elemento pai**|Nenhum|  
|**Elementos filho**|[Elemento DTAInput &#40;DTA&#41;](../../tools/dta/dtainput-element-dta.md)<br /><br /> Elemento **DTAOutput** (consulte [Esquema XML do Orientador de Otimização do Mecanismo de Banco de Dados](https://schemas.microsoft.com/sqlserver/) para obter informações)|  
  
## <a name="remarks"></a>Comentários  
 Para obter mais informações sobre namespaces XML, consulte [Namespaces em um documento XML](https://go.microsoft.com/fwlink/?LinkId=7341) na Biblioteca MSDN do [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
## <a name="example"></a>Exemplo  
 Para obter exemplos de elementos **DTAXML** típicos, consulte [Exemplos de arquivo de entrada XML &#40;DTA&#41;](../../tools/dta/xml-input-file-samples-dta.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Referência do arquivo de entrada XML &#40;Orientador de Otimização do Mecanismo de Banco de Dados&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)   
 [Iniciar e usar o Orientador de Otimização do Mecanismo de Banco de Dados](../../relational-databases/performance/start-and-use-the-database-engine-tuning-advisor.md)  
  
  
