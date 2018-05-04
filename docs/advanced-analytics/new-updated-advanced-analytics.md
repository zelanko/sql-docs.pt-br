---
title: Atualizado - Advanced Analytics para documentos do SQL Server | Microsoft Docs
description: Trechos de código de exibição de conteúdo atualizado recentemente alterada na documentação de, para Advanced Analytics para o Microsoft SQL Server.
manager: craigg
author: MightyPen
ms.author: genemi
ms.topic: article
ms.custom: UpdArt.exe
ms.suite: sql
ms.technology: release-landing
ms.prod: sql
ms.prod_service: sql-non-specified
ms.component: advanced-analytics
ms.date: 04/28/2018
ms.openlocfilehash: bbce32579b54647e167c25d2708a80027ae0e678
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="new-and-recently-updated-advanced-analytics-for-sql-server"></a>Novos e atualizados recentemente: Advanced Analytics para o SQL Server



Quase todos os dias Microsoft atualiza alguns de seus artigos existentes em seu [Docs.Microsoft.com](http://docs.microsoft.com/) site de documentação. Este artigo exibe trechos de artigos atualizados recentemente. Links para novos artigos também podem ser listados.

Este artigo é gerado por um programa que é executado novamente periodicamente. Ocasionalmente, um trecho pode aparecer com formatação imperfeita, ou como a redução do artigo de origem. Imagens nunca são exibidas aqui.

Atualizações recentes são relatadas para o intervalo de data a seguir e o assunto:



- *Intervalo de datas das atualizações:* &nbsp; **2018-02-03** &nbsp; - para - &nbsp; **2018-04-28**
- *Área de assunto:* &nbsp; **Advanced Analytics para o SQL Server**.

<!-- Repo = 'MicrosoftDocs/sql-docs'.   Branch = 'live'. -->



&nbsp;

## <a name="new-articles-created-recently"></a>Novos artigos criados recentemente

Os links a seguir direcionam para novos artigos que foram adicionados recentemente.


1. [Instalar o SQL Server 2017 máquina Learning Services (no banco de dados) no Windows](install/sql-machine-learning-services-windows-install.md)
2. [Instalar o SQL Server (autônomo) no Windows de aprendizado de máquina de servidor de 2017](install/sql-machine-learning-standalone-windows-install.md)
3. [Instalar componentes de aprendizado de máquina do SQL Server a partir da linha de comando](install/sql-ml-component-commandline-install.md)
4. [Instalar componentes sem acesso à internet de aprendizado de máquina do SQL Server](install/sql-ml-component-install-without-internet-access.md)
5. [Instalar o SQL Server 2016 R Services (no banco de dados)](install/sql-r-services-windows-install.md)
6. [Instalar o SQL Server 2016 R Server (autônomo)](install/sql-r-standalone-windows-install.md)
7. [Configurar o Python ferramentas de cliente para uso com o aprendizado de máquina do SQL Server](python/setup-python-client-tools-sql.md)
8. [Usar o modelo de Python no SQL para treinamento e pontuação](tutorials/train-score-using-python-in-tsql.md)
9. [Encapsular o código Python em um procedimento armazenado](tutorials/wrap-python-in-tsql-stored-procedure.md)
10. [O que são os Serviços de Machine Learning do SQL Server?](what-is-sql-server-machine-learning.md)
11. [Eventos estendidos para monitoramento de instruções PREDICT](xe-event-predict-tsql.md)



&nbsp;

## <a name="updated-articles-with-excerpts"></a>Artigo atualizado com trechos

Esta seção exibe os trechos de atualizações coletados de artigos que passaram por uma atualização extensa recentemente.

Os trechos exibidos aqui aparecerão separados de seu contexto de semântico apropriado. Além disso, às vezes, um trecho é separado da sintaxe de markdown importantes que circunda no artigo real. Portanto, esses trechos são para apenas diretrizes gerais. Os trechos só permitem que você saber se seus interesses garantem a pena clique e visite o artigo real.

Para essas e outras razões, não copiar o código desses trechos e não em como verdadeiro exato qualquer trecho de texto. Em vez disso, consulte o artigo real.





&nbsp;

<a name="compactupdatedlist"/>

### <a name="compact-list-of-articles-updated-recently"></a>Lista compacta dos artigos atualizados recentemente

Essa lista compacta fornece links para todos os artigos atualizados listados na seção Trechos.

1. [Exibindo R ou pacotes Python instalados no SQL Server](#TitleNum_1)
2. [Instalar os modelos no SQL Server de aprendizado de máquina previamente treinada](#TitleNum_2)
3. [Configurar um cliente de ciência de dados para o desenvolvimento de R no SQL Server](#TitleNum_3)
4. [R Services (no banco de dados) e aprendizado de máquina do SQL Server](#TitleNum_4)
5. [Executar Python usando o T-SQL](#TitleNum_5)
6. [Usar o Python com revoscalepy para criar um modelo](#TitleNum_6)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-viewing-r-or-python-packages-installed-on-sql-serverrdetermine-which-packages-are-installed-on-sql-servermd"></a>1. &nbsp; [Exibindo R ou pacotes Python instalados no SQL Server](r/determine-which-packages-are-installed-on-sql-server.md)

*Atualizado em: 2018-04-19* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([próxima](#TitleNum_2))

<!-- Source markdown line 208.  ms.author= heidist.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 7a1df11f57e7bbf0abc37d3aa240dedd2b88c45f ec6859ac91b27539dc36f21aec82c99937c0187a  (PR=5610  ,  Filename=determine-which-packages-are-installed-on-sql-server.md  ,  Dirpath=docs\advanced-analytics\r\  ,  MergeCommitSha40=f1f96a990644c0d6cfa5a1d88ccee959cab6c2b2) -->



**Python**


Este exemplo retorna a lista de pastas incluídas no Python `sys.path` variável. A lista inclui o diretório atual e o caminho de biblioteca padrão.

```
EXEC sp_execute_external_script
  @language =N'Python',
  @script=N'import sys; print("\n".join(sys.path))'
```

**Resultados**

```
C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\python35.zip
C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\DLLs
C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\lib
C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES
C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\lib\site-packages
C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\lib\site-packages\Sphinx-1.5.4-py3.5.egg
C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\lib\site-packages\win32
C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\lib\site-packages\win32\lib
C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\lib\site-packages\Pythonwin
C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\lib\site-packages\setuptools-27.2.0-py3.5.egg
```

Para obter mais informações sobre a variável `sys.path` e como ele é usado para definir o caminho de pesquisa do interpretador para módulos, consulte o [documentação Python](https://docs.python.org/2/tutorial/modules.html#the-module-search-path)



&nbsp;

&nbsp;

---

<a name="TitleNum_2"/>

### <a name="2-nbsp-install-pre-trained-machine-learning-models-on-sql-serverrinstall-pretrained-models-sql-servermd"></a>2. &nbsp; [Instalar os modelos no SQL Server de aprendizado de máquina previamente treinada](r/install-pretrained-models-sql-server.md)

*Atualizado em: 2018-04-12* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([anterior](#TitleNum_1) | [próxima](#TitleNum_3))

<!-- Source markdown line 140.  ms.author= heidist.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 aa03623d819750d4919feb7910b07ec1875bb509 7382228fa68b04b500a5fde73c29995e12aa20ac  (PR=5504  ,  Filename=install-pretrained-models-sql-server.md  ,  Dirpath=docs\advanced-analytics\r\  ,  MergeCommitSha40=f34765240b79a44167ca2af90f97a0fdd47c41d2) -->



1. Inicie o instalador baseado no Windows separado para cada uma [R Server](https://docs.microsoft.com/machine-learning-server/rebranding-microsoft-r-server) ou [Server de aprendizado de máquina](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install).

2. Selecione os idiomas que você deseja atualizar e selecione o **Pre-trained modelos** opção.

    > [!TIP]
    > Se você executou anteriormente o instalador para atualizar o R Server (autônomo) e deseja adicionar os modelos treinados previamente, deixe todas as seleções anteriores **como**e selecione apenas a versão anterior **-treinado modelos** opção . **Não** desmarque todas as opções selecionadas anteriormente; se você fizer isso, o instalador remove os componentes.

    É recomendável que você aceite as configurações padrão para os locais de modelo.

3. Clique em **Continuar**.

4. Aceite todos os prompts, incluindo os contratos de licença.

Após a conclusão da instalação, você deve executar algumas etapas adicionais para registrar os modelos treinados previamente.

1. Abra um prompt de comando do Windows **como administrador**.

2. Navegue até a pasta de inicialização de instalação para R Server (autônomo), que também contém o instalador do Microsoft R.

3. Execute `RSetup.exe` e indicar o componente a ser instalado, a versão e a pasta que contém os arquivos de origem do modelo, usando a seguinte sintaxe:

    `RSetup.exe /install /component MLM /version <version> /language 1033 /destdir "~\R_SERVER\library\MicrosoftML\mxLibs\x64"`

    Os valores a seguir têm suporte para o parâmetro version:



&nbsp;

&nbsp;

---

<a name="TitleNum_3"/>

### <a name="3-nbsp-set-up-a-data-science-client-for-r-development-on-sql-serverrset-up-a-data-science-clientmd"></a>3. &nbsp; [Configurar um cliente de ciência de dados para o desenvolvimento de R no SQL Server](r/set-up-a-data-science-client.md)

*Atualizado em: 2018-04-12* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([anterior](#TitleNum_2) | [próxima](#TitleNum_4))

<!-- Source markdown line 39.  ms.author= heidist.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 0583f8febcedc5dc2e14ca1a8073ca204ca37987 3d50ad8f35f2985944741a9b2211a461df2c13e4  (PR=5504  ,  Filename=set-up-a-data-science-client.md  ,  Dirpath=docs\advanced-analytics\r\  ,  MergeCommitSha40=f34765240b79a44167ca2af90f97a0fdd47c41d2) -->



**Ferramentas de R**


Quando você instala o R com o SQL Server, você obtém as mesmas ferramentas de R que são instaladas com qualquer **base** instalação do R, como RGui, Rterm e assim por diante. Portanto, tecnicamente, você tem todas as ferramentas que você precisa para desenvolver e testar o código de R.

As seguintes ferramentas de R padrão são incluídas em um *base instalação* do R e, portanto, são instalados por padrão.

+ **O RTerm**: um terminal de linha de comando para execução de scripts de R

+ **RGui.exe**: um editor interativo simples de R. Os argumentos de linha de comando são os mesmos para RGui.exe e RTerm.

+ **RScript**: uma ferramenta de linha de comando para executar scripts R no modo de lote.

Para localizar essas ferramentas, determine a biblioteca de R instalado quando você configurar o SQL Server ou a recurso de aprendizado de máquina autônomo. Por exemplo, em uma instalação padrão, as ferramentas de R estão localizadas nessas pastas:

+ SQL Server 2016 R Services: `~\Program Files\Microsoft SQL Server\MSSQL13.<instancename>\R_SERVICES\bin\x64`
+ Microsoft R Server autônomo: `~\Program Files\Microsoft R\R_SERVER\bin\x64`
+ SQL Server 2017 aprendizado de máquina serviços: `~\Program Files\Microsoft SQL Server\MSSQL14.<instancename>\R_SERVICES\bin\x64`
+ Server (autônomo) de aprendizado de máquina: `~\Program Files\Microsoft\ML Server\R_SERVER\bin\x64`

Se você precisar de ajuda com as ferramentas de R, basta abrir **RGui**, clique em **ajuda**e selecione uma das opções

**Cliente do Microsoft R**


O cliente do Microsoft R é um download gratuito que permite o acesso aos pacotes RevoScaleR para uso de desenvolvimento. Instalando o cliente do R, você pode criar soluções de R que podem ser executadas em todos os contextos de computação com suporte, incluindo a análise do SQL Server no banco de dados e computação distribuída de R no Hadoop, Spark ou Linux usando o servidor de aprendizado de máquina.

Se você já tiver instalado um ambiente de desenvolvimento R diferente, como RStudio, certifique-se reconfigurar o ambiente para usar as bibliotecas e executáveis fornecidos pelo cliente do Microsoft R. Ao fazer isso, você pode usar todos os recursos do pacote RevoScaleR, embora o desempenho será limitado.



&nbsp;

&nbsp;

---

<a name="TitleNum_4"/>

### <a name="4-nbsp-sql-server-machine-learning-and-r-services-in-databasersql-server-r-servicesmd"></a>4. &nbsp; [R Services (no banco de dados) e aprendizado de máquina do SQL Server](r/sql-server-r-services.md)

*Atualizado em: 2018-04-12* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([anterior](#TitleNum_3) | [próxima](#TitleNum_5))

<!-- Source markdown line 83.  ms.author= heidist.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 b1a95a7f6d391a518762eb271e8ea7e0d684d403 7fbfabf62917e03e2bcb99d297e1c9d0f0604440  (PR=5504  ,  Filename=sql-server-r-services.md  ,  Dirpath=docs\advanced-analytics\r\  ,  MergeCommitSha40=f34765240b79a44167ca2af90f97a0fdd47c41d2) -->



Escolha a melhor linguagem para a tarefa. R é melhor para cálculos estatísticos que são difíceis de implementar usando SQL. Para operações baseadas em conjunto de dados, aproveite a potência do *{incluídos-conteúdo-entrar-aqui}* para alcançar desempenho máximo. Use o mecanismo de banco de dados na memória para cálculos muito rápidos sobre colunas.

**Etapa 4: Otimizar sua solução**


Quando o modelo estiver pronto para dimensionar nos dados da empresa, o cientista de dados geralmente funciona com o desenvolvedor do DBA ou SQL para otimizar os processos, como:

+ Engenharia de recursos
+ Ingestão de dados e transformação de dados
+ Pontuação

Tradicionalmente, os cientistas de dados usando R teve problemas com desempenho e escala, especialmente ao usar o conjunto de dados grande. Isso ocorre porque a implementação de tempo de execução comum é de thread único e pode acomodar apenas os conjuntos de dados que cabem na memória disponível no computador local. Integração com serviços de aprendizado de máquina do SQl Server fornece vários recursos para melhorar o desempenho, com mais dados:

+ **RevoScaleR**: pacote R este contém implementações de algumas das funções R mais populares, remodeladas para oferecer paralelismo e escalabilidade. O pacote também inclui funções que aumentam ainda mais o desempenho e a escala enviando cálculos para o *{incluídos-conteúdo-entrar-aqui}* computador, que geralmente tem muito mais memória e potência computacional.

+ **revoscalepy**. Essa biblioteca do Python, disponível no SQL Server de 2017, implementa funções mais populares em RevoScaleR, como contextos de computação remota e processamento distribuído de muitos algoritmos que oferecem suporte.

**Recursos**

+ [Estudo de caso de desempenho]
+ [R e otimização de dados]

**Etapa 5: Implantar e consumir**




&nbsp;

&nbsp;

---

<a name="TitleNum_5"/>

### <a name="5-nbsp-run-python-using-t-sqltutorialsrun-python-using-t-sqlmd"></a>5. &nbsp; [Executar Python usando o T-SQL](tutorials/run-python-using-t-sql.md)

*Atualizado em: 2018-04-11* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([anterior](#TitleNum_4) | [próxima](#TitleNum_6))

<!-- Source markdown line 306.  ms.author= heidist.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 bde8c6476df259d225847c08224cefd02f3529d5 cad56997abe7928b588ac4a0302384c5edc1ede5  (PR=5497  ,  Filename=run-python-using-t-sql.md  ,  Dirpath=docs\advanced-analytics\tutorials\  ,  MergeCommitSha40=86c4e1879c5914676b9da384ab101b50b4a63bf1) -->



2. Observe que os valores de índice não são produzidas, mesmo se você usar o índice para obter valores específicos do data.frame.

    **Resultados**

    |ResultValue|
    |------|
    |0.5|
    |2|

**Valores de saída em data.frame usando um índice**


Vamos ver como a conversão para um data.frame funciona com nossas duas séries que contém os resultados de operações matemáticas simples. O primeiro tem um índice de valores sequenciais gerados pelo Python. O segundo usa um índice arbitrário de valores de cadeia de caracteres.

1. Este exemplo obtém um valor da série que usa um índice de inteiro.

```
    EXECUTE sp_execute_external_script
    @language = N'Python',
    @script = N'
    import pandas as pd
    a = 1
    b = 2
    c = a/b
    d = a*b
    s = pandas.Series([c,d])
    print(s)
    df = pd.DataFrame(s, index=[1])
    OutputDataSet = df
    '
    WITH RESULT SETS (( ResultValue float ))
```

Lembre-se de que o índice gerado automaticamente começa em 0. Tente usar um fora do valor de índice de intervalo e ver o que acontece.

2. Agora vamos em um único valor de outro quadro de dados que tem um índice de cadeia de caracteres.

```
    EXECUTE sp_execute_external_script
    @language = N'Python',
    @script = N'
    import pandas as pd
    a = 1
    b = 2
    c = a/b
    s = pandas.Series(c, index =["simple math example 1", "simple math example 2"])
    print(s)
    df = pd.DataFrame(s, index=["simple math example 1"])
    OutputDataSet = df
    '
    WITH RESULT SETS (( ResultValue float ))
```

**Resultados**

|ResultValue|
|------|
|0.5|

Se você tentar usar um índice numérico para obter um valor desta série, você obterá um erro.



&nbsp;

&nbsp;

---

<a name="TitleNum_6"/>

### <a name="6-nbsp-use-python-with-revoscalepy-to-create-a-modeltutorialsuse-python-revoscalepy-to-create-modelmd"></a>6. &nbsp; [Usar o Python com revoscalepy para criar um modelo](tutorials/use-python-revoscalepy-to-create-model.md)

*Atualizado em: 2018-04-11* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([anterior](#TitleNum_5))

<!-- Source markdown line 22.  ms.author= heidist.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 5b642b391ca571412c30c8470875d3d4d3c57246 bd83387eb8a1076a1396bbd48dca12872843aa2f  (PR=5497  ,  Filename=use-python-revoscalepy-to-create-model.md  ,  Dirpath=docs\advanced-analytics\tutorials\  ,  MergeCommitSha40=86c4e1879c5914676b9da384ab101b50b4a63bf1) -->



Se você instalou uma versão de pré-lançamento do SQL Server 2017, você deve atualizar para pelo menos a versão RTM. Versões mais recentes do serviço tem contínuo expandir e melhorar a funcionalidade de Python. Alguns recursos deste tutorial podem não funcionar em versões de pré-lançamento.

+ Este exemplo usa um ambiente de Python predefinido, denominado `PYTEST_SQL_SERVER`. O ambiente foi configurado para conter **revoscalepy** e outras bibliotecas necessárias.

    Se você não tiver um ambiente configurado para executar o Python, você deve fazer isso separadamente. Uma discussão sobre como criar ou modificar os ambientes de Python está fora do escopo deste tutorial. Para obter mais informações sobre como configurar um cliente do Python que contém as bibliotecas corretas, consulte [cliente instalar o Python](https://docs.microsoft.com/machine-learning-server/install/python-libraries-interpreter) e [Python links para ferramentas](https://docs.microsoft.com/machine-learning-server/python/quickstart-python-tools).

**Revoscalepy e contextos de computação remota**


Este exemplo demonstra o processo de criação de um modelo de Python no remoto _contexto de computação_, que permite a você trabalhar em um cliente, mas escolha um ambiente remoto, como o SQL Server, Spark ou servidor de aprendizado de máquina, em que o operações, na verdade, são executadas. Usar contextos de computação facilita escrever o código uma vez e implantá-lo a qualquer ambiente.

Para executar o código Python no SQL Server requer o **revoscalepy** pacote. Este é um pacote do Python especial fornecido pela Microsoft, como o **RevoScaleR** pacote para a linguagem R. O **revoscalepy** pacote suporta a criação de contextos de computação e fornece a infraestrutura para transmitir dados e modelos entre uma estação de trabalho local e um servidor remoto. O **revoscalepy** função que ofereça suporte a execução de código no banco de dados é [RxInSqlServer](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rxinsqlserver).







## <a name="similar-articles-about-new-or-updated-articles"></a>Artigos semelhantes sobre artigos novos ou atualizados

Esta seção lista artigos muito semelhantes a artigos atualizados recentemente em outras áreas de assunto, em nosso repositório público GitHub.com: [MicrosoftDocs/sql-docs](https://github.com/MicrosoftDocs/sql-docs/).



#### <a name="subject-areas-that-do-have-new-or-recently-updated-articles"></a>Áreas de assunto que *têm* artigos novos ou atualizados recentemente

- [Novo + atualizado (11 + 6): &nbsp; &nbsp; **Advanced Analytics para o SQL** documentos](../advanced-analytics/new-updated-advanced-analytics.md)
- [Novo + atualizado (18 + 0): &nbsp; &nbsp; **Analysis Services para SQL** documentos](../analysis-services/new-updated-analysis-services.md)
- [Novo + atualizado (218 + 14): **conectar-se ao SQL** documentos](../connect/new-updated-connect.md)
- [Novo + atualizado (14 + 0): &nbsp; &nbsp; **mecanismo de banco de dados do SQL** documentos](../database-engine/new-updated-database-engine.md)
- [Novo + atualizado (3 + 2): &nbsp; &nbsp; **Integration Services para SQL** documentos](../integration-services/new-updated-integration-services.md)
- [Novo + atualizado (3 + 3): &nbsp; &nbsp; **Linux para o SQL** documentos](../linux/new-updated-linux.md)
- [Novo + atualizado (7 + 10): &nbsp; &nbsp; **bancos de dados relacionais do SQL** documentos](../relational-databases/new-updated-relational-databases.md)
- [Novo + atualizado (0 + 2): &nbsp; &nbsp; **Reporting Services para SQL** documentos](../reporting-services/new-updated-reporting-services.md)
- [Novo + atualizado (1 + 3): &nbsp; &nbsp; **Studio de operações SQL** documentos](../sql-operations-studio/new-updated-sql-operations-studio.md)
- [Novo + atualizado (2 + 3): &nbsp; &nbsp; **Microsoft SQL Server** documentos](../sql-server/new-updated-sql-server.md)
- [Novo + atualizado (1 + 1): &nbsp; &nbsp; **SQL Server Data Tools (SSDT)** documentos](../ssdt/new-updated-ssdt.md)
- [Novo + atualizado (5 + 2): &nbsp; &nbsp; **SQL Server Management Studio (SSMS)** documentos](../ssms/new-updated-ssms.md)
- [Novo + atualizado (0 + 2): &nbsp; &nbsp; **Transact-SQL** documentos](../t-sql/new-updated-t-sql.md)
- [Novo + atualizado (1 + 1): &nbsp; &nbsp; **Tools para SQL** documentos](../tools/new-updated-tools.md)



#### <a name="subject-areas-that-do-not-have-any-new-or-recently-updated-articles"></a>Áreas de assunto que *não* têm nenhum artigo novo ou atualizado recentemente

- [Novo + atualizado (0 + 0): **Analytics Platform System para SQL** documentos](../analytics-platform-system/new-updated-analytics-platform-system.md)
- [Novo + atualizado (0 + 0): **Data Quality Services para SQL** documentos](../data-quality-services/new-updated-data-quality-services.md)
- [Novo + atualizado (0 + 0): **extensões DMX (Data Mining) para o SQL** documentos](../dmx/new-updated-dmx.md)
- [Novo + Atualizado (0+0): documentos sobre o **MDS (Master Data Services) para SQL**](../master-data-services/new-updated-master-data-services.md)
- [Novo + atualizado (0 + 0): **MDX (Multidimensional Expressions) para SQL** documentos](../mdx/new-updated-mdx.md)
- [Novo + atualizado (0 + 0): **ODBC (conectividade aberta de banco de dados) para o SQL** documentos](../odbc/new-updated-odbc.md)
- [Novo + atualizado (0 + 0): **PowerShell para SQL** documentos](../powershell/new-updated-powershell.md)
- [Novo + atualizado (0 + 0): **exemplos para SQL** documentos](../samples/new-updated-samples.md)
- [Novo + atualizado (0 + 0): **Migration Assistant SSMA (SQL Server)** documentos](../ssma/new-updated-ssma.md)
- [Novo + atualizado (0 + 0): **XQuery para o SQL** documentos](../xquery/new-updated-xquery.md)

