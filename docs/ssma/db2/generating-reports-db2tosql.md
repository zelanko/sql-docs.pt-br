---
title: Geração de relatórios (DB2ToSQL) | Microsoft Docs
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-db2
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 69ef5fd9-190d-4c58-8199-b3f77d5e1883
caps.latest.revision: 5
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 8938e54e18b5f9d4eef4cf657d53d447ff39b24c
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="generating-reports-db2tosql"></a>Geração de relatórios (DB2ToSQL)
Os relatórios de certas atividades executadas usando os comandos são gerados no Console SSMA no nível de árvore de objeto.  
  
Use o procedimento a seguir para gerar relatórios:  
  
1.  Especifique o **gravação-resumo-relatório-para** parâmetro. O relatório relacionado é armazenado como o nome do arquivo (se especificado) ou na pasta que você especificar. O nome do arquivo é predefinida pelo sistema conforme mencionado na tabela a seguir onde, **&lt;n&gt;** é o número de arquivo exclusivo que é incrementada com um dígito com cada execução do mesmo comando.  
  
    Os comandos de vis-relação de relatórios são:  
  
    ||||  
    |-|-|-|  
    |**Sl. Não.**|**Comando**|**Título do relatório**|  
    |1|relatório gerar de avaliação|AssessmentReport&lt;n&gt;.XML|  
    |2|convert-schema|SchemaConversionReport&lt;n&gt;.XML|  
    |3|migrar dados|DataMigrationReport&lt;n&gt;.XML|  
    |4|convert-sql-statement|ConvertSQLReport&lt;n&gt;.XML|  
    |5|Sincronizar de destino|TargetSynchronizationReport&lt;n&gt;.XML|  
    |6|atualização do banco de dados|SourceDBRefreshReport&lt;n&gt;.XML|  
  
    > [!IMPORTANT]  
    > Um relatório de saída é diferente do relatório de avaliação. O primeiro é um relatório sobre o desempenho de um comando executado ao mesmo tempo, o segundo é um relatório XML para o consumo de programação.  
  
    Para as opções de comando para relatórios de saída (de Sl. Nenhum. 2 a 4 acima), consulte o [executando o Console SSMA &#40;DB2ToSQL&#41; ](../../ssma/db2/executing-the-ssma-console-db2tosql.md) seção.  
  
2.  Indica que a extensão de detalhes desejados no relatório de saída usando as configurações de relatório de detalhamento:  
  
    ||||  
    |-|-|-|  
    |**Sl. Não.**|**Comando e parâmetro**|**Descrição de saída**|  
    |1|verbose = "false"|Gera um relatório resumido da atividade.|  
    |2|verbose = "true"|Gera um relatório de status resumidos e detalhados para cada atividade.|  
  
    > [!NOTE]  
    > As configurações de detalhamento do relatório especificado acima são aplicáveis para relatório gerar de avaliação, converter esquema, migrar dados, comandos de instrução de sql convert.  
  
3.  Indica que a extensão de detalhes desejados em relatórios de erros usando as configurações de relatório de erros:  
  
    ||||  
    |-|-|-|  
    |**Sl. Não.**|**Comando e parâmetro**|**Descrição de saída**|  
    |1|relatório de erros = "false"|Nenhum detalhe de erro / aviso / mensagens de informações.|  
    |2|relatório de erros = "true"|Detalhes do erro / aviso / mensagens de informações.|  
  
    > [!NOTE]  
    > As definições de relatório de erro especificada acima são aplicáveis para relatório gerar de avaliação, converter esquema, migrar dados, comandos de instrução de sql convert.  
  
**Exemplo:**  
  
```  
<generate-assessment-report  
  
   object-name="<object-name>"  
  
   object-type="<object-type>"  
  
   verbose="<true/false>"  
  
   report-erors="<true/false>"  
  
   write-summary-report-to="<file-name/folder-name>"  
  
   assessment-report-folder="<folder-name>"  
  
   assessment-report-overwrite="<true/false>"/>  
```  
  
### <a name="synchronize-target"></a>Sincronizar-destino:  
O comando **destino sincronizar** tem **erros de relatório para** parâmetro, que especifica o local do relatório de erros para a operação de sincronização. Em seguida, um arquivo com nome **TargetSynchronizationReport&lt;n&gt;. XML** é criado no local especificado, onde **&lt;n&gt;** é o número de arquivo exclusivo que é incrementada com um dígito com cada execução do mesmo comando.  
  
**Observação:** se o caminho da pasta é fornecido, 'relatório-erros-to' parâmetro torna-se um atributo opcional para o comando 'Sincronizar-target'.  
  
```  
<!-- Example: Synchronize target entire Database with all attributes-->  
  
<synchronize-target  
  
   object-name="<object-name>"  
  
   on-error="report-total-as-warning/report-each-as-warning/fail-script"  
  
   report-errors-to="<file-name/folder-name>"/>  
```  
**nome do objeto:** Especifica os objetos considerados para sincronização (ele também pode ter nomes de objeto indivdual ou um nome de objeto de grupo).  
  
**em caso de erro:** Especifica se deve especificar os erros de sincronização como avisos ou erros. Opções disponíveis para em erro:  
  
-   report-total-as-warning  
  
-   report-each-as-warning  
  
-   Falha de script  
  
### <a name="refresh-from-database"></a>atualização-do-banco de dados:  
O comando **atualização de banco de dados** tem **erros de relatório para** parâmetro, que especifica o local do relatório de erros para a operação de atualização. Em seguida, um arquivo com nome **SourceDBRefreshReport&lt;n&gt;. XML** é criado no local especificado, onde **&lt;n&gt;** é o número de arquivo exclusivo que é incrementada com um dígito com cada execução do mesmo comando.  
  
**Observação:** se o caminho da pasta é fornecido, 'relatório-erros-to' parâmetro torna-se um atributo opcional para o comando 'Sincronizar-target'.  
  
```  
<!-- Example: Refresh entire Schema (with all attributes)-->  
  
<refresh-from-database  
  
   object-name="<object-name>"  
  
   object-type ="<object-type>"  
  
   on-error="report-total-as-warning/report-each-as-warning/fail-script"  
  
   report-errors-to="<file-name/folder-name>"/>  
```  
**nome do objeto:** Especifica os objetos considerados para atualização (ele também pode ter nomes de objeto indivdual ou um nome de objeto de grupo).  
  
**em caso de erro:** Especifica se deve especificar os erros de atualização como avisos ou erros. Opções disponíveis para em erro:  
  
-   report-total-as-warning  
  
-   report-each-as-warning  
  
-   Falha de script  
  
## <a name="see-also"></a>Consulte também  
[Executar o console do SSMA](http://msdn.microsoft.com/en-us/ce63f633-067d-4f04-b8e9-e1abd7ec740b)  
  
