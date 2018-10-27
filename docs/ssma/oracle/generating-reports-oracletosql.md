---
title: Geração de relatórios (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Report Generation in Oracle Console, synchronize-target
- Report Generation in Oracle Console,refresh-from-database
- Report Generation in Oracle Console,write-summary-report-to
ms.assetid: ccad6262-01e1-447a-bd2b-c105154c80ce
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: 8d3a51f05159967505c22854817b0331ff607d7e
ms.sourcegitcommit: 9f2edcdf958e6afce9a09fb2e572ae36dfe9edb0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/25/2018
ms.locfileid: "50099507"
---
# <a name="generating-reports-oracletosql"></a>Geração de relatórios (OracleToSQL)
Os relatórios de determinadas atividades executadas usando os comandos são gerados no Console do SSMA no nível da árvore de objeto.  
  
Use o procedimento a seguir para gerar relatórios:  
  
1.  Especifique o **gravação-resumo-relatório-to** parâmetro. O relatório relacionado é armazenado como o nome do arquivo (se especificado) ou na pasta que você especificar. O nome do arquivo é predefinida pelo sistema conforme mencionado na tabela a seguir onde, **&lt;n&gt;** é o número de arquivo exclusivo que é incrementada com um dígito com cada execução do mesmo comando.  
  
    Os comandos de vis-à-vis relatórios são:  
  
    ||||  
    |-|-|-|  
    |**Sl. Não.**|**Comando**|**Título do relatório**|  
    |1|Gerar--relatório de avaliação|AssessmentReport&lt;n&gt;.XML|  
    |2|convert-schema|SchemaConversionReport&lt;n&gt;.XML|  
    |3|migrar dados|DataMigrationReport&lt;n&gt;.XML|  
    |4|convert-sql-statement|ConvertSQLReport&lt;n&gt;.XML|  
    |5|Sincronizar de destino|TargetSynchronizationReport&lt;n&gt;.XML|  
    |6|atualização de banco de dados|SourceDBRefreshReport&lt;n&gt;.XML|  
  
    > [!IMPORTANT]  
    > Um relatório de saída é diferente do relatório de avaliação. O primeiro é um relatório sobre o desempenho de um comando executado ao mesmo tempo, o último é um relatório XML para consumo programático.  
  
    Para as opções de comando para relatórios de saída (de Sl. Nenhum. 2 a 4 acima), consulte o [executar o Console do SSMA &#40;OracleToSQL&#41; ](../../ssma/oracle/executing-the-ssma-console-oracletosql.md) seção.  
  
2.  Indica que a extensão dos detalhes desejados no relatório de saída usando as configurações de detalhamento do relatório:  
  
    ||||  
    |-|-|-|  
    |**Sl. Não.**|**Comando e parâmetro**|**Descrição de saída**|  
    |1|verbose = "false"|Gera um relatório resumido da atividade.|  
    |2|verbose = "true"|Gera um relatório de status resumido e detalhado para cada atividade.|  
  
    > [!NOTE]  
    > As configurações de detalhamento do relatório especificado acima são aplicáveis para gerar--relatório de avaliação, convert esquema, migrar dados e comandos de instrução de sql convert.  
  
3.  Indica que a extensão dos detalhes escolhido nos relatórios de erros usando as configurações de relatório de erros:  
  
    ||||  
    |-|-|-|  
    |**Sl. Não.**|**Comando e parâmetro**|**Descrição de saída**|  
    |1|relatório de erros = "false"|Não há detalhes sobre o erro / aviso / mensagens de informações.|  
    |2|relatório de erros = "true"|Detalhes do erro / aviso / mensagens de informações.|  
  
    > [!NOTE]  
    > As definições de relatório de erro especificado acima são aplicáveis para gerar--relatório de avaliação, convert esquema, migrar dados e comandos de instrução de sql convert.  
  
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
  
### <a name="synchronize-target"></a>Sincronizar-target:  
O comando **destino sincronizar** tem **erros de relatório para** parâmetro, que especifica o local do relatório de erros para a operação de sincronização. Em seguida, um arquivo por nome **TargetSynchronizationReport&lt;n&gt;. XML** é criado no local especificado, onde **&lt;n&gt;** é o número de arquivo exclusivo que é incrementada com um dígito com cada execução do mesmo comando.  
  
**Observação:** se o caminho de pasta é fornecido, 'relatório-erros-to' parâmetro torna-se um atributo opcional para o destino do comando' Sincronizar-'.  
  
```  
<!-- Example: Synchronize target entire Database with all attributes-->  
  
<synchronize-target  
  
   object-name="<object-name>"  
  
   on-error="report-total-as-warning/report-each-as-warning/fail-script"  
  
   report-errors-to="<file-name/folder-name>"/>  
```  
**nome do objeto:** Especifica os objetos considerados para sincronização (ele também pode ter nomes de objetos individuais ou um nome de objeto de grupo).  
  
**em caso de erro:** Especifica se é necessário especificar os erros de sincronização como avisos ou erros. Opções disponíveis para em caso de erro:  
  
-   report-total-as-warning  
  
-   report-each-as-warning  
  
-   Falha-script  
  
### <a name="refresh-from-database"></a>atualização-do-banco de dados:  
O comando **atualização de banco de dados** tem **erros de relatório para** parâmetro, que especifica o local do relatório de erros para a operação de atualização. Em seguida, um arquivo por nome **SourceDBRefreshReport&lt;n&gt;. XML** é criado no local especificado, onde **&lt;n&gt;** é o número de arquivo exclusivo que é incrementada com um dígito com cada execução do mesmo comando.  
  
**Observação:** se o caminho de pasta é fornecido, 'relatório-erros-to' parâmetro torna-se um atributo opcional para o destino do comando' Sincronizar-'.  
  
```  
<!-- Example: Refresh entire Schema (with all attributes)-->  
  
<refresh-from-database  
  
   object-name="<object-name>"  
  
   object-type ="<object-type>"  
  
   on-error="report-total-as-warning/report-each-as-warning/fail-script"  
  
   report-errors-to="<file-name/folder-name>"/>  
```  
**nome do objeto:** Especifica os objetos considerados para a atualização (ele também pode ter nomes de objetos individuais ou um nome de objeto de grupo).  
  
**em caso de erro:** Especifica se é necessário especificar os erros de atualização como avisos ou erros. Opções disponíveis para em caso de erro:  
  
-   report-total-as-warning  
  
-   report-each-as-warning  
  
-   Falha-script  
  
## <a name="see-also"></a>Consulte também  
[Executar o Console do SSMA (Oracle)](http://msdn.microsoft.com/7228ccba-c69f-4b4c-8664-01a2750183c5)  
  
