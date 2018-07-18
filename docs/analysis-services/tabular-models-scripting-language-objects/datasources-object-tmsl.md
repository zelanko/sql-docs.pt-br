---
title: Objeto DataSources (TMSL) | Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tmsl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 7beabaaf63194cc699c3711a87dd1e59d244c068
ms.sourcegitcommit: c7a98ef59b3bc46245b8c3f5643fad85a082debe
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/12/2018
ms.locfileid: "38981328"
---
# <a name="datasources-object-tmsl"></a>Objeto DataSources (TMSL)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  Define uma conexão a uma fonte de dados usada pelo modelo durante a importação para adicionar dados ao modelo, ou em consultas passagem por meio do modo DirectQuery.  Modelos no modo DirectQuery só podem ter uma **fonte de dados** objeto.  
  
 A menos que você está criando, substituindo, ou alterando o próprio objeto de fonte de dados, qualquer fonte de dados referenciado no script (como no script de partição) deve ser um existente **fonte de dados** objeto em seu modelo.  
  
## <a name="object-definition"></a>Definição do objeto  
 Todos os objetos têm um conjunto comum de propriedades, incluindo nome, tipo, descrição, uma coleção de propriedades e anotações. **Fonte de dados** objetos também têm as propriedades a seguir.  
  
 Tipo  
 O tipo de DataSource. No momento, o único valor válido é o provedor (1) - cadeia de caracteres de conexão Normal.  
  
 connectionString  
 A cadeia de conexão que no mínimo Especifica o servidor e banco de dados, mas também pode incluir outras propriedades compatíveis com o RDBMS externo, como uma conta de usuário ou o provedor de dados. Esse valor é necessário. Ver [classe SqlConnectionStringBuilder](https://msdn.microsoft.com/library/ms254500\(v=vs.110\).aspx) para obter detalhes sobre o SQL Server do banco de dados propriedades de cadeia de caracteres de conexão.  
  
 impersonationMode  
 Especifica se o Analysis Services deve representar a identidade do usuário que está solicitando a consulta. Essa propriedade é um valor numérico que especifica as credenciais a usar para representação. Os valores de enumeração são os seguintes:  
  
-   Padrão (1) - o servidor usa o método de representação que ele considera para ser apropriada para o contexto no qual a representação é usada.  
  
-   ImpersonateAccount (2) - o servidor usa a conta de usuário especificada.  
  
-   ImpersonateAnonymous (3) - o servidor usa a conta de usuário anônimo.  Essa opção não é recomendada, mas às vezes é usada em cenários de acesso HTTP por aplicativos personalizados que lidar com a autenticação.  
  
-   ImpersonateCurrentUser (4) - o servidor usa a conta de usuário que o cliente está se conectando como.  
  
-   ImpersonateServiceAccount (5) - o servidor usa a conta de usuário que o servidor estiver em execução.  
  
-   ImpersonateUnattendedAccount (6) – o servidor usa uma conta de usuário autônoma. Isso é usado para modelos do PowerPivot ou Tabular que são executados em um ambiente do SharePoint.  
  
 O modo DirectQuery pode usar impersonateCurrentuser se o Analysis Services está configurado para delegação confiável, ou  
                      impersonateServiceAccount se a solicitação de consulta é feita no contexto de segurança da conta de serviço do Analysis Services. Ver [delegação restrita de configurar o Analysis Services para Kerberos](../../analysis-services/instances/configure-analysis-services-for-kerberos-constrained-delegation.md).  
  
 account  
 Usado para representação. Uma conta do Windows ou o banco de dados que tem um logon válido com permissões de leitura no banco de dados externo.  
  
 password  
 Uma cadeia de caracteres criptografada fornecendo a senha da conta.  
  
 maxConnections  
 O número máximo de conexões a serem abertas simultaneamente para a fonte de dados.  
  
 isolation  
 O tipo de isolamento usado durante a execução de comandos na fonte de dados. Os valores válidos são ReadCommitted (1) ou instantâneo (2).  
  
 tempo limite  
 Um inteiro que especifica o tempo limite em segundos para comandos executados na fonte de dados.  
  
 provedor  
 Uma cadeia de caracteres opcional que identifica o nome do provedor de dados gerenciado usado na conexão de banco de dados relacional, se não especificado em contrário na cadeia de conexão.  
  
## <a name="usage"></a>Uso  
 **Fonte de dados** objetos são usados no [comando Alter &#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-commands/alter-command-tmsl.md), [criar comando &#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-commands/create-command-tmsl.md), [comando CreateOrReplace &#40; TMSL&#41;](../../analysis-services/tabular-models-scripting-language-commands/createorreplace-command-tmsl.md), [comando Delete &#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-commands/delete-command-tmsl.md), [comandos de atualização &#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-commands/refresh-command-tmsl.md), e [comando MergePartitions &#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-commands/mergepartitions-command-tmsl.md).  
  
 Um **fonte de dados** é uma propriedade de um modelo de objeto, mas também pode ser especificado como uma propriedade de um objeto de banco de dados, considerando o mapeamento entre o modelo e o banco de dados.  Partições com base em consultas SQL também especificam um **fonte de dados**, apenas com um conjunto reduzido de propriedades.  
  
 Ao criar, substituir ou alterar um objeto de fonte de dados, especifique todas as propriedades de leitura / gravação da definição do objeto. A omissão de uma propriedade de leitura / gravação é considerada uma exclusão.  
  
## <a name="examples"></a>Exemplos  
 **Exemplo 1** -uma conexão para um *FoodMart* banco de dados em um instância nomeado do controle remoto *vendas* em um servidor de rede denominado *Server01*.  
  
```  
"dataSources": [  
      {  
        "name": "SqlServer Server01 FoodMart",  
        "connectionString": "Provider=SQLNCLI11;Data Source=Server01\Sales;Initial Catalog=Foodmart;Integrated Security=SSPI;Persist Security Info=false",  
        "impersonationMode": "impersonateServiceAccount",  
      }  
]  
```  
  
## <a name="full-syntax"></a>Sintaxe completa  
 Abaixo está a representação de esquema de um objeto de fonte de dados de um modelo.  
  
```  
"dataSources": {  
          "type": "array",  
          "items": {  
            "anyOf": [  
              {  
                "description": "ProviderDataSource object of Tabular Object Model (TOM)",  
                "type": "object",  
                "properties": {  
                  "name": {  
                    "type": "string"  
                  },  
                  "description": {  
                    "type": "string"  
                  },  
                  "type": {  
                    "enum": [  
                      "provider"  
                    ]  
                  },  
                  "connectionString": {  
                    "type": "string"  
                  },  
                  "impersonationMode": {  
                    "enum": [  
                      "default",  
                      "impersonateAccount",  
                      "impersonateAnonymous",  
                      "impersonateCurrentUser",  
                      "impersonateServiceAccount",  
                      "impersonateUnattendedAccount"  
                    ]  
                  },  
                  "account": {  
                    "type": "string"  
                  },  
                  "password": {  
                    "type": "string"  
                  },  
                  "maxConnections": {  
                    "type": "integer"  
                  },  
                  "isolation": {  
                    "enum": [  
                      "readCommitted",  
                      "snapshot"  
                    ]  
                  },  
                  "timeout": {  
                    "type": "integer"  
                  },  
                  "provider": {  
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
        },  
  
```  
  
## <a name="see-also"></a>Consulte também  
 [Referência de TMSL &#40;Linguagem de Scripts de Modelo de Tabela&#41;](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md)   
 [Modo DirectQuery](../../analysis-services/tabular-models/directquery-mode-ssas-tabular.md)   
 [Configurar o acesso HTTP ao Analysis Services no IIS &#40;(Serviços de Informações da Internet)&#41; 8.0](../../analysis-services/instances/configure-http-access-to-analysis-services-on-iis-8-0.md)  
  
  
