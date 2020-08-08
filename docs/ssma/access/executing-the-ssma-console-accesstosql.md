---
title: Executando o console do SSMA (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: aa1bf665-8dc0-4259-b36f-46ae67197a43
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: c10360a252847aec9f65b9e6e1709b9fbffecce4
ms.sourcegitcommit: e8f6c51d4702c0046aec1394109bc0503ca182f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/07/2020
ms.locfileid: "87933947"
---
# <a name="executing-the-ssma-console-accesstosql"></a>Executando o console do SSMA (AccessToSQL)
A Microsoft fornece um conjunto robusto de comandos de arquivo de script e opções de linha de comando para executar e controlar atividades do SSMA. As seções que mais profundos detalham o mesmo.  
  
## <a name="project--script-file-commands"></a>Comandos de arquivo de script do projeto  
Os comandos de projeto lidam com a criação de projetos, abertura, salvamento e saída de projetos.  
  
**Comando**  
  
Create-New-Project: cria um novo projeto do SSMA.  
  
**Script**  
  
-   `project-folder`indica a pasta do projeto que está sendo criado.  
  
-   `project-name`indica o nome do projeto. {string}  
  
-   `overwrite-if-exists`Atributo opcional indica se um projeto existente deve ser substituído. Boolean  
  
-   `project-type`é um atributo opcional.  As opções a seguir estão disponíveis para o tipo de projeto:  
  
    -   SQL-Server-2005  
  
    -   SQL-Server-2008  
  
    -   SQL-Server-2012  
  
    -   SQL-Server-2014  
  
    -   SQL-Server-2016  
  
    -   SQL – Azure  
  
    O padrão é "SQL-Server-2008".  
  
**Exemplo:**  
  
```xml  
<create-new-project  
  
  project-folder="<project-folder>"  
  
  project-name="<project-name>"  
  
  overwrite-if-exists="<true/false>"  
  
  project-type="<sql-server-2008 | sql-server-2005 | sql-server-2012 | sql-server-2014 | sql-azure>"  
  
/>  
```  
O atributo ' overwrite-if-exists ' é **false** por padrão.  
  
O atributo ' Project-Type ' é **SQL-Server-2008** por padrão.  
  
**Comando**  
  
Open-Project: abre um projeto existente.  
  
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
**Observação:** O aplicativo de console do SSMA para Access oferece suporte à compatibilidade com versões anteriores. Você pode abrir projetos criados pela versão anterior do SSMA.  
  
**Comando**  
  
Save-Project: salva o projeto de migração.  
  
**Script**  
  
**Exemplo de sintaxe:**  
  
```xml  
<save-project/>  
```  
**Comando**  
  
Close-Project: fecha o projeto de migração.  
  
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
  
Não há suporte para o recurso **procurar** da interface do usuário no console do.  
  
Os parâmetros de autenticação e **porta** do **Windows** não são aplicáveis ao se conectar a SQL Azure.  
  
Para obter mais informações sobre como criar arquivos de script, consulte [criando arquivos de script &#40;AccessToSQL&#41;](../../ssma/access/creating-script-files-accesstosql.md).  
  
**Comando**
  
Connect-Source-Database  
  
- Executa a conexão com o banco de dados de origem e carrega metadados de alto nível do banco de dados de origem, mas não todos os metadados.  
  
- Se a conexão com a origem não puder ser estabelecida, um erro será gerado e o aplicativo de console parará outra execução  
  
**Script**
  
A definição do servidor é recuperada do atributo Name definido para cada conexão na seção do servidor do arquivo de conexão do servidor ou do arquivo de script.  
  
**Exemplo de sintaxe:**  
  
```xml  
<connect-source-database  server="<server-unique-name>"/>  
```  
**Comando**  
  
Load-Access-Database: usado para carregar arquivos de banco de dados de acesso  
  
**Script**  
  
**Exemplo de sintaxe:**  
  
```xml  
<load-access-database  database-file="<Access-database>"/>  
```  
ou o  
  
```xml  
<load-access-database>  
  
  <access-database database-file="<Access-database1>"/>  
  
  <access-database database-file="<Access-database2>"/>  
  
</load-access-database>  
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
<force-load  
  
  object-name="<object-name>"  
  
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
  
- Reconecta-se ao banco de dados de origem, mas não carrega nenhum metadado diferente do comando Connect-Source-Database.  
  
- Se a conexão (re) com a origem não puder ser estabelecida, um erro será gerado e o aplicativo de console parará outra execução.  
  
**Script**
  
**Exemplo de sintaxe:**  
  
```xml  
<reconnect-source-database  server="<server-unique-name>"/>  
```

**Comando**
  
Connect-Target-Database  
  
- Conecta-se ao SQL Server de destino ou SQL Azure banco de dados e carrega metadados de alto nível do banco de dados de destino, mas não os metadados inteiramente.  
  
- Se a conexão com o destino não puder ser estabelecida, um erro será gerado e o aplicativo de console parará outra execução.  
  
**Script**
  
A definição do servidor é recuperada do atributo Name definido para cada conexão na seção do servidor do arquivo de conexão do servidor ou do arquivo de script  
  
**Exemplo de sintaxe:**  
  
```xml  
<connect-target-database  server="<server-unique-name>"/>  
```  

**Comando**
  
reconectar-destino-banco de dados  
  
- Reconecta-se ao banco de dados de destino, mas não carrega nenhum metadado, diferente do comando Connect-Target-Database.  
  
- Se a conexão (re) com o destino não puder ser estabelecida, um erro será gerado e o aplicativo de console interromperá a execução.  
  
**Script**
  
**Exemplo de sintaxe:**  
  
```xml  
<reconnect-target-database  server="<server-unique-name>"/>  
```  

## <a name="report-script-file-commands"></a>Comandos de arquivo de script de relatório

Os comandos de relatório geram relatórios sobre o desempenho de várias atividades do console do SSMA

**Comando**
  
gerar-avaliação-relatório  
  
- Gera relatórios de avaliação no banco de dados de origem.  
  
- Se a conexão do banco de dados de origem não for executada antes da execução desse comando, um erro será gerado e o aplicativo de console será encerrado.  
  
- Falha ao conectar-se ao servidor de banco de dados de origem durante a execução do comando, também resulta na finalização do aplicativo de console.  
  
**Script**

- `assessment-report-folder:`Especifica a pasta onde o relatório de avaliação pode ser armazenado. (atributo opcional)  
  
- `object-name:`Especifica os objetos considerados para geração de relatórios de avaliação (ele pode ter nomes de objetos individuais ou um nome de objeto de grupo).  
  
- `object-type:`Especifica o tipo do objeto especificado no atributo Object-Name (se a categoria de objeto for especificada, o tipo de objeto será "category").  
  
- `assessment-report-overwrite:`Especifica se a pasta do relatório de avaliação deve ser substituída, caso ela já exista.  
  
    **Valor padrão:** false. (atributo opcional)  
  
- `write-summary-report-to:`Especifica o caminho onde o relatório será gerado.  
  
    Se apenas o caminho da pasta for mencionado, clique em arquivo por nome **AssessmentReport &lt; n &gt; . XML** é criado. (atributo opcional)  
  
    A criação de relatório tem duas subcategorias adicionais:  
  
    - `report-errors`(= "true/false", com padrão como "false" (atributos opcionais))  
  
    - `verbose`(= "true/false", com padrão como "false" (atributos opcionais))  
  
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

ou o
  
```xml  
<generate-assessment-report  
  
  conversion-report-folder="<folder>"            (optional)  
  
  conversion-report-overwrite="<true/false>"     (optional)  
  
>  
    <metabase-object object-name="ssma.Procedures"  
  
        object-type="category"/>  
  
</generate-assessment-report>  
```  
  
## <a name="migration-script-file-commands"></a>Comandos de arquivo de script de migração

Os comandos de migração convertem o esquema de banco de dados de destino para o esquema de origem e migram os dados para o servidor de destino.  
  
A configuração de saída do console padrão para os comandos de migração é ' completo ' relatório de saída sem relatórios de erros detalhados: apenas Resumo no nó raiz da árvore do objeto de origem.  
  
**Comando**

converter esquema  
  
- Executa a conversão de esquema da origem para o esquema de destino.  
  
- Se a conexão de banco de dados de origem ou de destino não for executada antes da execução desse comando ou se a conexão com o servidor de banco de dados de origem ou destino falhar durante a execução do comando, um erro será gerado e o aplicativo de console será encerrado.  
  
**Script**

- `conversion-report-folder:`Especifica a pasta onde o relatório de avaliação pode ser armazenado. (atributo opcional)  
  
- `object-name:`Especifica os objetos de origem considerados para converter o esquema (ele pode ter nomes de objetos individuais ou um nome de objeto de grupo).  
  
- `object-type:`Especifica o tipo do objeto especificado no atributo Object-Name (se a categoria de objeto for especificada, o tipo de objeto será "category").  
  
- `conversion-report-overwrite:`Especifica se a pasta do relatório de avaliação deve ser substituída, caso ela já exista.  
  
    **Valor padrão:** false. (atributo opcional)  
  
- `write-summary-report-to:`Especifica o caminho onde o relatório será gerado.  
  
    Se apenas o caminho da pasta for mencionado, clique em arquivo por nome **SchemaConversionReport &lt; n &gt; . XML** é criado. (atributo opcional)  
  
    A criação de relatório tem duas subcategorias adicionais:  
  
    - `report-errors`(= "true/false", com padrão como "false" (atributos opcionais))  
  
    - `verbose`(= "true/false", com padrão como "false" (atributos opcionais))  
  
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

ou o  
  
```xml  
<convert-schema  
  
  conversion-report-folder="<folder>"         (optional)  
  
  conversion-report-overwrite="<true/false>"  (optional)  
  
  <metabase-object object-name="ssma.Procedures"  
  
    object-type="category"/>  
  
</convert-schema>  
```

**Comando**
  
migrar-dados  
  
- Migra os dados de origem para o destino.  
  
**Script**
  
- `object-name:`Especifica os objetos de origem considerados para a migração de dados (ele pode ter nomes de objetos individuais ou um nome de objeto de grupo).  
  
- `object-type:`Especifica o tipo do objeto especificado no atributo Object-Name (se a categoria de objeto for especificada, o tipo de objeto será "category").  
  
- `write-summary-report-to:`Especifica o caminho onde o relatório será gerado.  
  
    Se apenas o caminho da pasta for mencionado, clique em arquivo por nome **DataMigrationReport &lt; n &gt; . XML** é criado. (atributo opcional)  
  
    A criação de relatório tem duas subcategorias adicionais:  
  
    - `report-errors`(= "true/false", com padrão como "false" (atributos opcionais))  
  
    - `verbose`(= "true/false", com padrão como "false" (atributos opcionais))  
  
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

ou o  
  
```xml  
<migrate-data  
  
  object-name="ssma.Tables"  
  
  object-type="category"  
  
  write-summary-report-to="<filepath/folder>"  
  
  report-errors="true" verbose="true"/>  
```

**Comando**
  
link-Tables: esse comando vincula a tabela de origem (acesso) à tabela de destino.  
  
**Script**

**Exemplo de sintaxe:**  
  
```xml  
<link-tables>  
  
  <metabase-object object-name="AccessDatabase.table1" object-type="Tables"/>  
  
  <metabase-object object-name="AccessDatabase.table2" object-type="Tables"/>  
  
</link-tables>  
```

ou o  
  
```xml  
<link-tables>  
  
  <metabase-object object-name="AccessDatabase.Tables" object-type="category"/>  
  
</link-tables>  
```

**Comando**
  
Desvincular tabelas: esse comando desvincula a tabela de origem (acesso) da tabela de destino.  
  
**Script**
  
**Exemplos de sintaxe:**  
  
```xml  
<unlink-tables>  
  
  <metabase-object object-name="AccessDatabase.table1" object-type="Tables"/>  
  
  <metabase-object object-name="AccessDatabase.table2" object-type="Tables"/>  
  
</unlink-tables>  
```

ou o  
  
```xml  
<unlink-tables>  
  
  <metabase-object object-name="AccessDatabase.Tables" object-type="category"/>  
  
</unlink-tables>  
```  
  
## <a name="migration-preparation-script-file-commands"></a>Comandos de arquivo de script de preparação de migração

O comando de preparação de migração inicia o mapeamento de esquema entre os bancos de dados de origem e de destino.  
  
**Comando**
  
mapa-esquema: mapeamento de esquema do banco de dados de origem para o esquema de destino.  
  
**Script**
  
- `source-schema`Especifica o esquema de origem que pretendemos migrar.  
  
- `sql-server-schema`Especifica o esquema de destino onde queremos que ele seja migrado.  
  
**Exemplo de sintaxe:**  
  
```xml  
<map-schema source-schema="source-schema"  
  
            sql-server-schema="target-schema"/>  
```  
  
## <a name="manageability-commands"></a>Comandos de gerenciamento

Os comandos de gerenciamento ajudam a sincronizar os objetos de banco de dados de destino com o banco de dados de origem.  
  
A configuração de saída do console padrão para os comandos de migração é ' completo ' relatório de saída sem relatórios de erros detalhados: apenas Resumo no nó raiz da árvore do objeto de origem.  
  
**Comando**

sincronizar destino  
  
- Sincroniza os objetos de destino com o banco de dados de destino.  
  
- Se esse comando for executado no banco de dados de origem, você receberá um erro.  
  
- Se a conexão do banco de dados de destino não for executada antes da execução desse comando ou se a conexão com o servidor de banco de dados de destino falhar durante a execução do comando, um erro será gerado e o aplicativo de console será encerrado.  
  
**Script**
  
- `object-name:`Especifica os objetos de destino considerados para sincronização com o banco de dados de destino (ele pode ter nomes de objetos individuais ou um nome de objeto de grupo).  
  
- `object-type:`Especifica o tipo do objeto especificado no atributo Object-Name (se a categoria de objeto for especificada, o tipo de objeto será "category").  
  
- `on-error:`Especifica se os erros de sincronização devem ser especificados como avisos ou erro. Opções disponíveis para o no-erro:  
  
    - relatório-total-como-aviso  
  
    - relatório-cada-como-aviso  
  
    - script de falha  
  
- `report-errors-to:`Especifica o local do relatório de erros para a operação de sincronização (atributo opcional) se apenas o caminho da pasta for fornecido, o arquivo por nome **TargetSynchronizationReport.XML** será criado.  
  
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

ou o  
  
```xml  
<synchronize-target  
  
  object-name="ssma.dbo.Procedures"  
  
  object-type="category"/>  
```

ou o  
  
```xml  
<synchronize-target>  
  
  <metabase-object object-name="ssma.dbo.TT1"/>  
  
  <metabase-object object-name="ssma.dbo.TT2"/>  
  
  <metabase-object object-name="ssma.dbo.TT3"/>  
  
</synchronize-target>  
```

**Comando**
  
atualizar-do-banco de dados  
  
- Atualiza os objetos de origem do banco de dados.  
  
- Se esse comando for executado no banco de dados de destino, um erro será gerado.  
  
**Script**
  
Requer um ou vários nós da metabase como parâmetro de linha de comando.  
  
- `object-name:`Especifica os objetos de origem considerados para atualização do banco de dados de origem (ele pode ter nomes de objetos individuais ou um nome de objeto de grupo).  
  
- `object-type:`Especifica o tipo do objeto especificado no atributo Object-Name (se a categoria de objeto for especificada, o tipo de objeto será "category").  
  
- `on-error:`Especifica se é para especificar erros de atualização como avisos ou erro. Opções disponíveis para o no-erro:  
  
    - relatório-total-como-aviso  
  
    - relatório-cada-como-aviso  
  
    - script de falha  
  
- `report-errors-to:`Especifica o local do relatório de erros para a operação de atualização (atributo opcional) se apenas o caminho da pasta for fornecido, o arquivo por nome **SourceDBRefreshReport.XML** será criado.  
  
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

ou o  
  
```xml  
<refresh-from-database  
  
  object-name="ssma.Procedures"  
  
  object-type="category"/>  
```

ou o  
  
```xml  
<refresh-from-database>  
  
  <metabase-object object-name="ssma.TT_1"/>  
  
</refresh-from-database>  
```  
  
## <a name="script-generation-script-file-commands"></a>Comandos de arquivo de script de geração de script

Os comandos de geração de script ajudam a salvar a saída do console em um arquivo de script.  
  
**Comando**
  
salvar como script  
  
Usado para salvar os scripts dos objetos em um arquivo mencionado quando metabase = Target, essa é uma alternativa ao comando de sincronização no qual obtemos os scripts e executamos o mesmo no banco de dados de destino.  
  
**Script**
  
Requer um ou vários nós da metabase como parâmetro de linha de comando.  
  
- `object-name:`Especifica os objetos cujos scripts devem ser salvos. (Ele pode ter nomes de objetos individuais ou um nome de objeto de grupo)  
  
- `object-type:`Especifica o tipo do objeto especificado no atributo Object-Name (se a categoria de objeto for especificada, o tipo de objeto será "category").  
  
- `metabase:`Especifica se é a metabase de origem ou de destino.  
  
- `destination:`Especifica o caminho ou a pasta em que o script deve ser salvo; Se o nome do arquivo não for fornecido, um nome de arquivo no formato (object_name valor do atributo). out  
  
- `overwrite:`Se for true, ele substituirá se os mesmos nomes de fileexistirem. Ele pode ter os valores (true/false).  
  
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

ou o  
  
```xml  
<save-as-script  
  
  metabase="<source/target>"  
  
  destination="<file/folder>"  
  
    <metabase-object object-name="ssma.dbo.Procedures"  
  
                     object-type="category"/>  
  
</save-as-script>  
```  
  
## <a name="next-steps"></a>Próximas etapas

Para obter informações sobre opções de linha de comando, consulte [Opções de linha de comando no console do SSMA &#40;AccessToSQL&#41;](../../ssma/access/command-line-options-in-ssma-console-accesstosql.md) .  
  
Para obter informações sobre arquivos de script de console de exemplo, consulte [trabalhando com o script de console de exemplo FilesExecuting The SSMA console &#40;AccessToSQL&#41;](../../ssma/access/working-sample-console-script-filesexecuting-ssma-console-accesstosql.md)  
  
A próxima etapa depende dos requisitos do seu projeto:  
  
- Para especificar uma senha ou exportar/importar senhas, consulte [Gerenciando senhas &#40;AccessToSQL&#41;](../../ssma/access/managing-passwords-accesstosql.md).  
  
- Para gerar relatórios, consulte [gerando relatórios &#40;AccessToSQL&#41;](../../ssma/access/generating-reports-accesstosql.md).  
  
- Para solucionar problemas no console do, consulte solução de problemas [&#40;AccessToSQL&#41;](../../ssma/access/troubleshooting-accesstosql.md).  
