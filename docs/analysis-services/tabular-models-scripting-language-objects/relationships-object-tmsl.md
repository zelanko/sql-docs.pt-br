---
title: "O objeto de relações (TMSL) | Microsoft Docs"
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
ms.assetid: 7588565f-ea34-4402-8be9-331188bdb8c2
caps.latest.revision: "7"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 0c1865295c0c4a16737be0a7ea5789b60c14f42c
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/08/2017
---
# <a name="relationships-object-tmsl"></a>Objeto de relações (TMSL)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]Define uma relação entre uma tabela de origem e destino, com a capacidade de especificar a cardinalidade e a direção dos filtros de consulta e segurança.  
  
## <a name="object-definition"></a>Definição do objeto  
 Todos os objetos têm um conjunto comum de propriedades, incluindo nome, tipo, descrição, uma coleção de propriedades e anotações. **Relação** objetos também têm as seguintes propriedades.  
  
 isActive  
 Um booliano que indica se a relação está marcada como ativo ou inativo. Uma relação Ativa é usada automaticamente para filtragem entre tabelas. Uma relação Inativas pode ser usada explicitamente por cálculos DAX através da função USERELATIONSHIP.  
  
 crossFilteringBehavior  
 Indica como as relações influenciam a filtragem dos dados. Consulte [bidirecional entre os filtros para modelos de tabela no SQL Server 2016 Analysis Services](../../analysis-services/tabular-models/bi-directional-cross-filters-tabular-models-analysis-services.md) para obter mais informações. Estes são os valores válidos:  
  
-   OneDirection (1) - as linhas selecionadas na extremidade "Para" da relação filtrarão automaticamente verificações da tabela no final "De" da relação.  
  
-   BothDirections (2) - filtros em ambas as extremidades da relação filtrarão automaticamente a outra tabela.  
  
-   Automático (3) - o mecanismo analisará as relações e escolha um dos comportamentos usando heurística.  
  
 joinOnDateBehavior  
 Ao unir duas colunas de data hora, indica se deve associar partes de data e hora ou apenas em parte de data.  
  
-   DateAndTime (1) - ao unir duas colunas data e hora, associe as partes de data e hora.  
  
-   DatePartOnly (2) - ao unir duas colunas data e hora, associe somente a parte de data.  
  
 relyOnReferentialIntegrity  
 Não utilizado, reservado para uso futuro.  
  
 securityFilteringBehavior  
 Uma enumeração que indica como as relações influenciam a filtragem de dados ao avaliar expressões de segurança de nível de linha. Estes são os valores válidos:  
  
-   OneDirection (1) - as linhas selecionadas na extremidade "Para" da relação filtrarão automaticamente verificações da tabela no final "De" da relação.  
  
-   BothDirections (2) - filtros em ambas as extremidades da relação filtrarão automaticamente a outra tabela.  
  
## <a name="usage"></a>Uso  
 Objetos de relação são usados em [Alter comando &#40; TMSL &#41; ](../../analysis-services/tabular-models-scripting-language-commands/alter-command-tmsl.md), [Criar comando &#40; TMSL &#41; ](../../analysis-services/tabular-models-scripting-language-commands/create-command-tmsl.md), [CreateOrReplace comando &#40; TMSL &#41; ](../../analysis-services/tabular-models-scripting-language-commands/createorreplace-command-tmsl.md), e [excluir comando &#40; TMSL &#41; ](../../analysis-services/tabular-models-scripting-language-commands/delete-command-tmsl.md).  
  
 Ao criar, substituir ou alterar um objeto de relação, especifica todas as propriedades de leitura / gravação da definição de objeto. A omissão de uma propriedade de leitura / gravação é considerada uma exclusão.  
  
## <a name="full-syntax"></a>Sintaxe completa  
 Abaixo está a representação do esquema de um objeto de relação.  
  
```  
"relationships": {  
          "type": "array",  
          "items": {  
            "anyOf": [  
              {  
                "description": "SingleColumnRelationship object of Tabular Object Model (TOM)",  
                "type": "object",  
                "properties": {  
                  "name": {  
                    "type": "string"  
                  },  
                  "isActive": {  
                    "type": "boolean"  
                  },  
                  "type": {  
                    "enum": [  
                      "singleColumn"  
                    ]  
                  },  
                  "crossFilteringBehavior": {  
                    "enum": [  
                      "oneDirection",  
                      "bothDirections",  
                      "automatic"  
                    ]  
                  },  
                  "joinOnDateBehavior": {  
                    "enum": [  
                      "dateAndTime",  
                      "datePartOnly"  
                    ]  
                  },  
                  "relyOnReferentialIntegrity": {  
                    "type": "boolean"  
                  },  
                  "securityFilteringBehavior": {  
                    "enum": [  
                      "oneDirection",  
                      "bothDirections"  
                    ]  
                  },  
                  "fromCardinality": {  
                    "enum": [  
                      "none",  
                      "one",  
                      "many"  
                    ]  
                  },  
                  "toCardinality": {  
                    "enum": [  
                      "none",  
                      "one",  
                      "many"  
                    ]  
                  },  
                  "fromColumn": {  
                    "type": "string"  
                  },  
                  "fromTable": {  
                    "type": "string"  
                  },  
                  "toColumn": {  
                    "type": "string"  
                  },  
                  "toTable": {  
                    "type": "string"  
                  },  
                  "annotations": {  
                    "type": "array",  
                    "items": {  
                      "description": "Annotation object of Tabular Object Model (TOM)",  
                      "type": "object",  
                      "properties": {  
                        "name": {  
                          "type": "string"  
                        },  
                        "value": {  
                          "anyOf": [  
                            {  
                              "type": "string"  
                            },  
                            {  
                              "type": "array",  
                              "items": {  
                                "type": "string"  
                              }  
                            }  
                          ]  
                        }  
                      },  
                      "additionalProperties": false  
                    }  
                  }  
                },  
                "additionalProperties": false  
              }  
            ]  
          }  
        }  
```  
  
## <a name="see-also"></a>Consulte também  
 [Referência de TMSL &#40;Linguagem de Scripts de Modelo de Tabela&#41;](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md)   
 [Criar Relações](../../integration-services/data-flow/transformations/create-relationships.md)  
  
  
