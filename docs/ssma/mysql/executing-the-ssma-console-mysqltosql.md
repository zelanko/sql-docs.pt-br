---
description: Executar o console do SSMA (MySQLToSQL)
title: Executando o console do SSMA (MySQLToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Script file commands, Database connection commands
- Script file commands, Manageability commands
- Script file commands, Migration commands
- Script file commands, Migration preparation commands
- Script file commands, project commands
- Script file commands, Report commands
- Script file commands, Script generation commands
ms.assetid: e3e9f7e4-0619-4861-a202-3d5d39953b26
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 59a0075dfcee23c5e005853b0befd4b3eb0f39c8
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88463447"
---
# <a name="executing-the-ssma-console-mysqltosql"></a>Executar o console do SSMA (MySQLToSQL)
A Microsoft fornece um conjunto robusto de comandos de arquivo de script para executar e controlar atividades do SSMA.  
  
O aplicativo de console usa determinados comandos de arquivo de script padrão, conforme enumerado nesta seção.  
  
## <a name="project--script-file-commands"></a>Comandos de arquivo de script do projeto  
**Comando**  
  
criar novo projeto:   
                   Cria um novo projeto do SSMA.  
  
Os comandos de projeto lidam com a criação de projetos, abertura, salvamento e saída de projetos.  
  
**Script**  
  
1.  `project-folder` indica a pasta do projeto que está sendo criado.  
  
2.  `project-name` indica o nome do projeto. {string}  
  
3.  `overwrite-if-exists`Atributo opcional indica se um projeto existente deve ser substituído. Boolean  
  
4.  `project-type:`Atributo opcional. Indica o tipo de projeto, por exemplo, "SQL-Server-2005" Project ou "SQL-Server-2008" Project ou o projeto "SQL-Server-2012" ou "SQL-Server-2014" ou "SQL-Azure". O padrão é "SQL-Server-2008".  
  
**Exemplo de sintaxe:**  
  
```xml  
<create-new-project  
  
   project-folder="<project-folder>"  
  
   project-name="<project-name>"  
  
   overwrite-if-exists="<true/false>"   (optional)  
  
   project-type=="<sql-server-2008 | sql-server-2005 | sql-server-2012 | sql-server-2014 | sql-azure>"   (optional)  
  
/>  
```  
O atributo ' overwrite-if-exists ' é **false** por padrão.  
  
O atributo ' Project-Type ' é **SQL-Server-2008** por padrão.  
  
**Comando**  
  
projeto aberto:   
                  Abre um projeto existente.  
  
**Script**  
  
1.  `project-folder` indica a pasta do projeto que está sendo criado. O comando falhará se a pasta especificada não existir.  {string}  
  
2.  `project-name` indica o nome do projeto. O comando falhará se o projeto especificado não existir.  {string}  
  
**Exemplo de sintaxe:**  
  
```xml  
<open-project  
  
   project-folder="<project-folder>"  
  
   project-name="<project-name>"  
  
/>  
```  
> [!IMPORTANT]  
> O aplicativo do console do SSMA para MySQL dá suporte à compatibilidade com versões anteriores. Você poderá abrir projetos criados pela versão anterior do SSMA.  
  
**Comando**  
  
Save-Project: salva o projeto de migração.  
  
**Script**  
  
**Exemplo de sintaxe:**  
  
```xml  
<save-project/>  
```  
**Comando**  
  
fechar projeto  
                  : Fecha o projeto de migração.  
  
**Script**  
  
**Exemplo de sintaxe:**  
  
```xml  
<save-project/>  
```  
**Comando**  
  
fechar projeto  
                  : Fecha o projeto de migração.  
  
**Script**  
  
**Exemplo de sintaxe:**  
  
```xml  
<close-project  
  
   if-modified="<save/error/ignore>"   (optional)  
  
/>  
```  
O atributo ' If-Modified ' é opcional, **ignore** por padrão.  
  
## <a name="database-connection-script-file-commands"></a>Comandos de arquivo de script de conexão de banco de dados  
Os comandos de conexão do banco de dados ajudam a conectar-se ao banco de dados.  
  
1.  Não há suporte para o recurso **procurar** da interface do usuário no console do.  
  
2.  Os parâmetros de autenticação e **porta** do **Windows** não são aplicáveis ao se conectar a SQL Azure.  
  
3.  Para obter mais informações sobre como criar arquivos de script, consulte [criando arquivos de script &#40;MySQLToSQL&#41;](../../ssma/mysql/creating-script-files-mysqltosql.md).  
  
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
<force-load metabase="<source/target>"  
  
      <metabase-object object-name="<object-name>"/>  
  
</force-load>  
```  
**Comando**  
  
reconectar-fonte-banco de dados  
  
1.  Reconecta-se ao banco de dados de origem, mas não carrega nenhum metadado diferente do comando Connect-Source-Database.  
  
2.  Se a conexão (re) com a origem não puder ser estabelecida, um erro será gerado e o aplicativo de console parará outra execução.  
  
**Script**  
  
**Exemplo de sintaxe:**  
  
```xml  
<reconnect-source-database  server="<server-unique-name>"/>  
```  
**Comando**  
  
Connect-Target-Database  
  
1.  Conecta-se ao SQL Server de destino ou ao banco de dados SQL do Azure e carrega metadados de alto nível do banco de dados de destino, mas não os metadados inteiramente.  
  
2.  Se a conexão com o destino não puder ser estabelecida, um erro será gerado e o aplicativo de console parará outra execução.  
  
**Script**  
  
A definição do servidor é recuperada do atributo Name definido para cada conexão na seção do servidor do arquivo de conexão do servidor ou do arquivo de script  
  
**Exemplo de sintaxe:**  
  
```xml  
<connect-target-database  server="<server-unique-name>"/>  
```  
**Comando**  
  
reconectar-destino-banco de dados  
  
1.  Reconecta-se ao banco de dados de destino, mas não carrega nenhum metadado, diferente do comando Connect-Target-Database.  
  
2.  Se a conexão (re) com o destino não puder ser estabelecida, um erro será gerado e o aplicativo de console interromperá a execução.  
  
**Script**  
  
**Exemplo de sintaxe:**  
  
```xml  
<reconnect-target-database  server="<server-unique-name>"/>  
```  
  
## <a name="report-script-file-commands"></a>Comandos de arquivo de script de relatório  
Os comandos de relatório geram relatórios sobre o desempenho de várias atividades do console do SSMA.  
  
**Comando**  
  
gerar-avaliação-relatório  
  
1.  Gera relatórios de avaliação no banco de dados de origem.  
  
2.  Se a conexão do banco de dados de origem não for executada antes da execução desse comando, um erro será gerado e o aplicativo de console será encerrado.  
  
3.  Falha ao conectar-se ao servidor de banco de dados de origem durante a execução do comando, também resulta na finalização do aplicativo de console.  
  
**Script**  
  
1.  `assessment-report-folder:` Especifica a pasta onde o relatório de avaliação está armazenado. (atributo opcional)  
  
2.  `object-name:` Especifica os objetos considerados para geração de relatórios de avaliação (ele pode ter nomes de objetos individuais ou um nome de objeto de grupo).  
  
3.  `object-type:` Especifica o tipo do objeto especificado no atributo Object-Name (se a categoria de objeto for especificada, o tipo de objeto será "category").  
  
4.  `assessment-report-overwrite:` Especifica se a pasta do relatório de avaliação deve ser substituída, caso ela já exista.  
  
    **Valor padrão:** false. (atributo opcional)  
  
5.  `write-summary-report-to:` Especifica o caminho onde o relatório de resumo será gerado.  
  
    Se apenas o caminho da pasta for mencionado, clique em arquivo por nome **AssessmentReport &lt; n &gt; . XML** é criado. (atributo opcional)  
  
    A criação de relatório tem duas subcategorias adicionais:  
  
    -   `report-errors` (= "true/false", com padrão como "false" (atributos opcionais))  
  
    -   `verbose` (= "true/false", com padrão como "false" (atributos opcionais))  
  
**Exemplo de sintaxe:**  
  
```xml  
<generate-assessment-report  
  
   object-name="<object-name>"  
  
   object-type="<object-category>"  
  
   write-summary-report-to="<file-name/folder-name>"   (optional)  
  
   verbose="<true/false>"   (optional)  
  
   report-errors="<true/false>"   (optional)  
  
   conversion-report-folder="<folder-name>"   (optional)  
  
   conversion-report-overwrite="<true/false>"   (optional)  
  
/>  
```  
ou  
  
```xml  
<generate-assessment-report  
  
   conversion-report-folder="<folder-name>"   (optional)  
  
   conversion-report-overwrite="<true/false>"   (optional)  
  
>  
  
      <metabase-object object-name="<object-name>"  
  
         object-type="<object-category>"/>  
  
</generate-assessment-report>  
```  
  
## <a name="migration--script-file-commands"></a>Comandos de arquivo de script de migração  
Os comandos de migração convertem o esquema de banco de dados de destino para o esquema de origem e migram os dados para o servidor de destino.  
  
A configuração de saída do console padrão para os comandos de migração é ' completo ' relatório de saída sem relatórios de erros detalhados: apenas Resumo no nó raiz da árvore do objeto de origem.  
  
**Comando**  
  
converter esquema  
  
1.  Executa a conversão de esquema da origem para o esquema de destino.  
  
2.  Se a conexão de banco de dados de origem ou de destino não for executada antes da execução desse comando ou se a conexão com o servidor de banco de dados de origem ou destino falhar durante a execução do comando, um erro será gerado e o aplicativo de console será encerrado.  
  
**Script**  
  
1.  `conversion-report-folder:` Especifica a pasta onde o relatório de avaliação está armazenado. (atributo opcional)  
  
2.  `object-name:` Especifica os objetos considerados para converter o esquema (ele pode ter nomes de objetos individuais ou um nome de objeto de grupo).  
  
3.  `object-type:` Especifica o tipo do objeto especificado no atributo Object-Name (se a categoria de objeto for especificada, o tipo de objeto será "category").  
  
4.  `conversion-report-overwrite:` Especifica se a pasta do relatório de avaliação deve ser substituída, caso ela já exista.  
  
    **Valor padrão:** false. (atributo opcional)  
  
5.  `write-summary-report-to:` Especifica o caminho onde o relatório de resumo será gerado.  
  
    Se apenas o caminho da pasta for mencionado, clique em arquivo por nome **SchemaConversionReport &lt; n &gt; . XML** é criado. (atributo opcional)  
  
    A criação do relatório de resumo tem duas subcategorias adicionais:  
  
    -   `report-errors` (= "true/false", com padrão como "false" (atributos opcionais))  
  
    -   `verbose` (= "true/false", com padrão como "false" (atributos opcionais))  
  
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
ou  
  
```xml  
<convert-schema  
  
   conversion-report-folder="<folder-name>"   (optional)  
  
   conversion-report-overwrite="<true/false>"   (optional)  
  
      <metabase-object object-name="<object-names>"  
  
         object-type="<object-category>"/>  
  
</convert-schema>  
```  
**Comando**  
  
migrar-dados  
  
1.  Migra os dados de origem para o destino.  
  
**Script**  
  
1.  `object-name:` Especifica os objetos de origem considerados para a migração de dados (ele pode ter nomes de objetos individuais ou um nome de objeto de grupo).  
  
2.  `object-type:` Especifica o tipo do objeto especificado no atributo Object-Name (se a categoria de objeto for especificada, o tipo de objeto será "category").  
  
3.  `write-summary-report-to:` Especifica o caminho onde o relatório de resumo será gerado.  
  
    Se apenas o caminho da pasta for mencionado, clique em arquivo por nome **DataMigrationReport &lt; n &gt; . XML** é criado. (atributo opcional)  
  
    A criação de relatório tem duas subcategorias adicionais:  
  
    -   `report-errors` (= "true/false", com padrão como "false" (atributos opcionais))  
  
    -   `verbose` (= "true/false", com padrão como "false" (atributos opcionais))  
  
**Exemplo de sintaxe:**  
  
```xml  
<migrate-data  
  
   write-summary-report-to="<file-name/folder-name>"  
  
   report-errors="true" verbose="true">  
  
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
  
   report-errors="true" verbose="true"/>  
```  
  
## <a name="migration-preparation-script-file-command"></a>Comando de arquivo de script de preparação de migração  
O comando de preparação de migração inicia o mapeamento de esquema entre os bancos de dados de origem e de destino.  
  
**Comando**  
  
mapa-esquema  
  
Mapeamento de esquema do banco de dados de origem para o esquema de destino.  
  
**Script**  
  
1.  `source-schema` Especifica o esquema de origem que pretendemos migrar.  
  
2.  `sql-server-schema` Especifica o esquema de destino onde queremos que ele seja migrado.  
  
**Exemplo de sintaxe:**  
  
```xml  
<map-schema  
  
   source-schema="<source-schema>"  
  
   sql-server-schema="<target-schema>"/>  
```  
  
## <a name="manageability-script-file-commands"></a>Comandos de arquivo de script de capacidade de gerenciamento  
Os comandos de gerenciamento ajudam a sincronizar os objetos de banco de dados de destino com o banco de dados de origem.  
  
> [!NOTE]  
> A configuração de saída do console padrão para os comandos de migração é ' completo ' relatório de saída sem relatórios de erros detalhados: apenas Resumo no nó raiz da árvore do objeto de origem.  
  
**Comando**  
  
sincronizar destino  
  
1.  Sincroniza os objetos de destino com o banco de dados de destino.  
  
2.  Se esse comando for executado no banco de dados de origem, um erro será encontrado.  
  
3.  Se a conexão do banco de dados de destino não for executada antes da execução desse comando ou se a conexão com o servidor de banco de dados de destino falhar durante a execução do comando, um erro será gerado e o aplicativo de console será encerrado.  
  
**Script**  
  
1.  `object-name:` Especifica os objetos considerados para sincronização com o banco de dados de destino (ele pode ter nomes de objetos individuais ou um nome de objeto de grupo).  
  
2.  `object-type:` Especifica o tipo do objeto especificado no atributo Object-Name (se a categoria de objeto for especificada, o tipo de objeto será "category").  
  
3.  `on-error:` Especifica se os erros de sincronização devem ser especificados como avisos ou erro. Opções disponíveis para o no-erro:  
  
    -   relatório-total-como-aviso  
  
    -   relatório-cada-como-aviso  
  
    -   script de falha  
  
4.  `report-errors-to:` Especifica o local do relatório de erros para a operação de sincronização (atributo opcional) se apenas o caminho da pasta for fornecido, o arquivo por nome **TargetSynchronizationReport.XML** será criado.  
  
**Exemplo de sintaxe:**  
  
```xml  
<synchronize-target  
  
   object-name="<object-name>"  
  
   on-error="<report-total-as-warning/  
  
               report-each-as-warning/  
  
               fail-script>"   (optional)  
  
   report-errors-to="<file-name>"   (optional)  
  
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
**Comando**  
  
atualizar-do-banco de dados  
  
1.  Atualiza os objetos de origem do banco de dados.  
  
2.  Se esse comando for executado no banco de dados de destino, um erro será gerado.  
  
**Script**  
  
1.  `object-name:` Especifica os objetos de origem considerados para atualização do banco de dados de origem (ele pode ter nomes de objetos individuais ou um nome de objeto de grupo).  
  
2.  `object-type:` Especifica o tipo do objeto especificado no atributo Object-Name (se a categoria de objeto for especificada, o tipo de objeto será "category").  
  
3.  `on-error:` Especifica se os erros de sincronização devem ser especificados como avisos ou erro. Opções disponíveis para o no-erro:  
  
    -   relatório-total-como-aviso  
  
    -   relatório-cada-como-aviso  
  
    -   script de falha  
  
4.  `report-errors-to:` Especifica o local do relatório de erros para a operação de sincronização (atributo opcional) se apenas o caminho da pasta for fornecido, o arquivo por nome **SourceDBRefreshReport.XML** será criado.  
  
Requer um ou vários nós da metabase como parâmetro de linha de comando.  
  
**Exemplo de sintaxe:**  
  
```xml  
<refresh-from-database  
  
   object-name="<object-name>"  
  
   on-error="<report-total-as-warning/  
  
               report-each-as-warning/  
  
               fail-script>"   (optional)  
  
   report-errors-to="<file-name>"   (optional)  
  
/>  
```  
ou  
  
```xml  
<refresh-from-database  
  
   object-name="<object-name>"  
  
   object-type="<object-category>"/>  
```  
ou  
  
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
  
1.  `object-name:` Especifica os objetos cujos scripts devem ser salvos. (Ele pode ter nomes de objetos individuais ou um nome de objeto de grupo)  
  
2.  `object-type:` Especifica o tipo do objeto especificado no atributo Object-Name (se a categoria de objeto for especificada, o tipo de objeto será "category").  
  
3.  `metabase:` Especifica se é a metabase de origem ou de destino.  
  
4.  `destination:` Especifica o caminho ou a pasta em que o script deve ser salvo, se o nome do arquivo não for fornecido, em seguida, um nome de arquivo no formato (object_name valor do atributo). out  
  
5.  `overwrite:` Se for true, ele substituirá se o mesmo nome de arquivo existir. Ele pode ter os valores (true/false).  
  
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
**Comando**  
  
instrução Convert-SQL-  
  
1.  `context` Especifica o nome do esquema.  
  
2.  `destination` Especifica se a saída deve ser armazenada em um arquivo.  
  
    Se esse atributo não for especificado, a instrução T-SQL convertida será exibida no console do. (atributo opcional)  
  
3.  `conversion-report-folder` Especifica a pasta onde o relatório de avaliação está armazenado. (atributo opcional)  
  
4.  `conversion-report-overwrite` Especifica se a pasta do relatório de avaliação deve ser substituída, caso ela já exista.  
  
    **Valor padrão:** false. (atributo opcional)  
  
5.  `write-converted-sql-to` Especifica o arquivo (ou) caminho da pasta em que o T-SQL convertido será armazenado. Quando um caminho de pasta é especificado junto com o `sql-files` atributo, cada arquivo de origem terá um arquivo T-SQL de destino correspondente criado na pasta especificada. Quando um caminho de pasta é especificado junto com o `sql` atributo, o T-SQL convertido é gravado em um arquivo chamado Result. out na pasta especificada.  
  
6.  `sql` Especifica as instruções SQL do MySQL a serem convertidas, uma ou mais instruções podem ser separadas usando um ";"  
  
7.  `sql-files` Especifica o caminho dos arquivos SQL que deve ser convertido em código T-SQL.  
  
8.  `write-summary-report-to` Especifica o caminho onde o relatório de resumo será gerado. Se apenas o caminho da pasta for mencionado, o arquivo por nome **ConvertSQLReport.XML** será criado. (atributo opcional)  
  
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
  
   destination="stdout/file"   (optional)  
  
   write-converted-sql-to="<file-name/folder-name>"  
  
   sql="SELECT 1 FROM DUAL;">  
  
      <output-window suppress-messages="<true/false>" />  
  
</convert-sql-statement>  
```  
ou  
  
```  
<convert-sql-statement  
  
   context="<schema-name>"  
  
   conversion-report-folder="<folder-name>"  
  
   conversion-report-overwrite="<true/false>"  
  
   write-summary-report-to="<file-name/folder-name>"   (optional)  
  
   verbose="<true/false>"   (optional)  
  
   report-errors="<true/false>"   (optional)  
  
   destination="<stdout/file>"   (optional)  
  
   write-converted-sql-to="<file-name/folder-name>"  
  
   sql-files="<folder-name>\*.sql"  
  
/>  
```  
ou  
  
```  
<convert-sql-statement  
  
   context="<schema-name>"  
  
   conversion-report-folder="<folder-name>"  
  
   conversion-report-overwrite="<true/false>"  
  
   sql-files="<folder-name>\*.sql"  
  
/>  
```  
  
## <a name="next-step"></a>Próxima etapa  
Para obter informações sobre opções de linha de comando, consulte [Opções de linha de comando no console do SSMA &#40;MySQLToSQL&#41;](../../ssma/mysql/command-line-options-in-ssma-console-mysqltosql.md) .  
  
Para obter mais informações sobre arquivos de script de console de exemplo, consulte [trabalhando com os arquivos de script de console de exemplo &#40;MySQLToSQL&#41;](../../ssma/mysql/working-with-the-sample-console-script-files-mysqltosql.md)  
  
A próxima etapa depende dos requisitos do seu projeto:  
  
1.  Para especificar uma senha ou exportar/importar senhas, consulte [Gerenciando senhas &#40;MySQLToSQL&#41;](../../ssma/mysql/managing-passwords-mysqltosql.md).  
  
2.  Para gerar relatórios, consulte [gerando relatórios &#40;MySQLToSQL&#41;](../../ssma/mysql/generating-reports-mysqltosql.md).  
  
3.  Para solucionar problemas no console do, consulte solução de problemas [&#40;MySQLToSQL&#41;](../../ssma/mysql/troubleshooting-mysqltosql.md).  
  
