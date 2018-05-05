---
title: Comando CreateOrReplace (TMSL) | Microsoft Docs
ms.custom: ''
ms.date: 05/30/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: f77a0e04-461a-4fa8-b997-78057e410d56
caps.latest.revision: 12
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: fac0e43a8c1a8ec8dbdfdc3a255bdee1a74bddae
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="createorreplace-command-tmsl"></a>Comando CreateOrReplace (TMSL)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  Cria ou substitui o objeto especificado e todos os objetos descendentes são especificados. São criados objetos inexistente. Os objetos existentes são substituídos com a nova definição.  
  
 Sempre que você especificar uma propriedade de leitura / gravação, certifique-se de incluir todos eles. A omissão de um objeto de leitura / gravação é considerada uma exclusão.  
  
## <a name="request"></a>Solicitação  
 A estrutura da solicitação varia com base no objeto. Um objeto que é um pai deve incluir todos os seus filhos, embora as definições de objeto completo de irmãos e pais não são necessárias.  
  
 [Objeto de banco de dados &#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-objects/database-object-tmsl.md)  
  
 Substitui o banco de dados existente com uma definição de renomeado mínima de banco de dados que especifica uma conexão, propriedades de modelo modificado e seu nome. Como a definição do objeto não incluir tabelas, partições ou relações, todos os objetos são excluídos.  
  
```  
{  
  "createOrReplace": {  
    "object": {  
      "database": "AdventureWorksTabular1200"  
    },  
    "database": {  
      "name": "TestCreateOrReplaceDB",  
      "id": "newID",  
      "compatibilityLevel": 1200,  
      "model": {  
        "defaultMode": "import",  
        "culture": "en-US",  
        "dataSources": [  
          {  
            "name": "SqlServer localhost AdventureworksDW2016",  
            "connectionString": "Provider=SQLNCLI11;Data Source=localhost;Initial Catalog=AdventureworksDW2016;Integrated Security=SSPI;Persist Security Info=false",  
            "impersonationMode": "impersonateAccount",  
            "account": "   ",  
            "annotations": [  
              {  
                "name": "ConnectionEditUISource",  
                "value": "SqlServer"  
              }  
            ]  
          }  
        ]  
      }  
    }  
  }  
}  
```  
  
 [Fontes de dados objeto &#40;TMSL&#41; ](../../analysis-services/tabular-models-scripting-language-objects/datasources-object-tmsl.md) substitui um nome de conexão.  
  
```  
{  
  "createOrReplace": {  
    "object": {  
      "database": "TestCreateOrReplaceDB",  
      "dataSource": "SqlServer localhost AdventureworksDW2016"  
    },  
    "dataSource": {  
      "name": "New connection name",  
      "connectionString": "Provider=SQLNCLI11;Data Source=localhost;Initial Catalog=AdventureworksDW2016;Integrated Security=SSPI;Persist Security Info=false",  
      "impersonationMode": "impersonateAccount",  
      "account": "   ",  
      "annotations": [  
        {  
          "name": "ConnectionEditUISource",  
          "value": "SqlServer"  
        }  
      ]  
    }  
  }  
}  
```  
  
 [Objeto Tables &#40;TMSL&#41; ](../../analysis-services/tabular-models-scripting-language-objects/tables-object-tmsl.md) substitui todas as tabelas existentes, deixando apenas aquele especificado.  
  
```  
{  
  "createOrReplace": {  
    "object": {  
      "database": "AdventureWorksTabular1200"  
    },  
    "database": {  
      "name": "AdventureWorksTabular1200",  
      "id": "New-AdventureWorksTabular1200",  
      "compatibilityLevel": 1200,  
      "model": {  
        "defaultMode": "import",  
        "culture": "en-US",  
        "dataSources": [  
          {  
            "name": "SqlServer localhost AdventureworksDW2016",  
            "connectionString": "Provider=SQLNCLI11;Data Source=localhost;Initial Catalog=AdventureworksDW2016;Integrated Security=SSPI;Persist Security Info=false",  
            "impersonationMode": "impersonateAccount",  
            "account": "   ",  
            "annotations": [  
              {  
                "name": "ConnectionEditUISource",  
                "value": "SqlServer"  
              }  
            ]  
          }  
        ],  
        "tables": [  
          {  
            "name": "Date",  
            "columns": [  
              {  
                "name": "DateKey",  
                "dataType": "int64",  
                "sourceColumn": "DateKey",  
                "sourceProviderType": "Integer"  
              },  
              {  
                "name": "FullDateAlternateKey",  
                "dataType": "dateTime",  
                "sourceColumn": "FullDateAlternateKey",  
                "formatString": "General Date",  
                "sourceProviderType": "DBDate"  
              },  
              {  
                "name": "CalendarYear",  
                "dataType": "int64",  
                "sourceColumn": "CalendarYear",  
                "sourceProviderType": "SmallInt"  
              }  
            ],  
            "partitions": [  
              {  
                "name": "DimDate",  
                "dataView": "full",  
                "source": {  
                  "query": " SELECT [dbo].[DimDate].* FROM [dbo].[DimDate] ",  
                  "dataSource": "SqlServer localhost AdventureworksDW2016"  
                }  
              }  
            ],  
            "annotations": [  
              {  
                "name": "_TM_ExtProp_QueryDefinition",  
                "value": " SELECT [dbo].[DimDate].* FROM [dbo].[DimDate] "  
              },  
              {  
                "name": "_TM_ExtProp_DbTableName",  
                "value": "DimDate"  
              },  
              {  
                "name": "_TM_ExtProp_DbSchemaName",  
                "value": "dbo"  
              }  
            ]  
          }  
        ]  
     }  
   }  
 }  
}   
```  
  
 [Objeto de partições &#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-objects/partitions-object-tmsl.md)  
  
 Substitua um nome de partição. Objetos de partição tem três propriedades de leitura / gravação: nome, origem, descrição. Sempre que você especificar uma propriedade de leitura / gravação, certifique-se de incluir todos eles. A omissão de um objeto de leitura / gravação é considerada uma exclusão.  
  
 Como a definição do objeto é a partição, apenas a partição nomeada e sua definição é afetado. Outras tabelas, relações e partições não são afetadas.  
  
 A menos que você está criando, substituindo, ou alterando o próprio objeto de fonte de dados, qualquer fonte de dados referenciado em seu script (como o script de partição abaixo) deve ser um existente **DataSource** objeto em seu modelo. Se você precisar alterar a fonte de dados, adicioná-lo ao  
  
```  
{  
  "createOrReplace": {  
    "object": {  
      "database": "AdventureWorksTabular1200",  
      "table": "FactSalesQuota",  
      "partition": "FactSalesQuota - 2011"  
    },  
    "partition": {  
      "name": "Sales Quota for 2011",  
      "mode": "import",  
      "dataView": "full",  
      "source": {  
        "query": [  
          "SELECT [dbo].[FactSalesQuota].* FROM [dbo].[FactSalesQuota]",  
          "JOIN DimDate as DD",  
          "on DD.DateKey = FactSalesQuota.DateKey",  
          "WHERE DD.CalendarYear='2011'"  
        ],  
        "dataSource": "SqlServer localhost AdventureworksDW2016"  
      }  
    }  
  }  
}  
```  
  
 [Objeto de funções &#40;TMSL&#41; ](../../analysis-services/tabular-models-scripting-language-objects/roles-object-tmsl.md) substitui uma definição de função com o que inclui os membros.  
  
```  
{  
  "createOrReplace": {  
    "object": {  
      "database": "AdventureWorksTabular1200",  
      "role": "DataReader"  
    },  
    "role": {  
      "name": "DataReader",  
      "modelPermission": "read",  
      "members": [  
        {  
          "memberName": "ADVENTUREWORKS\\InternalSalesGrp"  
        }  
      ]  
    }  
  }  
}  
```  
  
## <a name="response"></a>Resposta  
 Retorna um resultado vazio quando o comando terá êxito. Caso contrário, uma exceção XMLA é retornada.  
  
## <a name="examples"></a>Exemplos  
 **Exemplo 1** -cria um novo banco de dados, substituindo o banco de dados existente de mesmo nome.  
  
```  
{  
  "createOrReplace": {  
    "object": {  
      "database": "AdventureWorksTabular1200"  
    },  
    "database": {  
      "name": "AdventureWorksTabular1200",  
      "id": "AdventureWorksTabular1200",  
      "compatibilityLevel": 1200,  
      "model": {  
        "defaultMode": "directQuery",  
        "culture": "en-US",  
        "dataSources": [  
          {  
            "name": "SqlServer localhost AdventureworksDW2016",  
            "connectionString": "Provider=SQLNCLI11;Data Source=localhost;Initial Catalog=AdventureworksDW2016;Integrated Security=SSPI;Persist Security Info=false",  
            "impersonationMode": "impersonateAccount",  
            "account": "   ",  
            "annotations": [  
              {  
                "name": "ConnectionEditUISource",  
                "value": "SqlServer"  
              }  
            ]  
          }  
        ],  
        "tables": [  
          {  
            "name": "DimDate",  
            "columns": [  
              {  
                "name": "DateKey",  
                "dataType": "int64",  
                "sourceColumn": "DateKey",  
                "sourceProviderType": "Integer"  
              },  
              {  
                "name": "FullDateAlternateKey",  
                "dataType": "dateTime",  
                "sourceColumn": "FullDateAlternateKey",  
                "formatString": "General Date",  
                "sourceProviderType": "DBDate"  
              },  
              {  
                "name": "CalendarYear",  
                "dataType": "int64",  
                "sourceColumn": "CalendarYear",  
                "sourceProviderType": "SmallInt"  
              }  
            ],  
            "partitions": [  
              {  
                "name": "DimDate",  
                "dataView": "full",  
                "source": {  
                  "query": " SELECT [dbo].[DimDate].* FROM [dbo].[DimDate] ",  
                  "dataSource": "SqlServer localhost AdventureworksDW2016"  
                }  
              }  
            ],  
            "annotations": [  
              {  
                "name": "_TM_ExtProp_QueryDefinition",  
                "value": " SELECT [dbo].[DimDate].* FROM [dbo].[DimDate] "  
              },  
              {  
                "name": "_TM_ExtProp_DbTableName",  
                "value": "DimDate"  
              },  
              {  
                "name": "_TM_ExtProp_DbSchemaName",  
                "value": "dbo"  
              }  
            ]  
          },  
          {  
            "name": "DimEmployee",  
            "columns": [  
              {  
                "name": "EmployeeKey",  
                "dataType": "int64",  
                "sourceColumn": "EmployeeKey",  
                "sourceProviderType": "Integer"  
              },  
              {  
                "name": "SalesTerritoryKey",  
                "dataType": "int64",  
                "sourceColumn": "SalesTerritoryKey",  
                "sourceProviderType": "Integer"  
              },  
              {  
                "name": "FirstName",  
                "dataType": "string",  
                "sourceColumn": "FirstName",  
                "sourceProviderType": "WChar"  
              },  
              {  
                "name": "LastName",  
                "dataType": "string",  
                "sourceColumn": "LastName",  
                "sourceProviderType": "WChar"  
              },  
              {  
                "name": "MiddleName",  
                "dataType": "string",  
                "sourceColumn": "MiddleName",  
                "sourceProviderType": "WChar"  
              },  
              {  
                "name": "SalesPersonFlag",  
                "dataType": "boolean",  
                "sourceColumn": "SalesPersonFlag",  
                "formatString": "\"TRUE\";\"TRUE\";\"FALSE\"",  
                "sourceProviderType": "Boolean"  
              },  
              {  
                "name": "DepartmentName",  
                "dataType": "string",  
                "sourceColumn": "DepartmentName",  
                "sourceProviderType": "WChar"  
              }  
            ],  
            "partitions": [  
              {  
                "name": "DimEmployee",  
                "dataView": "full",  
                "source": {  
                  "query": " SELECT [dbo].[DimEmployee].* FROM [dbo].[DimEmployee] ",  
                  "dataSource": "SqlServer localhost AdventureworksDW2016"  
                }  
              }  
            ],  
            "annotations": [  
              {  
                "name": "_TM_ExtProp_QueryDefinition",  
                "value": " SELECT [dbo].[DimEmployee].* FROM [dbo].[DimEmployee] "  
              },  
              {  
                "name": "_TM_ExtProp_DbTableName",  
                "value": "DimEmployee"  
              },  
              {  
                "name": "_TM_ExtProp_DbSchemaName",  
                "value": "dbo"  
              }  
            ]  
          },  
          {  
            "name": "FactSalesQuota",  
            "columns": [  
              {  
                "name": "SalesQuotaKey",  
                "dataType": "int64",  
                "sourceColumn": "SalesQuotaKey",  
                "sourceProviderType": "Integer"  
              },  
              {  
                "name": "EmployeeKey",  
                "dataType": "int64",  
                "sourceColumn": "EmployeeKey",  
                "sourceProviderType": "Integer"  
              },  
              {  
                "name": "DateKey",  
                "dataType": "int64",  
                "sourceColumn": "DateKey",  
                "sourceProviderType": "Integer"  
              },  
              {  
                "name": "CalendarYear",  
                "dataType": "int64",  
                "sourceColumn": "CalendarYear",  
                "sourceProviderType": "SmallInt"  
              },  
              {  
                "name": "SalesAmountQuota",  
                "dataType": "decimal",  
                "sourceColumn": "SalesAmountQuota",  
                "formatString": "\\$#,0.00;(\\$#,0.00);\\$#,0.00",  
                "sourceProviderType": "Currency",  
                "annotations": [  
                  {  
                    "name": "Format",  
                    "value": "\<Format Format=\"Currency\" Accuracy=\"2\" ThousandSeparator=\"True\">\<Currency LCID=\"1033\" DisplayName=\"$ English (United States)\" Symbol=\"$\" PositivePattern=\"0\" NegativePattern=\"0\" /></Format>"  
                  }  
                ]  
              },  
              {  
                "name": "Date",  
                "dataType": "dateTime",  
                "sourceColumn": "Date",  
                "formatString": "General Date",  
                "sourceProviderType": "DBTimeStamp"  
              }  
            ],  
            "partitions": [  
              {  
                "name": "FactSalesQuota",  
                "dataView": "full",  
                "source": {  
                  "query": " SELECT [dbo].[FactSalesQuota].* FROM [dbo].[FactSalesQuota] ",  
                  "dataSource": "SqlServer localhost AdventureworksDW2016"  
                }  
              },  
              {  
                "name": "FactSalesQuota - 2011",  
                "mode": "import",  
                "dataView": "sample",  
                "source": {  
                  "query": [  
                    "SELECT [dbo].[FactSalesQuota].* FROM [dbo].[FactSalesQuota]",  
                    "JOIN DimDate as DD",  
                    "on DD.DateKey = FactSalesQuota.DateKey",  
                    "WHERE DD.CalendarYear='2011'"  
                  ],  
                  "dataSource": "SqlServer localhost AdventureworksDW2016"  
                },  
                "annotations": [  
                  {  
                    "name": "QueryEditorSerialization",  
                    "value": [  
                      "\<?xml version=\"1.0\" encoding=\"UTF-16\"?>\<Gemini xmlns=\"QueryEditorSerialization\"><AnnotationContent><![CDATA[<RSQueryCommandText>SELECT [dbo].[FactSalesQuota].* FROM [dbo].[FactSalesQuota]",  
                      "JOIN DimDate as DD",  
                      "on DD.DateKey = FactSalesQuota.DateKey",  
                      "WHERE DD.CalendarYear='2011'</RSQueryCommandText><RSQueryCommandType>Text</RSQueryCommandType><RSQueryDesignState></RSQueryDesignState>]]></AnnotationContent></Gemini>"  
                    ]  
                  }  
                ]  
              }  
            ],  
            "annotations": [  
              {  
                "name": "_TM_ExtProp_QueryDefinition",  
                "value": " SELECT [dbo].[FactSalesQuota].* FROM [dbo].[FactSalesQuota] "  
              },  
              {  
                "name": "_TM_ExtProp_DbTableName",  
                "value": "FactSalesQuota"  
              },  
              {  
                "name": "_TM_ExtProp_DbSchemaName",  
                "value": "dbo"  
              }  
            ]  
          }  
        ],  
        "relationships": [  
          {  
            "name": "4426b078-193f-4a59-bc52-33f990bfb7da",  
            "fromTable": "FactSalesQuota",  
            "fromColumn": "DateKey",  
            "toTable": "DimDate",  
            "toColumn": "DateKey"  
          },  
          {  
            "name": "cde1e139-4553-4d0a-a025-1cd98e35aab2",  
            "fromTable": "FactSalesQuota",  
            "fromColumn": "EmployeeKey",  
            "toTable": "DimEmployee",  
            "toColumn": "EmployeeKey"  
          }  
        ]  
      }  
    }  
  }  
}  
  
```  
  
## <a name="usage-endpoints"></a>Uso (pontos de extremidade)  
 Esse elemento de comando é usado em uma instrução do [executar método &#40;XMLA&#41; ](../../analysis-services/xmla/xml-elements-methods-execute.md) chamada por um ponto de extremidade do XMLA, exposto das seguintes maneiras:  
  
-   Como uma janela de XMLA no SQL Server Management Studio (SSMS)  
  
-   Como um arquivo de entrada para o **invoke-ascmd** cmdlet do PowerShell  
  
-   Como uma entrada para um trabalho do SQL Server Agent ou uma tarefa do SSIS  
  
 Você pode gerar um script pronto para este comando do SSMS.  Por exemplo, você pode clique um banco de dados > **Script** > **banco de dados de Script como** > **criar ou substituir a**.  
  
 O [ \[MS-SSAS-T\]: SQL Server Analysis Services Tabular (protocolo técnicos do SQL Server)](http://go.microsoft.com/fwlink/p/?LinkId=784855) documento inclui seção 3.1.5.2.2 que descreve a estrutura de objetos e comandos de metadados de tabela do JSON. Atualmente, esse documento aborda recursos ainda não implementados no script TMSL e comandos. Consulte o tópico [linguagem de script de modelo de tabela &#40;TMSL&#41; referência](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md) para fins de esclarecimento sobre o que tem suporte  

## <a name="see-also"></a>Consulte também  
 [Referência de TMSL &#40;Linguagem de Scripts de Modelo de Tabela&#41;](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md)  
  
  
