---
title: Alterar o comando (TMSL) | Microsoft Docs
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
ms.assetid: 8bdc49f1-209e-4055-be19-c83862b81efa
caps.latest.revision: 13
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 48567b03017e6ded0aba940b64ef1db52e7f78a1
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="alter-command-tmsl"></a>Comando ALTER (TMSL)

[!INCLUDE[ssas-appliesto-sql2016-later-aas](../../includes/ssas-appliesto-sql2016-later-aas.md)]

  Altera um objeto existente, mas não seus filhos em uma instância do Analysis Services no modo de tabela.  Se o objeto não existir, o comando gera um erro.  
  
 Use **Alter** comando para atualizações de destino, como definir uma propriedade em uma tabela sem a necessidade de especificar todas as colunas também. Esse comando é semelhante a **CreateOrReplace**, mas sem a necessidade de ter que fornecer uma definição completa do objeto.  
  
 Para objetos têm propriedades de leitura / gravação, se você especificar uma propriedade de leitura / gravação, será necessário especificar todos os valores existentes ou -los usando o novo. Você pode usar o PowerShell do AMO para obter uma lista de propriedades. 
  
## <a name="request"></a>Solicitação  
 **ALTER** não tem nenhum atributo. Entradas incluem o objeto a ser alterado, seguido pela definição do objeto modificado.  
  
 O exemplo a seguir ilustra a sintaxe para alterar uma propriedade em um objeto de partição. O caminho do objeto estabelece qual partição é de objeto a ser alterado por meio de pares nome-valor de objetos pai. A segunda entrada é um objeto de partição que especifica o novo valor da propriedade.  
  
```  
{   
  "alter": {   
    "object": {   
      "database": "\<database-name>",   
      "table": "\<table-name>",   
      "partition": "\<partition-name>"   
    },   
    "partition": {   
      "name": "\<new-partition-name>",   
       . . .  << other properties   
    }   
  }   
}   
```  
  
 A estrutura da solicitação varia com base no objeto. **ALTER** pode ser usado com qualquer um dos seguintes objetos:  
  
 [Objeto de banco de dados &#40; TMSL &#41; ](../../analysis-services/tabular-models-scripting-language-objects/database-object-tmsl.md) Renomear um banco de dados.  
  
```  
"alter": {   
    "object": {   
      "database": "\<database-name>"  
    },   
    "database": {   
      "name": "\<new-database-name>",   
    }   
  }   
```  
  
 [Objeto de fonte de dados &#40; TMSL &#41; ](../../analysis-services/tabular-models-scripting-language-objects/datasources-object-tmsl.md) Renomear uma conexão, o que é um objeto filho do banco de dados.  
  
```  
{   
   "alter":{   
      "object":{   
         "database":"AdventureWorksTabular1200",  
         "dataSource":"SqlServer localhost AdventureworksDW2016"  
      },  
      "dataSource":{   
         "name":"A new connection name"  
      }  
   }  
}  
```  
  
 [Objeto Tables &#40; TMSL &#41; ](../../analysis-services/tabular-models-scripting-language-objects/tables-object-tmsl.md) Consulte **exemplo 1** abaixo.  
  
 [Objeto de partições &#40; TMSL &#41; ](../../analysis-services/tabular-models-scripting-language-objects/partitions-object-tmsl.md) Consulte **exemplo 2** abaixo.  
  
 [Objeto de funções &#40; TMSL &#41; ](../../analysis-services/tabular-models-scripting-language-objects/roles-object-tmsl.md) Alterar uma propriedade em um objeto de função.  
  
```  
{   
   "alter":{   
      "object":{   
         "database":"AdventureWorksTabular1200",  
         "role":"DataReader"  
      },  
      "role":{   
         "name":"New Name"  
      }  
   }  
}  
```  
  
## <a name="response"></a>Resposta  
 Retorna um resultado vazio quando o comando terá êxito. Caso contrário, uma exceção XMLA é retornada.  
  
## <a name="examples"></a>Exemplos  
 Os exemplos a seguir demonstram o script que você pode executar em uma janela XMLA no Management Studio ou usar como entrada em [cmdlet Invoke-ASCmd](../../analysis-services/powershell/invoke-ascmd-cmdlet.md) no AMO PowerShell.  
  
 **Exemplo 1** -esse script altera a propriedade de nome em uma tabela.  
  
```  
{   
  "alter": {   
    "object": {   
      "database": "AdventureWorksDW2016",   
      "table": "DimDate"  
    },   
    "table": {   
      "name": "DimDate2"  
    }   
  }   
}  
```  
  
 Supondo que uma instância nomeada local (nome da instância é "tabular") e um arquivo JSON com o script alter, esse comando altera o nome de uma tabela de DimDate para DimDate2:  
  
 `invoke-ascmd -inputfile '\\my-computer\my-shared-folder\altertablename.json' -server 'localhost\Tabular'`  
  
 **Exemplo 2** – este script renomeia uma partição, por exemplo, no final do ano ao ano atual se torna o ano anterior. Certifique-se de especificar todas as propriedades. Se você deixar **origem** não for especificado, ele pode interromper todas as suas definições de partição existente.  
  
 A menos que você está criando, substituindo, ou alterando o próprio objeto de fonte de dados, qualquer fonte de dados referenciado em seu script (como o script de partição abaixo) deve ser um existente **DataSource** objeto em seu modelo. Se você precisar alterar a fonte de dados, fazer isso como uma etapa separada.  
  
```  
{   
  "alter": {   
    "object": {   
      "database": "InternetSales",   
      "table": "DimDate",  
      "partition": "CurrentYear"  
    },   
    "partition": {   
      "name": "Year2009",  
       "source": {  
             "query":  "SELECT [dbo].[DimDate].* FROM [dbo].[DimDate] WHERE [dbo].[DimDate].CalendarYear = 2009",  
              "dataSource": "SqlServer localhost AdventureworksDW2016"  
        }  
    }   
  }   
}  
```  
  
## <a name="usage-endpoints"></a>Uso (pontos de extremidade)  
 Esse elemento de comando é usado em uma instrução do [executar método &#40; XMLA &#41; ](../../analysis-services/xmla/xml-elements-methods-execute.md) chamada por um ponto de extremidade do XMLA, exposto das seguintes maneiras:  
  
-   Como uma janela de XMLA no SQL Server Management Studio (SSMS)  
  
-   Como um arquivo de entrada para o **invoke-ascmd** cmdlet do PowerShell  
  
-   Como uma entrada para um trabalho do SQL Server Agent ou uma tarefa do SSIS  
  
 Você não pode gerar um script pronto para este comando do SSMS. Em vez disso, você pode começar com um exemplo ou escrever suas próprias.  
  
 O [ \[MS-SSAS-T\]: SQL Server Analysis Services Tabular (protocolo técnicos do SQL Server)](http://go.microsoft.com/fwlink/p/?LinkId=784855) documento inclui seção 3.1.5.2.2 que descreve a estrutura de objetos e comandos de metadados de tabela do JSON. Atualmente, esse documento aborda recursos ainda não implementados no script TMSL e comandos. Consulte o tópico ([linguagem de script de modelo de tabela &#40; TMSL &#41; Referência](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md)) para fins de esclarecimento sobre o que tem suporte.  

## <a name="see-also"></a>Consulte também  
 [Referência de TMSL &#40;Linguagem de Scripts de Modelo de Tabela&#41;](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md)  
  
  

