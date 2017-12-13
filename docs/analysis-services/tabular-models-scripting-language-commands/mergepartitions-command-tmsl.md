---
title: Comando MergePartitions (TMSL) | Microsoft Docs
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
ms.assetid: dd568426-a415-41bf-b1e9-ea2261babf81
caps.latest.revision: "8"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 5e8ea1e0ea3614926c05c50374dd9b00a527cec0
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/08/2017
---
# <a name="mergepartitions-command-tmsl"></a>Comando MergePartitions (TMSL)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]Mescla os dados de uma ou mais partições de origem em uma partição de destino e, em seguida, exclui a partição de origem. A consulta SQL da partição de destino não será atualizada como parte da mesclagem. Para garantir que o processamento subsequente da partição recupera todos os dados, você deve revisar a consulta para que ele seleciona todos os dados na partição mesclada.  
  
## <a name="request"></a>Solicitação  
 Você deve especificar o banco de dados, tabela e partições de origem e destino. Só é possível mesclar partições da mesma tabela.  
  
```  
{   
  "mergePartitions": {   
    "object": {   
      "database": "salesdatabase",   
      "table": "sales",   
      "partition": "may2015"   
    },   
    "sources": [   
      {   
        "database": "salesdatabase",   
        "table": "Sales",   
        "partition": "partition1"   
      },   
      {   
        "database": "salesdatabase",   
        "table": "Sales",   
        "partition": "partition2"   
      }   
    ]   
  }   
}  
  
```  
  
## <a name="response"></a>Resposta  
 Retorna um resultado vazio quando o comando terá êxito. Caso contrário, uma exceção XMLA é retornada.  
  
## <a name="usage-endpoints"></a>Uso (pontos de extremidade)  
 Esse elemento de comando é usado em uma instrução do [executar método &#40; XMLA &#41; ](../../analysis-services/xmla/xml-elements-methods-execute.md) chamada por um ponto de extremidade do XMLA, exposto das seguintes maneiras:  
  
-   Como uma janela de XMLA no SQL Server Management Studio (SSMS)  
  
-   Como um arquivo de entrada para o **invoke-ascmd** cmdlet do PowerShell  
  
-   Como uma entrada para um trabalho do SQL Server Agent ou uma tarefa do SSIS  
  
 Você pode gerar um script pronto para este comando do SSMS.  Por exemplo, você pode clicar no **Script** na caixa de diálogo de gerenciamento de partição.  
  
 O [ \[MS-SSAS-T\]: SQL Server Analysis Services Tabular (protocolo técnicos do SQL Server)](http://go.microsoft.com/fwlink/p/?LinkId=784855) documento inclui seção 3.1.5.2.2 que descreve a estrutura de objetos e comandos de metadados de tabela do JSON. Atualmente, esse documento aborda recursos ainda não implementados no script TMSL e comandos. Consulte o tópico [linguagem de script de modelo de tabela &#40; TMSL &#41; Referência](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md) para fins de esclarecimento sobre o que tem suporte  

## <a name="see-also"></a>Consulte também  
 [Referência de TMSL &#40;Linguagem de Scripts de Modelo de Tabela&#41;](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md)   
 [Criar e gerenciar partições de modelos de tabela &#40;SSAS de Tabela&#41;](../../analysis-services/tabular-models/create-and-manage-tabular-model-partitions-ssas-tabular.md)  
  
  
