---
title: Executar o Console do SSMA (MySQLToSQL) | Microsoft Docs
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
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: fd560a17c10b5e076236195107d0a9154921422a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47701804"
---
# <a name="executing-the-ssma-console-mysqltosql"></a>Executar o console do SSMA (MySQLToSQL)
Microsoft fornece um conjunto robusto de script de comandos de arquivo para executar e controlar atividades do SSMA.  
  
O aplicativo de console usa determinados comandos do arquivo de script padrão como enumerado nesta seção.  
  
## <a name="project--script-file-commands"></a>Comandos de arquivo de Script do projeto  
**Comando**  
  
Criar-novo projeto:   
                   Cria um novo projeto SSMA.  
  
Os comandos de projeto lidar com a criação de projetos, abrir, salvar e sair de projetos.  
  
**Script**  
  
1.  `project-folder` indica a pasta do projeto sendo criado.  
  
2.  `project-name` indica o nome do projeto. {string}  
  
3.  `overwrite-if-exists`Atributo opcional indica se um projeto existente deve ser substituído. {booliano}  
  
4.  `project-type:`Atributo opcional. Indica o tipo de projeto ou seja, "sql-server 2005" projeto ou projeto de "sql-server-2008" ou "sql-server-2012" ou "sql-server-2014" projeto ou "sql azure". Padrão é "sql-server-2008".  
  
**Exemplo de sintaxe:**  
  
```xml  
<create-new-project  
  
   project-folder="<project-folder>"  
  
   project-name="<project-name>"  
  
   overwrite-if-exists="<true/false>"   (optional)  
  
   project-type==”<sql-server-2008 | sql-server-2005 | sql-server-2012 | sql-server-2014 | sql-azure>”   (optional)  
  
/>  
```  
Atributo 'Substituir-if-exists' está **falsos** por padrão.  
  
É o atributo 'tipo de projeto' **sql-server-2008** por padrão.  
  
**Comando**  
  
Abrir projeto:   
                  Abre um projeto existente.  
  
**Script**  
  
1.  `project-folder` indica a pasta do projeto sendo criado. O comando falhará se a pasta especificada não existe.  {string}  
  
2.  `project-name` indica o nome do projeto. O comando falhará se o projeto especificado não existe.  {string}  
  
**Exemplo de sintaxe:**  
  
```xml  
<open-project  
  
   project-folder="<project-folder>"  
  
   project-name="<project-name>"  
  
/>  
```  
> [!IMPORTANT]  
> Aplicativo de Console do SSMA para MySQL dá suporte a compatibilidade com versões anteriores. Você poderá abrir projetos criados por uma versão anterior do SSMA.  
  
**Comando**  
  
projeto salvar: salva o projeto de migração.  
  
**Script**  
  
**Exemplo de sintaxe:**  
  
```xml  
<save-project/>  
```  
**Comando**  
  
Fechar projeto  
                  : Fecha o projeto de migração.  
  
**Script**  
  
**Exemplo de sintaxe:**  
  
```xml  
<save-project/>  
```  
**Comando**  
  
Fechar projeto  
                  : Fecha o projeto de migração.  
  
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
  
1.  O **procurar** não há suporte para o recurso da interface do usuário no console.  
  
2.  O **autenticação do windows** e **porta** parâmetros não são aplicáveis ao se conectar ao SQL Azure.  
  
3.  Para obter mais informações sobre 'Criando arquivos de Script', consulte [criando arquivos de Script &#40;MySQLToSQL&#41;](../../ssma/mysql/creating-script-files-mysqltosql.md).  
  
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
  
Force-carga-origem/destino-banco de dados  
  
-   Carrega os metadados da fonte.  
  
-   É útil para trabalhar no projeto de migração off-line.  
  
-   Se a conexão para o origem/destino não puder ser estabelecida, um erro será gerado e o aplicativo de console para ainda mais a execução  
  
**Script**  
  
Requer um ou vários nós de metabase como parâmetro de linha de comando.  
  
**Exemplo de sintaxe:**  
  
```xml  
<force-load metabase="<source/target>"  
  
      <metabase-object object-name="<object-name>"/>  
  
</force-load>  
```  
**Comando**  
  
Reconecte-origem-banco de dados  
  
1.  Reconecta-se à fonte de dados, mas não carrega todos os metadados ao contrário do comando connect-origem-banco de dados.  
  
2.  Se não é possível estabelecer (conexão com a fonte de re), um erro será gerado e o aplicativo de console ainda mais para a execução.  
  
**Script**  
  
**Exemplo de sintaxe:**  
  
```xml  
<reconnect-source-database  server="<server-unique-name>"/>  
```  
**Comando**  
  
connect-target-database  
  
1.  Conecta-se ao destino do SQL Server ou SQL Azure banco de dados e carrega os metadados de nível alto do banco de dados de destino, mas não os metadados inteiramente.  
  
2.  Se a conexão para o destino não puder ser estabelecida, um erro será gerado e o aplicativo de console ainda mais para a execução.  
  
**Script**  
  
Definição de servidor é recuperada do atributo nome definido para cada conexão na seção servidor de arquivo de conexão do servidor ou o arquivo de script  
  
**Exemplo de sintaxe:**  
  
```xml  
<connect-target-database  server="<server-unique-name>"/>  
```  
**Comando**  
  
reconnect-target-database  
  
1.  Reconecta-se ao banco de dados de destino, mas não carrega todos os metadados, ao contrário do comando de destino-connect-database.  
  
2.  Se a (re) conexão para o destino não puder ser estabelecida, um erro será gerado e o aplicativo de console ainda mais para a execução.  
  
**Script**  
  
**Exemplo de sintaxe:**  
  
```xml  
<reconnect-target-database  server="<server-unique-name>"/>  
```  
  
## <a name="report-script-file-commands"></a>Comandos de arquivo de Script de relatório  
Os comandos de relatório geram relatórios sobre o desempenho de várias atividades do Console do SSMA.  
  
**Comando**  
  
Gerar--relatório de avaliação  
  
1.  Gera relatórios de avaliação no banco de dados de origem.  
  
2.  Se a conexão de banco de dados de origem não é executada antes de executar esse comando, será gerado um erro e sai do aplicativo de console.  
  
3.  Falha ao se conectar ao servidor de banco de dados de origem durante a execução do comando, também resulta em encerrar o aplicativo de console.  
  
**Script**  
  
1.  `assessment-report-folder:` Especifica a pasta onde o relatório de avaliação pode ser armazenado. (atributo opcional)  
  
2.  `object-name:` Especifica os objetos considerados para a geração de relatório de avaliação (ele pode ter nomes de objetos individuais ou um nome de objeto de grupo).  
  
3.  `object-type:` Especifica o tipo do objeto especificado no atributo de nome de objeto (se a categoria de objeto for especificada, o tipo de objeto será "category").  
  
4.  `assessment-report-overwrite:` Especifica se deve substituir a pasta de relatório de avaliação se ele já existe.  
  
    **Valor padrão:** false. (atributo opcional)  
  
5.  `write-summary-report-to:` Especifica o caminho onde o relatório de resumo será gerado.  
  
    Se apenas o caminho da pasta for mencionado, em seguida, de arquivos por nome **AssessmentReport&lt;n&gt;. XML** é criado. (atributo opcional)  
  
    Criação de relatório tem duas subcategorias adicionais:  
  
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
ou em  
  
```xml  
<generate-assessment-report  
  
   conversion-report-folder="<folder-name>"   (optional)  
  
   conversion-report-overwrite="<true/false>"   (optional)  
  
>  
  
      <metabase-object object-name="<object-name>"  
  
         object-type="<object-category>"/>  
  
</generate-assessment-report>  
```  
  
## <a name="migration--script-file-commands"></a>Comandos de arquivo de Script de migração  
Os comandos de migração converter o esquema de banco de dados de destino para o esquema de origem e migra dados para o servidor de destino.  
  
A saída do console padrão definindo para os comandos de migração é o relatório de saída 'Full' com nenhum relatório de erro detalhada: resumo apenas no nó de raiz da árvore de objeto de origem.  
  
**Comando**  
  
convert-schema  
  
1.  Executa a conversão de esquema de origem ao esquema de destino.  
  
2.  Se a conexão de banco de dados de origem ou de destino não é executada antes de executar esse comando ou a conexão para o servidor de banco de dados de origem ou destino falha durante a execução do comando, será gerado um erro e sai do aplicativo de console.  
  
**Script**  
  
1.  `conversion-report-folder:` Especifica a pasta onde o relatório de avaliação pode ser armazenado. (atributo opcional)  
  
2.  `object-name:` Especifica os objetos considerados para a conversão de esquema (ele pode ter nomes de objetos individuais ou um nome de objeto de grupo).  
  
3.  `object-type:` Especifica o tipo do objeto especificado no atributo de nome de objeto (se a categoria de objeto for especificada, o tipo de objeto será "category").  
  
4.  `conversion-report-overwrite:` Especifica se deve substituir a pasta de relatório de avaliação se ele já existe.  
  
    **Valor padrão:** false. (atributo opcional)  
  
5.  `write-summary-report-to:` Especifica o caminho onde o relatório de resumo será gerado.  
  
    Se apenas o caminho da pasta for mencionado, em seguida, de arquivos por nome **SchemaConversionReport&lt;n&gt;. XML** é criado. (atributo opcional)  
  
    Criação de relatório de resumo tem duas subcategorias adicionais:  
  
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
ou em  
  
```xml  
<convert-schema  
  
   conversion-report-folder="<folder-name>"   (optional)  
  
   conversion-report-overwrite="<true/false>"   (optional)  
  
      <metabase-object object-name="<object-names>"  
  
         object-type="<object-category>"/>  
  
</convert-schema>  
```  
**Comando**  
  
migrar dados  
  
1.  Migra os dados de origem para o destino.  
  
**Script**  
  
1.  `object-name:` Especifica os objetos de origem considerados para a migração de dados (ele pode ter nomes de objetos individuais ou um nome de objeto de grupo).  
  
2.  `object-type:` Especifica o tipo do objeto especificado no atributo de nome de objeto (se a categoria de objeto for especificada, o tipo de objeto será "category").  
  
3.  `write-summary-report-to:` Especifica o caminho onde o relatório de resumo será gerado.  
  
    Se apenas o caminho da pasta for mencionado, em seguida, de arquivos por nome **DataMigrationReport&lt;n&gt;. XML** é criado. (atributo opcional)  
  
    Criação de relatório tem duas subcategorias adicionais:  
  
    -   `report-errors` (= "true/false", com padrão como "false" (atributos opcionais))  
  
    -   `verbose` (= "true/false", com padrão como "false" (atributos opcionais))  
  
**Exemplo de sintaxe:**  
  
```xml  
<migrate-data  
  
   write-summary-report-to="<file-name/folder-name>”  
  
   report-errors="true" verbose="true">  
  
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
  
   write-summary-report-to="<file-name/folder-name>”  
  
   report-errors="true" verbose="true"/>  
```  
  
## <a name="migration-preparation-script-file-command"></a>Comando de arquivo de Script de preparação de migração  
O comando de preparação de migração inicia o mapeamento de esquema entre os bancos de dados de origem e destino.  
  
**Comando**  
  
map-schema  
  
Mapeamento de esquema de banco de dados de origem ao esquema de destino.  
  
**Script**  
  
1.  `source-schema` Especifica o esquema de origem que nossa intenção é migrar.  
  
2.  `sql-server-schema` Especifica o esquema de destino onde desejamos a serem migrados.  
  
**Exemplo de sintaxe:**  
  
```xml  
<map-schema  
  
   source-schema="<source-schema>"  
  
   sql-server-schema="<target-schema>"/>  
```  
  
## <a name="manageability-script-file-commands"></a>Comandos de arquivo de Script de capacidade de gerenciamento  
Os comandos de capacidade de gerenciamento ajudam a sincronizar os objetos de banco de dados de destino com o banco de dados de origem.  
  
> [!NOTE]  
> A saída do console padrão definindo para os comandos de migração é o relatório de saída 'Full' com nenhum relatório de erro detalhada: resumo apenas no nó de raiz da árvore de objeto de origem.  
  
**Comando**  
  
Sincronizar de destino  
  
1.  Sincroniza os objetos de destino com o banco de dados de destino.  
  
2.  Se esse comando for executado no banco de dados de origem, um erro for encontrado.  
  
3.  Se a conexão de banco de dados de destino não é executada antes de executar esse comando ou a conexão ao servidor de banco de dados de destino falha durante a execução do comando, será gerado um erro e o aplicativo de console é encerrado.  
  
**Script**  
  
1.  `object-name:` Especifica os objetos considerados para sincronizar com o banco de dados de destino (ele pode ter nomes de objetos individuais ou um nome de objeto de grupo).  
  
2.  `object-type:` Especifica o tipo do objeto especificado no atributo de nome de objeto (se a categoria de objeto for especificada, o tipo de objeto será "category").  
  
3.  `on-error:` Especifica se deve especificar os erros de sincronização como avisos ou erros. Opções disponíveis para em caso de erro:  
  
    -   report-total-as-warning  
  
    -   report-each-as-warning  
  
    -   Falha-script  
  
4.  `report-errors-to:` Especifica o local do relatório de erros para a operação de sincronização (atributo opcional) se apenas o caminho da pasta for dado, em seguida, de arquivos por nome **TargetSynchronizationReport.XML** é criado.  
  
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
**Comando**  
  
atualização de banco de dados  
  
1.  Atualiza os objetos de origem do banco de dados.  
  
2.  Se esse comando é executado no banco de dados de destino, um erro será gerado.  
  
**Script**  
  
1.  `object-name:` Especifica os objetos de origem considerados para a atualização do banco de dados de origem (ele pode ter nomes de objetos individuais ou um nome de objeto de grupo).  
  
2.  `object-type:` Especifica o tipo do objeto especificado no atributo de nome de objeto (se a categoria de objeto for especificada, o tipo de objeto será "category").  
  
3.  `on-error:` Especifica se deve especificar os erros de sincronização como avisos ou erros. Opções disponíveis para em caso de erro:  
  
    -   report-total-as-warning  
  
    -   report-each-as-warning  
  
    -   Falha-script  
  
4.  `report-errors-to:` Especifica o local do relatório de erros para a operação de sincronização (atributo opcional) se apenas o caminho da pasta for dado, em seguida, de arquivos por nome **SourceDBRefreshReport.XML** é criado.  
  
Requer um ou vários nós de metabase como parâmetro de linha de comando.  
  
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
ou em  
  
```xml  
<refresh-from-database  
  
   object-name="<object-name>"  
  
   object-type="<object-category>"/>  
```  
ou em  
  
```xml  
<refresh-from-database>  
  
   <metabase-object object-name="<object-name>"/>  
  
</refresh-from-database>  
```  
  
## <a name="script-generation-script-file-commands"></a>Comandos de arquivo de Script de geração de script  
Os comandos de geração de Script executam duas tarefas: eles ajudam a salvar o console de saída em um arquivo de script; e registrar a saída do T-SQL para o console ou um arquivo de acordo com o parâmetro que você especificar.  
  
**Comando**  
  
Salvar como script  
  
Usado para salvar os Scripts dos objetos em um arquivo mencionado quando metabase Target, essa é uma alternativa ao comando de sincronização, onde podemos obter os scripts e execute o mesmo banco de dados de destino.  
  
**Script**  
  
Requer um ou vários nós de metabase como parâmetro de linha de comando.  
  
1.  `object-name:` Especifica os objetos cujos scripts serão salvos. (Ele pode ter nomes de objetos individuais ou um nome de objeto de grupo)  
  
2.  `object-type:` Especifica o tipo do objeto especificado no atributo de nome de objeto (se a categoria de objeto for especificada, o tipo de objeto será "category").  
  
3.  `metabase:` Especifica se é a origem ou destino da metabase.  
  
4.  `destination:` Especifica o caminho ou a pasta em que o script foi salvo, se o nome do arquivo não for fornecido, em seguida, um nome de arquivo na. out formato (valor do atributo object_name)  
  
5.  `overwrite:` Se for true, em seguida, ele substitui se o mesmo nome de arquivo existe. Ele pode ter os valores (true/false).  
  
**Exemplo de sintaxe:**  
  
```xml  
<save-as-script  
  
   metabase="<source/target>"  
  
   object-name="<object-name>"  
  
   object-type="<object-category>"  
  
   destination="<file-name/folder-name>”  
  
   overwrite="<true/false>"   (optional)  
  
/>  
```  
ou em  
  
```xml  
<save-as-script  
  
   metabase="<source/target>"  
  
   destination="<file-name/folder-name>”  
  
      <metabase-object object-name="<object-name>"  
  
            object-type="<object-category>"/>  
  
</save-as-script>  
```  
**Comando**  
  
convert-sql-statement  
  
1.  `context` Especifica o nome do esquema.  
  
2.  `destination` Especifica se a saída deve ser armazenada em um arquivo.  
  
    Se esse atributo não for especificado, a instrução T-SQL convertida é exibida no console. (atributo opcional)  
  
3.  `conversion-report-folder` Especifica a pasta onde o relatório de avaliação pode ser armazenado. (atributo opcional)  
  
4.  `conversion-report-overwrite` Especifica se deve substituir a pasta de relatório de avaliação se ele já existe.  
  
    **Valor padrão:** false. (atributo opcional)  
  
5.  `write-converted-sql-to` Especifica o caminho da pasta onde o T-SQL convertido deve ser armazenado arquivo (ou). Quando um caminho de pasta é especificado junto com o `sql-files` atributo, cada arquivo de origem terão um criado sob a pasta especificada do arquivo de T-SQL de destino correspondente. Quando um caminho de pasta é especificado junto com o `sql` atributo, o T-SQL convertido é gravado em um arquivo chamado Result.out sob a pasta especificada.  
  
6.  `sql` Especifica as instruções de sql do MySQL para ser convertido, uma ou mais instruções podem ser separados usando um ";"  
  
7.  `sql-files` Especifica o caminho dos arquivos de sql que tem a ser convertido em código T-SQL.  
  
8.  `write-summary-report-to` Especifica o caminho onde o relatório de resumo será gerado. Se apenas o caminho da pasta for mencionado, em seguida, de arquivos por nome **ConvertSQLReport.XML** é criado. (atributo opcional)  
  
    Criação tem 2 mais subcategorias, sobre visualização de relatório..,:  
  
    -   erros de relatório (= "true/false", com padrão como "false" (atributos opcionais)).  
  
    -   detalhado (= "true/false", com padrão como "false" (atributos opcionais)).  
  
**Script**  
  
Requer um ou vários nós de metabase como parâmetro de linha de comando.  
  
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
ou em  
  
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
ou em  
  
```  
<convert-sql-statement  
  
   context="<schema-name>"  
  
   conversion-report-folder="<folder-name>"  
  
   conversion-report-overwrite="<true/false>"  
  
   sql-files="<folder-name>\*.sql"  
  
/>  
```  
  
## <a name="next-step"></a>Próxima etapa  
Para obter informações sobre as opções de linha de comando, consulte [opções de linha de comando no Console do SSMA &#40;MySQLToSQL&#41; ](../../ssma/mysql/command-line-options-in-ssma-console-mysqltosql.md) .  
  
Para obter mais informações sobre arquivos de script de console de exemplo, consulte [trabalhando com os arquivos de Script de Console de exemplo &#40;MySQLToSQL&#41;](../../ssma/mysql/working-with-the-sample-console-script-files-mysqltosql.md)  
  
A próxima etapa depende de seus requisitos de projeto:  
  
1.  Para especificar uma senha ou a exportação / importação de senhas, consulte [gerenciamento de senhas &#40;MySQLToSQL&#41;](../../ssma/mysql/managing-passwords-mysqltosql.md).  
  
2.  Para gerar relatórios, consulte [geração de relatórios &#40;MySQLToSQL&#41;](../../ssma/mysql/generating-reports-mysqltosql.md).  
  
3.  Para solucionar problemas no console, consulte [solução de problemas &#40;MySQLToSQL&#41;](../../ssma/mysql/troubleshooting-mysqltosql.md).  
  
