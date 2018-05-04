---
title: Restaurar o comando (TMSL) | Microsoft Docs
ms.custom: ''
ms.date: 05/30/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 360a1567-67ae-459d-8865-9a2bef8d4186
caps.latest.revision: 13
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: bf1b4e2bdb8cfd9473c0c3b6fcd67909ad5d31c1
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="restore-command-tmsl"></a>Restaurar o comando (TMSL)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  Restaura um banco de dados do Analysis Services de um arquivo de backup.  
  
## <a name="request"></a>Solicitação  
  
```  
    {  
"restore": {  
            "description": "Parameters of Restore command of Analysis Services JSON API",  
            "properties": {  
            "database": {  
                "type": "string"  
            },  
            "file": {  
                "type": "string"  
            },  
            "password": {  
                "type": "string"  
            },  
            "dbStorageLocation": {  
                "type": "string"  
            },  
            "allowOverwrite": {  
                "type":boolean  
            },  
            "readWriteMode": {  
                "enum": [  
                "readWrite",  
                "readOnly",  
                "readOnlyExclusive"  
                ]  
. . .   
```  
  
 **Restaurar** tem várias propriedades.  
  
||||  
|-|-|-|  
|**Propriedade**|**Default**|**Descrição**|  
|Banco de Dados|[Obrigatório]|O nome do objeto de banco de dados a ser restaurado.|  
|file|[Obrigatório]|O nome do arquivo de backup/caminho.|  
|password|Empty (vazio)|A senha a ser usada para descriptografar o arquivo de backup.|  
|allowOverwrite|Falso|Um booliano que, quando for verdadeiro, indica que um arquivo de backup já existente será substituído; Caso contrário, false.|  
|readWriteMode|ReadWrite|Um valor de enumeração que indica os modos de acesso permitidos para o banco de dados.<br /><br /> **Os valores de enumeração são os seguintes:**<br /><br /> readWrite – acesso de leitura / gravação é permitido.<br /><br /> somente leitura – acesso somente leitura é permitido.<br /><br /> readOnlyExclusive – acesso exclusivo somente leitura é permitido.|  
|dbStorageLocation|Empty (vazio)|Local de armazenamento para o banco de dados restaurado.|  
  
## <a name="response"></a>Resposta  
 Retorna um resultado vazio quando o comando terá êxito. Caso contrário, uma exceção XMLA é retornada.  
  
## <a name="example"></a>Exemplo  
 **Exemplo 1** -restaurar um banco de dados de uma pasta local.  
  
```  
{   
   "restore": {   
      "database":"AdventureWorksDW2014",  
      "file":"c:\\awdbdwfile.abf",  
      "security":"...",  
      "allowOverwrite":"true",  
      "password":"..",  
      "locations":"d:\\SQL Server Analysis Services\\data\\",  
      "storageLocation":".."  
   }  
}  
```  
  
## <a name="usage-endpoints"></a>Uso (pontos de extremidade)  
 Esse elemento de comando é usado em uma instrução do [executar método &#40;XMLA&#41; ](../../analysis-services/xmla/xml-elements-methods-execute.md) chamada por um ponto de extremidade do XMLA, exposto das seguintes maneiras:  
  
-   Como uma janela de XMLA no SQL Server Management Studio (SSMS)  
  
-   Como um arquivo de entrada para o **invoke-ascmd** cmdlet do PowerShell  
  
-   Como uma entrada para um trabalho do SQL Server Agent ou uma tarefa do SSIS  
  
 Você pode gerar um script pronto para este comando do SSMS, clique no botão de Script na caixa de diálogo de restauração.  
  
 O [ \[MS-SSAS-T\]: SQL Server Analysis Services Tabular (protocolo técnicos do SQL Server)](http://go.microsoft.com/fwlink/p/?LinkId=784855) documento inclui seção 3.1.5.2.2 que descreve a estrutura de objetos e comandos de metadados de tabela do JSON. Atualmente, esse documento aborda recursos ainda não implementados no script TMSL e comandos. Consulte o tópico [linguagem de script de modelo de tabela &#40;TMSL&#41; referência](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md) para fins de esclarecimento sobre o que tem suporte  
  
## <a name="see-also"></a>Consulte também  
 [Referência de TMSL &#40;Linguagem de Scripts de Modelo de Tabela&#41;](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md)   
 [Backup e restauração de bancos de dados do Analysis Services](../../analysis-services/multidimensional-models/backup-and-restore-of-analysis-services-databases.md)  
  
  
