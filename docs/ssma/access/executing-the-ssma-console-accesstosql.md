---
title: Executar o Console do SSMA (AccessToSQL) | Microsoft Docs
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
- Azure SQL Database
- SQL Server
ms.assetid: aa1bf665-8dc0-4259-b36f-46ae67197a43
caps.latest.revision: 25
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 76f31cffc8f947449d6825a6659b1bb22e0c0b1d
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="executing-the-ssma-console-accesstosql"></a>Executar o Console do SSMA (AccessToSQL)
Microsoft fornece um conjunto robusto de comandos do arquivo de script e opções de linha de comando para executar e controlar as atividades do SSMA. As seções resultantes detalham os mesmos.  
  
## <a name="project--script-file-commands"></a>Comandos do arquivo de Script de projeto  
Os comandos de projeto lidar com a criação de projetos, abrir, salvar e sair de projetos.  
  
**Comando**  
  
Criar novo projeto: cria um novo projeto SSMA.  
  
**Script**  
  
-   `project-folder`indica a pasta de projeto obtendo criado.  
  
-   `project-name`indica o nome do projeto. {string}  
  
-   `overwrite-if-exists`Atributo opcional indica se um projeto existente deve ser substituído. {booliano}  
  
-   `project-type`é um atributo opcional.  As seguintes opções estão disponíveis para o tipo de projeto:  
  
    -   SQL-server-2005  
  
    -   o SQL-server-2008  
  
    -   o SQL-server-2012  
  
    -   SQL-server-2014  
  
    -   SQL-server-2016  
  
    -   o SQL azure  
  
    Padrão é "sql-server-2008".  
  
**Exemplo:**  
  
```xml  
<create-new-project  
  
  project-folder="<project-folder>"  
  
  project-name="<project-name>"  
  
  overwrite-if-exists="<true/false>"  
  
  project-type=”<sql-server-2008 | sql-server-2005 | sql-server-2012 | sql-server-2014 | sql-azure>”  
  
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
**Observação:** aplicativo de Console SSMA para Access dá suporte a compatibilidade com versões anteriores. Você poderá abrir projetos criados por uma versão anterior do SSMA.  
  
**Comando**  
  
projeto salvar: salva o projeto de migração.  
  
**Script**  
  
**Exemplo de sintaxe:**  
  
```xml  
<save-project/>  
```  
**Comando**  
  
projeto de fechamento: fecha o projeto de migração.  
  
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
  
O **procurar** recurso da interface do usuário não tem suporte no console.  
  
O **autenticação do windows** e **porta** parâmetros não são aplicáveis ao se conectar ao SQL Azure.  
  
Para obter mais informações sobre 'Criando arquivos de Script', consulte [criando arquivos de Script &#40; AccessToSQL &#41; ](../../ssma/access/creating-script-files-accesstosql.md).  
  
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
  
carga-acesso-banco de dados: usada para carregar arquivos de banco de dados do access  
  
**Script**  
  
**Exemplo de sintaxe:**  
  
```xml  
<load-access-database  database-file="<Access-database>"/>  
```  
ou  
  
```xml  
<load-access-database>  
  
  <access-database database-file="<Access-database1>"/>  
  
  <access-database database-file="<Access-database2>"/>  
  
</load-access-database>  
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
<force-load  
  
  object-name="<object-name>"  
  
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
  
-   Conecta-se para o banco de dados do destino do SQL Server ou SQL Azure e carrega os metadados de nível alto do banco de dados de destino, mas não os metadados inteiramente.  
  
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
  
## <a name="report-script-file-commands"></a>Comandos de Script de arquivo de relatório  
Os comandos de relatório geram relatórios sobre o desempenho de várias atividades do Console SSMA.  
  
**Comando**  
  
relatório gerar de avaliação  
  
-   Gera relatórios de avaliação no banco de dados de origem.  
  
-   Se a conexão de banco de dados de origem não é executada antes de executar esse comando, será gerado um erro e sai do aplicativo de console.  
  
-   Falha ao se conectar ao servidor de banco de dados de origem durante a execução do comando, também resulta em encerrar o aplicativo de console.  
  
**Script**  
  
-   `assessment-report-folder:`Especifica a pasta onde o relatório de avaliação pode ser armazenado. (atributo opcional)  
  
-   `object-name:`Especifica os objetos considerados para geração de relatórios de avaliação (ele pode ter nomes de objeto indivdual ou um nome de objeto de grupo).  
  
-   `object-type:`Especifica o tipo do objeto especificado no atributo nome do objeto (se a categoria de objeto for especificada, o tipo de objeto será 'categoria').  
  
-   `assessment-report-overwrite:`Especifica se deve substituir a pasta de relatórios de avaliação se ele já existe.  
  
    **Valor padrão:** false. (atributo opcional)  
  
-   `write-summary-report-to:`Especifica o caminho onde o relatório será gerado.  
  
    Se apenas o caminho da pasta for mencionado, do arquivo pelo nome **AssessmentReport&lt;n&gt;. XML** é criado. (atributo opcional)  
  
    Criação de relatório tem duas subcategorias adicionais:  
  
    -   `report-errors`(= "true/false", com padrão como "falso" (atributos opcionais))  
  
    -   `verbose`(= "true/false", com padrão como "falso" (atributos opcionais))  
  
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
ou  
  
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
  
-   `write-summary-report-to:`Especifica o caminho onde o relatório será gerado.  
  
    Se apenas o caminho da pasta for mencionado, do arquivo pelo nome **SchemaConversionReport&lt;n&gt;. XML** é criado. (atributo opcional)  
  
    Criação de relatório tem duas subcategorias adicionais:  
  
    -   `report-errors`(= "true/false", com padrão como "falso" (atributos opcionais))  
  
    -   `verbose`(= "true/false", com padrão como "falso" (atributos opcionais))  
  
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
ou  
  
```xml  
<convert-schema  
  
  conversion-report-folder="<folder>"         (optional)  
  
  conversion-report-overwrite="<true/false>"  (optional)  
  
  <metabase-object object-name="ssma.Procedures"  
  
    object-type="category"/>  
  
</convert-schema>  
```  
**Comando**  
  
migrar dados  
  
1.  Migra os dados de origem para o destino.  
  
**Script**  
  
-   `object-name:`Especifica os objetos de origem considerados para a migração de dados (ele pode ter nomes de objeto indivdual ou um nome de objeto de grupo).  
  
-   `object-type:`Especifica o tipo do objeto especificado no atributo nome do objeto (se a categoria de objeto for especificada, o tipo de objeto será 'categoria').  
  
-   `write-summary-report-to:`Especifica o caminho onde o relatório será gerado.  
  
    Se apenas o caminho da pasta for mencionado, do arquivo pelo nome **DataMigrationReport&lt;n&gt;. XML** é criado. (atributo opcional)  
  
    Criação de relatório tem duas subcategorias adicionais:  
  
    -   `report-errors`(= "true/false", com padrão como "falso" (atributos opcionais))  
  
    -   `verbose`(= "true/false", com padrão como "falso" (atributos opcionais))  
  
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
ou  
  
```xml  
<migrate-data  
  
  object-name="ssma.Tables"  
  
  object-type="category"  
  
  write-summary-report-to="<filepath/folder>"  
  
  report-errors="true" verbose="true"/>  
```  
**Comando**  
  
Vincular tabelas: este comando vincula a tabela de origem (acesso) para a tabela de destino.  
  
**Script**  
  
**Exemplo de sintaxe:**  
  
```xml  
<link-tables>  
  
  <metabase-object object-name="AccessDatabase.table1" object-type="Tables"/>  
  
  <metabase-object object-name="AccessDatabase.table2" object-type="Tables"/>  
  
</link-tables>  
```  
ou  
  
```xml  
<link-tables>  
  
  <metabase-object object-name="AccessDatabase.Tables" object-type="category"/>  
  
</link-tables>  
```  
**Comando**  
  
tabelas desvincular: este comando desvincula a tabela de origem (acesso) da tabela de destino.  
  
**Script**  
  
**Exemplos de sintaxe:**  
  
```xml  
<unlink-tables>  
  
  <metabase-object object-name="AccessDatabase.table1" object-type="Tables"/>  
  
  <metabase-object object-name="AccessDatabase.table2" object-type="Tables"/>  
  
</unlink-tables>  
```  
ou  
  
```xml  
<unlink-tables>  
  
  <metabase-object object-name="AccessDatabase.Tables" object-type="category"/>  
  
</unlink-tables>  
```  
  
## <a name="migration-preparation-script-file-commands"></a>Comandos de arquivo de Script de preparação de migração  
O comando de preparação de migração inicia o mapeamento de esquema entre os bancos de dados de origem e destino.  
  
**Comando**  
  
mapa de esquema: o mapeamento de esquema de banco de dados de origem para o esquema de destino.  
  
**Script**  
  
-   `source-schema`Especifica o esquema de origem que deseja migrar.  
  
-   `sql-server-schema`Especifica o esquema de destino onde desejamos a serem migradas.  
  
**Exemplo de sintaxe:**  
  
```xml  
<map-schema source-schema="source-schema"  
  
            sql-server-schema="target-schema"/>  
```  
  
## <a name="manageability-commands"></a>Comandos de capacidade de gerenciamento  
Os comandos de gerenciamento ajudam a sincronizar os objetos de banco de dados de destino com o banco de dados de origem.  
  
A saída de console padrão definindo para os comandos de migração é o relatório de saída 'Completa' com nenhum relatório de erro detalhado: resumo apenas no nó de raiz da árvore de objeto de origem.  
  
**Comando**  
  
Sincronizar de destino  
  
1.  Os objetos de destino será sincronizado com o banco de dados de destino.  
  
2.  Se esse comando é executado no banco de dados de origem, um erro for encontrado.  
  
3.  Se a conexão de banco de dados de destino não é executada antes de executar este comando ou a conexão ao servidor de banco de dados de destino falha durante a execução do comando, será gerado um erro e sai do aplicativo de console.  
  
**Script**  
  
1.  `object-name:`Especifica os objetos de destino considerados para sincronizar com o banco de dados de destino (ele pode ter nomes de objeto indivdual ou um nome de objeto de grupo).  
  
2.  `object-type:`Especifica o tipo do objeto especificado no atributo nome do objeto (se a categoria de objeto for especificada, o tipo de objeto será 'categoria').  
  
3.  `on-error:`Especifica se deve especificar os erros de sincronização como avisos ou erros. Opções disponíveis para em erro:  
  
    -   total de relatórios como aviso  
  
    -   relatório de cada-como-aviso  
  
    -   Falha de script  
  
4.  `report-errors-to:`Especifica o local do relatório de erro para a operação de sincronização (atributo opcional) se apenas o caminho da pasta for dado, do arquivo pelo nome **TargetSynchronizationReport.XML** é criado.  
  
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
ou  
  
```xml  
<synchronize-target  
  
  object-name="ssma.dbo.Procedures"  
  
  object-type="category"/>  
```  
ou  
  
```xml  
<synchronize-target>  
  
  <metabase-object object-name="ssma.dbo.TT1"/>  
  
  <metabase-object object-name="ssma.dbo.TT2"/>  
  
  <metabase-object object-name="ssma.dbo.TT3"/>  
  
</synchronize-target>  
```  
**Comando**  
  
atualização do banco de dados  
  
-   Atualiza os objetos de origem do banco de dados.  
  
-   Se esse comando é executado no banco de dados de destino, um erro será gerado.  
  
**Script**  
  
Exige um ou vários nós de metabase como parâmetro de linha de comando.  
  
1.  `object-name:`Especifica os objetos de origem considerados para a atualização do banco de dados de origem (ele pode ter nomes de objeto indivdual ou um nome de objeto de grupo).  
  
2.  `object-type:`Especifica o tipo do objeto especificado no atributo nome do objeto (se a categoria de objeto for especificada, o tipo de objeto será 'categoria').  
  
3.  `on-error:`Especifica se deve especificar os erros de atualização como avisos ou erros. Opções disponíveis para em erro:  
  
    -   total de relatórios como aviso  
  
    -   relatório de cada-como-aviso  
  
    -   Falha de script  
  
4.  `report-errors-to:`Especifica o local do relatório de erro para a operação de atualização (atributo opcional) se apenas o caminho da pasta for dado, do arquivo pelo nome **SourceDBRefreshReport.XML** é criado.  
  
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
ou  
  
```xml  
<refresh-from-database  
  
  object-name="ssma.Procedures"  
  
  object-type="category"/>  
```  
ou  
  
```xml  
<refresh-from-database>  
  
  <metabase-object object-name="ssma.TT_1"/>  
  
</refresh-from-database>  
```  
  
## <a name="script-generation-script-file-commands"></a>Comandos de arquivo de Script de geração de script  
A geração de Script de comandos ajudam a salvar a saída do console em um arquivo de script.  
  
**Comando**  
  
Salvar como script  
  
Usado para salvar os Scripts de objetos em um arquivo mencionado quando metabase = target, essa é uma alternativa ao comando de sincronização em que vamos obter os scripts e executar o mesmo do banco de dados de destino.  
  
**Script**  
  
Exige um ou vários nós de metabase como parâmetro de linha de comando.  
  
-   `object-name:`Especifica os objetos cujos scripts serão salvos. (Ele pode ter nomes de objetos individuais ou um nome de objeto de grupo)  
  
-   `object-type:`Especifica o tipo do objeto especificado no atributo nome do objeto (se a categoria de objeto for especificada, o tipo de objeto será 'categoria').  
  
-   `metabase:`Especifica se é a origem ou destino da metabase.  
  
-   `destination:`Especifica o caminho ou a pasta em que o script foi salvo, se o nome do arquivo não for especificado, em seguida, um nome de arquivo no .out formato (valor do atributo object_name)  
  
-   `overwrite:`Se true substitui se o mesmo nome de arquivo existe. Ele pode ter os valores (true/false).  
  
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
ou  
  
```xml  
<save-as-script  
  
  metabase="<source/target>"  
  
  destination="<file/folder>"  
  
    <metabase-object object-name="ssma.dbo.Procedures"  
  
                     object-type="category"/>  
  
</save-as-script>  
```  
  
## <a name="next-step"></a>Próxima etapa  
Para obter informações sobre opções de linha de comando, consulte [opções de linha de comando no Console do SSMA &#40; AccessToSQL &#41; ](../../ssma/access/command-line-options-in-ssma-console-accesstosql.md) .  
  
Para obter informações sobre arquivos de script do console de exemplo, consulte [trabalhando com o FilesExecuting de Script do Console de exemplo, o Console SSMA &#40; AccessToSQL &#41;](../../ssma/access/working-sample-console-script-filesexecuting-ssma-console-accesstosql.md)  
  
A próxima etapa depende de seus requisitos de projeto:  
  
-   Para especificar uma senha ou a exportação / importação de senhas, consulte [gerenciar senhas &#40; AccessToSQL &#41; ](../../ssma/access/managing-passwords-accesstosql.md).  
  
-   Para gerar relatórios, consulte [gerando relatórios &#40; AccessToSQL &#41; ](../../ssma/access/generating-reports-accesstosql.md).  
  
-   Para solucionar problemas no console, consulte [solução de problemas &#40; AccessToSQL &#41; ](../../ssma/access/troubleshooting-accesstosql.md).  
  

