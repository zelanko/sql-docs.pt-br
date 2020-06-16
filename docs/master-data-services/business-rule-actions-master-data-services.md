---
title: Ações de regras de negócio
description: Em Master Data Services, as regras de negócio causam ações. Saiba mais sobre ações de valor padrão, ações de valor de alteração, ações de validação e ações externas.
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: cdc4daca-3dff-46d8-b7f0-57f7826dd61a
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: adb0a6798291148cc03c7e9a0a80ca8a59f3952f
ms.sourcegitcommit: 7d6eb09588ff3477cf39a8fd507d537a603bc60d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/16/2020
ms.locfileid: "84796540"
---
# <a name="business-rule-actions-master-data-services"></a>Ações de regras de negócio (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  No [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], as ações de regras de negócio são consequência de avaliações de condições de regra de negócio. Se uma condição for verdadeira, a ação será iniciada.  
  
> [!NOTE]  
>  Para valor padrão e ações de valor de alteração, se o valor gerado exceder o comprimento máximo do atributo, o valor gerado será truncado.  
  
## <a name="default-value-actions"></a>Ações de valor padrão  
 As ações de**Valor padrão** definem o valor padrão de um atributo especificado. Os usuários com permissão podem alterar esses valores padrão.  
  
|Nome do valor|Description|  
|----------------|-----------------|  
|**segue o padrão**|O atributo selecionado **segue o padrão** de um atributo específico, um valor de atributo específico ou está em branco.<br /><br /> Esta ação é válida para valores de texto, número, data e link.|  
|**segue o padrão de um valor gerado**|O atributo selecionado **segue o padrão de um valor gerado** que é determinado pela inserção de um valor inicial e incremental.<br /><br /> Esta ação é válida para valores de texto e número.|  
|**segue o padrão de um valor concatenado**|O atributo selecionado **segue o padrão de um valor concatenado** que é determinado pela especificação de vários atributos.<br /><br /> Esta ação é válida para valores de texto e link.|  
  
## <a name="change-value-actions"></a>Ações de alteração de valor  
 As ações de**Alterar valor** atualizam o valor de um atributo especificado ou de um atributo. Os usuários somente poderão alterar esses valores se o novo valor fizer com que a ação seja verdadeira.  
  
|Nome do valor|Description|  
|----------------|-----------------|  
|**Seja**|O atributo selecionado é alterado para um valor de atributo definido, outro atributo ou espaço em branco.<br /><br /> Esta ação é válida para valores de texto, número, data e link.|  
|**igual a um valor concatenado**|O atributo selecionado é alterado para um valor concatenado, que é determinado pela especificação de vários atributos.<br /><br /> Esta ação é válida para valores de texto e link.|  
  
## <a name="validation-actions"></a>Ações de validação  
 As ações de**Validação** , quando não são avaliadas como verdadeiras, enviam um email a um usuário ou grupo especificado. Para confirmar uma versão, todas as ações de validação devem ser avaliadas como verdadeiras.  
  
 As únicas exceções são as ações **é obrigatório** e **não é válido** . Essas ações devem ser combinadas com uma ação de alteração de valor, de forma que os dados possam ser validados com êxito e a versão confirmada.  
  
|Nome da validação|Description|  
|---------------------|-----------------|  
|**é necessário**|O atributo selecionado **é necessário**, o que significa que não pode ser nulo ou em branco.<br /><br /> Esta ação é válida para valores de texto, número, data e link.|  
|**Não é válido**|O atributo selecionado **não é válido**.<br /><br /> Esta ação é válida para valores de texto, número, data e link.|  
|**deve conter o padrão**|O atributo selecionado **deve conter o padrão** que é especificado. Use expressões regulares do .NET Framework para especificar o padrão.<br /><br /> Para obter mais informações sobre expressões regulares, consulte [Elementos de linguagem das expressões regulares](https://go.microsoft.com/fwlink/?LinkId=164401) na Biblioteca MSDN.<br /><br /> Esta ação é válida para valores de texto e link.|  
|**deve ser exclusivo**|O atributo selecionado **deve ser exclusivo** , independentemente ou em combinação com os atributos definidos.<br /><br /> **Prática recomendada:** combine esta ação com uma condição obrigatória para assegurar a validade de campos de índice em sistemas de assinatura.<br /><br /> Esta ação é válida para valores de texto, número, data e link.<br /><br /> **OBSERVAÇÃO**: se o primeiro atributo for do tipo DateTime, ele não poderá ser usado em combinação com um atributo do tipo Numeric ou Text. Se o primeiro atributo for do tipo Numeric, ele não poderá ser usado em combinação com um atributo do tipo DateTime.|  
|**deve ter um dos seguintes valores**|O atributo selecionado **deve ter um dos valores** especificados em uma lista.<br /><br /> Esta ação é válida para valores de texto.|  
|**deve ser maior que**|O atributo selecionado **deve ser maior que** um atributo específico, um valor de atributo específico ou deve estar em branco.<br /><br /> Esta ação é válida para valores de texto, número e data.|  
|**deve ser igual a**|O atributo selecionado **deve ser igual a** um valor de atributo definido, outro atributo ou espaço em branco.<br /><br /> Esta ação é válida para valores de texto, número, data e link.|  
|**deve ser maior ou igual a**|O atributo selecionado **deve ser maior ou igual a** um atributo específico, um valor de atributo específico ou está em branco.<br /><br /> Esta ação é válida para valores de texto, número e data.|  
|**deve ser menor que**|O atributo selecionado **deve ser menor que** um atributo específico, um valor de atributo específico ou está em branco.<br /><br /> Esta ação é válida para valores de texto, número e data.|  
|**deve ser menor ou igual a**|O atributo selecionado **deve ser menor ou igual a** um atributo específico, um valor de atributo específico ou está em branco.<br /><br /> Esta ação é válida para valores de texto, número e data.|  
|**deve estar entre**|O atributo selecionado **deve estar entre** dois valores de atributo ou de atributos específicos.<br /><br /> Esta ação é válida para valores de texto, número e data.|  
|**deve ter um comprimento mínimo de**|O atributo selecionado **deve ter um comprimento mínimo de** correspondente ao valor especificado.<br /><br /> Esta ação é válida para valores de texto e link.|  
|**deve ter um comprimento máximo de**|O atributo selecionado **deve ter um comprimento máximo de** correspondente ao valor especificado.<br /><br /> Esta ação é válida para valores de texto e link.|  
  
## <a name="external-action"></a>Ação externa  
 As ações**externas** interagem com aplicativos fora do [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)].  
  
|Nome da ação|Description|  
|-----------------|-----------------|  
|**iniciar fluxo de trabalho**|Inicia um fluxo de trabalho externo. Os dados que fizeram com que essa ação ocorresse são passados para o fluxo de trabalho. Para obter mais informações, consulte [Integração do fluxo de trabalho do SharePoint com o Master Data Services](https://msdn.microsoft.com/library/gg690195.aspx).<br /><br /> Esta ação é válida para valores de texto, número, data e link.|  
  
## <a name="see-also"></a>Consulte Também  
 [Condições de regra de negócio &#40;Master Data Services&#41;](../master-data-services/business-rule-conditions-master-data-services.md)   
 [Regras de negócio &#40;Master Data Services&#41;](../master-data-services/business-rules-master-data-services.md)   
 [Criar e publicar uma regra de negócio &#40;Master Data Services&#41;](../master-data-services/create-and-publish-a-business-rule-master-data-services.md)  
  
  
