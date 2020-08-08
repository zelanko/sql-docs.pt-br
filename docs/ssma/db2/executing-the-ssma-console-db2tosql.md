---
title: Executando o console do SSMA (DB2ToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: ce63f633-067d-4f04-b8e9-e1abd7ec740b
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 7b3f7e776268eed28beed4e4349c1ae8909789d5
ms.sourcegitcommit: e8f6c51d4702c0046aec1394109bc0503ca182f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/07/2020
ms.locfileid: "87933807"
---
# <a name="executing-the-ssma-console-db2tosql"></a>Executando o console do SSMA (DB2ToSQL)
A Microsoft fornece um conjunto robusto de comandos de arquivo de script para executar e controlar atividades do SSMA. As seções que mais profundos detalham o mesmo. O aplicativo de console usa determinados comandos de arquivo de script padrão, conforme enumerado nesta seção.  
  
## <a name="project-script-file-commands"></a>Comandos de arquivo de script do projeto  
Os comandos de projeto lidam com a criação de projetos, abertura, salvamento e saída de projetos.  
  
**Comando**  
  
create-new-project  
  
Cria um novo projeto do SSMA.  
  
**Script**  
  
-   `project-folder`indica a pasta do projeto que está sendo criado.  
  
-   `project-name`indica o nome do projeto. {string}  
  
-   `overwrite-if-exists`Atributo opcional indica se um projeto existente deve ser substituído. Boolean  
  
-   `project-type:`Atributo opcional. Indica o tipo de projeto, por exemplo, "SQL-Server-2005" Project ou "SQL-Server-2008" Project ou "SQL-Server-2012" Project ou "SQL-Server-2014" ou "SQL-Azure". O padrão é "SQL-Server-2014".  
  
**Exemplo:**  
  
```xml  
<create-new-project  
  
   project-folder="<project-folder>"  
  
   project-name="<project-name>"  
  
   overwrite-if-exists="<true/false>"   (optional)  
  
   project-type="<sql-server-2008 | sql-server-2005 | sql-server-2012 | sql-server-2014>"   (optional)  
  
/>  
```  
O atributo ' overwrite-if-exists ' é **false** por padrão.  
  
O atributo ' Project-Type ' é **SQL-Server-2008** por padrão.  
  
**Comando**  
  
Abrir projeto  
  
Abre um projeto existente.  
  
**Script**  
  
-   `project-folder`indica a pasta do projeto que está sendo criado. O comando falhará se a pasta especificada não existir.  {string}  
  
-   `project-name`indica o nome do projeto. O comando falhará se o projeto especificado não existir.  {string}  
  
**Exemplo de sintaxe:**  
  
```xml  
<open-project  
  
   project-folder="<project-folder>"  
  
   project-name="<project-name>"  
  
/>  
```  
O aplicativo de console do SSMA para DB2 dá suporte à compatibilidade com versões anteriores. Você poderá abrir projetos criados pela versão anterior do SSMA.  
  
**Comando**  
  
save-project  
  
Salva o projeto de migração.  
  
**Script**  
  
**Exemplo de sintaxe:**  
  
```xml  
<save-project/>  
```  
**Comando**  
  
fechar projeto  
  
Fecha o projeto de migração.  
  
**Script**  
  
**Exemplo de sintaxe:**  
  
```xml  
<close-project  
  
   if-modified="<save/error/ignore>"   (optional)  
  
/>  
```  
  
## <a name="database-connection-script-file-commands"></a>Comandos de arquivo de script de conexão de banco de dados  
Os comandos de conexão do banco de dados ajudam a conectar-se ao banco de dados.  
  
-   Não há suporte para o recurso **procurar** da interface do usuário no console do.  
  
-   Para obter mais informações sobre como criar arquivos de script, consulte [criando arquivos de script &#40;OracleToSQL&#41;](../../ssma/oracle/creating-script-files-oracletosql.md).  
  
**Comando**  
  
Connect-Source-Database  
  
-   Executa a conexão com o banco de dados de origem e carrega metadados de alto nível do banco de dados de origem, mas não todos os metadados.  
  
-   Se a conexão com a origem não puder ser estabelecida, um erro será gerado e o aplicativo de console parará outra execução  
  
**Script**  
  
A definição do servidor é recuperada do atributo Name definido para cada conexão na seção do servidor do arquivo de conexão do servidor ou do arquivo de script.  
  
**Exemplo de sintaxe:**  
  
```xml  
<connect-source-database  server="<server-unique-name>"/>  
```  
**Comando**  
  
Force-Load-origem/destino-banco de dados  
  
-   Carrega os metadados de origem.  
  
-   Útil para trabalhar no projeto de migração offline.  
  
-   Se a conexão com a origem/destino não puder ser estabelecida, um erro será gerado e o aplicativo de console parará outra execução  
  
**Script**  
  
Requer um ou vários nós da metabase como parâmetro de linha de comando.  
  
**Exemplo de sintaxe:**  
  
```xml  
<force-load object-name="<object-name>"  
  
  metabase="<source/target>"/>  
```  
ou o  
  
```xml  
<force-load>  
  
   <metabase-object object-name="<object-name>"/>  
  
</force-load>  
```  
**Comando**  
  
reconectar-fonte-banco de dados  
  
-   Reconecta-se ao banco de dados de origem, mas não carrega nenhum metadado diferente do comando Connect-Source-Database.  
  
-   Se a conexão (re) com a origem não puder ser estabelecida, um erro será gerado e o aplicativo de console parará outra execução.  
  
**Script**  
  
**Exemplo de sintaxe:**  
  
```xml  
<reconnect-source-database  server="<server-unique-name>"/>  
```  
**Comando**  
  
Connect-Target-Database  
  
-   Conecta-se ao banco de dados de SQL Server de destino e carrega metadados de alto nível do banco de dados de destino, mas não os metadados inteiramente.  
  
-   Se a conexão com o destino não puder ser estabelecida, um erro será gerado e o aplicativo de console parará outra execução.  
  
**Script**  
  
A definição do servidor é recuperada do atributo Name definido para cada conexão na seção do servidor do arquivo de conexão do servidor ou do arquivo de script  
  
**Exemplo de sintaxe:**  
  
```xml  
<connect-target-database  server="<server-unique-name>"/>  
```  
**Comando**  
  
reconectar-destino-banco de dados  
  
-   Reconecta-se ao banco de dados de destino, mas não carrega nenhum metadado, diferente do comando Connect-Target-Database.  
  
-   Se a conexão (re) com o destino não puder ser estabelecida, um erro será gerado e o aplicativo de console interromperá a execução.  
  
**Script**  
  
**Exemplo de sintaxe:**  
  
```xml  
<reconnect-target-database  server="<server-unique-name>"/>  
```  
  
## <a name="report-script-file-commands"></a>Comandos de arquivo de script de relatório  
Os comandos de relatório geram relatórios sobre o desempenho de várias atividades do console do SSMA.  
  
**Comando**  
  
gerar-avaliação-relatório  
  
-   Gera relatórios de avaliação no banco de dados de origem.  
  
-   Se a conexão do banco de dados de origem não for executada antes da execução desse comando, um erro será gerado e o aplicativo de console será encerrado.  
  
-   Falha ao conectar-se ao servidor de banco de dados de origem durante a execução do comando, também resulta na finalização do aplicativo de console.  
  
**Script**  
  
-   `conversion-report-folder:`Especifica a pasta onde o relatório de avaliação pode ser armazenado. (atributo opcional)  
  
-   `object-name:`Especifica os objetos considerados para geração de relatórios de avaliação (ele pode ter nomes de objeto individuais ou um nome de objeto de grupo).  
  
-   `object-type:`Especifica o tipo do objeto especificado no atributo Object-Name (se a categoria de objeto for especificada, o tipo de objeto será "category").  
  
-   `conversion-report-overwrite:`Especifica se a pasta do relatório de avaliação deve ser substituída, caso ela já exista.  
  
    **Valor padrão:** false. (atributo opcional)  
  
-   `write-summary-report-to:`Especifica o caminho onde o relatório de resumo será gerado.  
  
    Se apenas o caminho da pasta for mencionado, clique em arquivo por nome **AssessmentReport &lt; n &gt; . XML** é criado. (atributo opcional)  
  
    A criação de relatório tem duas subcategorias adicionais:  
  
    -   `report-errors`(= "true/false", com padrão como "false" (atributos opcionais))  
  
    -   `verbose`(= "true/false", com padrão como "false" (atributos opcionais))  
  
**Exemplo de sintaxe:**  
  
```xml  
<generate-assessment-report  
  
   object-name="<object-name>"  
  
   object-type="<object-category>"  
  
   write-summary-report-to="<file>"   (optional)  
  
   verbose="<true/false>"   (optional)  
  
   report-errors="<true/false>"   (optional)  
  
   assessment-report-folder="<folder-name>"   (optional)  
  
   conversion-report-overwrite="<true/false>"   (optional)  
  
/>  
```  
ou o  
  
```xml  
<generate-assessment-report  
  
   conversion-report-folder="<folder-name>"   (optional)  
  
   conversion-report-overwrite="<true/false>"   (optional)  
  
>  
  
      <metabase-object object-name="<object-name>"  
  
         object-type="<object-category>"/>  
  
</generate-assessment-report>  
```  
  
## <a name="migration-script-file-commands"></a>Comandos de arquivo de script de migração  
Os comandos de migração convertem o esquema de banco de dados de destino para o esquema de origem e migram os dados para o servidor de destino. A configuração de saída do console padrão para os comandos de migração é ' completo ' relatório de saída sem relatórios de erros detalhados: apenas Resumo no nó raiz da árvore do objeto de origem.  
  
**Comando**  
  
converter esquema  
  
-   Executa a conversão de esquema da origem para o esquema de destino.  
  
-   Se a conexão de banco de dados de origem ou de destino não for executada antes da execução desse comando ou se a conexão com o servidor de banco de dados de origem ou destino falhar durante a execução do comando, um erro será gerado e o aplicativo de console será encerrado.  
  
**Script**  
  
-   `conversion-report-folder:`Especifica a pasta onde o relatório de avaliação pode ser armazenado. (atributo opcional)  
  
-   `object-name:`Especifica os objetos de origem considerados para converter o esquema (ele pode ter nomes de objeto individuais ou um nome de objeto de grupo).  
  
-   `object-type:`Especifica o tipo do objeto especificado no atributo Object-Name (se a categoria de objeto for especificada, o tipo de objeto será "category").  
  
-   `conversion-report-overwrite:`Especifica se a pasta do relatório de avaliação deve ser substituída, caso ela já exista.  
  
    **Valor padrão:** false. (atributo opcional)  
  
-   `write-summary-report-to:`Especifica o caminho onde o relatório de resumo será gerado.  
  
    Se apenas o caminho da pasta for mencionado, clique em arquivo por nome **SchemaConversionReport &lt; n &gt; . XML** é criado. (atributo opcional)  
  
    A criação de relatório tem duas subcategorias adicionais:  
  
    -   `report-errors`(= "true/false", com padrão como "false" (atributos opcionais))  
  
    -   `verbose`(= "true/false", com padrão como "false" (atributos opcionais))  
  
**Exemplo de sintaxe:**  
  
```xml  
<convert-schema  
  
   object-name="<object-name>"  
  
   object-type="<object-category>"  
  
   write-summary-report-to="<file-name/folder-name>"   (optional)  
  
   verbose="<true/false>"   (optional)  
  
   report-errors="<true/false>"   (optional)  
  
   conversion-report-folder="<folder-name>"   (optional)  
  
   conversion-report-overwrite="<true/false>"   (optional)  
  
/>  
```  
ou o  
  
```xml  
<convert-schema  
  
   conversion-report-folder="<folder-name>"   (optional)  
  
   conversion-report-overwrite="<true/false>"   (optional)  
  
      <metabase-object object-name="<object-name>"  
  
         object-type="<object-category>"/>  
  
</convert-schema>  
```  
**Comando**  
  
migrar-Data: migra os dados de origem para o destino.  
  
**Script**  
  
-   `conversion-report-folder:`Especifica a pasta onde o relatório de avaliação pode ser armazenado. (atributo opcional)  
  
-   `object-name:`Especifica os objetos de origem considerados para a migração de dados (ele pode ter nomes de objeto individuais ou um nome de objeto de grupo).  
  
-   `object-type:`Especifica o tipo do objeto especificado no atributo Object-Name (se a categoria de objeto for especificada, o tipo de objeto será "category").  
  
-   `conversion-report-overwrite:`Especifica se a pasta do relatório de avaliação deve ser substituída, caso ela já exista.  
  
    **Valor padrão:** false. (atributo opcional)  
  
-   `write-summary-report-to:`Especifica o caminho onde o relatório de resumo será gerado.  
  
    Se apenas o caminho da pasta for mencionado, clique em arquivo por nome **DataMigrationReport &lt; n &gt; . XML** é criado. (atributo opcional)  
  
    A criação de relatório tem duas subcategorias adicionais:  
  
    -   `report-errors`(= "true/false", com padrão como "false" (atributos opcionais))  
  
    -   `verbose`(= "true/false", com padrão como "false" (atributos opcionais))  
  
**Exemplo de sintaxe:**  
  
```xml  
<migrate-data  
  
   write-summary-report-to="<file-name/folder-name>"  
  
   report-errors="<true/false>"  
  
   verbose="<true/false>">  
  
      <metabase-object object-name="<object-name>"/>  
  
      <metabase-object object-name="<object-name>"/>  
  
      <metabase-object object-name="<object-name>"/>  
  
      <data-migration-connection  
  
         source-use-last-used="true"/source-server="<server-unique-name>"  
  
         target-use-last-used="true"/target-server="<server-unique-name>"/>  
  
</migrate-data>  
```  
ou o  
  
```xml  
<migrate-data  
  
   object-name="<object-name>"  
  
   object-type="<object-category>"  
  
   write-summary-report-to="<file-name/folder-name>"  
  
   report-errors="<true/false>"  
  
   verbose="<true/false>"/>  
```  
  
## <a name="migration-preparation-script-file-commands"></a>Comandos de arquivo de script de preparação de migração  
O comando de preparação de migração inicia o mapeamento de esquema entre os bancos de dados de origem e de destino.  
  
**Comando**  
  
mapa-esquema  
  
Mapeamento de esquema do banco de dados de origem para o esquema de destino.  
  
**Script**  
  
-   `source-schema`Especifica o esquema de origem que pretendemos migrar.  
  
-   `sql-server-schema`Especifica o esquema de destino onde queremos que ele seja migrado.  
  
**Exemplo de sintaxe:**  
  
```xml  
<map-schema  
  
   source-schema="<source-schema>"  
  
   sql-server-schema="<target-schema>"/>  
```  
**Comando**  
  
mapa-esquema  
  
Mapeamento de esquema do banco de dados de origem para o esquema de destino.  
  
**Script**  
  
`source-schema`Especifica o esquema de origem que pretendemos migrar.  
  
`sql-server-schema`Especifica o esquema de destino onde queremos que ele seja migrado.  
  
**Exemplo de sintaxe:**  
  
```xml  
<map-schema  
  
   source-schema="<source-schema>"  
  
   sql-server-schema="<target-schema>"/>  
```  
  
## <a name="manageability-script-file-commands"></a>Comandos de arquivo de script de capacidade de gerenciamento  
Os comandos de gerenciamento ajudam a sincronizar os objetos de banco de dados de destino com o banco de dados de origem.  
  
A configuração de saída do console padrão para os comandos de migração é ' completo ' relatório de saída sem relatórios de erros detalhados: apenas Resumo no nó raiz da árvore do objeto de origem.  
  
**Comando**  
  
sincronizar destino  
  
-   Sincroniza os objetos de destino com o banco de dados de destino.  
  
-   Se esse comando for executado no banco de dados de origem, um erro será encontrado.  
  
-   Se a conexão do banco de dados de destino não for executada antes da execução desse comando ou se a conexão com o servidor de banco de dados de destino falhar durante a execução do comando, um erro será gerado e o aplicativo de console será encerrado.  
  
**Script**  
  
-   `object-name:`Especifica os objetos de destino considerados para sincronização com o banco de dados de destino (ele pode ter nomes de objeto individuais ou um nome de objeto de grupo).  
  
-   `object-type:`Especifica o tipo do objeto especificado no atributo Object-Name (se a categoria de objeto for especificada, o tipo de objeto será "category").  
  
-   `on-error:`Especifica se os erros de sincronização devem ser especificados como avisos ou erro. Opções disponíveis para o no-erro:  
  
    -   relatório-total-como-aviso  
  
    -   relatório-cada-como-aviso  
  
    -   script de falha  
  
-   `report-errors-to:`Especifica o local do relatório de erros para a operação de sincronização (atributo opcional) se apenas o caminho da pasta for fornecido, o arquivo por nome **TargetSynchronizationReport.XML** será criado.  
  
**Exemplo de sintaxe:**  
  
```xml  
<synchronize-target  
  
   object-name="<object-name>"  
  
   on-error="<report-total-as-warning/  
  
               report-each-as-warning/  
  
               fail-script>"   (optional)  
  
   report-errors-to="<file-name/folder-name>"   (optional)  
  
/>  
```  
ou o  
  
```xml  
<synchronize-target  
  
   object-name="<object-name>"  
  
   object-type="<object-category>"/>  
```  
ou o  
  
```xml  
<synchronize-target>  
  
   <metabase-object object-name="<object-name>"/>  
  
   <metabase-object object-name="<object-name>"/>  
  
   <metabase-object object-name="<object-name>"/>  
  
</synchronize-target>  
```  
**Comando**  
  
atualizar-do-banco de dados  
  
-   Atualiza os objetos de origem do banco de dados.  
  
-   Se esse comando for executado no banco de dados de destino, um erro será gerado.  
  
**Script**  
  
Requer um ou vários nós da metabase como parâmetro de linha de comando.  
  
-   `object-name:`Especifica os objetos de origem considerados para atualização do banco de dados de origem (ele pode ter nomes de objeto individuais ou um nome de objeto de grupo).  
  
-   `object-type:`Especifica o tipo do objeto especificado no atributo Object-Name (se a categoria de objeto for especificada, o tipo de objeto será "category").  
  
-   `on-error:`Especifica se é para especificar erros de atualização como avisos ou erro. Opções disponíveis para o no-erro:  
  
    -   relatório-total-como-aviso  
  
    -   relatório-cada-como-aviso  
  
    -   script de falha  
  
-   `report-errors-to:`Especifica o local do relatório de erros para a operação de atualização (atributo opcional) se apenas o caminho da pasta for fornecido, o arquivo por nome **SourceDBRefreshReport.XML** será criado.  
  
**Exemplo de sintaxe:**  
  
```xml  
<refresh-from-database  
  
   object-name="<object-name>"  
  
   on-error="<report-total-as-warning/  
  
               report-each-as-warning/  
  
               fail-script>"   (optional)  
  
   report-errors-to="<file-name/folder-name>"   (optional)  
  
/>  
```  
ou o  
  
```xml  
<refresh-from-database  
  
   object-name="<object-name>"  
  
   object-type="<object-category>"/>  
```  
ou o  
  
```xml  
<refresh-from-database>  
  
   <metabase-object object-name="<object-name>"/>  
  
</refresh-from-database>  
```  
  
## <a name="script-generation-script-file-commands"></a>Comandos de arquivo de script de geração de script  
Os comandos de geração de script executam tarefas duplas: elas ajudam a salvar a saída do console em um arquivo de script; e registre a saída T-SQL no console ou em um arquivo com base no parâmetro especificado.  
  
**Comando**  
  
salvar como script  
  
Usado para salvar os scripts dos objetos em um arquivo mencionado quando metabase = Target, essa é uma alternativa ao comando de sincronização no qual obtemos os scripts e executamos o mesmo no banco de dados de destino.  
  
**Script**  
  
Requer um ou vários nós da metabase como parâmetro de linha de comando.  
  
-   `object-name:`Especifica os objetos cujos scripts devem ser salvos. (Ele pode ter nomes de objetos individuais ou um nome de objeto de grupo)  
  
-   `object-type:`Especifica o tipo do objeto especificado no atributo Object-Name (se a categoria de objeto for especificada, o tipo de objeto será "category").  
  
-   `metabase:`Especifica se é a metabase de origem ou de destino.  
  
-   `destination:`Especifica o caminho ou a pasta em que o script deve ser salvo, se o nome do arquivo não for fornecido, em seguida, um nome de arquivo no formato (object_name valor do atributo). out  
  
-   `overwrite:`Se for true, ele substituirá se o mesmo nome de arquivo existir. Ele pode ter os valores (true/false).  
  
**Exemplo de sintaxe:**  
  
```xml  
<save-as-script  
  
   metabase="<source/target>"  
  
   object-name="<object-name>"  
  
   object-type="<object-category>"  
  
   destination="<file/folder>"  
  
   overwrite="<true/false>"   (optional)  
  
/>  
```  
ou o  
  
```xml  
<save-as-script  
  
   metabase="<source/target>"  
  
   destination="<file/folder>"  
  
      <metabase-object object-name="<object-name>"  
  
         object-type="<object-category>"/>  
  
</save-as-script>  
```  
**Comando**  
  
instrução Convert-SQL-  
  
-   `context`Especifica o nome do esquema.  
  
-   `destination`Especifica se a saída deve ser armazenada em um arquivo.  
  
    Se esse atributo não for especificado, a instrução T-SQL convertida será exibida no console do. (atributo opcional)  
  
-   `conversion-report-folder`Especifica a pasta onde o relatório de avaliação pode ser armazenado. (atributo opcional)  
  
-   `conversion-report-overwrite`Especifica se a pasta do relatório de avaliação deve ser substituída, caso ela já exista.  
  
    **Valor padrão:** false. (atributo opcional)  
  
-   `write-converted-sql-to`Especifica o arquivo (ou) caminho da pasta em que o T-SQL convertido será armazenado. Quando um caminho de pasta é especificado junto com o `sql-files` atributo, cada arquivo de origem terá um arquivo T-SQL de destino correspondente criado na pasta especificada. Quando um caminho de pasta é especificado junto com o `sql` atributo, o T-SQL convertido é gravado em um arquivo chamado **Result. out** na pasta especificada.  
  
-   `sql`Especifica as instruções SQL do DB2 a serem convertidas, uma ou mais instruções podem ser separadas usando um ";"  
  
-   `sql-files`Especifica o caminho dos arquivos SQL que deve ser convertido em código T-SQL.  
  
-   `write-summary-report-to`Especifica o caminho onde o relatório será gerado. Se apenas o caminho da pasta for mencionado, o arquivo por nome **ConvertSQLReport.XML** será criado. (atributo opcional)  
  
    A criação de relatório tem duas subcategorias adicionais, aula sobre visualização..,:  
  
    -   relatório-erros (= "true/false", com padrão como "false" (atributos opcionais)).  
  
    -   Verbose (= "true/false", com padrão como "false" (atributos opcionais)).  
  
**Script**  
  
Requer um ou vários nós da metabase como parâmetro de linha de comando.  
  
**Exemplo de sintaxe:**  
  
```  
<convert-sql-statement  
  
   context="<schema-name>"  
  
   conversion-report-folder="<folder-name>"  
  
   conversion-report-overwrite="<true/false>"  
  
   write-summary-report-to="<file-name/folder-name>"   (optional)  
  
   verbose="<true/false>"   (optional)  
  
   report-errors="<true/false>"   (optional)  
  
   destination="<stdout/file>"   (optional)  
  
   file-name="<file-name>"  
  
   sql="SELECT 1 FROM DUAL;">  
  
   <output-window suppress-messages="<true/false>" />  
  
</convert-sql-statement>  
```  
ou o  
  
```  
<convert-sql-statement  
  
   context="<schema-name>"  
  
   conversion-report-folder="<folder-name>"  
  
   conversion-report-overwrite="<true/false>"  
  
   write-summary-report-to="<file-name/folder-name>" (optional)  
  
   verbose="<true/false>" (optional)  
  
   report-errors="<true/false>"  
  
   destination="<stdout/file>"   (optional)  
  
   write-converted-sql-to="<file-name/folder-name>"  
  
   sql-files="<folder-name>\*.sql" />  
```  
ou o  
  
```  
<convert-sql-statement  
  
   context="<schema-name>"  
  
   conversion-report-folder="<folder-name>"  
  
   conversion-report-overwrite="<true/false>"  
  
   sql-files="<folder-name>\*.sql" />  
```  
  
## <a name="next-step"></a>Próxima etapa  
Para obter informações sobre opções de linha de comando, consulte [Opções de linha de comando no console do SSMA &#40;DB2ToSQL&#41;](../../ssma/db2/command-line-options-in-ssma-console-db2tosql.md) .  
  
Para obter informações sobre arquivos de script de console de exemplo, consulte [trabalhando com os arquivos de script de console de exemplo &#40;DB2ToSQL&#41;](../../ssma/db2/working-with-the-sample-console-script-files-db2tosql.md)  
  
A próxima etapa depende dos requisitos do seu projeto:  
  
-   Para especificar uma senha ou exportar/importar senhas, consulte [Gerenciando senhas &#40;DB2ToSQL&#41;](../../ssma/db2/managing-passwords-db2tosql.md).  
  
-   Para gerar relatórios, consulte [gerando relatórios &#40;DB2ToSQL&#41;](../../ssma/db2/generating-reports-db2tosql.md).  
  
-   Para solucionar problemas no console do, consulte solução de problemas [&#40;DB2ToSQL&#41;](../../ssma/db2/troubleshooting-db2tosql.md).  
  
