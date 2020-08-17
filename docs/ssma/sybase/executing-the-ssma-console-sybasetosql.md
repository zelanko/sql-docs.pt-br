---
description: Executar o console do SSMA (SybaseToSQL)
title: Executando o console do SSMA (SybaseToSQL) | Microsoft Docs
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
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: fee973fdcb79105d5fe7c412c10bdda2cd1bbec5
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88372232"
---
# <a name="executing-the-ssma-console-sybasetosql"></a>Executar o console do SSMA (SybaseToSQL)
A Microsoft fornece um conjunto robusto de comandos de arquivo de script para executar e controlar atividades do SSMA. As seções que mais profundos detalham o mesmo.  
  
## <a name="script-file-commands"></a>Comandos de arquivo de script  
O aplicativo de console usa determinados comandos de arquivo de script padrão, conforme enumerado nesta seção.  
  
## <a name="project-commands"></a>Comandos de projeto  
Os comandos de projeto lidam com a criação de projetos, abertura, salvamento e saída de projetos.  
  
### <a name="create-new-project"></a>create-new-project  
Este comando cria um novo projeto do SSMA.  
  
-   `project-folder` indica a pasta do projeto que está sendo criado.  
  
-   `project-name` indica o nome do projeto. {string}  
  
-   `overwrite-if-exists`Atributo opcional indica se um projeto existente deve ser substituído. Boolean  
  
-   `project-type:`Atributo opcional. Indica o tipo de projeto, que é "SQL-Server-2005" Project ou "SQL-Server-2008" Project ou "SQL-Server-2012" Project ou "SQL-Server-2014" Project ou o projeto "SQL-Azure". O padrão é "SQL-Server-2008."  
  
**Exemplo de sintaxe:**  
  
```xml  
<create-new-project  
  
  project-folder="<project-folder>"  
  
  project-name="<project-name>"  
  
  overwrite-if-exists="<true/false>" (optional)  
  
   project-type="<sql-server-2008/sql-server-2005/sql-server-2012/sql-server-2014/sql-azure>"  
/>  
```  
O atributo ' overwrite-if-exists ' é **false** por padrão.  
  
O atributo ' Project-Type ' é **SQL-Server-2008** por padrão.  
  
### <a name="open-project"></a>Abrir projeto  
Esse comando abre o projeto.

-   `project-folder` indica a pasta do projeto que está sendo criado. O comando falhará se a pasta especificada não existir.  {string}  
  
-   `project-name` indica o nome do projeto. O comando falhará se o projeto especificado não existir.  {string}  
  
**Exemplo de sintaxe:**  
  
```xml  
<open-project  
  
  project-folder="<project-folder>"  
  
  project-name="<project-name>"  
  
/>  
```  
> [!NOTE]  
> O aplicativo de console do SSMA para SAP ASE dá suporte à compatibilidade com versões anteriores. Você pode usá-lo para abrir projetos criados pela versão anterior do SSMA.  
  
### <a name="save-project"></a>save-project  
Esse comando salva o projeto de migração.  
  
**Exemplo de sintaxe:**  
  
```xml  
<save-project/>  
```  
  
### <a name="close-project"></a>fechar projeto  
Esse comando fecha o projeto de migração.  
  
**Exemplo de sintaxe:**  
  
```xml  
<close-project   
  if-modified="<save/error/ignore>"   (optional)  
/>  
```  
O atributo ' If-Modified ' é opcional, **ignore** por padrão.  
  
## <a name="database-connection-commands"></a>Comandos de conexão de banco de dados  
Os comandos de conexão do banco de dados ajudam a conectar-se ao banco de dados.  
  
> [!NOTE]  
> - Não há suporte para o recurso **procurar** da interface do usuário no console do.  
> - Para obter mais informações sobre como criar arquivos de script, consulte [criando arquivos de script &#40;SybaseToSQL&#41;](../../ssma/sybase/creating-script-files-sybasetosql.md).  
  
### <a name="connect-source-database"></a>Connect-Source-Database  
Esse comando executa a conexão com o banco de dados de origem e carrega metadados de alto nível do banco de dados de origem, mas não todos os metadados.
  
Se a conexão com a origem não puder ser estabelecida, um erro será gerado e o aplicativo de console parará outra execução.
  
A definição de servidor é recuperada do atributo de nome definido para cada conexão na seção do servidor do arquivo de conexão do servidor ou do arquivo de script.  
  
**Exemplo de sintaxe:**  
  
```xml  
<connect-source-database  server="<server-unique-name>"/>  
```  
  
### <a name="force-load-sourcetarget-database"></a>Force-Load-origem/destino-banco de dados  
Esse comando carrega os metadados de origem e é útil para trabalhar no projeto de migração offline.  
  
Se a conexão com a origem/destino não puder ser estabelecida, um erro será gerado e o aplicativo de console parará outra execução.  
  
Este comando requer um ou vários nós da metabase como parâmetro de linha de comando.  
  
**Exemplo de sintaxe:**  
  
```xml  
<force-load metabase="<source/target>" >  
  
  <metabase-object object-name="<object-name>"/>  
  
</force-load>  
```  
  
### <a name="reconnect-source-database"></a>reconectar-fonte-banco de dados  
Esse comando reconecta-se ao banco de dados de origem, mas não carrega nenhum metadado diferente do comando Connect-Source-Database.  
  
Se a conexão (re) com a origem não puder ser estabelecida, um erro será gerado e o aplicativo de console parará outra execução.  
  
**Exemplo de sintaxe:**  
  
```xml  
<reconnect-source-database  server="<server-unique-name>"/>  
```  
  
### <a name="connect-target-database"></a>Connect-Target-Database  
Esse comando conecta-se ao banco de dados de destino SQL Server e carrega metadados de alto nível do banco de dados de destino, mas não os metadados inteiramente.  
  
Se a conexão com o destino não puder ser estabelecida, um erro será gerado e o aplicativo de console parará outra execução.  
  
A definição de servidor é recuperada do atributo de nome definido para cada conexão na seção do servidor do arquivo de conexão do servidor ou do arquivo de script.  
  
**Exemplo de sintaxe:**  
  
```xml  
<connect-target-database  server="<server-unique-name>"/>  
```  
  
### <a name="reconnect-target-database"></a>reconectar-destino-banco de dados  
  
Esse comando reconecta-se ao banco de dados de destino, mas não carrega nenhum metadado, ao contrário do comando Connect-Target-Database.  
  
Se a conexão (re) com o destino não puder ser estabelecida, um erro será gerado e o aplicativo de console interromperá a execução.  
  
**Exemplo de sintaxe:**  
  
```xml  
<reconnect-target-database  server="<server-unique-name>"/>  
```  
  
## <a name="report-commands"></a>Comandos de relatório  
Os comandos de relatório geram relatórios sobre o desempenho de várias atividades do console do SSMA.  
  
### <a name="generate-assessment-report"></a>gerar-avaliação-relatório  
  
Esse comando gera relatórios de avaliação no banco de dados de origem.  
  
Se a conexão do banco de dados de origem não for executada antes da execução desse comando, um erro será gerado e o aplicativo de console será encerrado.  
  
Falha ao conectar-se ao servidor de banco de dados de origem durante a execução do comando, também resulta na finalização do aplicativo de console.  
  
-   `conversion-report-folder:` Especifica a pasta na qual o relatório de avaliação pode ser armazenado. (atributo opcional)  
  
-   `object-name:` Especifica os objetos considerados para geração de relatórios de avaliação (dá suporte a nomes de objetos individuais ou a um nome de objeto de grupo).  
  
-   `object-type:` Especifica o tipo do objeto chamado no atributo Object-Name (se a categoria de objeto for especificada, o tipo de objeto será "category").  
  
-   `conversion-report-overwrite:` Especifica se a pasta do relatório de avaliação deve ser substituída, caso ela já exista.  
  
    **Valor padrão:** false. (atributo opcional)  
  
-   `write-summary-report-to:` Especifica o caminho no qual o relatório será gerado.  
  
    Se apenas o caminho da pasta for mencionado, clique em arquivo por nome **AssessmentReport &lt; n &gt; . XML** é criado. (atributo opcional)  
  
    A criação de relatório tem duas subcategorias adicionais:  
  
    -   `report-errors` (= "true/false", com padrão como "false" (atributos opcionais))  
  
    -   `verbose` (= "true/false", com padrão como "false" (atributos opcionais))  
  
**Exemplo de sintaxe:**  
  
```xml  
<generate-assessment-report  
  
  object-name="<object-name>"  
  
  object-type="<object-category>"  
  
  write-summary-report-to="<file-name/folder-name>"             (optional)  
  
  verbose="<true/false>"                       (optional)  
  
  report-errors="<true/false>"                 (optional)  
  
  assessment-report-folder="<folder-name>"          (optional)  
  
  conversion-report-overwrite="<true/false>"   (optional)  
  
/>  
```  
ou  
  
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
Os comandos de migração convertem o esquema de banco de dados de destino para o esquema de origem e migram dados para o servidor de destino.  
  
### <a name="convert-schema"></a>converter esquema  
Esse comando executa a conversão de esquema da origem para o esquema de destino.  
  
Se a conexão de banco de dados de origem ou de destino não for executada antes da execução desse comando ou se a conexão com o servidor de banco de dados de origem ou destino falhar durante a execução do comando, um erro será gerado e o aplicativo de console será encerrado.  
  
-   `conversion-report-folder:` Especifica a pasta na qual o relatório de avaliação pode ser armazenado. (atributo opcional)  
  
-   `object-name:` Especifica os objetos de origem considerados para converter o esquema (dá suporte a nomes de objetos individuais ou a um nome de objeto de grupo).  
  
-   `object-type:` Especifica o tipo do objeto chamado no atributo Object-Name (se a categoria de objeto for especificada, o tipo de objeto será "category").  
  
-   `conversion-report-overwrite:` Especifica se a pasta do relatório de avaliação deve ser substituída, caso ela já exista.  
  
    **Valor padrão:** false. (atributo opcional)  
  
-   `write-summary-report-to:` Especifica o caminho no qual o relatório de resumo será gerado.  
  
    Se apenas o caminho da pasta for mencionado, clique em arquivo por nome **SchemaConversionReport &lt; n &gt; . XML** é criado. (atributo opcional)  
  
    A criação de relatório tem duas subcategorias adicionais:  
  
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
ou  
  
```xml  
<convert-schema  
  
  conversion-report-folder="<folder-name>"         (optional)  
  
  conversion-report-overwrite="<true/false>"> (optional)  
  
  <metabase-object object-name="<object-name>"  
  
    object-type="<object-category>"/>  
  
</convert-schema>  
```  
  
### <a name="migrate-data"></a>migrar-dados  
Esse comando migra os dados de origem para o destino.  
  
-   `object-name:` Especifica os objetos de origem considerados para migrar dados (dá suporte a nomes de objetos individuais ou a um nome de objeto de grupo).  
  
-   `object-type:` Especifica o tipo do objeto chamado no atributo Object-Name (se a categoria de objeto for especificada, o tipo de objeto será "category").  
  
-   `write-summary-report-to:` Especifica o caminho no qual o relatório será gerado.  
  
    Se apenas o caminho da pasta for mencionado, clique em arquivo por nome **DataMigrationReport &lt; n &gt; . XML** é criado. (atributo opcional)  
  
    A criação de relatório tem duas subcategorias adicionais:  
  
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
ou  
  
```xml  
<migrate-data  
  
  object-name="<object-name>"  
  
  object-type="<object-category>"  
  
  write-summary-report-to="<file-name/folder-name>"  
  
  report-errors="<true/false>" verbose="<true/false>"/>  
```  
  
## <a name="migration-preparation-command"></a>Comando de preparação de migração  
O comando de preparação de migração inicia o mapeamento de esquema entre os bancos de dados de origem e de destino.  
  
> [!NOTE]  
> A configuração de saída do console padrão para os comandos de migração é ' completo ' relatório de saída sem relatórios de erros detalhados: apenas Resumo no nó raiz da árvore do objeto de origem.  
  
### <a name="map-schema"></a>mapa-esquema  
Esse comando fornece o mapeamento de esquema do banco de dados de origem para o esquema de destino.  
  
-   `source-schema` Especifica o esquema de origem a ser migrado.  
  
-   `sql-server-schema` Especifica o esquema de destino para o qual o esquema de origem será migrado.  
  
**Exemplo de sintaxe:**  
  
```xml  
<map-schema source-schema="<source-schema>"  
  
sql-server-schema="<target-schema>"/>  
```  
  
## <a name="manageability-commands"></a>Comandos de gerenciamento  
Os comandos de gerenciamento ajudam a sincronizar os objetos de banco de dados de destino com o banco de dados de origem.  
  
> [!NOTE]  
> A configuração de saída do console padrão para os comandos de migração é ' completo ' relatório de saída sem relatórios de erros detalhados: apenas Resumo no nó raiz da árvore do objeto de origem.  
  
### <a name="synchronize-target"></a>sincronizar destino  
Esse comando sincroniza os objetos de destino com o banco de dados de destino.  
 
Se esse comando for executado no banco de dados de origem, um erro será encontrado.  
  
Se a conexão do banco de dados de destino não for executada antes da execução desse comando ou se a conexão com o servidor de banco de dados de destino falhar durante a execução do comando, um erro será gerado e o aplicativo de console será encerrado.  
  
-   `object-name:` Especifica os objetos de destino considerados para sincronização com o banco de dados de destino (dá suporte a nomes de objetos individuais ou a um nome de objeto de grupo).  
  
-   `object-type:` Especifica o tipo do objeto chamado no atributo Object-Name (se a categoria de objeto for especificada, o tipo de objeto será "category").  
  
-   `on-error:` Especifica se os erros de sincronização devem ser especificados como avisos ou erro. Opções disponíveis para o no-erro:  
  
    -   relatório-total-como-aviso  
  
    -   relatório-cada-como-aviso  
  
    -   script de falha  
  
-   `report-errors-to:` Especifica o local do relatório de erros para a operação de sincronização (atributo opcional). Se apenas o caminho da pasta for fornecido, o arquivo por nome **TargetSynchronizationReport.XML** será criado.  
  
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
ou  
  
```xml  
<synchronize-target  
  
  object-name="<object-name>"  
  
  object-type="<object-category>"/>  
```  
ou  
  
```xml  
<synchronize-target>  
  
  <metabase-object object-name="<object-name>"/>  
  
  <metabase-object object-name="<object-name>"/>  
  
  <metabase-object object-name="<object-name>"/>  
  
</synchronize-target>  
```  
  
### <a name="refresh-from-database"></a>atualizar-do-banco de dados  
Este comando atualiza os objetos de origem do banco de dados.  
  
Se esse comando for executado no banco de dados de destino, um erro será gerado.  
  
Este comando requer um ou vários nós da metabase como parâmetro de linha de comando.  
  
-   `object-name:` Especifica os objetos de origem considerados para atualização do banco de dados de origem (dá suporte a nomes de objetos individuais ou a um nome de objeto de grupo).  
  
-   `object-type:` Especifica o tipo do objeto especificado no atributo Object-Name (se a categoria de objeto for especificada, o tipo de objeto será "category").  
  
-   `on-error:` Especifica se os erros de atualização devem ser cancelados como avisos ou erros. Opções disponíveis para o no-erro:  
  
    -   relatório-total-como-aviso  
  
    -   relatório-cada-como-aviso  
  
    -   script de falha  
  
-   `report-errors-to:` Especifica o local do relatório de erros para a operação de atualização (atributo opcional). Se apenas o caminho da pasta for fornecido, o arquivo por nome **SourceDBRefreshReport.XML** será criado.  
  
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
ou  
  
```xml  
<refresh-from-database  
  
  object-name="<object-name>"  
  
  object-type="<object-category>" />  
```  
ou  
  
```xml  
<refresh-from-database>  
  
  <metabase-object object-name="<object-name>"/>  
  
</refresh-from-database>  
```  
  
## <a name="script-generation-commands"></a>Comandos de geração de script  
Os comandos de geração de script executam tarefas duplas: elas ajudam a salvar a saída do console em um arquivo de script e registram a saída do T-SQL no console do ou em um arquivo com base no parâmetro especificado.  
  
### <a name="save-as-script"></a>salvar como script  
Esse comando é usado para salvar os scripts dos objetos em um arquivo mencionado quando metabase = destino. Essa é uma alternativa ao comando de sincronização, pois obtemos os scripts e executamos o mesmo no banco de dados de destino.  
  
Este comando requer um ou vários nós da metabase como parâmetro de linha de comando.  
  
-   `object-name:` Especifica os objetos cujos scripts devem ser salvos (dá suporte a nomes de objetos individuais ou a um nome de objeto de grupo).  
  
-   `object-type:` Especifica o tipo do objeto chamado no atributo Object-Name (se a categoria de objeto for especificada, o tipo de objeto será "category").  
  
-   `metabase:` Especifica se é a metabase de origem ou de destino.  
  
-   `destination:` Especifica o caminho ou a pasta na qual o script deve ser salvo. Se o nome do arquivo não for fornecido, um nome de arquivo no formato (object_name valor do atributo). out será fornecido.
  
-   `overwrite:` Se for true, ele substituirá o mesmo nome de arquivo, se existir. Ele pode ter os valores (true/false).  
  
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
ou  
  
```xml  
<save-as-script  
  
  metabase="<source/target>"  
  
  destination="<file-name/folder-name>"  
  
    <metabase-object object-name="<object-name>"  
  
                     object-type="<object-category>"/>  
  
</save-as-script>  
```  
  
### <a name="convert-sql-statement"></a>instrução Convert-SQL-
Esse comando converte a instrução SQL.  
  
-   `context` Especifica o nome do esquema.  
  
-   `destination` Especifica se a saída deve ser armazenada em um arquivo.  
  
    Se esse atributo não for especificado, a instrução T-SQL convertida será exibida no console do. (atributo opcional)  
  
-   `conversion-report-folder` Especifica a pasta na qual o relatório de avaliação pode ser armazenado. (atributo opcional)  
  
-   `conversion-report-overwrite` Especifica se a pasta do relatório de avaliação deve ser substituída, caso ela já exista.  
  
    **Valor padrão:** false. (atributo opcional)  
  
-   `write-converted-sql-to` Especifica o arquivo (ou) caminho da pasta para o qual o T-SQL convertido deve ser armazenado. Quando um caminho de pasta é especificado junto com o `sql-files` atributo, cada arquivo de origem tem um arquivo T-SQL de destino correspondente criado na pasta especificada. Quando um caminho de pasta é especificado junto com o `sql` atributo, o T-SQL convertido é gravado em um arquivo chamado Result. out na pasta especificada.  
  
-   `sql` Especifica as instruções do Sybase SQL a serem convertidas, uma ou mais instruções podem ser separadas usando um ";"  
  
-   `sql-files` Especifica o caminho dos arquivos SQL que precisa ser convertido em código T-SQL.  
  
-   `write-summary-report-to` Especifica o caminho onde o relatório de resumo será gerado. Se apenas o caminho da pasta for mencionado, o arquivo por nome **ConvertSQLReport.XML** será criado. (atributo opcional)  
  
    A criação do relatório de resumo tem duas subcategorias adicionais, ou seja:  
  
    -   relatório-erros (= "true/false", com padrão como "false" (atributos opcionais)).  
  
    -   Verbose (= "true/false", com padrão como "false" (atributos opcionais)).  
  
Este comando requer um ou vários nós da metabase como parâmetro de linha de comando.  
  
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
ou  
  
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
ou  
  
```  
<convert-sql-statement  
  
         context="<database-name>.<schema-name>"  
  
         conversion-report-folder="<folder-name>"  
  
         conversion-report-overwrite="<true/false>"  
  
         sql-files="<folder-name>\*.sql"  
  
/>  
```  
  
## <a name="next-steps"></a>Próximas etapas  
Para obter informações sobre opções de linha de comando, consulte [Opções de linha de comando no console do SSMA (AccessToSQL)](../access/command-line-options-in-ssma-console-accesstosql.md).  
  
Para obter informações sobre um exemplo de arquivo de script de console, consulte [trabalhando com os arquivos de script de console de exemplo &#40;SybaseToSQL&#41;](../../ssma/sybase/working-with-the-sample-console-script-files-sybasetosql.md)  
  
A próxima etapa depende dos requisitos do seu projeto:  
  
-   Para especificar uma senha ou exportar/importar senhas, consulte [Gerenciando senhas &#40;SybaseToSQL&#41;](../../ssma/sybase/managing-passwords-sybasetosql.md).  
  
-   Para gerar relatórios, consulte [gerando relatórios &#40;SybaseToSQL&#41;](../../ssma/sybase/generating-reports-sybasetosql.md).  
  
-   Para solucionar problemas no console do, consulte solução de problemas [&#40;SybaseToSQL&#41;](../../ssma/sybase/troubleshooting-sybasetosql.md).  
  
