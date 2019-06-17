---
title: Executar o Console do SSMA (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: aa1bf665-8dc0-4259-b36f-46ae67197a43
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: d1dbbb57527fc2d362837e0340f35a241d764b75
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63473531"
---
# <a name="executing-the-ssma-console-accesstosql"></a>Executar o Console do SSMA (AccessToSQL)
Microsoft fornece um conjunto robusto de comandos do arquivo de script e opções de linha de comando para executar e controlar atividades do SSMA. Seções a seguir detalham os mesmos.  
  
## <a name="project--script-file-commands"></a>Comandos de arquivo de Script do projeto  
Os comandos de projeto lidar com a criação de projetos, abrir, salvar e sair de projetos.  
  
**Comando**  
  
create-new-project: Cria um novo projeto SSMA.  
  
**Script**  
  
-   `project-folder` indica a pasta do projeto sendo criado.  
  
-   `project-name` indica o nome do projeto. {string}  
  
-   `overwrite-if-exists`Atributo opcional indica se um projeto existente deve ser substituído. {booliano}  
  
-   `project-type` é um atributo opcional.  As seguintes opções estão disponíveis para o tipo de projeto:  
  
    -   sql-server-2005  
  
    -   sql-server-2008  
  
    -   sql-server-2012  
  
    -   sql-server-2014  
  
    -   sql-server-2016  
  
    -   sql-azure  
  
    Padrão é "sql-server-2008".  
  
**Exemplo:**  
  
```xml  
<create-new-project  
  
  project-folder="<project-folder>"  
  
  project-name="<project-name>"  
  
  overwrite-if-exists="<true/false>"  
  
  project-type="<sql-server-2008 | sql-server-2005 | sql-server-2012 | sql-server-2014 | sql-azure>"  
  
/>  
```  
Atributo 'Substituir-if-exists' está **falsos** por padrão.  
  
É o atributo 'tipo de projeto' **sql-server-2008** por padrão.  
  
**Comando**  
  
Abrir projeto: Abre um projeto existente.  
  
**Script**  
  
-   `project-folder` indica a pasta do projeto sendo criado. O comando falhará se a pasta especificada não existe.  {string}  
  
-   `project-name` indica o nome do projeto. O comando falhará se o projeto especificado não existe.  {string}  
  
**Exemplo de sintaxe:**  
  
```xml  
<open-project  
  
  project-folder="<project-folder>"  
  
  project-name="<project-name>"  
  
/>  
```  
**Observação:** Aplicativo de Console do SSMA para Access dá suporte a compatibilidade com versões anteriores. Você poderá abrir projetos criados por uma versão anterior do SSMA.  
  
**Comando**  
  
save-project: Salva o projeto de migração.  
  
**Script**  
  
**Exemplo de sintaxe:**  
  
```xml  
<save-project/>  
```  
**Comando**  
  
close-project: Fecha o projeto de migração.  
  
**Script**  
  
**Exemplo de sintaxe:**  
  
```xml  
<close-project  
  
  if-modified="<save/error/ignore>"   (optional)  
  
/>  
```  
Atributo 'if-modificada' é opcional, **ignorar** por padrão.  
  
## <a name="database-connection-script-file-commands"></a>Comandos de arquivo de Script de Conexão de banco de dados  
Os comandos de Conexão de banco de dados ajudam a conectar-se ao banco de dados.  
  
O **procurar** não há suporte para o recurso da interface do usuário no console.  
  
O **autenticação do windows** e **porta** parâmetros não são aplicáveis ao se conectar ao SQL Azure.  
  
Para obter mais informações sobre 'Criando arquivos de Script', consulte [criando arquivos de Script &#40;AccessToSQL&#41;](../../ssma/access/creating-script-files-accesstosql.md).  
  
**Comando**  
  
conectar-se-origem-banco de dados  
  
-   Executa a conexão à fonte de dados e carrega os metadados de nível alto do banco de dados de origem, mas não todos os metadados.  
  
-   Se a conexão à fonte não pode ser estabelecida, um erro será gerado e o aplicativo de console para ainda mais a execução  
  
**Script**  
  
Definição de servidor é recuperada do atributo nome definido para cada conexão na seção servidor de arquivo de conexão do servidor ou o arquivo de script.  
  
**Exemplo de sintaxe:**  
  
```xml  
<connect-source-database  server="<server-unique-name>"/>  
```  
**Comando**  
  
carga-acesso-banco de dados: Usado para carregar arquivos de banco de dados do access  
  
**Script**  
  
**Exemplo de sintaxe:**  
  
```xml  
<load-access-database  database-file="<Access-database>"/>  
```  
ou em  
  
```xml  
<load-access-database>  
  
  <access-database database-file="<Access-database1>"/>  
  
  <access-database database-file="<Access-database2>"/>  
  
</load-access-database>  
```  
**Comando**  
  
Force-carga-origem/destino-banco de dados  
  
-   Carrega os metadados da fonte.  
  
-   É útil para trabalhar no projeto de migração off-line.  
  
-   Se a conexão para o origem/destino não puder ser estabelecida, um erro será gerado e o aplicativo de console para ainda mais a execução  
  
**Script**  
  
Requer um ou vários nós de metabase como parâmetro de linha de comando.  
  
**Exemplo de sintaxe:**  
  
```xml  
<force-load  
  
  object-name="<object-name>"  
  
  metabase="<source/target>"/>  
```  
ou em  
  
```xml  
<force-load>  
  
  <metabase-object object-name="<object-name>"/>  
  
</force-load>  
```  
**Comando**  
  
reconnect-source-database  
  
-   Reconecta-se à fonte de dados, mas não carrega todos os metadados ao contrário do comando connect-origem-banco de dados.  
  
-   Se não é possível estabelecer (conexão com a fonte de re), um erro será gerado e o aplicativo de console ainda mais para a execução.  
  
**Script**  
  
**Exemplo de sintaxe:**  
  
```xml  
<reconnect-source-database  server="<server-unique-name>"/>  
```  
**Comando**  
  
connect-target-database  
  
-   Conecta-se ao destino do SQL Server ou SQL Azure banco de dados e carrega os metadados de nível alto do banco de dados de destino, mas não os metadados inteiramente.  
  
-   Se a conexão para o destino não puder ser estabelecida, um erro será gerado e o aplicativo de console ainda mais para a execução.  
  
**Script**  
  
Definição de servidor é recuperada do atributo nome definido para cada conexão na seção servidor de arquivo de conexão do servidor ou o arquivo de script  
  
**Exemplo de sintaxe:**  
  
```xml  
<connect-target-database  server="<server-unique-name>"/>  
```  
**Comando**  
  
reconnect-target-database  
  
-   Reconecta-se ao banco de dados de destino, mas não carrega todos os metadados, ao contrário do comando de destino-connect-database.  
  
-   Se a (re) conexão para o destino não puder ser estabelecida, um erro será gerado e o aplicativo de console ainda mais para a execução.  
  
**Script**  
  
**Exemplo de sintaxe:**  
  
```xml  
<reconnect-target-database  server="<server-unique-name>"/>  
```  
  
## <a name="report-script-file-commands"></a>Comandos de arquivo de Script de relatório  
Os comandos de relatório geram relatórios sobre o desempenho de várias atividades do Console do SSMA.  
  
**Comando**  
  
generate-assessment-report  
  
-   Gera relatórios de avaliação no banco de dados de origem.  
  
-   Se a conexão de banco de dados de origem não é executada antes de executar esse comando, será gerado um erro e sai do aplicativo de console.  
  
-   Falha ao se conectar ao servidor de banco de dados de origem durante a execução do comando, também resulta em encerrar o aplicativo de console.  
  
**Script**  
  
-   `assessment-report-folder:` Especifica a pasta onde o relatório de avaliação pode ser armazenado. (atributo opcional)  
  
-   `object-name:` Especifica os objetos considerados para a geração de relatório de avaliação (ele pode ter nomes de objetos individuais ou um nome de objeto de grupo).  
  
-   `object-type:` Especifica o tipo do objeto especificado no atributo de nome de objeto (se a categoria de objeto for especificada, o tipo de objeto será "category").  
  
-   `assessment-report-overwrite:` Especifica se deve substituir a pasta de relatório de avaliação se ele já existe.  
  
    **Valor padrão:** false. (atributo opcional)  
  
-   `write-summary-report-to:` Especifica o caminho onde o relatório será gerado.  
  
    Se apenas o caminho da pasta for mencionado, em seguida, de arquivos por nome **AssessmentReport&lt;n&gt;. XML** é criado. (atributo opcional)  
  
    Criação de relatório tem duas subcategorias adicionais:  
  
    -   `report-errors` (= "true/false", com padrão como "false" (atributos opcionais))  
  
    -   `verbose` (= "true/false", com padrão como "false" (atributos opcionais))  
  
**Exemplo de sintaxe:**  
  
```xml  
<generate-assessment-report  
  
  object-name="ssma.Procedures"  
  
  object-type="category"  
  
  write-summary-report-to="<file>"             (optional)  
  
  verbose="<true/false>"                       (optional)  
  
  report-errors="<true/false>"                 (optional)  
  
  conversion-report-folder="<folder>"          (optional)  
  
  conversion-report-overwrite="<true/false>"   (optional)  
  
/>  
```  
ou em  
  
```xml  
<generate-assessment-report  
  
  conversion-report-folder="<folder>"            (optional)  
  
  conversion-report-overwrite="<true/false>"     (optional)  
  
>  
    <metabase-object object-name="ssma.Procedures"  
  
        object-type="category"/>  
  
</generate-assessment-report>  
```  
  
## <a name="migration-script-file-commands"></a>Comandos de arquivo de Script de migração  
Os comandos de migração converter o esquema de banco de dados de destino para o esquema de origem e migra dados para o servidor de destino.  
  
A saída do console padrão definindo para os comandos de migração é o relatório de saída 'Full' com nenhum relatório de erro detalhada: Resumo somente no nó de raiz da árvore de objeto de origem.  
  
**Comando**  
  
convert-schema  
  
-   Executa a conversão de esquema de origem ao esquema de destino.  
  
-   Se a conexão de banco de dados de origem ou de destino não é executada antes de executar esse comando ou a conexão para o servidor de banco de dados de origem ou destino falha durante a execução do comando, será gerado um erro e sai do aplicativo de console.  
  
**Script**  
  
-   `conversion-report-folder:` Especifica a pasta onde o relatório de avaliação pode ser armazenado. (atributo opcional)  
  
-   `object-name:` Especifica os objetos de origem considerados para a conversão de esquema (ele pode ter nomes de objetos individuais ou um nome de objeto de grupo).  
  
-   `object-type:` Especifica o tipo do objeto especificado no atributo de nome de objeto (se a categoria de objeto for especificada, o tipo de objeto será "category").  
  
-   `conversion-report-overwrite:` Especifica se deve substituir a pasta de relatório de avaliação se ele já existe.  
  
    **Valor padrão:** false. (atributo opcional)  
  
-   `write-summary-report-to:` Especifica o caminho onde o relatório será gerado.  
  
    Se apenas o caminho da pasta for mencionado, em seguida, de arquivos por nome **SchemaConversionReport&lt;n&gt;. XML** é criado. (atributo opcional)  
  
    Criação de relatório tem duas subcategorias adicionais:  
  
    -   `report-errors` (= "true/false", com padrão como "false" (atributos opcionais))  
  
    -   `verbose` (= "true/false", com padrão como "false" (atributos opcionais))  
  
**Exemplo de sintaxe:**  
  
```xml  
<convert-schema  
  
  object-name="ssma.Procedures"  
  
  object-type="category"  
  write-summary-report-to="<filepath/folder>"     (optional)  
  
  verbose="<true/false>"                          (optional)  
  
  report-errors="<true/false>"                    (optional)  
  
  conversion-report-folder="<folder>"             (optional)  
  
  conversion-report-overwrite="<true/false>"      (optional)  
  
/>  
```  
ou em  
  
```xml  
<convert-schema  
  
  conversion-report-folder="<folder>"         (optional)  
  
  conversion-report-overwrite="<true/false>"  (optional)  
  
  <metabase-object object-name="ssma.Procedures"  
  
    object-type="category"/>  
  
</convert-schema>  
```  
**Comando**  
  
migrate-data  
  
1.  Migra os dados de origem para o destino.  
  
**Script**  
  
-   `object-name:` Especifica os objetos de origem considerados para a migração de dados (ele pode ter nomes de objetos individuais ou um nome de objeto de grupo).  
  
-   `object-type:` Especifica o tipo do objeto especificado no atributo de nome de objeto (se a categoria de objeto for especificada, o tipo de objeto será "category").  
  
-   `write-summary-report-to:` Especifica o caminho onde o relatório será gerado.  
  
    Se apenas o caminho da pasta for mencionado, em seguida, de arquivos por nome **DataMigrationReport&lt;n&gt;. XML** é criado. (atributo opcional)  
  
    Criação de relatório tem duas subcategorias adicionais:  
  
    -   `report-errors` (= "true/false", com padrão como "false" (atributos opcionais))  
  
    -   `verbose` (= "true/false", com padrão como "false" (atributos opcionais))  
  
**Exemplo de sintaxe:**  
  
```xml  
<migrate-data  
  
  write-summary-report-to="<filepath/folder>"  
  
  report-errors="true" verbose="true">  
  
    <metabase-object object-name="ssma.TT1"/>  
  
    <metabase-object object-name="ssma.TT2"/>  
  
    <metabase-object object-name="ssma.TT3"/>  
  
    <data-migration-connection  
  
      source-use-last-used="true"/source-server="<server-unique-name>"  
  
      target-use-last-used="true"/target-server="<server-unique-name>"/>  
  
</migrate-data>  
```  
ou em  
  
```xml  
<migrate-data  
  
  object-name="ssma.Tables"  
  
  object-type="category"  
  
  write-summary-report-to="<filepath/folder>"  
  
  report-errors="true" verbose="true"/>  
```  
**Comando**  
  
Vincular tabelas: Esse comando vincula a tabela de origem (acesso) para a tabela de destino.  
  
**Script**  
  
**Exemplo de sintaxe:**  
  
```xml  
<link-tables>  
  
  <metabase-object object-name="AccessDatabase.table1" object-type="Tables"/>  
  
  <metabase-object object-name="AccessDatabase.table2" object-type="Tables"/>  
  
</link-tables>  
```  
ou em  
  
```xml  
<link-tables>  
  
  <metabase-object object-name="AccessDatabase.Tables" object-type="category"/>  
  
</link-tables>  
```  
**Comando**  
  
Desvincular-tabelas: Esse comando desvincula a tabela de origem (acesso) da tabela de destino.  
  
**Script**  
  
**Exemplos de sintaxe:**  
  
```xml  
<unlink-tables>  
  
  <metabase-object object-name="AccessDatabase.table1" object-type="Tables"/>  
  
  <metabase-object object-name="AccessDatabase.table2" object-type="Tables"/>  
  
</unlink-tables>  
```  
ou em  
  
```xml  
<unlink-tables>  
  
  <metabase-object object-name="AccessDatabase.Tables" object-type="category"/>  
  
</unlink-tables>  
```  
  
## <a name="migration-preparation-script-file-commands"></a>Comandos de arquivo de Script de preparação de migração  
O comando de preparação de migração inicia o mapeamento de esquema entre os bancos de dados de origem e destino.  
  
**Comando**  
  
map-schema: Mapeamento de esquema de banco de dados de origem ao esquema de destino.  
  
**Script**  
  
-   `source-schema` Especifica o esquema de origem que nossa intenção é migrar.  
  
-   `sql-server-schema` Especifica o esquema de destino onde desejamos a serem migrados.  
  
**Exemplo de sintaxe:**  
  
```xml  
<map-schema source-schema="source-schema"  
  
            sql-server-schema="target-schema"/>  
```  
  
## <a name="manageability-commands"></a>Comandos de capacidade de gerenciamento  
Os comandos de capacidade de gerenciamento ajudam a sincronizar os objetos de banco de dados de destino com o banco de dados de origem.  
  
A saída do console padrão definindo para os comandos de migração é o relatório de saída 'Full' com nenhum relatório de erro detalhada: Resumo somente no nó de raiz da árvore de objeto de origem.  
  
**Comando**  
  
synchronize-target  
  
1.  Sincroniza os objetos de destino com o banco de dados de destino.  
  
2.  Se esse comando for executado no banco de dados de origem, um erro for encontrado.  
  
3.  Se a conexão de banco de dados de destino não é executada antes de executar esse comando ou a conexão ao servidor de banco de dados de destino falha durante a execução do comando, será gerado um erro e o aplicativo de console é encerrado.  
  
**Script**  
  
1.  `object-name:` Especifica os objetos de destino considerados para sincronizar com o banco de dados de destino (ele pode ter nomes de objetos individuais ou um nome de objeto de grupo).  
  
2.  `object-type:` Especifica o tipo do objeto especificado no atributo de nome de objeto (se a categoria de objeto for especificada, o tipo de objeto será "category").  
  
3.  `on-error:` Especifica se deve especificar os erros de sincronização como avisos ou erros. Opções disponíveis para em caso de erro:  
  
    -   report-total-as-warning  
  
    -   report-each-as-warning  
  
    -   Falha-script  
  
4.  `report-errors-to:` Especifica o local do relatório de erros para a operação de sincronização (atributo opcional) se apenas o caminho da pasta for dado, em seguida, de arquivos por nome **TargetSynchronizationReport.XML** é criado.  
  
**Exemplo de sintaxe:**  
  
```xml  
<synchronize-target  
  
  object-name="ots_triggers.dbo"  
  
  on-error="<report-total-as-warning|  
  
             report-each-as-warning|  
  
             fail-script>"              (optional)  
  
  report-errors-to="<file-name>"        (optional)  
  
/>  
```  
ou em  
  
```xml  
<synchronize-target  
  
  object-name="ssma.dbo.Procedures"  
  
  object-type="category"/>  
```  
ou em  
  
```xml  
<synchronize-target>  
  
  <metabase-object object-name="ssma.dbo.TT1"/>  
  
  <metabase-object object-name="ssma.dbo.TT2"/>  
  
  <metabase-object object-name="ssma.dbo.TT3"/>  
  
</synchronize-target>  
```  
**Comando**  
  
refresh-from-database  
  
-   Atualiza os objetos de origem do banco de dados.  
  
-   Se esse comando é executado no banco de dados de destino, um erro será gerado.  
  
**Script**  
  
Requer um ou vários nós de metabase como parâmetro de linha de comando.  
  
1.  `object-name:` Especifica os objetos de origem considerados para a atualização do banco de dados de origem (ele pode ter nomes de objetos individuais ou um nome de objeto de grupo).  
  
2.  `object-type:` Especifica o tipo do objeto especificado no atributo de nome de objeto (se a categoria de objeto for especificada, o tipo de objeto será "category").  
  
3.  `on-error:` Especifica se deve especificar os erros de atualização como avisos ou erros. Opções disponíveis para em caso de erro:  
  
    -   report-total-as-warning  
  
    -   report-each-as-warning  
  
    -   Falha-script  
  
4.  `report-errors-to:` Especifica o local do relatório de erros para a operação de atualização (atributo opcional) se apenas o caminho da pasta for dado, em seguida, de arquivos por nome **SourceDBRefreshReport.XML** é criado.  
  
**Exemplo de sintaxe:**  
  
```xml  
<refresh-from-database  
  
  object-name="ssma.TT1"  
  
  on-error="<report-total-as-warning|  
  
             report-each-as-warning|  
  
             fail-script>"              (optional)  
  
  report-errors-to="<file-name>"        (optional)  
  
/>  
```  
ou em  
  
```xml  
<refresh-from-database  
  
  object-name="ssma.Procedures"  
  
  object-type="category"/>  
```  
ou em  
  
```xml  
<refresh-from-database>  
  
  <metabase-object object-name="ssma.TT_1"/>  
  
</refresh-from-database>  
```  
  
## <a name="script-generation-script-file-commands"></a>Comandos de arquivo de Script de geração de script  
A geração de Script de comandos ajudam a salvar a saída do console em um arquivo de script.  
  
**Comando**  
  
Salvar como script  
  
Usado para salvar os Scripts dos objetos em um arquivo mencionado quando metabase Target, essa é uma alternativa ao comando de sincronização, onde podemos obter os scripts e execute o mesmo banco de dados de destino.  
  
**Script**  
  
Requer um ou vários nós de metabase como parâmetro de linha de comando.  
  
-   `object-name:` Especifica os objetos cujos scripts serão salvos. (Ele pode ter nomes de objetos individuais ou um nome de objeto de grupo)  
  
-   `object-type:` Especifica o tipo do objeto especificado no atributo de nome de objeto (se a categoria de objeto for especificada, o tipo de objeto será "category").  
  
-   `metabase:` Especifica se é a origem ou destino da metabase.  
  
-   `destination:` Especifica o caminho ou a pasta em que o script foi salvo, se o nome do arquivo não for fornecido, em seguida, um nome de arquivo na. out formato (valor do atributo object_name)  
  
-   `overwrite:` Se for true, em seguida, ele substitui se o mesmo nome de arquivo existe. Ele pode ter os valores (true/false).  
  
**Exemplo de sintaxe:**  
  
```xml  
<save-as-script  
  
  metabase="<source/target>"  
  
  object-name="ssma.dbo.Procedures"  
  
  object-type="category"  
  
  destination="<file/folder>"  
  
  overwrite="<true/false>"             (optional)  
  
/>  
```  
ou em  
  
```xml  
<save-as-script  
  
  metabase="<source/target>"  
  
  destination="<file/folder>"  
  
    <metabase-object object-name="ssma.dbo.Procedures"  
  
                     object-type="category"/>  
  
</save-as-script>  
```  
  
## <a name="next-step"></a>Próxima etapa  
Para obter informações sobre as opções de linha de comando, consulte [opções de linha de comando no Console do SSMA &#40;AccessToSQL&#41; ](../../ssma/access/command-line-options-in-ssma-console-accesstosql.md) .  
  
Para obter informações sobre arquivos de script de console de exemplo, consulte [trabalhando com o FilesExecuting de Script de Console de exemplo o Console do SSMA &#40;AccessToSQL&#41;](../../ssma/access/working-sample-console-script-filesexecuting-ssma-console-accesstosql.md)  
  
A próxima etapa depende de seus requisitos de projeto:  
  
-   Para especificar uma senha ou a exportação / importação de senhas, consulte [gerenciamento de senhas &#40;AccessToSQL&#41;](../../ssma/access/managing-passwords-accesstosql.md).  
  
-   Para gerar relatórios, consulte [geração de relatórios &#40;AccessToSQL&#41;](../../ssma/access/generating-reports-accesstosql.md).  
  
-   Para solucionar problemas no console, consulte [solução de problemas &#40;AccessToSQL&#41;](../../ssma/access/troubleshooting-accesstosql.md).  
  
