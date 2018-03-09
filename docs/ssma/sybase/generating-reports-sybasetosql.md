---
title: "Geração de relatórios (SybaseToSQL) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssma-sybase
ms.reviewer: 
ms.suite: sql
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Sybase Console,generating reports
- Sybase Console,refresh-from-database report
- Sybase Console,synchronize-target report
ms.assetid: 19278f6a-6d58-4867-9d71-c6228040466e
caps.latest.revision: "6"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 8fb70116001dddf0995de2aebb836d04d8f56441
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="generating-reports-sybasetosql"></a>Geração de relatórios (SybaseToSQL)
Os relatórios de certas atividades executadas usando os comandos são gerados no Console SSMA no nível de árvore de objeto.  
  
Use o procedimento a seguir para gerar relatórios:  
  
1.  Especifique o **gravação-resumo-relatório-para** parâmetro. O relatório relacionado é armazenado como o nome do arquivo (se especificado) ou na pasta que você especificar. O nome do arquivo é predefinida pelo sistema conforme mencionado na tabela a seguir onde,  **&lt; n &gt;**  é o número de arquivo exclusivo que é incrementada com um dígito com cada execução do mesmo comando.  
  
    Os comandos de vis-relação de relatórios são:  
  
    ||||  
    |-|-|-|  
    |**SL. Não.**|**Comando**|**Título do relatório**|  
    |1|relatório gerar de avaliação|AssessmentReport&lt;n&gt;. XML|  
    |2|Converter esquema|SchemaConversionReport&lt;n&gt;. XML|  
    |3|migrar dados|DataMigrationReport&lt;n&gt;. XML|  
    |4|instrução de sql Convert|ConvertSQLReport&lt;n&gt;. XML|  
    |5|Sincronizar de destino|TargetSynchronizationReport&lt;n&gt;. XML|  
    |6|atualização do banco de dados|SourceDBRefreshReport&lt;n&gt;. XML|  
  
    > [!IMPORTANT]  
    > Um relatório de saída é diferente do relatório de avaliação. O primeiro é um relatório sobre o desempenho de um comando executado ao mesmo tempo, o segundo é um relatório XML para o consumo de programação.  
  
    Para as opções de comando para relatórios de saída (de Sl. Nenhum. 2 a 4 acima), consulte o [executando o Console SSMA &#40; SybaseToSQL &#41; ](../../ssma/sybase/executing-the-ssma-console-sybasetosql.md) seção.  
  
2.  Indica que a extensão de detalhes desejados no relatório de saída usando as configurações de relatório de detalhamento:  
  
    ||||  
    |-|-|-|  
    |**SL. Não.**|**Comando e parâmetro**|**Descrição de saída**|  
    |1|verbose = "false"|Gera um relatório resumido da atividade.|  
    |2|verbose = "true"|Gera um relatório de status resumidos e detalhados para cada atividade.|  
  
    > [!NOTE]  
    > As configurações de detalhamento do relatório especificado acima são aplicáveis para relatório gerar de avaliação, converter esquema, migrar dados, comandos de instrução de sql convert.  
  
3.  Indica que a extensão de detalhes desejados em relatórios de erros usando as configurações de relatório de erros:  
  
    ||||  
    |-|-|-|  
    |**SL. Não.**|**Comando e parâmetro**|**Descrição de saída**|  
    |1|relatório de erros = "false"|Nenhum detalhe de erro / aviso / mensagens de informações.|  
    |2|relatório de erros = "true"|Detalhes do erro / aviso / mensagens de informações.|  
  
    > [!NOTE]  
    > As definições de relatório de erro especificada acima são aplicáveis para relatório gerar de avaliação, converter esquema, migrar dados, comandos de instrução de sql convert.  
  
```xml  
<generate-assessment-report  
  
    object-name="<object-name>"  
  
    object-type="<object-type>"  
  
    verbose="<true/false>"  
  
    report-erors="<true/false>"  
  
    write-summary-report-to="<file-name/folder-name>"  
  
    assessment-report-folder="<folder-name>"  
  
    assessment-report-overwrite="<true/false>"  
  
/>  
```  
  
### <a name="synchronize-target"></a>Sincronizar-destino:  
O comando **destino sincronizar** tem **erros de relatório para** parâmetro, que especifica o local do relatório de erros para a operação de sincronização. Em seguida, um arquivo com nome **TargetSynchronizationReport&lt;n&gt;. XML** é criado no local especificado, onde  **&lt; n &gt;**  é o número de arquivo exclusivo que é incrementada com um dígito com cada execução do mesmo comando.  
  
**Observação:** se o caminho da pasta é fornecido, 'relatório-erros-to' parâmetro torna-se um atributo opcional para o comando 'Sincronizar-target'.  
  
```xml  
<!-- Example: Synchronize target entire Database with all attributes-->  
  
<synchronize-target  
  
    object-name="<object-name>"  
  
    on-error="<object-type>"  
  
    report-errors-to="<file-name/folder-name>"  
  
/>  
```  
**nome do objeto:** Especifica os objetos considerados para sincronização (ele também pode ter nomes de objeto indivdual ou um nome de objeto de grupo).  
  
**em caso de erro:** Especifica se deve especificar os erros de sincronização como avisos ou erros. Opções disponíveis para em erro:  
  
-   total de relatórios como aviso  
  
-   relatório de cada-como-aviso  
  
-   Falha de script  
  
### <a name="refresh-from-database"></a>atualização-do-banco de dados:  
O comando **atualização de banco de dados** tem **erros de relatório para** parâmetro, que especifica o local do relatório de erros para a operação de atualização. Em seguida, um arquivo com nome **SourceDBRefreshReport&lt;n&gt;. XML** é criado no local especificado, onde  **&lt; n &gt;**  é o número de arquivo exclusivo que é incrementada com um dígito com cada execução do mesmo comando.  
  
**Observação:** se o caminho da pasta é fornecido, 'relatório-erros-to' parâmetro torna-se um atributo opcional para o comando 'Sincronizar-target'.  
  
```xml  
<!-- Example: Refresh entire Schema (with all attributes)-->  
  
<refresh-from-database  
  
    object-name="<object-name>"  
  
    object-type ="<object-type>"  
  
    on-error="report-total-as-warning/report-each-as-warning/fail-script"  
  
    report-errors-to="<file-name/folder-name> "  
  
/>  
```  
**nome do objeto:** Especifica os objetos considerados para atualização (ele também pode ter nomes de objeto indivdual ou um nome de objeto de grupo).  
  
**em caso de erro:** Especifica se deve especificar os erros de atualização como avisos ou erros. Opções disponíveis para em erro:  
  
-   total de relatórios como aviso  
  
-   relatório de cada-como-aviso  
  
-   Falha de script  
  
## <a name="see-also"></a>Consulte Também  
[Executar o Console do SSMA (Sybase)](http://msdn.microsoft.com/en-us/ea8950b7-fabc-4aa4-89f8-9573a2617d70)  
  
