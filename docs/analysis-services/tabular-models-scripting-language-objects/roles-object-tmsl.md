---
title: Objeto roles (TMSL) | Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tmsl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 19da91838703adc4ae224a645e1f0a6e65fe032c
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/16/2018
ms.locfileid: "40396026"
---
# <a name="roles-object-tmsl"></a>Objeto Roles (TMSL)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  Define uma função no modelo que especifica uma coleção de permissões. Associação de função consiste em princípios de segurança do Windows. Você pode definir filtros em uma função para restringir o acesso a objetos específicos.  
  
## <a name="object-definition"></a>Definição do objeto  
 Todos os objetos têm um conjunto comum de propriedades, incluindo nome, tipo, descrição, uma coleção de propriedades e anotações. **Função** objetos também têm as propriedades a seguir.  
  
 modelPermission  
 Estabelece um escopo de permissões em um banco de dados. Os valores válidos são none,  
                  ler,  
                  readRefresh,  
                  atualização,  
                  e o administrador. Ver [funções e permissões &#40;Analysis Services&#41; ](../../analysis-services/multidimensional-models/roles-and-permissions-analysis-services.md) para obter informações sobre permissões de banco de dados.  
  
 membros  
 Membros consistem em um nome de membro e ID, onde o nome do membro é o alias ou nome amigável de um princípio de segurança do Windows, e a ID é o identificador de segurança. Ambos são especificadas na definição de função. Ver [componentes de SID](/windows/desktop/SecAuthZ/sid-components) para obter detalhes sobre os identificadores.  
  
 tablePermissions  
 Uma permissão de tabela é um objeto nomeado com permissões definidas por meio de uma expressão DAX. Essa propriedade é opcional, usado para aplicar um filtro de segurança.  
  
## <a name="usage"></a>Uso  
 **Função** objetos são usados no [comando Alter &#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-commands/alter-command-tmsl.md), [criar comando &#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-commands/create-command-tmsl.md), [comando CreateOrReplace &#40;TMSL &#41; ](../../analysis-services/tabular-models-scripting-language-commands/createorreplace-command-tmsl.md), e [comando Delete &#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-commands/delete-command-tmsl.md).  
  
 Um **função** é uma propriedade de um modelo de objeto, mas também pode ser especificado como uma propriedade de um objeto de banco de dados, considerando o mapeamento entre o modelo e o banco de dados.  
  
 Ao criar, substituir ou alterar um objeto de função, especifique todas as propriedades de leitura / gravação da definição do objeto. A omissão de uma propriedade de leitura / gravação é considerada uma exclusão.  
  
## <a name="full-syntax"></a>Sintaxe completa  
 Abaixo está a representação de esquema de um objeto de função de um modelo.  
  
```  
"roles": {  
          "type": "array",  
          "items": {  
            "description": "ModelRole object of Tabular Object Model (TOM)",  
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
              "modelPermission": {  
                "enum": [  
                  "none",  
                  "read",  
                  "readRefresh",  
                  "refresh",  
                  "administrator"  
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
              },  
              "members": {  
                "type": "array",  
                "items": {  
                  "anyOf": [  
                    {  
                      "description": "WindowsModelRoleMember object of Tabular Object Model (TOM)",  
                      "type": "object",  
                      "properties": {  
                        "memberName": {  
                          "type": "string"  
                        },  
                        "memberId": {  
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
                    },  
                    {  
                      "description": "ExternalModelRoleMember object of Tabular Object Model (TOM)",  
                      "type": "object",  
                      "properties": {  
                        "memberName": {  
                          "type": "string"  
                        },  
                        "memberId": {  
                          "type": "string"  
                        },  
                        "identityProvider": {  
                          "type": "string"  
                        },  
                        "memberType": {  
                          "enum": [  
                            "auto",  
                            "user",  
                            "group"  
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
                  ]  
                }  
              },  
              "tablePermissions": {  
                "type": "array",  
                "items": {  
                  "description": "TablePermission object of Tabular Object Model (TOM)",  
                  "type": "object",  
                  "properties": {  
                    "name": {  
                      "type": "string"  
                    },  
                    "filterExpression": {  
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
              }  
            },  
            "additionalProperties": false  
          }  
        }  
```  
  
## <a name="see-also"></a>Consulte também  
 [Referência de TMSL &#40;Linguagem de Scripts de Modelo de Tabela&#41;](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md)   
 [Funções e permissões &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/roles-and-permissions-analysis-services.md)  
  
  
