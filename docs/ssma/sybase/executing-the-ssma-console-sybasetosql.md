---
title: Executar o Console do SSMA (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/27/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Sybase Console,Database Connection Commands
- Sybase Console,Manageability Commands
- Sybase Console,Migration Commands
- Sybase Console,Migration Preparation Command
- Sybase Console,Project Commands
- Sybase Console,Report Commands
- Sybase Console,Script File Commands
- Sybase Console,Script Generation Commands
ms.assetid: ea8950b7-fabc-4aa4-89f8-9573a2617d70
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 517c96deaf37934e82c1161c66b8e5825d1b14b1
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47780435"
---
# <a name="executing-the-ssma-console-sybasetosql"></a>Executar o console do SSMA (SybaseToSQL)
Microsoft fornece um conjunto robusto de script de comandos de arquivo para executar e controlar atividades do SSMA. Seções a seguir detalham os mesmos.  
  
## <a name="script-file-commands"></a>Comandos do arquivo de script  
O aplicativo de console usa determinados comandos do arquivo de script padrão como enumerado nesta seção.  
  
## <a name="project-commands"></a>Comandos de projeto  
Os comandos de projeto lidar com a criação de projetos, abrir, salvar e sair de projetos.  
  
### <a name="create-new-project"></a>create-new-project  
Este comando cria um novo projeto SSMA.  
  
-   `project-folder` indica a pasta do projeto sendo criado.  
  
-   `project-name` indica o nome do projeto. {string}  
  
-   `overwrite-if-exists`Atributo opcional indica se um projeto existente deve ser substituído. {booliano}  
  
-   `project-type:`Atributo opcional. Indica o tipo de projeto, que é o projeto "sql-server 2005" ou "sql-server-2008" projeto ou projeto "sql-server-2012" ou "sql-server-2014" projeto ou projeto "sql azure". O padrão é "sql-server-2008".  
  
**Exemplo de sintaxe:**  
  
```xml  
<create-new-project  
  
  project-folder="<project-folder>"  
  
  project-name="<project-name>"  
  
  overwrite-if-exists="<true/false>" (optional)  
  
   project-type=”<sql-server-2008/sql-server-2005/sql-server-2012/sql-server-2014/sql-azure>”  
/>  
```  
Atributo 'Substituir-if-exists' está **falsos** por padrão.  
  
É o atributo 'tipo de projeto' **sql-server-2008** por padrão.  
  
### <a name="open-project"></a>Abrir projeto  
Esse comando abre o projeto.

-   `project-folder` indica a pasta do projeto sendo criado. O comando falhará se a pasta especificada não existe.  {string}  
  
-   `project-name` indica o nome do projeto. O comando falhará se o projeto especificado não existe.  {string}  
  
**Exemplo de sintaxe:**  
  
```xml  
<open-project  
  
  project-folder="<project-folder>"  
  
  project-name="<project-name>"  
  
/>  
```  
> [!NOTE]  
> O SSMA para o aplicativo de Console do SAP ASE dá suporte à compatibilidade com versões anteriores. Você pode usá-lo para abrir projetos criados por uma versão anterior do SSMA.  
  
### <a name="save-project"></a>Salvar projeto  
Este comando salva o projeto de migração.  
  
**Exemplo de sintaxe:**  
  
```xml  
<save-project/>  
```  
  
### <a name="close-project"></a>Fechar projeto  
Esse comando fecha o projeto de migração.  
  
**Exemplo de sintaxe:**  
  
```xml  
<close-project   
  if-modified="<save/error/ignore>"   (optional)  
/>  
```  
Atributo 'if-modificada' é opcional, **ignorar** por padrão.  
  
## <a name="database-connection-commands"></a>Comandos de Conexão de banco de dados  
Os comandos de Conexão de banco de dados ajudam a conectar-se ao banco de dados.  
  
> [!NOTE]  
> - O **procurar** não há suporte para o recurso da interface do usuário no console.  
> - Para obter mais informações sobre 'Criando arquivos de Script', consulte [criando arquivos de Script &#40;SybaseToSQL&#41;](../../ssma/sybase/creating-script-files-sybasetosql.md).  
  
### <a name="connect-source-database"></a>conectar-se-origem-banco de dados  
Esse comando executa a conexão à fonte de dados e carrega os metadados de alto nível do banco de dados de origem, mas não todos os metadados.
  
Se a conexão à fonte não pode ser estabelecida, um erro será gerado e o aplicativo de console ainda mais para a execução.
  
A definição de servidor é recuperada do atributo nome definido para cada conexão na seção servidor de arquivo de conexão do servidor ou o arquivo de script.  
  
**Exemplo de sintaxe:**  
  
```xml  
<connect-source-database  server="<server-unique-name>"/>  
```  
  
### <a name="force-load-sourcetarget-database"></a>Force-carga-origem/destino-banco de dados  
Esse comando carrega os metadados da fonte, e é útil para trabalhar no projeto de migração off-line.  
  
Se a conexão para o origem/destino não puder ser estabelecida, um erro será gerado e o aplicativo de console ainda mais para a execução.  
  
Este comando requer um ou vários nós de metabase como parâmetro de linha de comando.  
  
**Exemplo de sintaxe:**  
  
```xml  
<force-load metabase=”<source/target>” >  
  
  <metabase-object object-name="<object-name>"/>  
  
</force-load>  
```  
  
### <a name="reconnect-source-database"></a>Reconecte-origem-banco de dados  
Esse comando se reconecta ao banco de dados de origem, mas não carrega todos os metadados ao contrário do comando connect-origem-banco de dados.  
  
Se não é possível estabelecer (conexão com a fonte de re), um erro será gerado e o aplicativo de console ainda mais para a execução.  
  
**Exemplo de sintaxe:**  
  
```xml  
<reconnect-source-database  server="<server-unique-name>"/>  
```  
  
### <a name="connect-target-database"></a>connect-target-database  
Esse comando conecta-se para o banco de dados do SQL Server de destino e carrega os metadados de alto nível do banco de dados de destino, mas não os metadados inteiramente.  
  
Se a conexão para o destino não puder ser estabelecida, um erro será gerado e o aplicativo de console ainda mais para a execução.  
  
A definição de servidor é recuperada do atributo nome definido para cada conexão na seção servidor de arquivo de conexão do servidor ou o arquivo de script.  
  
**Exemplo de sintaxe:**  
  
```xml  
<connect-target-database  server="<server-unique-name>"/>  
```  
  
### <a name="reconnect-target-database"></a>reconnect-target-database  
  
Esse comando se reconecta ao banco de dados de destino, mas não carrega todos os metadados, ao contrário do comando de destino-connect-database.  
  
Se a (re) conexão para o destino não puder ser estabelecida, um erro será gerado e o aplicativo de console ainda mais para a execução.  
  
**Exemplo de sintaxe:**  
  
```xml  
<reconnect-target-database  server="<server-unique-name>"/>  
```  
  
## <a name="report-commands"></a>Comandos de relatório  
Os comandos de relatório geram relatórios sobre o desempenho de várias atividades do Console do SSMA.  
  
### <a name="generate-assessment-report"></a>Gerar--relatório de avaliação  
  
Este comando gera relatórios de avaliação no banco de dados de origem.  
  
Se a conexão de banco de dados de origem não é executada antes de executar esse comando, será gerado um erro e sai do aplicativo de console.  
  
Falha ao se conectar ao servidor de banco de dados de origem durante a execução do comando, também resulta em encerrar o aplicativo de console.  
  
-   `conversion-report-folder:` Especifica a pasta na qual o relatório de avaliação pode ser armazenado. (atributo opcional)  
  
-   `object-name:` Especifica os objetos considerados para a geração de relatório de avaliação (dá suporte a nomes de objeto individual ou um nome de objeto de grupo).  
  
-   `object-type:` Especifica o tipo do objeto chamado no atributo de nome de objeto (se a categoria de objeto for especificada, o tipo de objeto será "category").  
  
-   `conversion-report-overwrite:` Especifica se deve substituir a pasta de relatório de avaliação se ele já existe.  
  
    **Valor padrão:** false. (atributo opcional)  
  
-   `write-summary-report-to:` Especifica o caminho no qual o relatório será gerado.  
  
    Se apenas o caminho da pasta for mencionado, em seguida, de arquivos por nome **AssessmentReport&lt;n&gt;. XML** é criado. (atributo opcional)  
  
    Criação de relatório tem duas subcategorias adicionais:  
  
    -   `report-errors` (= "true/false", com padrão como "false" (atributos opcionais))  
  
    -   `verbose` (= "true/false", com padrão como "false" (atributos opcionais))  
  
**Exemplo de sintaxe:**  
  
```xml  
<generate-assessment-report  
  
  object-name="<object-name>"  
  
  object-type="<object-category>"  
  
  write-summary-report-to="<file-name/folder-name>”             (optional)  
  
  verbose="<true/false>"                       (optional)  
  
  report-errors="<true/false>"                 (optional)  
  
  assessment-report-folder="<folder-name>"          (optional)  
  
  conversion-report-overwrite="<true/false>"   (optional)  
  
/>  
```  
ou em  
  
```xml  
<generate-assessment-report  
  
  assessment-report-folder="<folder-name>"            (optional)  
  
  conversion-report-overwrite="<true/false>"     (optional)  
  
>  
<metabase-object object-name="<object-name>"  
  
        object-type="<object-category>"/>  
  
</generate-assessment-report>  
```  
  
## <a name="migration-commands"></a>Comandos de migração  
Os comandos de migração converter o esquema de banco de dados de destino para o esquema de origem e migrar dados para o servidor de destino.  
  
### <a name="convert-schema"></a>convert-schema  
Esse comando executa a conversão de esquema de origem ao esquema de destino.  
  
Se a conexão de banco de dados de origem ou de destino não é executada antes de executar esse comando ou a conexão para o servidor de banco de dados de origem ou destino falha durante a execução do comando, será gerado um erro e sai do aplicativo de console.  
  
-   `conversion-report-folder:` Especifica a pasta na qual o relatório de avaliação pode ser armazenado. (atributo opcional)  
  
-   `object-name:` Especifica os objetos de origem considerados para a conversão de esquema (dá suporte a nomes de objeto individual ou um nome de objeto de grupo).  
  
-   `object-type:` Especifica o tipo do objeto chamado no atributo de nome de objeto (se a categoria de objeto for especificada, o tipo de objeto será "category").  
  
-   `conversion-report-overwrite:` Especifica se deve substituir a pasta de relatório de avaliação se ele já existe.  
  
    **Valor padrão:** false. (atributo opcional)  
  
-   `write-summary-report-to:` Especifica o caminho no qual o relatório de resumo será gerado.  
  
    Se apenas o caminho da pasta for mencionado, em seguida, de arquivos por nome **SchemaConversionReport&lt;n&gt;. XML** é criado. (atributo opcional)  
  
    Criação de relatório tem duas subcategorias adicionais:  
  
    -   `report-errors` (= "true/false", com padrão como "false" (atributos opcionais))  
  
    -   `verbose` (= "true/false", com padrão como "false" (atributos opcionais))  
  
**Exemplo de sintaxe:**  
  
```xml  
<convert-schema  
  
  object-name="<object-name>"  
  
  object-type="<object-category>"  
  write-summary-report-to="<file-name/folder-name>"     (optional)  
  
  verbose="<true/false>"                          (optional)  
  
  report-errors="<true/false>"                    (optional)  
  
  conversion-report-folder="<folder-name>"             (optional)  
  
  conversion-report-overwrite="<true/false>"      (optional)  
  
/>  
```  
ou em  
  
```xml  
<convert-schema  
  
  conversion-report-folder="<folder-name>"         (optional)  
  
  conversion-report-overwrite="<true/false>"> (optional)  
  
  <metabase-object object-name="<object-name>"  
  
    object-type="<object-category>"/>  
  
</convert-schema>  
```  
  
### <a name="migrate-data"></a>migrar dados  
Esse comando migra os dados de origem ao destino.  
  
-   `object-name:` Especifica os objetos de origem considerados para a migração de dados (dá suporte a nomes de objeto individual ou um nome de objeto de grupo).  
  
-   `object-type:` Especifica o tipo do objeto chamado no atributo de nome de objeto (se a categoria de objeto for especificada, o tipo de objeto será "category").  
  
-   `write-summary-report-to:` Especifica o caminho no qual o relatório será gerado.  
  
    Se apenas o caminho da pasta for mencionado, em seguida, de arquivos por nome **DataMigrationReport&lt;n&gt;. XML** é criado. (atributo opcional)  
  
    Criação de relatório tem duas subcategorias adicionais:  
  
    -   `report-errors` (= "true/false", com padrão como "false" (atributos opcionais))  
  
    -   `verbose` (= "true/false", com padrão como "false" (atributos opcionais))  
  
**Exemplo de sintaxe:**  
  
```xml  
<migrate-data  
  
  write-summary-report-to="<file-name/folder-name>"  
  
  report-errors="<true/false>" verbose="<true/false>">  
  
    <metabase-object object-name="<object-name>"/>  
  
    <metabase-object object-name="<object-name>"/>  
  
    <metabase-object object-name="<object-name>"/>  
  
    <data-migration-connection  
  
      source-use-last-used="true"/source-server="<server-unique-name>"  
  
      target-use-last-used="true"/target-server="<server-unique-name>"/>  
  
</migrate-data>  
```  
ou em  
  
```xml  
<migrate-data  
  
  object-name="<object-name>"  
  
  object-type="<object-category>"  
  
  write-summary-report-to="<file-name/folder-name>"  
  
  report-errors="<true/false>" verbose="<true/false>"/>  
```  
  
## <a name="migration-preparation-command"></a>Comando de preparação de migração  
O comando de preparação de migração inicia o mapeamento de esquema entre os bancos de dados de origem e destino.  
  
> [!NOTE]  
> A saída do console padrão definindo para os comandos de migração é o relatório de saída 'Full' com nenhum relatório de erro detalhada: resumo apenas no nó de raiz da árvore de objeto de origem.  
  
### <a name="map-schema"></a>map-schema  
Esse comando fornece o mapeamento de esquema do banco de dados de origem ao esquema de destino.  
  
-   `source-schema` Especifica o esquema de origem para migrar.  
  
-   `sql-server-schema` Especifica o esquema de destino ao qual o esquema de origem será migrado.  
  
**Exemplo de sintaxe:**  
  
```xml  
<map-schema source-schema="<source-schema>"  
  
sql-server-schema="<target-schema>"/>  
```  
  
## <a name="manageability-commands"></a>Comandos de capacidade de gerenciamento  
Os comandos de capacidade de gerenciamento ajudam a sincronizar os objetos de banco de dados de destino com o banco de dados de origem.  
  
> [!NOTE]  
> A saída do console padrão definindo para os comandos de migração é o relatório de saída 'Full' com nenhum relatório de erro detalhada: resumo apenas no nó de raiz da árvore de objeto de origem.  
  
### <a name="synchronize-target"></a>Sincronizar de destino  
Este comando sincroniza os objetos de destino com o banco de dados de destino.  
 
Se esse comando for executado no banco de dados de origem, um erro for encontrado.  
  
Se a conexão de banco de dados de destino não é executada antes de executar esse comando ou a conexão ao servidor de banco de dados de destino falha durante a execução do comando, será gerado um erro e o aplicativo de console é encerrado.  
  
-   `object-name:` Especifica os objetos de destino considerados para sincronizar com o banco de dados de destino (dá suporte a nomes de objeto individual ou um nome de objeto de grupo).  
  
-   `object-type:` Especifica o tipo do objeto chamado no atributo de nome de objeto (se a categoria de objeto for especificada, o tipo de objeto será "category").  
  
-   `on-error:` Especifica se deve especificar os erros de sincronização como avisos ou erros. Opções disponíveis para em caso de erro:  
  
    -   report-total-as-warning  
  
    -   report-each-as-warning  
  
    -   Falha-script  
  
-   `report-errors-to:` Especifica o local do relatório de erro para a operação de sincronização (atributo opcional). Se apenas o caminho da pasta for dado, em seguida, de arquivos por nome **TargetSynchronizationReport.XML** é criado.  
  
**Exemplo de sintaxe:**  
  
```xml  
<synchronize-target  
  
object-name="<object-name>"  
  
on-error="<report-total-as-warning/  
  
report-each-as-warning/  
  
fail-script>" (optional)  
  
  report-errors-to="<file-name/folder-name>"        (optional)  
  
/>  
```  
ou em  
  
```xml  
<synchronize-target  
  
  object-name="<object-name>"  
  
  object-type="<object-category>"/>  
```  
ou em  
  
```xml  
<synchronize-target>  
  
  <metabase-object object-name="<object-name>"/>  
  
  <metabase-object object-name="<object-name>"/>  
  
  <metabase-object object-name="<object-name>"/>  
  
</synchronize-target>  
```  
  
### <a name="refresh-from-database"></a>atualização de banco de dados  
Esse comando atualiza os objetos de origem do banco de dados.  
  
Se esse comando é executado no banco de dados de destino, um erro será gerado.  
  
Este comando requer um ou vários nós de metabase como parâmetro de linha de comando.  
  
-   `object-name:` Especifica os objetos de origem considerados para a atualização do banco de dados de origem (dá suporte a nomes de objeto individual ou um nome de objeto de grupo).  
  
-   `object-type:` Especifica o tipo do objeto especificado no atributo de nome de objeto (se a categoria de objeto for especificada, o tipo de objeto será "category").  
  
-   `on-error:` Especifica se a chamada atualização erros como avisos ou erros. Opções disponíveis para em caso de erro:  
  
    -   report-total-as-warning  
  
    -   report-each-as-warning  
  
    -   Falha-script  
  
-   `report-errors-to:` Especifica o local do relatório de erro para a operação de atualização (atributo opcional). Se apenas o caminho da pasta for dado, em seguida, de arquivos por nome **SourceDBRefreshReport.XML** é criado.  
  
**Exemplo de sintaxe:**  
  
```xml  
<refresh-from-database  
  
  object-name="<object-name>"  
  
  on-error="<report-total-as-warning/  
  
             report-each-as-warning/  
  
             fail-script>"              (optional)  
  
  report-errors-to="<file-name/folder-name>"        (optional)  
  
/>  
```  
ou em  
  
```xml  
<refresh-from-database  
  
  object-name="<object-name>"  
  
  object-type="<object-category>" />  
```  
ou em  
  
```xml  
<refresh-from-database>  
  
  <metabase-object object-name="<object-name>"/>  
  
</refresh-from-database>  
```  
  
## <a name="script-generation-commands"></a>Comandos de geração de script  
Os comandos de geração de Script executam duas tarefas: eles ajudam a salvar a saída em um arquivo de script do console, e eles gravam a saída do T-SQL para o console ou um arquivo de acordo com o parâmetro que você especificar.  
  
### <a name="save-as-script"></a>Salvar como script  
Esse comando é usado para salvar os Scripts dos objetos em um arquivo mencionado quando metabase Target. Essa é uma alternativa ao comando de sincronização que podemos obter os scripts e executar o mesmo banco de dados de destino.  
  
Este comando requer um ou vários nós de metabase como parâmetro de linha de comando.  
  
-   `object-name:` Especifica os objetos cujos scripts serão salvos (dá suporte a nomes de objeto individual ou um nome de objeto de grupo).  
  
-   `object-type:` Especifica o tipo do objeto chamado no atributo de nome de objeto (se a categoria de objeto for especificada, o tipo de objeto será "category").  
  
-   `metabase:` Especifica se é a origem ou destino da metabase.  
  
-   `destination:` Especifica o caminho ou a pasta na qual o script deve ser salvo. Se o nome do arquivo não for fornecido, será fornecido um nome de arquivo a. out formato (valor do atributo object_name).
  
-   `overwrite:` Se for true, ele substitui o mesmo nome de arquivo se ele existir. Ele pode ter os valores (true/false).  
  
**Exemplo de sintaxe:**  
  
```xml  
<save-as-script  
  
  metabase="<source/target>"  
  
  object-name="<object-name>"  
  
  object-type="<object-category>"  
  
  destination="<file-name/folder-name>"  
  
  overwrite="<true/false>"   (optional)  
  
/>  
```  
ou em  
  
```xml  
<save-as-script  
  
  metabase="<source/target>"  
  
  destination="<file-name/folder-name>"  
  
    <metabase-object object-name="<object-name>"  
  
                     object-type="<object-category>"/>  
  
</save-as-script>  
```  
  
### <a name="convert-sql-statement"></a>convert-sql-statement
Este comando converte a instrução SQL.  
  
-   `context` Especifica o nome do esquema.  
  
-   `destination` Especifica se a saída deve ser armazenada em um arquivo.  
  
    Se esse atributo não for especificado, a instrução T-SQL convertida é exibida no console. (atributo opcional)  
  
-   `conversion-report-folder` Especifica a pasta na qual o relatório de avaliação pode ser armazenado. (atributo opcional)  
  
-   `conversion-report-overwrite` Especifica se deve substituir a pasta de relatório de avaliação se ele já existe.  
  
    **Valor padrão:** false. (atributo opcional)  
  
-   `write-converted-sql-to` Especifica o caminho da pasta de arquivo (ou) para que o T-SQL convertido deve ser armazenado. Quando um caminho de pasta é especificado junto com o `sql-files` atributo, cada arquivo de origem tem um destino correspondente arquivo T-SQL criado sob a pasta especificada. Quando um caminho de pasta é especificado junto com o `sql` atributo, o T-SQL convertido é gravado em um arquivo chamado Result.out sob a pasta especificada.  
  
-   `sql` Especifica as instruções de sql do Sybase para ser convertido, uma ou mais instruções podem ser separadas usando um ";"  
  
-   `sql-files` Especifica o caminho dos arquivos de sql que deve ser convertido em código T-SQL.  
  
-   `write-summary-report-to` Especifica o caminho onde o relatório de resumo será gerado. Se apenas o caminho da pasta for mencionado, em seguida, de arquivos por nome **ConvertSQLReport.XML** é criado. (atributo opcional)  
  
    Criação de relatório de resumo tem duas subcategorias adicionais, ou seja:  
  
    -   erros de relatório (= "true/false", com padrão como "false" (atributos opcionais)).  
  
    -   detalhado (= "true/false", com padrão como "false" (atributos opcionais)).  
  
Este comando requer um ou vários nós de metabase como parâmetro de linha de comando.  
  
**Exemplo de sintaxe:**  
  
```  
<convert-sql-statement  
  
       context="<database-name>.<schema-name>"  
  
        conversion-report-folder="<folder-name>"  
  
        conversion-report-overwrite="<true/false>"  
  
        write-summary-report-to="<file-name/folder-name>"   (optional)  
  
        verbose="<true/false>"   (optional)  
  
        report-errors="<true/false>"   (optional)  
  
        destination="<stdout/file>"   (optional)  
  
        write-converted-sql-to ="<file-name/folder-name>"  
  
        sql="SELECT 1 FROM DUAL;">  
  
    <output-window suppress-messages="<true/false>" />  
  
</convert-sql-statement>  
```  
ou em  
  
```  
<convert-sql-statement  
  
         context="<database-name>.<schema-name>"  
  
         conversion-report-folder="<folder-name>"  
  
         conversion-report-overwrite="<true/false>"  
  
         write-summary-report-to="<file-name/folder-name>"   (optional)  
  
         verbose="<true/false>"   (optional)  
  
         report-errors="<true/false>"   (optional)  
  
         destination="<stdout/file>"   (optional)  
  
         write-converted-sql-to ="<file-name/folder-name>"  
  
         sql-files="<folder-name>\*.sql"  
  
/>  
```  
ou em  
  
```  
<convert-sql-statement  
  
         context="<database-name>.<schema-name>"  
  
         conversion-report-folder="<folder-name>"  
  
         conversion-report-overwrite="<true/false>"  
  
         sql-files="<folder-name>\*.sql"  
  
/>  
```  
  
## <a name="next-steps"></a>Próximas etapas  
Para obter informações sobre as opções de linha de comando, consulte [opções de linha de comando no Console do SSMA (AccessToSQL)](../access/command-line-options-in-ssma-console-accesstosql.md).  
  
Para obter informações sobre um arquivo de script de console de exemplo, consulte [trabalhando com os arquivos de Script de Console de exemplo &#40;SybaseToSQL&#41;](../../ssma/sybase/working-with-the-sample-console-script-files-sybasetosql.md)  
  
A próxima etapa depende de seus requisitos de projeto:  
  
-   Para especificar uma senha ou a exportação / importação de senhas, consulte [gerenciamento de senhas &#40;SybaseToSQL&#41;](../../ssma/sybase/managing-passwords-sybasetosql.md).  
  
-   Para gerar relatórios, consulte [geração de relatórios &#40;SybaseToSQL&#41;](../../ssma/sybase/generating-reports-sybasetosql.md).  
  
-   Para solucionar problemas no console, consulte [solução de problemas &#40;SybaseToSQL&#41;](../../ssma/sybase/troubleshooting-sybasetosql.md).  
  
