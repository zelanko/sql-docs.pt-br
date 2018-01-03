---
title: "Condições de regras de negócios (Master Data Services) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: mds
ms.service: 
ms.component: non-specific
ms.reviewer: 
ms.suite: sql
ms.technology: master-data-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d2e0a8c3-4c2e-407c-856e-68d95ebda9ed
caps.latest.revision: "10"
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 9544b1b37f32ba54c3ea88b5df4091ce6c46d7a7
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="business-rule-conditions-master-data-services"></a>Condições de regras de negócio (Master Data Services)
  No [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], as condições das regras de negócio determinam as condições que devem ser verdadeiras para que uma ou mais ações sejam executadas.  
  
> [!NOTE]  
>  As condições são opcionais. Se você não especificar uma condição, as ações serão executadas a qualquer momento em que os dados forem validados em relação a regras de negócio.  
  
## <a name="business-rule-conditions"></a>Condições de regras de negócio  
  
|Nome da condição|Description|  
|--------------------|-----------------|  
|**é igual a**|O atributo selecionado **é igual a** um atributo específico, um valor de atributo específico ou está em branco.<br /><br /> Esta condição é válida para valores de texto, número, data e link.|  
|**não é igual a**|O atributo selecionado **não é igual a** um atributo específico, um valor de atributo específico ou está em branco.<br /><br /> Esta condição é válida para valores de texto, número, data e link.|  
|**é maior que**|O atributo selecionado **é maior que** um atributo específico, um valor de atributo específico ou está em branco.<br /><br /> Esta condição é válida para valores de texto, número e data.|  
|**é maior ou igual a**|O atributo selecionado **é maior ou igual a** um atributo específico, um valor de atributo específico ou está em branco.<br /><br /> Esta condição é válida para valores de texto, número e data.|  
|**é menor que**|O atributo selecionado **é menor que** um atributo específico, um valor de atributo específico ou está em branco.<br /><br /> Esta condição é válida para valores de texto, número e data.|  
|**é menor ou igual a**|O atributo selecionado **é menor ou igual a** um atributo específico, um valor de atributo específico ou está em branco.<br /><br /> Esta condição é válida para valores de texto, número e data.|  
|**inicia com**|O atributo selecionado **inicia com** um atributo específico, um valor de atributo específico ou está em branco.<br /><br /> Esta condição é válida para valores de texto e link.|  
|**não começa com**|O atributo selecionado **não começa com** um atributo específico, um valor de atributo específico ou está em branco.<br /><br /> Esta condição é válida para valores de texto e link.|  
|**termina com**|O atributo selecionado **termina com** um atributo específico, um valor de atributo específico ou está em branco.<br /><br /> Esta condição é válida para valores de texto e link.|  
|**não termina com**|O atributo selecionado **não termina com** um atributo específico, um valor de atributo específico ou está em branco.<br /><br /> Esta condição é válida para valores de texto e link.|  
|**contains**|O atributo selecionado **contém** um atributo específico, um valor de atributo específico ou está em branco.<br /><br /> Esta condição é válida para valores de texto e link.|  
|**não contém**|O atributo selecionado **não contém** um atributo específico, um valor de atributo específico ou está em branco.<br /><br /> Esta condição é válida para valores de texto e link.|  
|**contém o padrão**|O atributo selecionado **contém o padrão** de um atributo específico, um valor de atributo específico ou está em branco. Use expressões regulares do .NET Framework para especificar o padrão.<br /><br /> Para obter mais informações sobre expressões regulares, consulte [Elementos de linguagem das expressões regulares](http://go.microsoft.com/fwlink/?LinkId=164401) na Biblioteca MSDN.<br /><br /> Esta condição é válida para valores de texto e link.|  
|**não contém o padrão**|O atributo selecionado **não contém o padrão** um atributo específico, um valor de atributo específico ou está em branco. Use expressões regulares do .NET Framework para especificar o padrão.<br /><br /> Para obter mais informações sobre expressões regulares, consulte [Elementos de linguagem das expressões regulares](http://go.microsoft.com/fwlink/?LinkId=164401) na Biblioteca MSDN.<br /><br /> Esta condição é válida para valores de texto e link.|  
|**contém o subconjunto**|O atributo selecionado **contém o subconjunto** de um atributo específico ou de um valor de atributo específico. Você deve especificar a posição inicial para a pesquisa (por exemplo, 1 significa que a pesquisa inicia no primeiro caractere).<br /><br /> Esta condição é válida para valores de texto e link.|  
|**não contém o subconjunto**|O atributo selecionado **não contém o subconjunto** de um atributo específico ou de um valor de atributo específico. Você deve especificar a posição inicial para a pesquisa (por exemplo, 1 significa que a pesquisa inicia no primeiro caractere).<br /><br /> Esta condição é válida para valores de texto e link.|  
|**has changed**|O atributo selecionado **has changed** desde a última vez em que as regras de negócios foram aplicadas ao membro. Você deve especificar o grupo de alterações do qual o atributo é membro.<br /><br /> Para obter mais informações sobre grupos de controle de alterações, consulte [Adicionar atributos a um grupo de controle de alterações &#40;Master Data Services&#41;](../master-data-services/add-attributes-to-a-change-tracking-group-master-data-services.md).<br /><br /> Esta condição é válida para valores de texto, número, data e link.|  
|**não foi alterado**|O atributo selecionado **não foi alterado** desde a última vez em que as regras de negócios foram aplicadas ao membro. Você deve especificar o grupo de alterações do qual o atributo é membro.<br /><br /> Para obter mais informações sobre grupos de controle de alterações, consulte [Adicionar atributos a um grupo de controle de alterações &#40;Master Data Services&#41;](../master-data-services/add-attributes-to-a-change-tracking-group-master-data-services.md).<br /><br /> Esta condição é válida para valores de texto, número, data e link.|  
|**está entre**|O atributo selecionado **está entre** dois valores de atributo específicos.<br /><br /> Esta condição é válida para valores de texto, número e data.|  
|**não está entre**|O atributo selecionado **não está entre** dois valores de atributo específicos.<br /><br /> Esta condição é válida para valores de texto, número e data.|  
  
> [!NOTE]  
>  Quando uma regra de negócios contém uma condição que compara dois valores, e a regra é aplicada a um membro para o qual ambos os valores são NULL, esse membro falhará a validação.  
  
## <a name="see-also"></a>Consulte Também  
 [Ações de regras de negócio &#40;Master Data Services&#41;](../master-data-services/business-rule-actions-master-data-services.md)   
 [Regras de negócio &#40;Master Data Services&#41;](../master-data-services/business-rules-master-data-services.md)   
 [Criar e publicar uma regra de negócio &#40;Master Data Services&#41;](../master-data-services/create-and-publish-a-business-rule-master-data-services.md)  
  
  
