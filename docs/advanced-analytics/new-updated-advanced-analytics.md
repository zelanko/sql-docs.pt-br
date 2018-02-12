---
title: Atualizado - Advanced Analytics para documentos do SQL Server | Microsoft Docs
description: "Trechos de código de exibição de conteúdo atualizado recentemente alterada na documentação de, para Advanced Analytics para o Microsoft SQL Server."
manager: craigg
author: MightyPen
ms.author: genemi
ms.topic: article
ms.custom: UpdArt.exe
ms.suite: sql
ms.prod_service: sql-non-specified
ms.component: advanced-analytics
ms.date: 02/03/2018
ms.openlocfilehash: a40a991abe8f82b553ae621c24f9d4e81a92f8f6
ms.sourcegitcommit: 99102cdc867a7bdc0ff45e8b9ee72d0daade1fd3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/11/2018
---
# <a name="new-and-recently-updated-advanced-analytics-for-sql-server"></a>Novos e atualizados recentemente: Advanced Analytics para o SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Quase todos os dias Microsoft atualiza alguns de seus artigos existentes em seu [Docs.Microsoft.com](http://docs.microsoft.com/) site de documentação. Este artigo exibe trechos de artigos atualizados recentemente. Links para novos artigos também podem ser listados.

Este artigo é gerado por um programa que é executado novamente periodicamente. Ocasionalmente, um trecho pode aparecer com formatação imperfeita, ou como a redução do artigo de origem. Imagens nunca são exibidas aqui.

Atualizações recentes são relatadas para o intervalo de data a seguir e o assunto:



- *Intervalo de datas das atualizações:* &nbsp; **2017-12-03** &nbsp; - para - &nbsp; **2018-02-03**
- *Área de assunto:* &nbsp; **Advanced Analytics para o SQL Server**.

<!-- Repo = 'MicrosoftDocs/sql-docs'.   Branch = 'live'. -->



&nbsp;

## <a name="new-articles-created-recently"></a>Novos artigos criados recentemente

Os links a seguir direcionam para novos artigos que foram adicionados recentemente.


1. [Instalar os novos pacotes Python no SQL Server](python/install-additional-python-packages-on-sql-server.md)



&nbsp;

## <a name="updated-articles-with-excerpts"></a>Artigo atualizado com trechos

Esta seção exibe os trechos de atualizações coletados de artigos que passaram por uma atualização extensa recentemente.

Os trechos exibidos aqui aparecerão separados de seu contexto de semântico apropriado. Além disso, às vezes, um trecho é separado da sintaxe de markdown importantes que circunda no artigo real. Portanto, esses trechos são para apenas diretrizes gerais. Os trechos só permitem que você saber se seus interesses garantem a pena clique e visite o artigo real.

Para essas e outras razões, não copiar o código desses trechos e não em como verdadeiro exato qualquer trecho de texto. Em vez disso, consulte o artigo real.





&nbsp;

<a name="compactupdatedlist"/>

### <a name="compact-list-of-articles-updated-recently"></a>Lista compacta dos artigos atualizados recentemente

Essa lista compacta fornece links para todos os artigos atualizados listados na seção Trechos.

1. [Problemas conhecidos nos serviços de aprendizado de máquina](#TitleNum_1)
2. [Converter o código de R para execução no banco de dados](#TitleNum_2)
3. [Determinar quais pacotes de R são instalados no SQL Server](#TitleNum_3)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-known-issues-in-machine-learning-servicesknown-issues-for-sql-server-machine-learning-servicesmd"></a>1. &nbsp;[Problemas conhecidos de serviços de aprendizado de máquina](known-issues-for-sql-server-machine-learning-services.md)

*Atualizado em: 2018-02-02* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([próxima](#TitleNum_2))

<!-- Source markdown line 163.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 c6f46adcf795c43f818120b88407a3a89304cb27 c781562605f5cd77f6c43bfe5e89810cb72ceae0  (PR=4789  ,  Filename=known-issues-for-sql-server-machine-learning-services.md  ,  Dirpath=docs\advanced-analytics\  ,  MergeCommitSha40=386bfb688843bac7fa4d83dc1cfef94dd19db110) -->



Para mais problemas conhecidos que podem afetar a soluções de R, consulte o [Server de aprendizado de máquina](https://docs.microsoft.com/machine-learning-server/resources-known-issues) site.

**Acesso negado aviso durante a execução de scripts do R no SQL Server em um local diferente do padrão**


Se a instância do SQL Server foi instalada em um local diferente do padrão, como fora de `Program Files` pasta, o aviso ACCESS_DENIED é gerado quando você tentar executar scripts que instalam um pacote. Por exemplo:

> *Em normalizePath(path.expand(path), winslash, mustWork): o caminho [2] = "~ExternalLibraries/R/8/1": acesso negado*

O motivo é que uma função R tenta ler o caminho e falhará se o grupo de usuários internos **SQLRUserGroup**, não tem acesso de leitura. O aviso é gerado não bloqueia a execução do script R atual, mas o aviso pode ocorrer repetidamente, sempre que o usuário executa qualquer outro script de R.

Se você tiver instalado o SQL Server para o local padrão, esse erro não ocorrer, porque todos os usuários do Windows têm permissões de leitura no `Program Files` pasta.

Esse problema será corrigido em uma versão futura do serviço. Como alternativa, forneça o grupo **SQLRUserGroup**, com acesso de leitura para todas as pastas pai dos `ExternalLibraries`.

**Erro de serialização entre versões antigas e novas de RevoScaleR**


Quando você passar um modelo usando um formato serializado para uma instância remota do SQL Server, você poderá receber o erro:

> *Erro no memDecompress (dados, tipo = descompactar) erro interno -3 no memDecompress(2).*

Esse erro é gerado se você salvou o modelo usando uma versão recente da função de serialização, [rxSerializeModel](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxserializemodel), mas a instância do SQL Server onde Desserialize o modelo tem uma versão mais antiga das APIs RevoScaleR, do SQL Servidor de 2017 CU2 ou anterior.



&nbsp;

&nbsp;

---

<a name="TitleNum_2"/>

### <a name="2-nbsp-converting-r-code-for-execution-in-databaserconverting-r-code-for-use-in-sql-servermd"></a>2. &nbsp;[Código R convertendo para execução no banco de dados](r/converting-r-code-for-use-in-sql-server.md)

*Atualizado em: 2018-01-08* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([anterior](#TitleNum_1) | [próxima](#TitleNum_3))

<!-- Source markdown line 136.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 a1d156fac1af5813ef75965071686b177e2aede7 fc8beff0aa0d7ea298e493b90984875e81e9143e  (PR=4493  ,  Filename=converting-r-code-for-use-in-sql-server.md  ,  Dirpath=docs\advanced-analytics\r\  ,  MergeCommitSha40=f486d12078a45c87b0fcf52270b904ca7b0c7fc8) -->



**Empacotar seu código R em um procedimento armazenado**

+ Se seu código é relativamente simple, você pode inseri-lo em uma função definida pelo usuário do T-SQL sem modificação, conforme descrito nesses exemplos:

    + [Criar uma função de R que é executado em rxExec](r/../tutorials/deepdive-create-a-simple-simulation.md)
    + [Engenharia de recurso usando o T-SQL e R](r/../tutorials/sqldev-create-data-features-using-t-sql.md)

+ Se o código for mais complexo, use o pacote R **sqlrutils** para converter seu código. Esse pacote foi projetado para ajudar usuários experientes do R a escrever código bom procedimento armazenado.

    A primeira etapa é reescrever o código de R como uma única função com claramente definidas entradas e saídas.

    Em seguida, use o **sqlrutils** pacote para gerar a entrada e saída no formato correto. O **sqlrutils** pacote gera o código de procedimento armazenado completa para você e também pode registrar o procedimento armazenado no banco de dados.

    Para obter mais informações e exemplos, consulte [SqlRUtils](r/../r/generating-an-r-stored-procedure-for-r-code-using-the-sqlrutils-package.md).

**Integrar com outros fluxos de trabalho**

+ Utilizar ferramentas de T-SQL e os processos ETL. Execute engenharia de recurso, a extração do recurso e a limpeza de dados com antecedência como parte dos fluxos de trabalho de dados.

    Quando você estiver trabalhando em um ambiente de desenvolvimento R dedicado, como ferramentas de R para Visual Studio ou RStudio, você pode extrair dados em seu computador, analisar os dados interativamente e, em seguida, gravar ou exibir os resultados.

    No entanto, quando o código de R autônomo é migrado para o SQL Server, grande parte desse processo pode ser simplificado ou delegado para outras ferramentas do SQL Server.

+ Use as estratégias de visualização segura e assíncrona.

    Os usuários do SQL Server geralmente não podem acessar arquivos no servidor e ferramentas de cliente SQL normalmente não oferecem suporte a dispositivo de gráficos de R. Se você gerar gráficos ou outros elementos gráficos como parte da solução, considere exportar os gráficos como dados binários e salvando em uma tabela ou gravação.



&nbsp;

&nbsp;

---

<a name="TitleNum_3"/>

### <a name="3-nbsp-determine-which-r-packages-are-installed-on-sql-serverrdetermine-which-packages-are-installed-on-sql-servermd"></a>3. &nbsp;[Determinar quais pacotes de R são instalados no SQL Server](r/determine-which-packages-are-installed-on-sql-server.md)

*Atualizado em: 24-01-2018* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([anterior](#TitleNum_2))

<!-- Source markdown line 78.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 9a065066398843a4bed318fa46d4982d712915a9 7a1df11f57e7bbf0abc37d3aa240dedd2b88c45f  (PR=4715  ,  Filename=determine-which-packages-are-installed-on-sql-server.md  ,  Dirpath=docs\advanced-analytics\r\  ,  MergeCommitSha40=9e6a029456f4a8daddb396bc45d7874a43a47b45) -->




**Obter a versão e o local da biblioteca**


O exemplo a seguir obtém a localização da biblioteca de RevoScaleR no contexto de computação local e a versão do pacote.

```
rxFindPackage(RevoScaleR, "local")
packageVersion("RevoScaleR")
```

**Determinar o caminho de biblioteca usada pelo SQL Server**


Se você atualizou a componentes usando associação de aprendizado de máquina, pode alterar o caminho para a biblioteca de R. Quando isso acontece, atalhos anteriores das ferramentas podem fazer referência a uma versão anterior. Para ter certeza da versão pacote e o caminho usado pelo SQL Server, você pode executar um comando como o seguinte:

```
EXEC sp_execute_external_script
    @language =N'R',
    @script=N'
    sql_r_path <- rxSqlLibPaths("local")
      print(sql_r_path)
    version_info <-packageVersion("RevoScaleR")
      print(version_info)'
```

**Resultados**

```
STDOUT message(s) from external script:
[1] "C:/Program Files/Microsoft SQL Server/MSSQL14.MSSQLSERVER1000/R_SERVICES/library"
[1] '9.2.1'
```







## <a name="similar-articles-about-new-or-updated-articles"></a>Artigos semelhantes sobre artigos novos ou atualizados

Esta seção lista artigos muito semelhantes a artigos atualizados recentemente em outras áreas de assunto, em nosso repositório público GitHub.com: [MicrosoftDocs/sql-docs](https://github.com/MicrosoftDocs/sql-docs/).


#### <a name="subject-areas-that-do-have-new-or-recently-updated-articles"></a>Áreas de assunto que *fazer* new ou recentemente atualizou artigos


- [Novo + atualizado (1 + 3):&nbsp; **Advanced Analytics para o SQL** documentos](../advanced-analytics/new-updated-advanced-analytics.md)
- [Novo + atualizado (0 + 1):&nbsp; **Analytics Platform System para SQL** documentos](../analytics-platform-system/new-updated-analytics-platform-system.md)
- [Novo + atualizado (0 + 1):&nbsp; **conectar-se ao SQL** documentos](../connect/new-updated-connect.md)
- [Novo + atualizado (0 + 1):&nbsp; **mecanismo de banco de dados do SQL** documentos](../database-engine/new-updated-database-engine.md)
- [Novo + atualizado (12 + 1): **Integration Services para SQL** documentos](../integration-services/new-updated-integration-services.md)
- [Novo + atualizado (6 + 2):&nbsp; **Linux para o SQL** documentos](../linux/new-updated-linux.md)
- [Novo + atualizado (15 + 0): **PowerShell para SQL** documentos](../powershell/new-updated-powershell.md)
- [Novo + atualizado (2 + 9):&nbsp; **bancos de dados relacionais do SQL** documentos](../relational-databases/new-updated-relational-databases.md)
- [Novo + atualizado (1 + 0):&nbsp; **Reporting Services para SQL** documentos](../reporting-services/new-updated-reporting-services.md)
- [Novo + atualizado (1 + 1):&nbsp; **Studio de operações SQL** documentos](../sql-operations-studio/new-updated-sql-operations-studio.md)
- [Novo + atualizado (1 + 1):&nbsp; **Microsoft SQL Server** documentos](../sql-server/new-updated-sql-server.md)
- [Novo + atualizado (0 + 1):&nbsp; **SQL Server Data Tools (SSDT)** documentos](../ssdt/new-updated-ssdt.md)
- [Novo + atualizado (1 + 2):&nbsp; **SQL Server Management Studio (SSMS)** documentos](../ssms/new-updated-ssms.md)
- [Novo + atualizado (0 + 2):&nbsp; **Transact-SQL** documentos](../t-sql/new-updated-t-sql.md)



#### <a name="subject-areas-that-do-not-have-any-new-or-recently-updated-articles"></a>Entidade áreas que fazer *não* qualquer novo ou recentemente atualizou artigos


- [Novo + Atualizado (0 + 0): documentos sobre **DMA (Assistente de Migração de Dados) para o SQL**](../dma/new-updated-dma.md)
- [Novo + atualizado (0 + 0): **ActiveX Data Objects (ADO) para o SQL** documentos](../ado/new-updated-ado.md)
- [Novo + Atualizado (0+0): documentos sobre o **Analysis Services para SQL**](../analysis-services/new-updated-analysis-services.md)
- [Novo + atualizado (0 + 0): **Data Quality Services para SQL** documentos](../data-quality-services/new-updated-data-quality-services.md)
- [Novo + atualizado (0 + 0): **extensões DMX (Data Mining) para o SQL** documentos](../dmx/new-updated-dmx.md)
- [Novo + Atualizado (0+0): documentos sobre o **MDS (Master Data Services) para SQL**](../master-data-services/new-updated-master-data-services.md)
- [Novo + atualizado (0 + 0): **MDX (Multidimensional Expressions) para SQL** documentos](../mdx/new-updated-mdx.md)
- [Novo + atualizado (0 + 0): **ODBC (conectividade aberta de banco de dados) para o SQL** documentos](../odbc/new-updated-odbc.md)
- [Novo + atualizado (0 + 0): **exemplos para SQL** documentos](../sample/new-updated-sample.md)
- [Novo + atualizado (0 + 0): **Migration Assistant SSMA (SQL Server)** documentos](../ssma/new-updated-ssma.md)
- [Novo + Atualizado (0 + 0): documentos de **Ferramentas para SQL**](../tools/new-updated-tools.md)
- [Novo + atualizado (0 + 0): **XQuery para o SQL** documentos](../xquery/new-updated-xquery.md)


