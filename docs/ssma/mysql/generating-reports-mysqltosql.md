---
title: Geração de relatórios (MySQLToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Generating reports
ms.assetid: 1c0202e8-546d-4cb3-a37f-1d2e35d53839
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: a5b94ef545285cd7dfa4597820da00552b9f3930
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68103007"
---
# <a name="generating-reports-mysqltosql"></a>Geração de relatórios (MySQLToSQL)
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
    |6|refresh-from-database|SourceDBRefreshReport&lt;n&gt;.XML|  
  
    > [!IMPORTANT]  
    > Um relatório de saída é diferente do relatório de avaliação. O primeiro é um relatório sobre o desempenho de um comando executado ao mesmo tempo, o último é um relatório XML para consumo programático.  
  
    Para as opções de comando para relatórios de saída (de Sl. Não. 2 a 4 acima), consulte o [executar o Console do SSMA &#40;MySQLToSQL&#41; ](../../ssma/mysql/executing-the-ssma-console-mysqltosql.md) seção.  
  
2.  Indica que a extensão dos detalhes desejados no relatório de saída usando as configurações de detalhamento do relatório:  
  
    ||||  
    |-|-|-|  
    |**Sl. Não.**|**Comando e parâmetro**|**Descrição de saída**|  
    |1|verbose="false"|Gera um relatório resumido da atividade.|  
    |2|verbose="true"|Gera um relatório de status resumido e detalhado para cada atividade.|  
  
    > [!NOTE]  
    > As configurações de detalhamento do relatório especificado acima são aplicáveis para gerar--relatório de avaliação, convert esquema, migrar dados e comandos de instrução de sql convert.  
  
3.  Indica que a extensão dos detalhes escolhido nos relatórios de erros usando as configurações de relatório de erros:  
  
    ||||  
    |-|-|-|  
    |**Sl. Não.**|**Comando e parâmetro**|**Descrição de saída**|  
    |1|report-errors="false"|Não há detalhes sobre o erro / aviso / mensagens de informações.|  
    |2|report-errors="true"|Detalhes do erro / aviso / mensagens de informações.|  
  
    > [!NOTE]  
    > As definições de relatório de erro especificado acima são aplicáveis para gerar--relatório de avaliação, convert esquema, migrar dados e comandos de instrução de sql convert.  
  
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
  
### <a name="synchronize-target"></a>Sincronizar-target:  
O comando **destino sincronizar** tem **erros de relatório para** parâmetro, que especifica o local do relatório de erros para a operação de sincronização. Em seguida, um arquivo por nome **TargetSynchronizationReport&lt;n&gt;. XML** é criado no local especificado, onde **&lt;n&gt;** é o número de arquivo exclusivo que é incrementada com um dígito com cada execução do mesmo comando.  
  
**Observação:** Se o caminho da pasta for fornecido, 'relatório-erros-to' parâmetro torna-se um atributo opcional para o destino do comando' Sincronizar-'.  
  
```xml  
<!-- Example: Synchronize target entire Database with all attributes-->  
  
<synchronize-target  
  
   object-name="<object-name>"  
  
   on-error="<report-total-as-warning/report-each-as-warning/fail-script>"  
  
   report-errors-to="<file-name/folder-name>"  
  
/>  
```  
**object-name:** Especifica os objetos considerados para sincronização (ele também pode ter nomes de objetos individuais ou um nome de objeto de grupo).  
  
**em caso de erro:** Especifica se deve especificar os erros de sincronização como avisos ou erros. Opções disponíveis para em caso de erro:  
  
-   report-total-as-warning  
  
-   report-each-as-warning  
  
-   Falha-script  
  
### <a name="refresh-from-database"></a>atualização-do-banco de dados:  
O comando **atualização de banco de dados** tem **erros de relatório para** parâmetro, que especifica o local do relatório de erros para a operação de atualização. Em seguida, um arquivo por nome **SourceDBRefreshReport&lt;n&gt;. XML** é criado no local especificado, onde **&lt;n&gt;** é o número de arquivo exclusivo que é incrementada com um dígito com cada execução do mesmo comando.  
  
**Observação:** Se o caminho da pasta for fornecido, 'relatório-erros-to' parâmetro torna-se um atributo opcional para o destino do comando' Sincronizar-'.  
  
```xml  
<!-- Example: Refresh entire Schema (with all attributes)-->  
  
<refresh-from-database  
  
   object-name="<object-name>"  
  
   object-type ="<object-type>"  
  
   on-error="<report-total-as-warning/report-each-as-warning/fail-script>"  
  
   report-errors-to="<file-name/folder-name>"  
  
/>  
```  
**object-name:** Especifica os objetos considerados para a atualização (ele também pode ter nomes de objetos individuais ou um nome de objeto de grupo).  
  
**em caso de erro:** Especifica se deve especificar os erros de atualização como avisos ou erros. Opções disponíveis para em caso de erro:  
  
-   report-total-as-warning  
  
-   report-each-as-warning  
  
-   Falha-script  
  
## <a name="see-also"></a>Consulte também  
[Executar o Console do SSMA (MySQL)](https://msdn.microsoft.com/e3e9f7e4-0619-4861-a202-3d5d39953b26)  
  
