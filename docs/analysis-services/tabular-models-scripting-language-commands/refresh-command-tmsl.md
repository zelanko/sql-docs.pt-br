---
title: "Atualização de comando (TMSL) | Microsoft Docs"
ms.custom: 
ms.date: 05/30/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: 97ff6ba8-c236-4ba6-8220-b0fcb9e1dc5c
caps.latest.revision: 14
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: d66a5c0ccaccf6480e0e82053b1ca6f22c5fcc0f
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="refresh-command-tmsl"></a>Atualização de comando (TMSL)

[!INCLUDE[ssas-appliesto-sql2016-later-aas](../../includes/ssas-appliesto-sql2016-later-aas.md)]

  Processa objetos no banco de dados atual.   
**Atualizar** sempre é executado em paralelo, a menos que você acelerar com [de sequência de comando &#40; TMSL &#41; ](../../analysis-services/tabular-models-scripting-language-commands/sequence-command-tmsl.md).  
  
 Você pode substituir algumas propriedades de alguns objetos durante uma operação de atualização de dados:  
  
-   Alterar o **QueryDefinition** propriedade de um **partição** objeto para importar dados usando uma expressão de filtro durante a execução.  
  
-   Fornecer credenciais de fonte de dados como parte de um **atualizar** comando no **ConnectionString** propriedade de um **fonte de dados** objeto. Essa abordagem pode ser considerada mais segura, como as credenciais são fornecidas e usadas temporariamente para a duração da operação, em vez de armazenados.  
  
 Consulte os exemplos neste tópico para obter uma ilustração essas substituições de propriedade.  
  
> [!NOTE]  
>  Ao contrário do processamento multidimensional, não há nenhum tratamento especial de processamento de erros de processamento de tabela.  

  
## <a name="request"></a>Solicitação  
 **Atualizar** usa uma definição de objeto e o parâmetro de tipo.  
  
```  
    {  
        "refresh": {  
            "description": "Parameters of Refresh command of Analysis Services JSON API",  
            "properties": {  
            "type": {  
                "enum": [  
                "full",  
                "clearValues",  
                "calculate",  
                "dataOnly",  
                "automatic",  
                "add",  
                "defragment"  
                ]  
            },  
            "objects": {  
. . .   
```  
  
 O **tipo** parâmetro define um escopo para a operação de processamento.  
  
||||  
|-|-|-|  
|**Tipo de atualização**|**Aplica-se a**|**Description**|  
|completa|Banco de dados<br />Tabela,<br />Partition|Para todas as partições na partição, tabela ou banco de dados especificado, atualize os dados e recalcule todos os dependentes. Para uma partição de cálculo, recalcule a partição e todos os seus dependentes.|  
|clearValues|Banco de dados<br />Tabela,<br />Partition|Limpe os valores nesse objeto e todos os seus dependentes.|  
|calcular|Banco de dados<br />Tabela,<br />Partition|Recalcule este objeto e todos os seus dependentes, mas somente se necessário. Esse valor não força o recálculo, exceto fórmulas voláteis.|  
|dataOnly|Banco de dados<br />Tabela,<br />Partition|Atualize os dados neste objeto e limpe todos os dependentes.|  
|automatic|Banco de dados<br />Tabela,<br />Partition|Se o objeto precisar ser atualizado e recalculado, atualize e recalcule o objeto e todos os seus dependentes. Será aplicado se a partição estiver em um estado diferente de Ready.|  
|add|Partition|Acrescente dados a esta partição e recalcule todos os dependentes. Este comando é válido apenas para partições regulares, e não para partições de cálculo.|  
|desfragmentar|Banco de dados<br />Table|Desfragmente os dados na tabela especificada. Como os dados são adicionados ou removidos de uma tabela, os dicionários de cada coluna podem ficar poluídos com valores que não existem mais nos valores de coluna reais. A opção de desfragmentar limpará os valores nos dicionários que não são mais usados.|  
  
 Você pode atualizar os seguintes objetos:  
  
 [Objeto de banco de dados &#40; TMSL &#41; ](../../analysis-services/tabular-models-scripting-language-objects/database-object-tmsl.md) Processar um banco de dados.  
  
```  
{  
  "refresh": {  
    "type": "automatic",  
    "objects": [  
      {  
        "database": "AdventureWorksTabular1200"  
      }  
    ]  
  }  
}  
```  
  
 [Objeto Tables &#40; TMSL &#41; ](../../analysis-services/tabular-models-scripting-language-objects/tables-object-tmsl.md) Processar uma única tabela.  
  
```  
{  
  "refresh": {  
    "type": "automatic",  
    "objects": [  
      {  
        "database": "AdventureWorksTabular1200",  
        "table": "Date"  
      }  
    ]  
  }  
}  
```  
  
 [Objeto de partições &#40; TMSL &#41; ](../../analysis-services/tabular-models-scripting-language-objects/partitions-object-tmsl.md) Processar uma única partição em uma tabela.  
  
```  
{  
  "refresh": {  
    "type": "automatic",  
    "objects": [  
      {  
        "database": "AdventureWorksTabular1200",  
        "table": "FactSalesQuota",  
        "partition": "FactSalesQuota"  
      },  
      {  
        "database": "AdventureWorksTabular1200",  
        "table": "FactSalesQuota",  
        "partition": "FactSalesQuota - 2011"  
      }  
    ]  
  }  
}  
```  
  
## <a name="response"></a>Resposta  
 Retorna um resultado vazio quando o comando terá êxito. Caso contrário, uma exceção XMLA é retornada.  
  
## <a name="examples"></a>Exemplos  
 Substituir ambos os **ConnectionString** e definição de uma partição de consulta.  
  
```  
{   
    "refresh": {   
        "type": "data",   
        "objects": [   
            {   
                "database": "tmtestdb",   
                "table": "sales"   
            },   
            {   
                "database": "tmtestdb",   
                "table": "customer"   
            }   
        ],   
        "overrides": [   
            {   
                "dataSources": [ // Bindings for Data Sources   
                    {   
                        "object": {   
                            "database": "tmtestdb",   
                            "dataSource": "contoso"   
                        },   
                        "dataSource": {   
                        "connectionString": "Provider=SQLNCLI11;Data Source=localhost;Initial Catalog=contoso;Integrated Security=SSPI;Persist Security Info=false"   
"   
                        }   
                    }   
                ],   
                "partitions": [ // Bindings for Partitions   
                    {   
                        "object": {   
                            "database": "tmtestdb",   
                            "table": "sales",   
                            "partition": "2015"   
                        },   
                        "partition": {   
                            "source": {   
                                "query": [  
                                     "SELECT sales.salesamount, customer.customername FROM sales",  
                                     "JOIN customer on custKey = sales.custkey",  
                                     "JOIN date on date.DateKey = customer.OrderDate",  
                                     "WHERE date.CalendarYear='2015'"  
                                  ],  
                            }   
                        }   
                    }   
                ]   
            }   
        ]   
    }   
}   
```  
  
 Substituições de escopo específico, definindo o parâmetro de tipo para um **dataOnly** atualização de metadados permanece intacto.  
  
```  
{   
        "refresh" : {   
            "type" : "dataOnly",   
            "objects" : [   
                {   
                    "database" : "TMTestDB",   
                    "table" : "Customer"   
                },   
                {   
                    "database" : "TMTestDB",   
                    "table" : "Sales"   
                }   
            ],   
            "overrides" : [{   
                "scope" : {   
                    "database" : "TMTestDB",   
                    "table" : "Sales"   
                },   
                "dataSources" : [{   
                    "originalObject" : {   
                        "dataSource" : "SqlServer sqlcldb2 AS_foodmart_2000"   
                    },   
                    "connectionString" : "Provider=SQLNCLI11;Data Source=sqlcldb2;Initial Catalog=AS_foodmart_2000;Integrated Security=SSPI;Persist Security Info=false"   
                }]   
            }]   
        }   
    }   
```  
  
## <a name="usage-endpoints"></a>Uso (pontos de extremidade)  
 Esse elemento de comando é usado em uma instrução do [executar método &#40; XMLA &#41; ](../../analysis-services/xmla/xml-elements-methods-execute.md) chamada por um ponto de extremidade do XMLA, exposto das seguintes maneiras:  
  
-   Como uma janela de XMLA no SQL Server Management Studio (SSMS)  
  
-   Como um arquivo de entrada para o **invoke-ascmd** cmdlet do PowerShell  
  
-   Como uma entrada para um trabalho do SQL Server Agent ou uma tarefa do SSIS  
  
 Você pode gerar um script pronto para este comando do SSMS.  Por exemplo, você pode clicar no **Script** em uma caixa de diálogo de processamento.  
  
 O [ \[MS-SSAS-T\]: SQL Server Analysis Services Tabular (protocolo técnicos do SQL Server)](http://go.microsoft.com/fwlink/p/?LinkId=784855) documento inclui seção 3.1.5.2.2 que descreve a estrutura de objetos e comandos de metadados de tabela do JSON. Atualmente, esse documento aborda recursos ainda não implementados no script TMSL e comandos. Consulte o tópico ([linguagem de script de modelo de tabela &#40; TMSL &#41; Referência](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md)) para fins de esclarecimento sobre o que tem suporte.  
  
## <a name="see-also"></a>Consulte também  
 [Referência de TMSL &#40;Linguagem de Scripts de Modelo de Tabela&#41;](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md)   
 [Opções de processamento e as configurações de &#40; Analysis Services &#41;](../../analysis-services/multidimensional-models/processing-options-and-settings-analysis-services.md)  
  
  

