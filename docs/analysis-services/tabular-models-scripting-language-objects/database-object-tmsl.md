---
title: O objeto de banco de dados (TMSL) | Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: tabular-models
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: b2b706afd63db34837e490133176356cf761d24f
ms.sourcegitcommit: 1aedef909f91dc88dc741748f36eabce3a04b2b1
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/08/2018
---
# <a name="database-object-tmsl"></a>Objeto de banco de dados (TMSL)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  Define um banco de dados Tabular no nível de compatibilidade 1200 ou superior, com base em um modelo do mesmo nível. Este tópico documenta a definição do objeto de banco de dados, fornecendo a carga de solicitações que criarem, alteram, excluam e executam tarefas de gerenciamento de banco de dados.  
  
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
 **Banco de dados** objetos são usados em quase todos os comandos. Consulte [comandos na linguagem de script de modelo de tabela &#40;TMSL&#41; ](../../analysis-services/tabular-models-scripting-language-commands/tmsl-reference-commands.md) para obter uma lista. Um **banco de dados** objeto é um filho de um objeto de servidor.  
  
 Ao criar, substituir ou alterar um objeto de banco de dados, especifica todas as propriedades de leitura / gravação da definição de objeto. A omissão de uma propriedade de leitura / gravação é considerada uma exclusão.  
  
## <a name="partial-syntax"></a>Sintaxe parcial  
 Como essa definição de objeto é muito grande, somente diretas propriedades são listadas. O **modelo** objeto fornece a maior parte da definição do banco de dados. Consulte [o objeto de modelo &#40;TMSL&#41; ](../../analysis-services/tabular-models-scripting-language-objects/model-object-tmsl.md) como o objeto é definido.  
  
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
  
  
