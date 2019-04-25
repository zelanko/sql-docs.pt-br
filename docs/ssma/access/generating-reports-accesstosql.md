---
title: Geração de relatórios (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: abb4264a-622e-4215-af5b-14e309b8a399
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: fe6f45b2e35761fac5f8c49012b1eb370645bcb1
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62759497"
---
# <a name="generating-reports-accesstosql"></a>Geração de relatórios (AccessToSQL)
Os relatórios de determinadas atividades executadas usando os comandos são gerados no Console do SSMA no nível da árvore de objeto.  
  
Use o procedimento a seguir para gerar relatórios:  
  
1.  Especifique o **gravação-resumo-relatório-to** parâmetro. O relatório relacionado é armazenado como o nome do arquivo (se especificado) ou na pasta que você especificar. O nome do arquivo é predefinida pelo sistema conforme mencionado na tabela a seguir onde, **&lt;n&gt;** é o número de arquivo exclusivo que é incrementada com um dígito com cada execução do mesmo comando.  
  
    Os comandos de vis-à-vis relatórios são:  
  
    ||||  
    |-|-|-|  
    |**Sl. Não.**|**Comando**|**Título do relatório**|  
    |1|generate-assessment-report|AssessmentReport&lt;n&gt;.XML|  
    |2|convert-schema|SchemaConversionReport&lt;n&gt;.XML|  
    |3|migrate-data|DataMigrationReport&lt;n&gt;.XML|  
    |4|synchronize-target|TargetSynchronizationReport&lt;n&gt;.XML|  
    |5|refresh-from-database|SourceDBRefreshReport&lt;n&gt;.XML|  
  
    > [!IMPORTANT]  
    > Um relatório de saída é diferente do relatório de avaliação. O primeiro é um relatório sobre o desempenho de um comando executado ao mesmo tempo, o último é um relatório XML para consumo programático.  
  
    Para as opções de comando para relatórios de saída (de Sl. Não. 2 a 4 acima), consulte o [executar o Console do SSMA &#40;AccessToSQL&#41; ](../../ssma/access/executing-the-ssma-console-accesstosql.md) seção.  
  
2.  Indica que a extensão dos detalhes desejados no relatório de saída usando as configurações de detalhamento do relatório:  
  
    ||||  
    |-|-|-|  
    |**Sl. Não.**|**Comando e parâmetro**|**Descrição de saída**|  
    |1|verbose="false"|Gera um relatório resumido da atividade.|  
    |2|verbose="true"|Gera um relatório de status resumido e detalhado para cada atividade.|  
  
    > [!NOTE]  
    > As configurações de detalhamento do relatório especificado acima são aplicáveis para gerar--relatório de avaliação, esquema de convert, comandos de migração de dados.  
  
3.  Indica que a extensão dos detalhes escolhido nos relatórios de erros usando as configurações de relatório de erros:  
  
    ||||  
    |-|-|-|  
    |**Sl. Não.**|**Comando e parâmetro**|**Descrição de saída**|  
    |1|report-errors="false"|Não há detalhes sobre o erro / aviso / mensagens de informações.|  
    |2|report-errors="true"|Detalhes do erro / aviso / mensagens de informações.|  
  
    > [!NOTE]  
    > As definições de relatório de erro especificado acima são aplicáveis para gerar--relatório de avaliação, esquema de convert, comandos de migração de dados.  
  
**Exemplo:**  
  
```xml  
<generate-assessment-report  
  
    object-name="testschema"  
  
    object-type="Schemas"  
  
    verbose="yes"  
  
    report-erors="yes"  
  
    write-summary-report-to="$AssessmentFolder$\Report1.xml"  
  
    assessment-report-folder="$AssessmentFolder$\assesment_report"  
  
    assessment-report-overwrite="true"  
  
/>  
```  
  
### <a name="synchronize-target"></a>synchronize-target:  
O comando **destino sincronizar** tem **erros de relatório para** parâmetro, que especifica o local do relatório de erros para a operação de sincronização. Em seguida, um arquivo por nome **TargetSynchronizationReport&lt;n&gt;. XML** é criado no local especificado, onde **&lt;n&gt;** é o número de arquivo exclusivo que é incrementada com um dígito com cada execução do mesmo comando.  
  
**Observação:** Se o caminho da pasta for fornecido, 'relatório-erros-to' parâmetro torna-se um atributo opcional para o destino do comando' Sincronizar-'.  
  
```xml  
<!-- Example: Synchronize target entire Database with all attributes-->  
  
<synchronize-target  
  
    object-name="$TargetDB$.dbo"  
  
    on-error="fail-script"  
  
    report-errors-to="$SynchronizationReports$"  
  
/>  
```  
**object-name:** Especifica os objetos considerados para sincronização (ele também pode ter nomes de objetos individuais ou um nome de objeto de grupo).  
  
**on-error:** Especifica se deve especificar os erros de sincronização como avisos ou erros. Opções disponíveis para em caso de erro:  
  
-   report-total-as-warning  
  
-   report-each-as-warning  
  
-   Falha-script  
  
### <a name="refresh-from-database"></a>refresh-from-database:  
O comando **atualização de banco de dados** tem **erros de relatório para** parâmetro, que especifica o local do relatório de erros para a operação de atualização. Em seguida, um arquivo por nome **SourceDBRefreshReport&lt;n&gt;. XML** é criado no local especificado, onde **&lt;n&gt;** é o número de arquivo exclusivo que é incrementada com um dígito com cada execução do mesmo comando.  
  
**Observação:** Se o caminho da pasta for fornecido, 'relatório-erros-to' parâmetro torna-se um atributo opcional para o destino do comando' Sincronizar-'.  
  
```xml  
<!-- Example: Refresh entire Schema (with all attributes)-->  
  
<refresh-from-database  
  
    object-name="$SourceDatabaseStandard$"  
  
    object-type ="Databases"  
  
    on-error="fail-script"  
  
    report-errors-to="$RefreshDBFolder$\RefreshReport.xml"  
  
/>  
```  
**object-name:** Especifica os objetos considerados para a atualização (ele também pode ter nomes de objetos individuais ou um nome de objeto de grupo).  
  
**on-error:** Especifica se deve especificar os erros de atualização como avisos ou erros. Opções disponíveis para em caso de erro:  
  
-   report-total-as-warning  
  
-   report-each-as-warning  
  
-   Falha-script  
  
## <a name="see-also"></a>Consulte também  
[Executar o Console do SSMA (acesso)](https://msdn.microsoft.com/aa1bf665-8dc0-4259-b36f-46ae67197a43)  
  
