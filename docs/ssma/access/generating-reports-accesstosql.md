---
title: Gerando relatórios (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: abb4264a-622e-4215-af5b-14e309b8a399
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: d9d1879cd5583ee7b87c12edb19bf5486cee4fcf
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67986427"
---
# <a name="generating-reports-accesstosql"></a>Gerando relatórios (AccessToSQL)
Os relatórios de determinadas atividades executadas usando comandos são gerados no console do SSMA no nível da árvore de objetos.  
  
Use o procedimento a seguir para gerar relatórios:  
  
1.  Especifique o parâmetro **Write-summary-report-to** . O relatório relacionado é armazenado como o nome do arquivo (se especificado) ou na pasta que você especificar. O nome do arquivo é predefinido pelo sistema conforme mencionado na tabela abaixo, ** &lt;em&gt; que n** é o número de arquivo exclusivo que é incrementado com um dígito com cada execução do mesmo comando.  
  
    Os comandos vis-to-vis de relatórios são:  
  
    ||||  
    |-|-|-|  
    |**SL. no.**|**Comando**|**Título do relatório**|  
    |1|gerar-avaliação-relatório|AssessmentReport&lt;n&gt;. XML|  
    |2|converter esquema|SchemaConversionReport&lt;n&gt;. XML|  
    |3|migrar-dados|DataMigrationReport&lt;n&gt;. XML|  
    |4|sincronizar destino|TargetSynchronizationReport&lt;n&gt;. XML|  
    |5|atualizar-do-banco de dados|SourceDBRefreshReport&lt;n&gt;. XML|  
  
    > [!IMPORTANT]  
    > Um relatório de saída é diferente do relatório de avaliação. O primeiro é um relatório sobre o desempenho de um comando executado, e o último é um relatório XML para consumo programático.  
  
    Para obter as opções de comando para relatórios de saída (de SL. Não. 2-4 acima), consulte a seção [executando o console do SSMA &#40;AccessToSQL&#41;](../../ssma/access/executing-the-ssma-console-accesstosql.md) .  
  
2.  Indique a extensão dos detalhes que você deseja no relatório de saída usando as configurações de detalhamento do relatório:  
  
    ||||  
    |-|-|-|  
    |**SL. no.**|**Comando e parâmetro**|**Descrição da saída**|  
    |1|verbose = "false"|Gera um relatório resumido da atividade.|  
    |2|verbose = "verdadeiro"|Gera um relatório de status resumido e detalhado para cada atividade.|  
  
    > [!NOTE]  
    > As configurações de detalhamento de relatório especificadas acima são aplicáveis aos comandos Generate-Assessment-Report, Convert-Schema, Migrate-Data.  
  
3.  Indique a extensão dos detalhes que você deseja nos relatórios de erro usando as configurações de relatório de erros:  
  
    ||||  
    |-|-|-|  
    |**SL. no.**|**Comando e parâmetro**|**Descrição da saída**|  
    |1|relatório-erros = "falso"|Não há detalhes sobre mensagens de erro/aviso/informação.|  
    |2|relatório-erros = "verdadeiro"|Mensagens de erro/aviso/informações detalhadas.|  
  
    > [!NOTE]  
    > As configurações de relatório de erros especificadas acima são aplicáveis aos comandos Generate-Assessment-Report, Convert-Schema, Migrate-Data.  
  
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
  
### <a name="synchronize-target"></a>sincronizar-destino:  
O comando **Synchronize-Target** tem o parâmetro **Report-Errors-to** , que especifica o local do relatório de erros para a operação de sincronização. Em seguida, um arquivo por **nome&lt;TargetSynchronizationReport&gt;n. O XML** é criado no local especificado, em ** &lt;que&gt; n** é o número de arquivo exclusivo que é incrementado com um dígito com cada execução do mesmo comando.  
  
**Observação:** Se o caminho da pasta for fornecido, o parâmetro ' Report-Errors-to ' se tornará um atributo opcional para o comando ' Synchronize-target '.  
  
```xml  
<!-- Example: Synchronize target entire Database with all attributes-->  
  
<synchronize-target  
  
    object-name="$TargetDB$.dbo"  
  
    on-error="fail-script"  
  
    report-errors-to="$SynchronizationReports$"  
  
/>  
```  
**nome do objeto:** Especifica os objetos considerados para sincronização (ele também pode ter nomes de objeto individuais ou um nome de objeto de grupo).  
  
**em caso de erro:** Especifica se os erros de sincronização devem ser especificados como avisos ou erro. Opções disponíveis para o no-erro:  
  
-   relatório-total-como-aviso  
  
-   relatório-cada-como-aviso  
  
-   script de falha  
  
### <a name="refresh-from-database"></a>atualizar-do-banco de dados:  
O comando **Atualizar-de-banco de dados** tem o parâmetro **Report-Errors-to** , que especifica o local do relatório de erros para a operação de atualização. Em seguida, um arquivo por **nome&lt;SourceDBRefreshReport&gt;n. O XML** é criado no local especificado, em ** &lt;que&gt; n** é o número de arquivo exclusivo que é incrementado com um dígito com cada execução do mesmo comando.  
  
**Observação:** Se o caminho da pasta for fornecido, o parâmetro ' Report-Errors-to ' se tornará um atributo opcional para o comando ' Synchronize-target '.  
  
```xml  
<!-- Example: Refresh entire Schema (with all attributes)-->  
  
<refresh-from-database  
  
    object-name="$SourceDatabaseStandard$"  
  
    object-type ="Databases"  
  
    on-error="fail-script"  
  
    report-errors-to="$RefreshDBFolder$\RefreshReport.xml"  
  
/>  
```  
**nome do objeto:** Especifica os objetos considerados para atualização (ele também pode ter nomes de objeto individuais ou um nome de objeto de grupo).  
  
**em caso de erro:** Especifica se é para especificar erros de atualização como avisos ou erro. Opções disponíveis para o no-erro:  
  
-   relatório-total-como-aviso  
  
-   relatório-cada-como-aviso  
  
-   script de falha  
  
## <a name="see-also"></a>Consulte Também  
[Executando o console do SSMA (Access)](https://msdn.microsoft.com/aa1bf665-8dc0-4259-b36f-46ae67197a43)  
  
