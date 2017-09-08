---
title: "Sequência de comando (TMSL) | Microsoft Docs"
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
ms.assetid: 898d6ec2-9b40-441b-be2b-5728d1d2882e
caps.latest.revision: 11
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: e7fc7f1541131ac6a8e7249940a31104e50f0b09
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="sequence-command-tmsl"></a>Comando de sequência (TMSL)

[!INCLUDE[ssas-appliesto-sql2016-later-aas](../../includes/ssas-appliesto-sql2016-later-aas.md)]

  Use o **sequência** comando para executar um conjunto consecutivo de operações no modo de lote em uma instância do Analysis Services.  O comando inteiro e todos os seus componentes devem concluir para que a transação tenha êxito.  
  
 Os seguintes comandos podem ser executados em sequência, exceto para o **atualização** comando que é executado em paralelo para processar vários objetos ao mesmo tempo.  
  
-   [Criar comando &#40; TMSL &#41;](../../analysis-services/tabular-models-scripting-language-commands/create-command-tmsl.md)  
  
-   [Comando CreateOrReplace &#40; TMSL &#41;](../../analysis-services/tabular-models-scripting-language-commands/createorreplace-command-tmsl.md)  
  
-   [Alterar o comando &#40; TMSL &#41;](../../analysis-services/tabular-models-scripting-language-commands/alter-command-tmsl.md)  
  
-   [Excluir comando &#40; TMSL &#41;](../../analysis-services/tabular-models-scripting-language-commands/delete-command-tmsl.md)  
  
-   [Atualização de comando &#40; TMSL &#41;](../../analysis-services/tabular-models-scripting-language-commands/refresh-command-tmsl.md)  
  
-   [Comando de backup &#40; TMSL &#41;](../../analysis-services/tabular-models-scripting-language-commands/backup-command-tmsl.md)  
  
-   [Restaurar comando &#40; TMSL &#41;](../../analysis-services/tabular-models-scripting-language-commands/restore-command-tmsl.md)  
  
-   [Anexar comando &#40; TMSL &#41;](../../analysis-services/tabular-models-scripting-language-commands/attach-command-tmsl.md)  
  
-   [Desanexar comando &#40; TMSL &#41;](../../analysis-services/tabular-models-scripting-language-commands/detach-command-tmsl.md)  
  
## <a name="request"></a>Solicitação  
 **maxParallelism** é uma propriedade opcional que determina se **atualização** operações executadas em sequência ou em paralelo.  
  
 O comportamento padrão é usar o paralelismo de quanto possível. Inserindo **atualizar** em **sequência**, você pode controlar o número exato de threads usados durante o processamento, incluindo limitando a apenas um segmento da operação.  
  
> [!NOTE]  
>  O número de inteiro atribuído a **maxParallelism** determina o número máximo de threads usados durante o processamento. Os valores válidos são qualquer inteiro positivo. Definir o valor para 1 equals não paralelas (usa um thread).  
  
 Somente **atualização** é executado em paralelo. Se você modificar **maxParallelism** para usar um número fixo de threads, certifique-se de examinar as propriedades de [de atualização de comando &#40; TMSL &#41; ](../../analysis-services/tabular-models-scripting-language-commands/refresh-command-tmsl.md) para entender o impacto potencial. É possível definir propriedades de uma maneira que distorcerem paralelismo, mesmo quando você fez vários threads disponíveis. A seguinte sequência de atualização de tipos fornecem o melhor grau de paralelismo:  
  
-   Primeiro, especifique a atualização para todos os objetos usando ClearValues  
  
-   Em seguida, especifique a atualização para todos os objetos usando DataOnly  
  
-   Especificar última atualização para todos os objetos usando completo, Calculate, automático ou adicionar  
  
 Qualquer variação Isso interromperá o paralelismo.  
  
```  
{   
  "sequence":    
    {   
      "maxParallelism": 3,   
      "operations": [   
        {   
          "mergepartitions": {   
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
        },   
        {   
          "refresh": {   
            "type": "calculate",   
            "object": {   
             "database": "salesdatabase"   
            }   
          }   
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
  
 Você não pode gerar um script pronto para este comando do SSMS. Em vez disso, você pode começar com um exemplo ou escrever suas próprias.  
  
 O [ \[MS-SSAS-T\]: SQL Server Analysis Services Tabular (protocolo técnicos do SQL Server)](http://go.microsoft.com/fwlink/p/?LinkId=784855) documento inclui seção 3.1.5.2.2 que descreve a estrutura de objetos e comandos de metadados de tabela do JSON . Atualmente, esse documento aborda recursos ainda não implementados no script TMSL e comandos. Consulte o tópico ([linguagem de script de modelo de tabela &#40; TMSL &#41; Referência](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md)) para fins de esclarecimento sobre o que tem suporte.  
  
## <a name="see-also"></a>Consulte também  
 [Referência de TMSL &#40;Linguagem de Scripts de Modelo de Tabela&#41;](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md)  
  
  
