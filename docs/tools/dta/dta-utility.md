---
title: "Utilitário DTA | Microsoft Docs"
ms.custom: 
ms.date: 01/09/2017
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: dta
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- physical design structures [SQL Server]
- command prompt utilities [SQL Server], dta
- dta utility
- tuning databases [SQL Server], Database Engine Tuning Advisor
- workloads [SQL Server], analyzing
- dta utility, about dta utility
- performance [SQL Server], Database Engine Tuning Advisor
- Database Engine Tuning Advisor [SQL Server], command prompt
- optimizing databases [SQL Server]
ms.assetid: a0b210ce-9b58-4709-80cb-9363b68a1f5a
caps.latest.revision: "58"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 192a28c8833fb801e19d1dee7485b667ea56128d
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2017
---
# <a name="dta-utility"></a>utilitário dta
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]O **dta** utilitário é a versão do prompt de comando do Orientador de otimização do mecanismo de banco de dados. O utilitário **dta** foi projetado para permitir o uso da funcionalidade do Orientador de Otimização do Mecanismo de Banco de Dados em aplicativos e scripts.  
  
 Assim como o Orientador de Otimização do Mecanismo de Banco de Dados, o utilitário **dta** analisa uma carga de trabalho e recomenda estruturas de design físico para melhorar o desempenho do servidor para a carga de trabalho. A carga de trabalho pode ser um cache de plano, um arquivo de rastreamento ou tabela do [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] , ou um script [!INCLUDE[tsql](../../includes/tsql-md.md)] . Estruturas de design físico incluem índices, exibições indexadas e particionamento. Depois de analisar uma carga de trabalho, o utilitário **dta** produz uma recomendação para o design físico de bancos de dados e gera o script necessário para implementar a recomendação. Podem ser especificadas cargas de trabalho no prompt de comando com o argumento **-if** ou **-it** . Também é possível especificar um arquivo de entrada XML no prompt de comando com o argumento **-ix** . Nesse caso, a carga de trabalho é especificada no arquivo de entrada XML.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
dta  
[ -? ] |  
[  
      [ -S server_name[ \instance ] ]  
      { { -U login_id [-P password ] } | –E  }  
      { -D database_name [ ,...n ] }  
      [ -d database_name ]   
      [ -Tl table_list | -Tf table_list_file ]  
      { -if workload_file | -it workload_trace_table_name  |   
        -ip | -iq }  
      { -ssession_name | -IDsession_ID }  
      [ -F ]  
      [ -of output_script_file_name ]  
      [ -or output_xml_report_file_name ]  
      [ -ox output_XML_file_name ]  
      [ -rl analysis_report_list [ ,...n ] ]  
      [ -ix input_XML_file_name ]  
      [ -A time_for_tuning_in_minutes ]  
      [ -n number_of_events ]
      [ -I time_window_in_hours ]  
      [ -m minimum_improvement ]  
      [ -fa physical_design_structures_to_add ]  
      [ -fi filtered_indexes]  
      [ -fc columnstore_indexes]  
      [ -fp partitioning_strategy ]  
      [ -fk keep_existing_option ]  
      [ -fx drop_only_mode ]  
      [ -B storage_size ]  
      [ -c max_key_columns_in_index ]  
      [ -C max_columns_in_index ]  
      [ -e | -e tuning_log_name ]  
      [ -N online_option]  
      [ -q ]  
      [ -u ]  
      [ -x ]  
      [ -a ]  
]  
```  
  
## <a name="arguments"></a>Argumentos  
 **-?**  
 Exibe informações de uso.  
  
 **-A** *time_for_tuning_in_minutes*  
 Especifica o prazo de ajuste em minutos. O**dta** usa a quantidade especificada de tempo para ajustar a carga de trabalho e gerar um script com as mudanças de design físico recomendadas. Por padrão, o **dta** assume um tempo de ajuste de 8 horas. Especificar 0 permite um tempo de ajuste ilimitado. O**dta** pode terminar o ajuste da carga de trabalho inteira antes que o prazo expire. No entanto, para garantir que a carga de trabalho inteira seja ajustada, é aconselhável que você especifique um tempo de ajuste ilimitado (-A 0).  
  
 **-a**  
 Ajusta a carga de trabalho e aplica a recomendação sem uma solicitação.  
  
 **-B** *storage_size*  
 Especifica o espaço máximo em megabytes que pode ser consumido pelo índice e particionamento recomendados. Quando múltiplos bancos de dados são ajustados, as recomendações para todos os bancos de dados são consideradas no cálculo do espaço. Por padrão, **dta** assume o menor dos seguintes tamanhos de armazenamento:  
  
-   Três vezes o tamanho de dados brutos atuais, o que inclui o tamanho total de heaps e índices cluster em tabelas no banco de dados.  
  
-   Os espaços livres em todas as unidades de disco anexas mais o tamanho dos dados brutos.  
  
 O tamanho de armazenamento padrão não inclui índices não clusterizados e exibições indexadas.  
  
 **-C** *max_columns_in_index*  
 Especifica o número máximo de colunas nos índices proposto por **dta** . O valor máximo é 1024. Por padrão, esse argumento é definido como 16.  
  
 **-c** *max_key_columns_in_index*  
 Especifica o número máximo de colunas principais nos índices proposto por **dta** . O valor padrão é 16, o valor máximo permitido. O**dta** também considera a criação de índices com colunas incluídas. Os índices recomendados com colunas incluídas podem exceder o número de colunas especificado neste argumento.  
  
 **-D** *database_name*  
 Especifica o nome de cada banco de dados que será ajustado. O primeiro banco de dados é o banco de dados padrão. É possível especificar bancos de dados múltiplos separando os nomes do banco de dados com vírgulas, por exemplo:  
  
```  
dta –D database_name1, database_name2...  
```  
  
 Como alternativa, você pode especificar bancos de dados múltiplos usando o argumento **–D** para cada nome de banco de dados, por exemplo:  
  
```  
dta –D database_name1 -D database_name2... n  
```  
  
 O argumento **-D** é obrigatório. Se o argumento **-d** não foi especificado, **dta** se conectará inicialmente ao banco de dados que é especificado com a primeira cláusula `USE database_name` na carga de trabalho. Se não houver a cláusula explícita `USE database_name` na carga de trabalho, será necessário usar o argumento **-d** .  
  
 Por exemplo, caso tenha uma carga de trabalho que não contém nenhuma cláusula `USE database_name` explícita e você usar o seguinte comando **dta** , uma recomendação não será gerada:  
  
```  
dta -D db_name1, db_name2...  
```  
  
 Mas, se você usar a mesma carga de trabalho e usar o seguinte comando **dta** que usa o argumento **-d** , uma recomendação será gerada:  
  
```  
dta -D db_name1, db_name2 -d db_name1  
```  
  
 **-d** *database_name*  
 Especifica o primeiro banco de dados ao qual **dta** se conecta ao ajustar uma carga de trabalho. Apenas um banco de dados pode ser especificado para esse argumento. Por exemplo:  
  
```  
dta -d AdventureWorks2012 ...  
```  
  
 Se forem especificados vários nomes de banco de dados, **dta** retornará um erro. O argumento **-d** é opcional.  
  
 Se você estiver usando uma entrada de arquivo XML, poderá especificar o primeiro banco de dados ao qual **dta** se conecta, usando o elemento **DatabaseToConnect** que está localizado no elemento **TuningOptions** . Para saber mais, confira [Database Engine Tuning Advisor](../../relational-databases/performance/database-engine-tuning-advisor.md).  
  
 Se você estiver ajustando apenas um banco de dados, o argumento **-d** fornecerá uma funcionalidade que é semelhante ao argumento **-d** no utilitário **sqlcmd** , mas não executará a instrução USE *database_name* . Para saber mais, confira [sqlcmd Utility](../../tools/sqlcmd-utility.md).  
  
 **-E**  
 Usa uma conexão confiável em vez de pedir uma senha. O argumento **-E** ou **-U** , que especifica uma ID de logon, deve ser usado.  
  
 **-e** *tuning_log_name*  
 Especifica o nome da tabela ou do arquivo em que **dta** registra eventos que não puderam ser ajustados. A tabela é criada no servidor onde o ajuste é executado.  
  
 Se uma tabela for usada, especifique seu nome no formato: *[database_name].[owner_name].table_name*. A seguinte tabela mostra os valores padrão para cada parâmetro:  
  
|Parâmetro|Valor padrão|Detalhes|  
|---------------|-------------------|-------------|  
|*database_name*|*database_name* especificado com a opção **–D**||  
|*owner_name*|**dbo**|*owner_name* deve ser **dbo**. Se qualquer outro valor for especificado, a execução de **dta** falhará e retornará um erro.|  
|*table_name*|Nenhuma||  
  
 Se um arquivo for usado, especifique .xml como sua extensão. Por exemplo, TuningLog.xml.  
  
> [!NOTE]  
>  O utilitário **dta** não excluirá o conteúdo das tabelas de log de ajuste especificadas pelo usuário se a sessão for excluída. Ao ajustar cargas de trabalho muito grandes, é recomendável que uma tabela seja especificada para o log de ajuste. Como o ajuste de cargas de trabalho grandes pode resultar em logs de ajuste grandes, as sessões podem ser excluídas muito mais rapidamente ao usar uma tabela.  
  
 **-F**  
 Permite que **dta** substitua um arquivo de saída existente. Se um arquivo de saída com o mesmo nome já existir e **-F** não for especificado, **dta**retornará um erro. Você pode usar **-F** com **-of**, **-or**ou **-ox**.  
  
 **-fa** *physical_design_structures_to_add*  
 Especifica que tipos de estruturas de design físico **dta** deve incluir na recomendação. A tabela a seguir lista e descreve os valores que podem ser especificados para esse argumento. Quando nenhum valor é especificado, **dta** usa o padrão **-fa****IDX**.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|IDX_IV|Índices e exibições indexadas.|  
|IDX|Somente índices.|  
|IV|Somente exibições indexadas.|  
|NCL_IDX|Somente índices não clusterizados|  
  
 **-fi**  
 Especifica que os índices filtrados serão considerados em novas recomendações. Para saber mais, confira [Create Filtered Indexes](../../relational-databases/indexes/create-filtered-indexes.md).  
  
**-fc**  
 Especifica que os índices columnstore serão considerados em novas recomendações. DTA considerará índices columnstore clusterizados e não clusterizados. Para obter mais informações, consulte    
[Recomendações de índice ColumnStore no banco de dados ajuste de DTA (orientador mecanismo)](../../relational-databases/performance/columnstore-index-recommendations-in-database-engine-tuning-advisor-dta.md).
 ||  
|-|  
|**Aplica-se a**: do [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|  

  
 **-fk** *keep_existing_option*  
 Especifica quais estruturas de design físico **dta** deve reter ao gerar sua recomendação. A tabela a seguir lista e descreve os valores que podem ser especificados para esse argumento.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|Nenhuma|Nenhuma estrutura existente|  
|ALL|Todas as estruturas existentes|  
|ALIGNED|Todas as estruturas alinhadas por partição.|  
|CL_IDX|Todos os índices clusterizados em tabelas|  
|IDX|Todos os índices clusterizados e não clusterizados em tabelas|  
  
 **-fp** *partitioning_strategy*  
 Especifica se as novas estruturas de design físico (índices e exibições indexadas) propostas por **dta** devem ser particionadas e como particioná-las. A tabela a seguir lista e descreve os valores que podem ser especificados para esse argumento.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|Nenhuma|Nenhum particionamento|  
|FULL|Particionamento completo (escolha para melhorar o desempenho).|  
|ALIGNED|Somente particionamento alinhado (escolha para melhorar a capacidade de gerenciamento)|  
  
 ALIGNED significa que, na recomendação gerada por **dta** , todo índice proposto é particionado exatamente do mesmo modo que a tabela subjacente para a qual o índice foi definido. Índices não clusterizados em uma exibição indexada são alinhados com a exibição indexada. Só um valor pode ser especificado para esse argumento. O padrão é **-fp****NONE**.  
  
 **-fx** *drop_only_mode*  
 Especifica que **dta** só considera a remoção das estruturas de design físico existentes. Nenhuma estrutura de design físico nova é considerada. Quando esta opção é especificada, o **dta** avalia a utilidade de estruturas de design físico existentes e recomenda descartar as estruturas raramente usadas. Este argumento não leva nenhum valor. Não pode ser usado com os argumentos **-fa**, **-fp**ou **-fk ALL**  
  
 **-ID** *session_ID*  
 Especifica um identificador numérico para a sessão de ajuste. Se não estiver especificado, **dta** gerará um número de identificação. Você pode usar esse identificador para exibir informações para sessões de ajuste existentes. Se você não especificar um valor para **-ID**, um nome de sessão deverá ser especificado com **-s**.  
  
 **-ip**  
 Especifica que o cache de plano seja usado como a carga de trabalho. Os primeiros 1.000 eventos de cache de plano para bancos de dados selecionados explicitamente são analisados. Esse valor pode ser alterado usando a opção **–n** .  
 
**-QI**  
 Especifica que o repositório de consultas seja usado como a carga de trabalho. Os primeiros 1.000 eventos do repositório de consultas para bancos de dados selecionados explicitamente são analisados. Esse valor pode ser alterado usando a opção **–n** .  Consulte [repositório de consultas](../../relational-databases/performance/how-query-store-collects-data.md) e [ajuste de banco de dados usando cargas de trabalho do repositório de consultas](../../relational-databases/performance/tuning-database-using-workload-from-query-store.md) para obter mais informações.
 ||  
|-|  
|**Aplica-se a**: do [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|  
     
  
 **-if** *workload_file*  
 Especifica o caminho e o nome do arquivo de carga de trabalho a ser usado como entrada para ajuste. O arquivo deve estar em um destes formatos: .trc (arquivo de rastreamento do SQL Server Profiler), .sql (arquivo de SQL) ou .log (arquivo de rastreamento do[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ). Um arquivo de carga de trabalho ou uma tabela de carga de trabalho deve ser especificada.  
  
 **-it** *workload_trace_table_name*  
 Especifica o nome de uma tabela que contém o rastreamento de carga de trabalho para ajuste. O nome é especificado no formato: [*database_name*]**.**[*owner_name*]**.***table_name*.  
  
 A tabela a seguir mostra os valores padrão de cada um:  
  
|Parâmetro|Valor padrão|  
|---------------|-------------------|  
|*database_name*|*database_name* especificado com a opção **–D** .|  
|*owner_name*|**dbo**.|  
|*table_name*|Nenhum.|  
  
> [!NOTE]  
>  *owner_name* deve ser **dbo**. Se qualquer outro valor for especificado, a execução de **dta** falhará e um erro será retornado. Também observe que uma tabela de carga de trabalho ou um arquivo de carga de trabalho deve ser especificado.  
  
 **-ix** *input_XML_file_name*  
 Especifica o nome do arquivo XML que contém informações de entrada de **dta** . Esse deve ser um documento XML válido em conformidade com o DTASchema.xsd. Argumentos em conflito especificados no prompt de comando para opções de ajuste anulam o valor correspondente no arquivo XML. A única exceção será se uma configuração especificada pelo usuário for digitada dentro do modo de avaliação no arquivo de entrada XML. Por exemplo, se uma configuração for digitada no elemento **Configuration** do arquivo de entrada XML e o elemento **EvaluateConfiguration** também for especificado como um das opções de ajuste, as opções de ajuste especificadas no arquivo de entrada XML substituirão a opção de ajuste digitada no prompt de comando.  
  
 **-m** *minimum_improvement*  
 Especifica a porcentagem mínima de melhoria que a configuração recomendada deve satisfazer.  
  
 **-N** *online_option*  
 Especifica se são criadas estruturas de design físico online. A tabela a seguir lista e descreve os valores que podem ser especificados para esse argumento.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|OFF|Nenhuma estrutura de design físico recomendada pode ser criada online.|  
|ON|Todas as estruturas de design físico recomendadas podem ser criadas online.|  
|MIXED|O Orientador de Otimização do Mecanismo de Banco de Dados tenta recomendar estruturas de design físico que podem ser criadas online quando possível.|  
  
 Se forem criados índices online, ONLINE = ON será anexado à definição de objeto.  
  
 **-n** *number_of_events*  
 Especifica o número de eventos na carga de trabalho que **dta** deve ajustar. Se esse argumento for especificado e a carga de trabalho for um arquivo de rastreamento que contém informações de duração, **dta** ajustará os eventos em ordem decrescente de duração. Esse argumento é útil para comparar duas configurações de estruturas de design físico. Para comparar duas configurações, especifique o mesmo número de eventos a serem ajustados para ambas as configurações e também especifique um tempo de ajuste ilimitado para ambos como segue:  
  
```  
dta -n number_of_events -A 0  
```  
  
 Nessecaso, é importante especificar um tempo de ajuste ilimitado (`-A 0`). Caso contrário, o Orientador de Otimização do Mecanismo de Banco de Dados assume, por padrão, um tempo de ajuste de 8 horas.
 
 **-I** *time_window_in_hours*   
   Especifica a janela de tempo (em horas) quando uma consulta deve ter executado para que ela seja considerada pelo DTA para ajustar ao usar **-QI** opção (carga de trabalho do repositório de consultas). 
```  
dta -iq -I 48  
```  
Nesse caso, DTA será usar o repositório de consultas como a fonte de carga de trabalho e considerar apenas consultas que foram executadas nas últimas 48 horas.  
  ||  
|-|  
|**Aplica-se a**: do [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|  


  
 **-of** *output_script_file_name*  
 Especifica que **dta** grava a recomendação como um script [!INCLUDE[tsql](../../includes/tsql-md.md)] no nome de arquivo e destino especificados.  
  
 Você pode usar **-F** com essa opção. Verifique se o nome de arquivo é exclusivo, especialmente se você também estiver usando **-or** e **-ox**.  
  
 **-or** *output_xml_report_file_name*  
 Especifica que **dta** grava a recomendação em um relatório de saída em XML. Se um nome de arquivo for fornecido, as recomendações serão gravadas nesse destino. Caso contrário, o **dta** usa o nome de sessão para gerar o nome de arquivo e grava-o no diretório atual.  
  
 Você pode usar **-F** com essa opção. Verifique se o nome de arquivo é exclusivo, especialmente se você também estiver usando **-of** e **-ox**.  
  
 **-ox** *output_XML_file_name*  
 Especifica que **dta** grava a recomendação como um arquivo XML no nome de arquivo e destino fornecidos. Verifique se o Orientador de Otimização do Mecanismo de Banco de Dados tem permissões para gravar no diretório de destino.  
  
 Você pode usar **-F** com essa opção. Verifique se o nome de arquivo é exclusivo, especialmente se você também estiver usando **-of** e **-or**.  
  
 **-P** *password*  
 Especifica a senha para a ID de logon. Se essa opção não for usada, o **dta** solicitará a senha.  
  
 **-q**  
 Define o modo silencioso. Nenhuma informação é gravada no console, inclusive informações de progresso e de cabeçalho.  
  
 **-rl** *analysis_report_list*  
 Especifica a lista de relatórios de análise a serem gerados. A seguinte tabela lista os valores que podem ser especificados para esse argumento:  
  
|Valor|Relatório|  
|-----------|------------|  
|ALL|Todos os relatórios de análise|  
|STMT_COST|Relatório de custo da instrução|  
|EVT_FREQ|Relatório de frequência de evento|  
|STMT_DET|Relatório de detalhe de instrução|  
|CUR_STMT_IDX|Relatório de relações do índice de instrução (configuração atual)|  
|REC_STMT_IDX|Relatório de relações do índice de instrução (configuração recomendada)|  
|STMT_COSTRANGE|Relatório de intervalo de custo da instrução|  
|CUR_IDX_USAGE|Relatório de uso de índice (configuração atual)|  
|REC_IDX_USAGE|Relatório de uso de índice (configuração recomendada)|  
|CUR_IDX_DET|Relatório de detalhe de índice (configuração atual)|  
|REC_IDX_DET|Relatório de detalhe de índice (configuração recomendada)|  
|VIW_TAB|Relatório de relações da tabela de exibição|  
|WKLD_ANL|Relatório de análise da carga de trabalho|  
|DB_ACCESS|Relatório de acesso ao banco de dados|  
|TAB_ACCESS|Relatório de acesso à tabela|  
|COL_ACCESS|Relatório de acesso à coluna|  
  
 Especifica relatórios múltiplos separando os valores com vírgulas, por exemplo:  
  
```  
... -rl EVT_FREQ, VIW_TAB, WKLD_ANL ...  
```  
  
 **-S** *server_name*[ *\instance*]  
 Especifica o nome do computador e a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para conexão. Se nenhum *server_name* for especificado, **dta** se conectará à instância padrão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no computador local. Essa opção é requerida na conexão à uma instância nomeada ou na execução de **dta** de um computador remoto na rede.  
  
 **-s** *session_name*  
 Especifica o nome da sessão de ajuste. Isso será obrigatório se **-ID** não for especificado.  
  
 **-Tf** *table_list_file*  
 Especifica o nome de um arquivo que contém uma lista de tabelas a ser ajustada. Cada tabela listada dentro do arquivo deve começar em uma linha nova. Nomes de tabela devem ser qualificados com nomeação de três partes, por exemplo, **AdventureWorks2012.HumanResources.Department**. Opcionalmente, para invocar o recurso do escalamento de tabela, o nome de uma tabela existente pode ser seguido de um número que indica o número projetado de linhas na tabela. O Orientador de Otimização do Mecanismo de Banco de Dados leva em conta o número projetado de linhas ao ajustar ou avaliar as instruções na carga de trabalho que referenciam estas tabelas. Observe que pode haver um ou mais espaços entre a contagem *number_of_rows* e *table_name*.  
  
 Este é o formato de arquivo para *table_list_file*:  
  
 *database_name*.[*schema_name*].*table_name* [*number_of_rows*]  
  
 *database_name*.[*schema_name*].*table_name* [*number_of_rows*]  
  
 *database_name*.[*schema_name*].*table_name* [*number_of_rows*]  
  
 Esse argumento é uma alternativa à inserção de uma lista de tabela no prompt de comando (**-Tl**). Não use um arquivo de lista de tabela (**-Tf**) se você estiver usando **-Tl**. Se ambos os argumentos forem usados, o **dta** falhará e retornará um erro.  
  
 Se os argumentos **-Tf** e **-Tl** forem omitidos, todas as tabelas de usuário nos bancos de dados especificados serão consideradas para o ajuste.  
  
 **-Tl** *table_list*  
 Especifica ao prompt de comando uma lista de tabelas a serem ajustadas. Coloque vírgulas entre os nomes de tabela para separá-los. Se apenas um banco de dados for especificado com o argumento **-D** , os nomes de tabela não precisarão ser qualificados com um nome de banco de dados. Caso contrário, o nome totalmente qualificado no formato: *database_name.schema_name.table_name* será obrigatório para cada tabela.  
  
 Esse argumento é uma alternativa ao uso de um arquivo de lista de tabela (**-Tf**). Se **-Tl** e **-Tf** forem usados, **dta** falhará e retornará um erro.  
  
 **-U** *login_id*  
 Especifica a ID de logon usada para conectar-se ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 **-u**  
 Inicia a GUI do Orientador de Otimização do Mecanismo de Banco de Dados. Todos os parâmetros são tratados como as configurações iniciais para a interface com o usuário.  
  
 **-x**  
 Inicia a sessão de ajuste e sai.  
  
## <a name="remarks"></a>Comentários  
 Pressione CTRL+C uma vez para parar a sessão de ajuste e gerar recomendações com base na análise do **dta** concluída até este ponto. Você será solicitado a indicar se deseja ou não gerar recomendações. Pressione CTRL+C novamente para parar a sessão de ajuste sem gerar recomendações.  
  
## <a name="examples"></a>Exemplos  
 **A. Ajustar uma carga de trabalho que inclui índices e exibições indexadas em sua recomendação**  
  
 Esse exemplo usa uma conexão segura (`-E`) para se conectar ao banco de dados **tpcd1G** no MyServer para analisar uma carga de trabalho e criar recomendações. Grava a saída em um arquivo de script nomeado script.sql. Se o script.sql já existir, **dta** substituirá o arquivo porque o argumento `-F` foi especificado. A sessão de ajuste é executada por um tempo ilimitado para garantir uma análise completa da carga de trabalho (`-A 0`). A recomendação deve fornecer uma melhoria mínima de 5% (`-m 5`). **dta** deve incluir índices e exibições indexadas em sua recomendação final (`-fa IDX_IV`).  
  
```  
dta –S MyServer –E -D tpcd1G -if tpcd_22.sql -F –of script.sql –A 0 -m 5 -fa IDX_IV  
```  
  
 **B. Limite o uso de disco**  
  
 Esse exemplo limita o tamanho de banco de dados total, que inclui os dados brutos e os índices adicionais, a 3 gigabytes (GB) (`-B 3000`) e direciona a saída para d:\result_dir\script1.sql. Ele é executado por no máximo 1 hora (`-A 60`).  
  
```  
dta –D tpcd1G –if tpcd_22.sql -B 3000 –of "d:\result_dir\script1.sql" –A 60  
```  
  
 **C. Limitar o número de consultas de ajuste**  
  
 Esse exemplo limita o número de consultas lidas do arquivo orders_wkld.sql a um máximo de 10 (`-n 10`) e é executado por 15 minutos (`-A 15`), o que ocorrer primeiro. Para garantir que todas as 10 consultas sejam ajustadas, especifique um tempo de ajuste ilimitado com `-A 0`. Se o tempo for importante, determine um prazo apropriado, especificando o número de minutos que estão disponíveis para ajuste com o argumento `-A` , como mostrado neste exemplo.  
  
```  
dta –D orders –if orders_wkld.sql –of script.sql –A 15 -n 10  
```  
  
 **D. Ajusta tabelas específicas listadas em um arquivo**  
  
 Este exemplo demonstra o uso de *table_list_file* (o argumento **-Tf** ). O conteúdo do arquivo table_list.txt é:  
  
```  
AdventureWorks2012.Sales.Customer  100000  
AdventureWorks2012.Sales.Store  
AdventureWorks2012.Production.Product  2000000  
```  
  
 O conteúdo de table_list.txt especifica que:  
  
-   Deve-se ajustar apenas as tabelas **Customer**, **Store**e **Product** no banco de dados.  
  
-   Presume-se que o número de linhas nas tabelas **Customer** e **Product** seja 100.000 e 2.000.000, respectivamente.  
  
-   Presume-se que em **Store** o número de linhas seja o número atual de linhas na tabela.  
  
 Observe que pode haver um ou mais espaços entre a contagem de número de linhas e o nome de tabela anterior em *table_list_file*.  
  
 O tempo de ajuste é de 2 horas (`-A 120`) e a saída é gravada em um arquivo XML (`-ox XMLTune.xml`).  
  
```  
dta –D pubs –if pubs_wkld.sql –ox XMLTune.xml –A 120 –Tf table_list.txt  
```  
  
## <a name="see-also"></a>Consulte também  
 [Referência de utilitários de prompt de comando &#40;Mecanismo de Banco de Dados&#41;](../../tools/command-prompt-utility-reference-database-engine.md)   
 [Orientador de Otimização do Mecanismo de Banco de Dados](../../relational-databases/performance/database-engine-tuning-advisor.md)  
  
  
