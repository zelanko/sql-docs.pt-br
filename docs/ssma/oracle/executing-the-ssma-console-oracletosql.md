---
title: Executar o Console do SSMA (OracleToSQL) | Microsoft Docs
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- Oracle SSMA Console
- Script File Commands, Script Generation Commands,Manageability Commands
- Script File Commands,Project Commands
ms.assetid: 7228ccba-c69f-4b4c-8664-01a2750183c5
caps.latest.revision: 43
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 685286966599c4dcd3dc2f7029413c77f3ff2689
ms.openlocfilehash: 4ca3c3557b7f57b93dc41b23232754c5df046bdb
ms.contentlocale: pt-br
ms.lasthandoff: 10/20/2017

---
# <a name="executing-the-ssma-console-oracletosql"></a>Executar o Console do SSMA (OracleToSQL)
Microsoft fornece um conjunto robusto de script de comandos do arquivo para executar e controlar as atividades do SSMA. O aplicativo de console usa alguns comandos do arquivo de script padrão como enumerada nesta seção.  
  
## <a name="project-script-file-commands"></a>Comandos do arquivo de Script de projeto  
Os comandos de projeto lidar com a criação de projetos, abrir, salvar e sair de projetos.  
  
**Comando**  
  
Criar novo projeto  
                  : Cria um novo projeto SSMA.  
  
**Script**  
  
-   `project-folder`indica a pasta de projeto obtendo criado.  
  
-   `project-name`indica o nome do projeto. {string}  
  
-   `overwrite-if-exists`Atributo opcional indica se um projeto existente deve ser substituído. {booliano}  
  
-   `project-type:`Atributo opcional. Indica o tipo de projeto ou seja, o projeto "sql-server-2005" ou "sql-server-2008" projeto ou projeto "sql-server-2012" ou "sql-server-2014" projeto ou "sql azure". O padrão é "sql-server-2014".  
  
**Exemplo:**  
  
```xml  
<create-new-project  
  
   project-folder="<project-folder>"  
  
   project-name="<project-name>"  
  
   overwrite-if-exists="<true/false>"   (optional)  
  
   project-type="<sql-server-2008 | sql-server-2005 | sql-server-2012 | sql-server-2014>"   (optional)  
  
/>  
```  
Atributo 'Substituir se-existente' é **false** por padrão.  
  
O atributo 'tipo de projeto' é **sql-server-2008** por padrão.  
  
**Comando**  
  
Abrir projeto: abre um projeto existente.  
  
**Script**  
  
-   `project-folder`indica a pasta de projeto obtendo criado. O comando falhará se a pasta especificada não existe.  {string}  
  
-   `project-name`indica o nome do projeto. O comando falhará se o projeto especificado não existe.  {string}  
  
**Exemplo de sintaxe:**  
  
```xml  
<open-project  
  
   project-folder="<project-folder>"  
  
   project-name="<project-name>"  
  
/>  
```  
SSMA para aplicativo de Console do Oracle oferece suporte a compatibilidade com versões anteriores. Você poderá abrir projetos criados por uma versão anterior do SSMA.  
  
**Comando**  
  
Salvar projeto  
  
Salva o projeto de migração.  
  
**Script**  
  
**Exemplo de sintaxe:**  
  
```xml  
<save-project/>  
```  
**Comando**  
  
projeto de fechamento  
  
Fecha o projeto de migração.  
  
**Script**  
  
**Exemplo de sintaxe:**  
  
```xml  
<close-project  
  
   if-modified="<save/error/ignore>"   (optional)  
  
/>  
```  
  
## <a name="database-connection-script-file-commands"></a>Comandos de arquivo de Script de Conexão de banco de dados  
Os comandos de Conexão de banco de dados ajudam a conectar-se ao banco de dados.  
  
-   O **procurar** recurso da interface do usuário não tem suporte no console.  
  
-   Para obter mais informações sobre 'Criando arquivos de Script', consulte [criando arquivos de Script &#40; OracleToSQL &#41;](../../ssma/oracle/creating-script-files-oracletosql.md).  
  
**Comando**  
  
Conecte-se-origem-banco de dados  
  
-   Executa a conexão à fonte de dados e carrega os metadados de nível alto de banco de dados de origem, mas não todos os metadados.  
  
-   Se a conexão com a fonte não pode ser estabelecida, será gerado um erro e o aplicativo de console adicional para a execução  
  
**Script**  
  
Definição de servidor é recuperada do atributo do nome definido para cada conexão na seção do servidor de arquivo de conexão do servidor ou o arquivo de script.  
  
**Exemplo de sintaxe:**  
  
```xml  
<connect-source-database  server="<server-unique-name>"/>  
```  
**Comando**  
  
Force-carga-origem/destino-banco de dados  
  
-   Carrega os metadados de origem.  
  
-   Útil para trabalhar no projeto de migração offline.  
  
-   Se a conexão para o origem/destino não puder ser estabelecida, será gerado um erro e o aplicativo de console adicional para a execução  
  
**Script**  
  
Exige um ou vários nós de metabase como parâmetro de linha de comando.  
  
**Exemplo de sintaxe:**  
  
```xml  
<force-load object-name="<object-name>"  
  
  metabase="<source/target>"/>  
```  
ou  
  
```xml  
<force-load>  
  
   <metabase-object object-name="<object-name>"/>  
  
</force-load>  
```  
**Comando**  
  
Reconecte-origem-banco de dados  
  
-   Reconecta-se à fonte de dados, mas não carrega todos os metadados ao contrário do comando de conexão de fonte de dados.  
  
-   Se não é possível estabelecer (conexão com a fonte de re), um erro será gerado e o aplicativo de console adicional para a execução.  
  
**Script**  
  
**Exemplo de sintaxe:**  
  
```xml  
<reconnect-source-database  server="<server-unique-name>"/>  
```  
**Comando**  
  
dados conexão de destino  
  
-   Conecta-se para o banco de dados do SQL Server de destino e carrega os metadados de nível alto do banco de dados de destino, mas não os metadados inteiramente.  
  
-   Se a conexão para o destino não puder ser estabelecida, será gerado um erro e o aplicativo de console adicional para a execução.  
  
**Script**  
  
Definição de servidor é recuperada do atributo do nome definido para cada conexão na seção do servidor de arquivo de conexão do servidor ou o arquivo de script  
  
**Exemplo de sintaxe:**  
  
```xml  
<connect-target-database  server="<server-unique-name>"/>  
```  
**Comando**  
  
dados reconectar-se de destino  
  
-   Reconecta-se ao banco de dados de destino, mas não carrega todos os metadados, ao contrário do comando de dados de destino de conexão.  
  
-   Se a (re) conexão para o destino não puder ser estabelecida, será gerado um erro e o aplicativo de console adicional para a execução.  
  
**Script**  
  
**Exemplo de sintaxe:**  
  
```xml  
<reconnect-target-database  server="<server-unique-name>"/>  
```  
  
## <a name="report-script-file--commands"></a>Comandos de Script de arquivo de relatório  
Os comandos de relatório geram relatórios sobre o desempenho de várias atividades do Console SSMA.  
  
**Comando**  
  
relatório gerar de avaliação  
  
-   Gera relatórios de avaliação no banco de dados de origem.  
  
-   Se a conexão de banco de dados de origem não é executada antes de executar esse comando, será gerado um erro e sai do aplicativo de console.  
  
-   Falha ao se conectar ao servidor de banco de dados de origem durante a execução do comando, também resulta em encerrar o aplicativo de console.  
  
**Script**  
  
-   `conversion-report-folder:`Especifica a pasta onde o relatório de avaliação pode ser armazenado. (atributo opcional)  
  
-   `object-name:`Especifica os objetos considerados para geração de relatórios de avaliação (ele pode ter nomes de objeto indivdual ou um nome de objeto de grupo).  
  
-   `object-type:`Especifica o tipo do objeto especificado no atributo nome do objeto (se a categoria de objeto for especificada, o tipo de objeto será 'categoria').  
  
-   `conversion-report-overwrite:`Especifica se deve substituir a pasta de relatórios de avaliação se ele já existe.  
  
    **Valor padrão:** false. (atributo opcional)  
  
-   `write-summary-report-to:`Especifica o caminho onde o relatório de resumo será gerado.  
  
    Se apenas o caminho da pasta for mencionado, do arquivo pelo nome **AssessmentReport&lt;n&gt;. XML** é criado. (atributo opcional)  
  
    Criação de relatório tem duas subcategorias adicionais:  
  
    -   `report-errors`(= "true/false", com padrão como "falso" (atributos opcionais))  
  
    -   `verbose`(= "true/false", com padrão como "falso" (atributos opcionais))  
  
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
  
## <a name="migration-script-file-commands"></a>Comandos de arquivo de Script de migração  
Os comandos de migração converter o esquema de banco de dados de destino para o esquema de origem e migra dados para o servidor de destino.  
  
A saída de console padrão definindo para os comandos de migração é o relatório de saída 'Completa' com nenhum relatório de erro detalhado: resumo apenas no nó de raiz da árvore de objeto de origem.  
  
**Comando**  
  
Converter esquema  
  
-   Executa a conversão de esquema de origem para o esquema de destino.  
  
-   Se a conexão de banco de dados de origem ou de destino não é executada antes de executar este comando ou a conexão para o servidor de banco de dados de origem ou de destino falha durante a execução do comando, será gerado um erro e sai do aplicativo de console.  
  
**Script**  
  
-   `conversion-report-folder:`Especifica a pasta onde o relatório de avaliação pode ser armazenado. (atributo opcional)  
  
-   `object-name:`Especifica os objetos de origem considerados para converter o esquema (ele pode ter nomes de objeto indivdual ou um nome de objeto de grupo).  
  
-   `object-type:`Especifica o tipo do objeto especificado no atributo nome do objeto (se a categoria de objeto for especificada, o tipo de objeto será 'categoria').  
  
-   `conversion-report-overwrite:`Especifica se deve substituir a pasta de relatórios de avaliação se ele já existe.  
  
    **Valor padrão:** false. (atributo opcional)  
  
-   `write-summary-report-to:`Especifica o caminho onde o relatório de resumo será gerado.  
  
    Se apenas o caminho da pasta for mencionado, do arquivo pelo nome **SchemaConversionReport&lt;n&gt;. XML** é criado. (atributo opcional)  
  
    Criação de relatório tem duas subcategorias adicionais:  
  
    -   `report-errors`(= "true/false", com padrão como "falso" (atributos opcionais))  
  
    -   `verbose`(= "true/false", com padrão como "falso" (atributos opcionais))  
  
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
  
      <metabase-object object-name="<object-name>"  
  
         object-type="<object-category>"/>  
  
</convert-schema>  
```  
**Comando**  
  
migrar dados  
  
Migra os dados de origem para o destino.  
  
**Script**  
  
-   `conversion-report-folder:`Especifica a pasta onde o relatório de avaliação pode ser armazenado. (atributo opcional)  
  
-   `object-name:`Especifica os objetos de origem considerados para a migração de dados (ele pode ter nomes de objeto indivdual ou um nome de objeto de grupo).  
  
-   `object-type:`Especifica o tipo do objeto especificado no atributo nome do objeto (se a categoria de objeto for especificada, o tipo de objeto será 'categoria').  
  
-   `conversion-report-overwrite:`Especifica se deve substituir a pasta de relatórios de avaliação se ele já existe.  
  
    **Valor padrão:** false. (atributo opcional)  
  
-   `write-summary-report-to:`Especifica o caminho onde o relatório de resumo será gerado.  
  
    Se apenas o caminho da pasta for mencionado, do arquivo pelo nome **DataMigrationReport&lt;n&gt;. XML** é criado. (atributo opcional)  
  
    Criação de relatório tem duas subcategorias adicionais:  
  
    -   `report-errors`(= "true/false", com padrão como "falso" (atributos opcionais))  
  
    -   `verbose`(= "true/false", com padrão como "falso" (atributos opcionais))  
  
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
ou  
  
```xml  
<migrate-data  
  
   object-name="<object-name>"  
  
   object-type="<object-category>"  
  
   write-summary-report-to="<file-name/folder-name>"  
  
   report-errors="<true/false>"  
  
   verbose="<true/false>"/>  
```  
  
## <a name="migration-preparation-script-file-commands"></a>Comandos de arquivo de Script de preparação de migração  
O comando de preparação de migração inicia o mapeamento de esquema entre os bancos de dados de origem e destino.  
  
**Comando**  
  
esquema de mapa  
  
Mapeamento de esquema de banco de dados de origem para o esquema de destino.  
  
Migra os dados de origem para o destino.  
  
**Script**  
  
-   `source-schema`Especifica o esquema de origem que deseja migrar.  
  
-   `sql-server-schema`Especifica o esquema de destino onde desejamos a serem migradas.  
  
**Exemplo de sintaxe:**  
  
```xml  
<map-schema  
  
   source-schema="<source-schema>"  
  
   sql-server-schema="<target-schema>"/>  
```  
  
## <a name="manageability-script-file-commands"></a>Comandos de gerenciamento de arquivo de Script  
Os comandos de gerenciamento ajudam a sincronizar os objetos de banco de dados de destino com o banco de dados de origem. A saída de console padrão definindo para os comandos de migração é o relatório de saída 'Completa' com nenhum relatório de erro detalhado: resumo apenas no nó de raiz da árvore de objeto de origem.  
  
**Comando**  
  
Sincronizar de destino  
  
-   Os objetos de destino será sincronizado com o banco de dados de destino.  
  
-   Se esse comando é executado no banco de dados de origem, um erro for encontrado.  
  
-   Se a conexão de banco de dados de destino não é executada antes de executar este comando ou a conexão ao servidor de banco de dados de destino falha durante a execução do comando, será gerado um erro e sai do aplicativo de console.  
  
**Script**  
  
-   `object-name:`Especifica os objetos de destino considerados para sincronizar com o banco de dados de destino (ele pode ter nomes de objeto indivdual ou um nome de objeto de grupo).  
  
-   `object-type:`Especifica o tipo do objeto especificado no atributo nome do objeto (se a categoria de objeto for especificada, o tipo de objeto será 'categoria').  
  
-   `on-error:`Especifica se deve especificar os erros de sincronização como avisos ou erros. Opções disponíveis para em erro:  
  
    -   total de relatórios como aviso  
  
    -   relatório de cada-como-aviso  
  
    -   Falha de script  
  
-   `report-errors-to:`Especifica o local do relatório de erro para a operação de sincronização (atributo opcional) se apenas o caminho da pasta for dado, do arquivo pelo nome **TargetSynchronizationReport.XML** é criado.  
  
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
  
atualização do banco de dados  
  
-   Atualiza os objetos de origem do banco de dados.  
  
-   Se esse comando é executado no banco de dados de destino, um erro será gerado.  
  
**Script**  
  
Exige um ou vários nós de metabase como parâmetro de linha de comando.  
  
-   `object-name:`Especifica os objetos de origem considerados para a atualização do banco de dados de origem (ele pode ter nomes de objetos individuais ou um nome de objeto de grupo).  
  
-   `object-type:`Especifica o tipo do objeto especificado no atributo nome do objeto (se a categoria de objeto for especificada, o tipo de objeto será 'categoria').  
  
-   `on-error:`Especifica se deve especificar os erros de atualização como avisos ou erros. Opções disponíveis para em erro:  
  
    -   total de relatórios como aviso  
  
    -   relatório de cada-como-aviso  
  
    -   Falha de script  
  
-   `report-errors-to:`Especifica o local do relatório de erro para a operação de atualização (atributo opcional) se apenas o caminho da pasta for dado, do arquivo pelo nome **SourceDBRefreshReport.XML** é criado.  
  
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
  
## <a name="script-generation-script-file-commands"></a>Comandos de arquivo de Script de geração de script  
Os comandos de geração de Script executam duas tarefas: elas ajudam a salvar o console de saída em um arquivo de script. e gravar a saída do T-SQL para o console ou um arquivo com base no parâmetro que você especificar.  
  
**Comando**  
  
Salvar como script  
  
Usado para salvar os scripts de objetos em um arquivo mencionado quando metabase = target, essa é uma alternativa ao comando de sincronização em que vamos obter os scripts e executar o mesmo do banco de dados de destino.  
  
**Script**  
  
Exige um ou vários nós de metabase como parâmetro de linha de comando.  
  
-   `object-name:`Especifica os objetos cujos scripts serão salvos. (Ele pode ter nomes de objetos individuais ou um nome de objeto de grupo)  
  
-   `object-type:`Especifica o tipo do objeto especificado no atributo nome do objeto (se a categoria de objeto for especificada, o tipo de objeto será 'categoria').  
  
-   `metabase:`Especifica se ele IO de origem ou destino da metabase.  
  
-   `destination:`Especifica o caminho ou a pasta em que o script foi salvo, se o nome do arquivo não for especificado, em seguida, um nome de arquivo no .out formato (valor do atributo object_name)  
  
-   `overwrite:`Se true substitui se o mesmo nome de arquivo existe. Ele pode ter os valores (true/false).  
  
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
ou  
  
```xml  
<save-as-script  
  
   metabase="<source/target>"  
  
   destination="<file/folder>"  
  
      <metabase-object object-name="<object-name>"  
  
         object-type="<object-category>"/>  
  
</save-as-script>  
```  
**Comando**  
  
instrução de sql Convert  
  
-   `context`Especifica o nome do esquema.  
  
-   `destination`Especifica se a saída deve ser armazenada em um arquivo.  
  
    Se esse atributo não for especificado, a instrução T-SQL convertida é exibida no console. (atributo opcional)  
  
-   `conversion-report-folder`Especifica a pasta onde o relatório de avaliação pode ser armazenado. (atributo opcional)  
  
-   `conversion-report-overwrite`Especifica se deve substituir a pasta de relatórios de avaliação se ele já existe.  
  
    **Valor padrão:** false. (atributo opcional)  
  
-   `write-converted-sql-to`Especifica o caminho da pasta onde o T-SQL convertido é a ser armazenado arquivo (ou). Quando um caminho de pasta é especificado junto com o `sql-files` atributo, cada arquivo de origem terá um destino correspondente arquivo T-SQL criado na pasta especificada. Quando um caminho de pasta é especificado junto com o `sql` atributo, o T-SQL convertido é gravado em um arquivo chamado **Result.out** sob a pasta especificada.  
  
-   `sql`Especifica as instruções sql de Oracle a ser convertido, uma ou mais instruções podem ser separados usando um ";"  
  
-   `sql-files`Especifica o caminho dos arquivos de sql que deve ser convertido no código do T-SQL.  
  
-   `write-summary-report-to`Especifica o caminho onde o relatório será gerado. Se apenas o caminho da pasta for mencionado, do arquivo pelo nome **ConvertSQLReport.XML** é criado. (atributo opcional)  
  
    Relatório de criação tem 2 mais subcategorias, viz.:  
  
    -   erros de relatório (= "true/false", com padrão como "falso" (atributos opcionais)).  
  
    -   detalhado (= "true/false", com padrão como "falso" (atributos opcionais)).  
  
**Script**  
  
Exige um ou vários nós de metabase como parâmetro de linha de comando.  
  
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
ou  
  
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
ou  
  
```  
<convert-sql-statement  
  
   context="<schema-name>"  
  
   conversion-report-folder="<folder-name>"  
  
   conversion-report-overwrite="<true/false>"  
  
   sql-files="<folder-name>\*.sql" />  
```  
  
## <a name="next-step"></a>Próxima etapa  
Para obter informações sobre opções de linha de comando, consulte [opções de linha de comando no Console do SSMA &#40; OracleToSQL &#41;](../../ssma/oracle/command-line-options-in-ssma-console-oracletosql.md) .  
  
Para obter informações sobre arquivos de script do console de exemplo, consulte [trabalhando com arquivos de Script do Console do exemplo &#40; OracleToSQL &#41;](../../ssma/oracle/working-with-the-sample-console-script-files-oracletosql.md)  
  
A próxima etapa depende de seus requisitos de projeto:  
  
-   Para especificar uma senha ou a exportação / importação de senhas, consulte [gerenciar senhas &#40; OracleToSQL &#41;](../../ssma/oracle/managing-passwords-oracletosql.md).  
  
-   Para gerar relatórios, consulte [gerando relatórios &#40; OracleToSQL &#41;](../../ssma/oracle/generating-reports-oracletosql.md).  
  
-   Para solucionar problemas no console, consulte [solução de problemas &#40; OracleToSQL &#41;](../../ssma/oracle/troubleshooting-oracletosql.md).  
  

