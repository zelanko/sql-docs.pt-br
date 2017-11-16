---
title: "O objeto de partições (TMSL) | Microsoft Docs"
ms.custom: 
ms.date: 05/30/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: tabular-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: df1da0d2-d824-42ba-b9dc-47fbd8edc10f
caps.latest.revision: 10
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 7580d00c4fa5fa35b215fed991c811489c3f5571
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="partitions-object-tmsl"></a>Objeto de partições (TMSL)

[!INCLUDE[ssas-appliesto-sql2016-later-aas](../../includes/ssas-appliesto-sql2016-later-aas.md)]

  Define uma partição ou uma segmentação lógica, do conjunto de linhas de tabela. Uma partição consiste em uma consulta SQL usada para importar dados para dados de exemplo no ambiente de modelagem, ou como uma consulta de dados completa para passar por meio da execução de consulta por meio de DirectQuery.  
  
 As propriedades da partição determinam como os dados são originados da tabela.  Na hierarquia de objetos, o objeto pai de uma partição é um objeto de tabela.  
  
## <a name="object-definition"></a>Definição do objeto  
 Todos os objetos têm um conjunto comum de propriedades, incluindo nome, tipo, descrição, uma coleção de propriedades e anotações. **Partição** objetos também têm as seguintes propriedades.  
  
 Tipo  
 O tipo de partição. Os valores válidos são numéricos e incluem o seguinte:  
  
-   Consulta (1) – dados nessa partição é recuperada executando uma consulta em uma **DataSource**. O **DataSource** deve ser uma fonte de dados definida no arquivo model.bim.  
  
-   Calculado (2) – os dados nessa partição são preenchidos executando uma expressão calculada.  
  
-   Nenhum (3) – dados nessa partição é preenchida por push um conjunto de linhas de dados para o servidor como parte da operação de atualização.  
  
 mode  
 Define o modo de consulta da partição. Os valores válidos são **importar**, **DirectQuery**, ou **padrão** (herdado). Esse valor é necessário.  
  
|||  
|-|-|  
|**Importar**|Indica as solicitações são emitidas em relação o mecanismo analítico na memória armazenar dados importados de consulta.|  
|**DirectQuery**|Passar por meio da execução de consulta para um banco de dados relacional externo. O modo DirectQuery usa partições para fornecer dados de exemplo usados durante o design do modelo. Quando implantado em um servidor de produção, você deve alternar para exibição de dados completa. Lembre-se de que o modo DirectQuery requer uma partição por tabela e uma fonte de dados por modelo.|  
|**padrão**|Defina se você deseja alternar os modos de nível superiores da árvore de objetos, no nível do modelo ou banco de dados. Quando você escolhe o padrão, o modo de consulta será importação ou DirectQuery.|  
  
 origem  
 Identifica o local dos dados a ser consultado. Os valores válidos são **consulta, calculada**, ou **nenhum**. Esse valor é necessário.  
  
|||  
|-|-|  
|**Nenhum**|Usado para o modo de importação, onde os dados são carregados e armazenados na memória.|  
|**consulta**|Para o modo DirectQuery, isso é uma consulta SQL executada no banco de dados relacional especificado no modelo de **DataSource**. Consulte [fontes de dados de objeto &#40; TMSL &#41; ](../../analysis-services/tabular-models-scripting-language-objects/datasources-object-tmsl.md).|  
|**calculado**|Tabelas calculadas são originadas de uma expressão especificada quando a tabela é criada. Essa expressão é considerada a origem da partição criada para a tabela calculada.|  
  
 exibição de dados  
 Para partições DirectQuery, uma propriedade dataView adicionais mais Especifica se a consulta que recupera dados é um exemplo ou conjunto de dados completo. Os valores válidos são **completo**, **exemplo**, ou **padrão** (herdado). Conforme observado, os exemplos são usados somente durante o teste e modelagem de dados. Consulte [adicionar dados de exemplo para um modelo DirectQuery no modo de Design](../../analysis-services/tabular-models/add-sample-data-to-a-directquery-model-in-design-mode.md) para obter mais informações.  
  
## <a name="usage"></a>Uso  
 Objetos de partição são usados em [Alter comando &#40; TMSL &#41; ](../../analysis-services/tabular-models-scripting-language-commands/alter-command-tmsl.md), [Criar comando &#40; TMSL &#41; ](../../analysis-services/tabular-models-scripting-language-commands/create-command-tmsl.md), [CreateOrReplace comando &#40; TMSL &#41; ](../../analysis-services/tabular-models-scripting-language-commands/createorreplace-command-tmsl.md), [Excluir comando &#40; TMSL &#41; ](../../analysis-services/tabular-models-scripting-language-commands/delete-command-tmsl.md), [De atualização de comando &#40; TMSL &#41; ](../../analysis-services/tabular-models-scripting-language-commands/refresh-command-tmsl.md), e [MergePartitions comando &#40; TMSL &#41; ](../../analysis-services/tabular-models-scripting-language-commands/mergepartitions-command-tmsl.md).  
  
 Ao criar, substituir ou alterar um objeto de partição, especifica todas as propriedades de leitura / gravação da definição de objeto. A omissão de uma propriedade de leitura / gravação é considerada uma exclusão. Propriedades de leitura-gravação incluem nome, descrição, modo e fonte.  
  
## <a name="examples"></a>Exemplos  
 **Exemplo 1** -uma estrutura de partição simples de uma tabela (não uma tabela de fatos).  
  
```  
"partitions": [  
          {  
            "name": "Customer",  
            "source": {  
              "query": "SELECT [dbo].[Customer].* FROM [dbo].[Customer]",  
              "dataSource": "SqlServer localhost FoodmartDB"  
            }  
]  
```  
  
 **Exemplo 2** - particionada dados de fato normalmente se baseiam em uma cláusula WHERE que cria partições não sobrepostas para dados da mesma tabela.  
  
```  
"partitions": [  
          {  
            "name": "sales_fact_2015",  
            "source": {  
              "query": "SELECT [dbo].[sales_fact_2015].* FROM [dbo].[sales_fact_2015] WHERE [dbo].[sales_fact_2015].[Quarter]=4",                                                                                          
              "dataSource": "SqlServer localhost FoodmartDB"  
            },  
          }  
        ]  
```  
  
 **Exemplo 3** -uma tabela calculada com base em uma expressão DAX.  
  
```  
"partitions": [  
          {  
            "name": "CalcTable1",  
            "source": {  
              "type": "calculated",  
              "expression": "'Product Class'"  
            },  
            }  
]  
```  
  
## <a name="full-syntax"></a>Sintaxe completa  
 Abaixo está a representação do esquema de um objeto de partição.  
  
```  
"partitions": {  
                "type": "array",  
                "items": {  
                  "description": "Partition object of Tabular Object Model (TOM)",  
                  "type": "object",  
                  "properties": {  
                    "name": {  
                      "type": "string"  
                    },  
                    "description": {  
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
                    },  
                    "mode": {  
                      "enum": [  
                        "import",  
                        "directQuery",  
                        "default"  
                      ]  
                    },  
                    "dataView": {  
                      "enum": [  
                        "full",  
                        "sample",  
                        "default"  
                      ]  
                    },  
                    "source": {  
                      "anyOf": [  
                        {  
                          "description": "QueryPartitionSource object of Tabular Object Model (TOM)",  
                          "type": "object",  
                          "properties": {  
                            "type": {  
                              "enum": [  
                                "query",  
                                "calculated",  
                                "none"  
                              ]  
                            },  
                            "query": {  
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
                            },  
                            "dataSource": {  
                              "type": "string"  
                            }  
                          },  
                          "additionalProperties": false  
                        },  
                        {  
                          "description": "CalculatedPartitionSource object of Tabular Object Model (TOM)",  
                          "type": "object",  
                          "properties": {  
                            "type": {  
                              "enum": [  
                                "query",  
                                "calculated",  
                                "none"  
                              ]  
                            },  
                            "expression": {  
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
                      ]  
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
              },  
  
```  
  
## <a name="see-also"></a>Consulte também  
 [Referência de TMSL &#40;Linguagem de Scripts de Modelo de Tabela&#41;](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md)  
  
  

