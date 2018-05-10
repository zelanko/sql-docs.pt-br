---
title: Comando (TMSL) | Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: tabular-models
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 90766fb06141f290e5b6a284332a48a9944b2764
ms.sourcegitcommit: 1aedef909f91dc88dc741748f36eabce3a04b2b1
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/08/2018
---
# <a name="synchronize-command-tmsl"></a>Sincronizar comando (TMSL)
[!INCLUDE[ssas-appliesto-sqlas-all](../../includes/ssas-appliesto-sqlas-all.md)]

  Sincroniza um banco de dados do Analysis Services com outro banco de dados existente.  
  
## <a name="request"></a>Solicitação  
 Comando para sincronizar as propriedades aceitas por JSON são da seguinte maneira.  
  
```  
{   
   "synchronize":{   
      "database":"AdventureWorksDW_Production",  
      "source":"Provider=MSOLAP.7;Data Source=localhost;Integrated Security=SSPI;Initial Catalog=AdventureWorksDW_Dev",  
      "synchronizeSecurity":"copyAll",  
      "applyCompression":true  
   }  
}  
```  
  
 Comando para sincronizar as propriedades aceitas por JSON são da seguinte maneira.  
  
||||  
|-|-|-|  
|**Propriedade**|**Default**|**Descrição**|  
|Banco de Dados||O nome do objeto de banco de dados a serem sincronizados.|  
|origem||A cadeia de caracteres de conexão para usar para se conectar ao servidor de origem.|  
|synchronizeSecurity|skipMembership|Um valor de enumeração que especifica como restaurar definições de segurança, incluindo funções e permissões. Os valores válidos incluem skipMembership, copyAll, ignoreSecurity.|  
|applyCompression|Verdadeiro|Um booliano que, quando for verdadeiro, indica que a compactação será aplicado durante a operação de sincronização. Caso contrário, false.|  
  
## <a name="response"></a>Resposta  
 Retorna um resultado vazio quando o comando terá êxito. Caso contrário, uma exceção XMLA é retornada.  
  
## <a name="usage-endpoints"></a>Uso (pontos de extremidade)  
 Esse elemento de comando é usado em uma instrução do [executar método &#40;XMLA&#41; ](../../analysis-services/xmla/xml-elements-methods-execute.md) chamada por um ponto de extremidade do XMLA, exposto das seguintes maneiras:  
  
-   Como uma janela de XMLA no SQL Server Management Studio (SSMS)  
  
-   Como um arquivo de entrada para o **invoke-ascmd** cmdlet do PowerShell  
  
-   Como uma entrada para um trabalho do SQL Server Agent ou uma tarefa do SSIS  
  
 Você pode gerar um script pronto para este comando do SSMS, clique no botão de Script na caixa de diálogo Sincronizar banco de dados.  
  
 O [ \[MS-SSAS-T\]: SQL Server Analysis Services Tabular (protocolo técnicos do SQL Server)](http://go.microsoft.com/fwlink/p/?LinkId=784855) documento inclui seção 3.1.5.2.2 que descreve a estrutura de objetos e comandos de metadados de tabela do JSON. Atualmente, esse documento aborda recursos ainda não implementados no script TMSL e comandos. Consulte o tópico [linguagem de script de modelo de tabela &#40;TMSL&#41; referência](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md) para fins de esclarecimento sobre o que tem suporte  
  
## <a name="see-also"></a>Consulte também  
 [Referência de TMSL &#40;Linguagem de Scripts de Modelo de Tabela&#41;](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md)  
  
  
