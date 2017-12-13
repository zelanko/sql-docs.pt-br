---
title: O objeto de banco de dados (TMSL) | Microsoft Docs
ms.custom: 
ms.date: 05/30/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: ae5c046b-8242-4046-ae76-2c070503fd93
caps.latest.revision: "9"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: c8506cdf1917fb803c701ca0acd9f1bf1f25b141
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/08/2017
---
# <a name="database-object-tmsl"></a>Objeto de banco de dados (TMSL)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]Define um banco de dados Tabular no nível de compatibilidade 1200 ou superior, com base em um modelo do mesmo nível. Este tópico documenta a definição do objeto de banco de dados, fornecendo a carga de solicitações que criarem, alteram, excluam e executam tarefas de gerenciamento de banco de dados.  
  
> [!NOTE]  
>  Em qualquer script pode ser referenciado apenas um banco de dados no momento. Para qualquer objeto que não seja o próprio banco de dados, a propriedade de banco de dados é opcional se você especificar o modelo. Há um mapeamento entre um modelo e um banco de dados que pode ser usado para deduzir o nome do banco de dados se ele não foi explicitamente é fornecido.   
> Da mesma forma, você pode deixar o modelo, defina suas propriedades no banco de dados.  
  
## <a name="object-definition"></a>Definição do objeto  
 Todos os objetos têm um conjunto comum de propriedades, incluindo nome, tipo, descrição, uma coleção de propriedades e anotações. **Banco de dados** objetos também têm as seguintes propriedades.  
  
 nível de compatibilidade  
 Atualmente, os valores válidos são 1200, 1400. Níveis de compatibilidade inferiores usam um mecanismo diferente de metadados.  
  
 readwritemode  
 Enumera o modo do banco de dados. É comum para tornar um banco de dados somente leitura em configurações alto de disponibilidade e escalabilidade. Os valores válidos incluem readWrite,  
                somente leitura,  
                ou readOnlyExclusive. Consulte [alta disponibilidade e escalabilidade no Analysis Services](../../analysis-services/instances/high-availability-and-scalability-in-analysis-services.md) e [alternar um banco de dados do Analysis Services entre os modos ReadOnly e ReadWrite](../../analysis-services/multidimensional-models/switch-an-analysis-services-database-between-readonly-and-readwrite-modes.md) para obter mais informações sobre quando essa propriedade é usada.  
  
## <a name="usage"></a>Uso  
 **Banco de dados** objetos são usados em quase todos os comandos. Consulte [comandos na tabela de linguagem de scripts &#40; modelo TMSL &#41; ](../../analysis-services/tabular-models-scripting-language-commands/tmsl-reference-commands.md) para obter uma lista. Um **banco de dados** objeto é um filho de um objeto de servidor.  
  
 Ao criar, substituir ou alterar um objeto de banco de dados, especifica todas as propriedades de leitura / gravação da definição de objeto. A omissão de uma propriedade de leitura / gravação é considerada uma exclusão.  
  
## <a name="partial-syntax"></a>Sintaxe parcial  
 Como essa definição de objeto é muito grande, somente diretas propriedades são listadas. O **modelo** objeto fornece a maior parte da definição do banco de dados. Consulte [modelo de objeto &#40; TMSL &#41; ](../../analysis-services/tabular-models-scripting-language-objects/model-object-tmsl.md) como o objeto é definido.  
  
```  
    "database": {  
      "type": "object",  
      "properties": {  
        "name": {  
          "type": "string"  
        },  
        "id": {  
          "type": "string"  
        },  
        "description": {  
          "type": "string"  
        },  
        "compatibilityLevel": {  
          "type": "integer"  
        },  
        "readWriteMode": {  
          "enum": [  
            "readWrite",  
            "readOnly",  
            "readOnlyExclusive"  
          ]  
        },  
        "model": {  
          "type": "object",  
          ...  
        }  
    }  
  
```  
  
## <a name="see-also"></a>Consulte também  
 [Referência de TMSL &#40;Linguagem de Scripts de Modelo de Tabela&#41;](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md)   
 [Alta disponibilidade e escalabilidade no Analysis Services](../../analysis-services/instances/high-availability-and-scalability-in-analysis-services.md)  
  
  
