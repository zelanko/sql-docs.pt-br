---
title: Atualizado - Advanced Analytics para documentos do SQL Server | Microsoft Docs
description: "Trechos de código de exibição de conteúdo atualizado recentemente alterada na documentação de, para Advanced Analytics para o Microsoft SQL Server."
services: na
documentationcenter: 
author: MightyPen
manager: jhubbard
editor: 
ms.service: na
ms.topic: updart-autogen
ms.technology: database-engine
ms.custom: UpdArt.exe
ms.tgt_pltfrm: na
ms.devlang: na
ms.date: 12/02/2017
ms.author: genemi
ms.workload: advanced-analytics
ms.openlocfilehash: 636e243f1f39f0bfa688c6caada1e03078de9a32
ms.sourcegitcommit: 29265ad41fbe3326c21c6908ec4275a3a38f1c09
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/04/2017
---
# <a name="new-and-recently-updated-advanced-analytics-for-sql-server"></a>Novos e atualizados recentemente: Advanced Analytics para o SQL Server



A Microsoft atualiza alguns de seus artigos existentes no site de documentação [Docs.Microsoft.com](http://docs.microsoft.com/) todos os dias. Este artigo exibe trechos de artigos atualizados recentemente. Links para novos artigos também podem ser listados.

Este artigo é gerado por um programa que é reexecutado periodicamente. Ocasionalmente, um trecho pode aparecer com formatação imperfeita ou como markdown do artigo de origem. Imagens nunca são exibidas aqui.

Atualizações recentes são relatadas para o intervalo de datas e o assunto a seguir:



- *Intervalo de datas das atualizações:* &nbsp; **2017-09-28** &nbsp; - para - &nbsp; **2017-12-02**
- *Área de assunto:* &nbsp; **Advanced Analytics para o SQL Server**.

<!-- Repo = 'MicrosoftDocs/sql-docs'.   Branch = 'live'. -->



&nbsp;

## <a name="new-articles-created-recently"></a>Novos artigos criados recentemente

Os links a seguir direcionam para novos artigos que foram adicionados recentemente.


1. [Adicionar SQLRUserGroup como um usuário de banco de dados](r/add-sqlrusergroup-to-database.md)
2. [Como usar funções de RevoScaleR para localizar ou instalar pacotes R no SQL Server](r/use-revoscaler-to-manage-r-packages.md)
3. [Usando o R no banco de dados SQL do Azure](r/using-r-in-azure-sql-database.md)



&nbsp;

## <a name="updated-articles-with-excerpts"></a>Artigo atualizado com trechos

Esta seção exibe os trechos de atualizações coletados de artigos que passaram por uma atualização extensa recentemente.

Os trechos exibidos aqui aparecerão separados de seu contexto de semântico apropriado. Além disso, às vezes um trecho é separado da sintaxe de markdown importante que circunda no artigo real. Portanto, esses trechos servem apenas como orientações gerais. Os trechos só mostram a você se vale a pena clicar e visitar o artigo real conforme seus interesses.

Por essas e outras razões, não copie o código desses trechos, nem considere-os como verdade exata. Em vez disso, visite o artigo real.





&nbsp;

<a name="compactupdatedlist"/>

### <a name="compact-list-of-articles-updated-recently"></a>Lista compacta dos artigos atualizados recentemente

Essa lista compacta fornece links para todos os artigos atualizados listados na seção Trechos.

1. [Problemas conhecidos nos serviços de aprendizado de máquina](#TitleNum_1)
2. [Criar um repositório de pacotes local usando o miniCRAN](#TitleNum_2)
3. [Determinar quais pacotes de R são instalados no SQL Server](#TitleNum_3)
4. [Instalar pacotes R adicionais no SQL Server](#TitleNum_4)
5. [Instalando recursos em uma máquina virtual do Azure de aprendizado de máquina do SQL Server](#TitleNum_5)
6. [Instalar pré-treinado modelos no SQL Server de aprendizado de máquina](#TitleNum_6)
7. [Evitando erros de pacotes R instalados nas bibliotecas de usuário](#TitleNum_7)
8. [Provisionar uma máquina virtual para o aprendizado de máquina do Azure](#TitleNum_8)
9. [RevoScaleR](#TitleNum_9)
10. [Habilitar ou desabilitar o gerenciamento de pacotes de R para o SQL Server](#TitleNum_10)
11. [Configurar um cliente de ciência de dados para uso com o SQL Server](#TitleNum_11)
12. [Configurar os serviços de Machine Learning do SQL Server (no banco de dados)](#TitleNum_12)
13. [Instalação autônoma dos serviços de aprendizado de máquina (no banco de dados)](#TitleNum_13)
14. [Etapa 3: Explorar e visualizar os dados](#TitleNum_14)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-known-issues-in-machine-learning-servicesknown-issues-for-sql-server-machine-learning-servicesmd"></a>1. &nbsp;[Problemas conhecidos de serviços de aprendizado de máquina](known-issues-for-sql-server-machine-learning-services.md)

*Atualizado em: 2017-11-16* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([próxima](#TitleNum_2))

<!-- Source markdown line 321.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 00121c648c21576d5c86494137de1d4d81e2e265 c65973f6ae9253af5ecc621916ef36d7c0398789  (PR=3980  ,  Filename=known-issues-for-sql-server-machine-learning-services.md  ,  Dirpath=docs\advanced-analytics\  ,  MergeCommitSha40=06bb91d138a4d6395c7603a2d8f99c69a20642d3) -->



**A execução de código Python ou problemas de pacotes do Python**


Esta seção contém os problemas conhecidos que são específicos para em execução Python no SQL Server, bem como problemas relacionados aos pacotes Python publicados pela Microsoft, incluindo [revoscalepy](https://docs.microsoft.com/r-server/python-reference/revoscalepy/revoscalepy-package) e [microsoftml](https://docs.microsoft.com/r-server/python-reference/microsoftml/microsoftml-package).

**Chamada para o modelo pré-treinado falha se o caminho para o modelo é muito longo**


Se você instalar os modelos pré-treinado em uma instalação padrão, dependendo do nome do computador e o nome da instância, o caminho completo resultante para o arquivo de modelo treinado pode ser muito longo para Python para leitura. Essa limitação será corrigida em uma versão futura do serviço.

Há várias possíveis soluções alternativas:

+ Quando você instala os modelos pré-treinado, escolha um local personalizado.
+ Se possível, instale a instância do SQL Server em um caminho de instalação personalizada, como C:\SQL\MSSQL14. MSSQLSERVER.
+ Use o utilitário Windows [Fsutil](https://technet.microsoft.com/library/cc788097(v=ws.11).aspx) para criar um vínculo físico que mapeia o arquivo de modelo para um caminho mais curto.

**Falha ao inicializar uma variável varbinary causa um erro no BxlServer**


Se você executar o código Python no SQL Server usando `sp_execute_external_script`e o código de saída variáveis do tipo varbinary (max), varchar (max) ou tipos semelhantes, a variável deve ser inicializada ou definida como parte do script. Caso contrário, o componente de troca de dados, BxlServer, gera um erro e parar de funcionar.

Essa limitação será corrigida em uma versão futura do serviço. Como alternativa, certifique-se de que a variável é inicializada dentro do script de Python. Qualquer valor válido pode ser usado, como nos exemplos a seguir:

```sql
declare @b varbinary(max);
exec sp_execute_external_script
  @language = N'Python'
```



&nbsp;

&nbsp;

---

<a name="TitleNum_2"/>

### <a name="2-nbsp-create-a-local-package-repository-using-minicranrcreate-a-local-package-repository-using-minicranmd"></a>2. &nbsp;[Criar um repositório de pacote local usando miniCRAN](r/create-a-local-package-repository-using-minicran.md)

*Atualizado em: 2017-11-30* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([anterior](#TitleNum_1) | [próxima](#TitleNum_3))

<!-- Source markdown line 43.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 44b77cb127e9ffab1777216a66f0e5be9c82f3d2 65e30f10fc36acb3ce95f60f51f3501fbc98ad08  (PR=4150  ,  Filename=create-a-local-package-repository-using-minicran.md  ,  Dirpath=docs\advanced-analytics\r\  ,  MergeCommitSha40=578bd1c2760866ddeb3523f830cfc3cb6b4ab9af) -->



-   **Fácil instalação offline**: para instalar o pacote a um servidor offline requer que você também baixar todas as dependências do pacote, usando miniCRAN torna mais fácil de obter todas as dependências no formato correto.

-   **Melhor gerenciamento de versão**: em um ambiente multiusuário, há boas razões para evitar irrestrita instalação de várias versões de pacote no servidor.

Depois de criar o repositório, você pode modificá-lo adicionando novos pacotes ou atualizar a versão de pacotes existentes.

**Etapa 1. Instalar o pacote de miniCRAN**


Você começa criando um repositório miniCRAN para usar como uma fonte. Você deve criar esse repositório em um computador que tenha acesso à internet.

1.  Instalar o pacote de miniCRAN e obrigatório **igraph** pacote.

```
    if(!require("miniCRAN")) install.packages("miniCRAN") if(!require("igraph"))
    install.packages("igraph") library(miniCRAN)
```

**Etapa 2. Definir uma origem de pacote: um espelho CRAN ou um instantâneo MRAN**


1. Especifique um site do espelho para usar na obtenção de pacotes.

```
    CRAN_mirror \<- c(CRAN = "https://mran.microsoft.com/snapshot/2017-08-01")
```

2.  Indica uma pasta local no qual armazenar os pacotes coletados. Você não precisa nomear miniCRAN a pasta; pode ser um nome mais descritivo, como "GeneticsPackages" ou "ClientRPackages1.0.2".

    Apenas certifique-se de criar a pasta com antecedência. Um erro será gerado se o `local_repo` pasta não existir quando você executar o código de R mais tarde.



&nbsp;

&nbsp;

---

<a name="TitleNum_3"/>

### <a name="3-nbsp-determine-which-r-packages-are-installed-on-sql-serverrdetermine-which-packages-are-installed-on-sql-servermd"></a>3. &nbsp;[Determinar quais pacotes de R são instalados no SQL Server](r/determine-which-packages-are-installed-on-sql-server.md)

*Atualizado em: 2017-11-30* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([anterior](#TitleNum_2) | [próxima](#TitleNum_4))

<!-- Source markdown line 55.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 13d93acedc6e6b4615f1a244a2a1542910feb69e 9a065066398843a4bed318fa46d4982d712915a9  (PR=4150  ,  Filename=determine-which-packages-are-installed-on-sql-server.md  ,  Dirpath=docs\advanced-analytics\r\  ,  MergeCommitSha40=578bd1c2760866ddeb3523f830cfc3cb6b4ab9af) -->



+ Se o pacote for encontrado, a mensagem retornada deve ser algo como "Comandos concluída com êxito."

+ Se o pacote não pode ser localizado ou carregado, você receberá um erro como esse: "Ocorreu um erro de script externo: erro em library("RevoScaleR"): não há nenhum pacote chamado RevoScaleR"

**Obter uma lista de pacotes instalados usando o R**


Há várias maneiras de se obter uma lista de pacotes instalados ou carregados, usando ferramentas de R e funções de R. Muitas ferramentas de desenvolvimento do R fornecem um pesquisador de objetos ou uma lista de pacotes instalados ou carregados no espaço de trabalho atual do R.

+ Do utilitário local do R, use uma função de base R, como `installed.packages()`, que está incluído o `utils` pacote. Para obter uma lista que é precisa para uma instância, você deve especificar explicitamente o caminho da biblioteca ou usar as ferramentas de R associadas com a biblioteca de instância.

+ Para verificar um pacote em um contexto de computação específico, você pode usar as seguintes funções do pacote RevoScaleR. Essas funções ajudam a identificar os pacotes em contextos de computação especificado:

+ [rxFindPackage](https://msdn.microsoft.com/microsoft-r/scaler/packagehelp/rxfindpackage)

+ [rxInstalledPackages](https://msdn.microsoft.com/microsoft-r/scaler/packagehelp/rxinstalledpackages)

Por exemplo, execute o seguinte código de R para obter uma lista de pacotes disponíveis no contexto de computação do SQL Server especificado.

```r
sqlServerCompute <- RxInSqlServer(connectionString = "Driver=SQL Server;Server=myServer;Database=TestDB;Uid=myID;Pwd=myPwd;")
sqlPackages <- rxInstalledPackages(computeContext = sqlServerCompute)
sqlPackages
```
**Consulte também**




&nbsp;

&nbsp;

---

<a name="TitleNum_4"/>

### <a name="4-nbsp-install-additional-r-packages-on-sql-serverrinstall-additional-r-packages-on-sql-servermd"></a>4. &nbsp;[Instalar pacotes R adicionais no SQL Server](r/install-additional-r-packages-on-sql-server.md)

*Atualizado em: 2017-11-30* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([anterior](#TitleNum_3) | [próxima](#TitleNum_5))

<!-- Source markdown line 266.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 ba48f1838857d90d6692aafc48f393777ac602fa 37de2586a344a99969bcd9a20723c021db2604a4  (PR=4150  ,  Filename=install-additional-r-packages-on-sql-server.md  ,  Dirpath=docs\advanced-analytics\r\  ,  MergeCommitSha40=578bd1c2760866ddeb3523f830cfc3cb6b4ab9af) -->



Esta seção fornece dicas variadas e código de exemplo relacionadas à instalação do pacote de R no SQL Server.

**<a name="packageVersion"></a>Obter a versão correta do pacote e o formato**


Há várias fontes de pacotes R, os mais conhecidos entre eles são CRAN e Bioconductor. O site oficial da linguagem R (<https://www.r-project.org/>) lista vários desses recursos. Muitos pacotes são publicados no GitHub, onde é possível obter o código-fonte. No entanto, você talvez tenha recebido pacotes R desenvolvidos por alguém de sua empresa.

Independentemente da origem, você deve garantir que o pacote que você deseja instalar tem um formato binário para a plataforma Windows. Caso contrário, o pacote baixado não é possível executar no ambiente do SQL Server.

Antes de baixar, você também deve verificar se o pacote é compatível com a versão do R que está em execução no SQL Server.

**<a name="bkmk_zipPreparation"></a>Baixe o pacote como um arquivo compactado**


Para instalação em um servidor sem acesso à internet, baixe uma cópia do pacote no formato de um arquivo compactado para instalação offline. Não descompacte o pacote.

Por exemplo, o procedimento a seguir descreve agora para obter a versão correta do [FISHalyseR](http://bioconductor.org/packages/release/bioc/html/FISHalyseR.html) pacote da Bioconductor, supondo que o computador tem acesso à internet.

1.  Na lista **Arquivos de Pacote** , localize a versão **Binário do Windows** .

2.  Clique no link para o. Arquivo ZIP e selecione **Salvar destino como**.

3.  Navegue até a pasta local onde os pacotes compactados são armazenados e clique em **salvar**.

Esse processo cria uma cópia local do pacote. Em seguida, você pode instalar o pacote ou copiar o pacote compactado em um servidor que não tenha acesso à internet.

Para obter mais informações sobre o conteúdo do formato de arquivo zip e como criar um pacote R, é recomendável neste tutorial, o que pode ser baixado no formato PDF no site do projeto R: [criação de pacotes de R](http://cran.r-project.org/doc/contrib/Leisch-CreatingPackages.pdf).



&nbsp;

&nbsp;

---

<a name="TitleNum_5"/>

### <a name="5-nbsp-installing-sql-server-machine-learning-features-on-an-azure-virtual-machinerinstalling-sql-server-r-services-on-an-azure-virtual-machinemd"></a>5. &nbsp;[Recursos em uma máquina virtual do Azure de aprendizado de máquina de instalação do SQL Server](r/installing-sql-server-r-services-on-an-azure-virtual-machine.md)

*Atualizado em: 2017-11-30* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([anterior](#TitleNum_4) | [próxima](#TitleNum_6))

<!-- Source markdown line 55.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 f4d287044b8bfda2dbe77fbf65b0d9cdd8f2ff42 2a8e33de6383f5d3af52256c5dfcb60184659eb8  (PR=4150  ,  Filename=installing-sql-server-r-services-on-an-azure-virtual-machine.md  ,  Dirpath=docs\advanced-analytics\r\  ,  MergeCommitSha40=578bd1c2760866ddeb3523f830cfc3cb6b4ab9af) -->



6. Se você pretende conectar-se à instância de um cliente de ciência de dados remotos, conclua [etapas adicionais – #additional-etapas) conforme necessário.

**Desativar os recursos de aprendizado de máquina em uma VM do SQL Server**


Você também pode habilitar ou desabilitar o recurso em uma máquina de virtual do SQL Server existente a qualquer momento.

1. Abra a folha de máquina virtual.
2. Clique em **Configurações** e selecione **Configuração do SQL Server**.
3. Fazer alterações em recursos e aplicar.

**<a name="existing"></a>Adicionar R Services a uma VM existente do SQL Server 2016 Enterprise**


Se você tiver criado uma máquina virtual do Azure que incluiu o SQL Server sem aprendizado de máquina, você pode adicionar o recurso seguindo estas etapas:

1. Execute novamente...! NCLUIR-NotShown – ssNoVersion –. /.. /Includes/ssNoVersion-MD.MD]) de instalação e adicionar o recurso de **configuração do servidor** página do assistente.
2. Habilitar a execução de scripts externos e reinicie o...! NCLUIR-NotShown – ssNoVersion –. /.. instância de /Includes/ssNoVersion-MD.MD]). Para obter mais informações, consulte [conjunto de backup SQL Server R Services--... /.. / advanced-analytics/r/set-up-sql-server-r-services-in-database.md).
3. (Opcional) Se isto for necessário para a execução de scripts remotos, configure o acesso de banco de dados para contas de trabalho do R.
   Para obter mais informações, consulte [definir o SQL Server R Services--... /.. / advanced-analytics/r/set-up-sql-server-r-services-in-database.md).
3. (Opcional) Se você pretende permitir a execução de scripts R de clientes de ciência de dados remotos, modifique uma regra de firewall na máquina virtual do Azure. Para obter mais informações, consulte [Unblock firewall – #firewall).
4. Instale ou habilite as bibliotecas de rede necessárias. Para obter mais informações, consulte [Adicionar rede protocolos – #network).



&nbsp;

&nbsp;

---

<a name="TitleNum_6"/>

### <a name="6-nbsp-install-pretrained-machine-learning-models-on-sql-serverrinstall-pretrained-models-sql-servermd"></a>6. &nbsp;[Instalação classificação modelos de aprendizado de máquina no SQL Server](r/install-pretrained-models-sql-server.md)

*Atualizado em: 2017-11-30* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([anterior](#TitleNum_5) | [próxima](#TitleNum_7))

<!-- Source markdown line 96.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 07b51584a90568cccceea382c44155e40e09c967 db083f8536fbb2ea5886fed787872867b5de5750  (PR=4150  ,  Filename=install-pretrained-models-sql-server.md  ,  Dirpath=docs\advanced-analytics\r\  ,  MergeCommitSha40=578bd1c2760866ddeb3523f830cfc3cb6b4ab9af) -->



    For example, to enable use of the latest version of the pretrained models for Python, in a default instance of SQL Server 2017, you would run this statement:

    `RSetup.exe /install /component MLM /version 9.2.0.24 /language 1033 /destdir "C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\library\MicrosoftML\mxLibs\x64"`

    On a named instance, the command would be something like this:

    `RSetup.exe /install /component MLM /version 9.2.0.24 /language 1033 /destdir "C:\Program Files\Microsoft SQL Server\MSSQL14.MyInstanceName\PYTHON_SERVICES\library\MicrosoftML\mxLibs\x64"`

    + Para usar o Python classificação modelos ao servidor de aprendizado de máquina (autônomo):

    `RSetup.exe /install /component MLM /version <version> /language 1033 /destdir "<sql_folder>\PYTHON_SERVER\site-packages\microsoftml\mxLibs"`

    Por exemplo, supondo que uma instalação padrão do servidor de aprendizado de máquina (autônomo) usando a instalação do SQL Server 2017, execute esta instrução:

    `RSetup.exe /install /component MLM /version 9.2.0.24 /language 1033 /destdir "C:\Program Files\Microsoft SQL Server\140\PYTHON_SERVER\Lib\site-packages\microsoftml\mxLibs"`

5. Os valores a seguir têm suporte para o parâmetro version:



&nbsp;

&nbsp;

---

<a name="TitleNum_7"/>

### <a name="7-nbsp-avoiding-errors-on-r-packages-installed-in-user-librariesrpackages-installed-in-user-librariesmd"></a>7. &nbsp;[Evitando erros de pacotes R instalados nas bibliotecas de usuário](r/packages-installed-in-user-libraries.md)

*Atualizado em: 2017-10-23* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([anterior](#TitleNum_6) | [próxima](#TitleNum_8))

<!-- Source markdown line 33.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 52cb9a53d7d9c31ee9bc6977464ebd2a18081ff3 3537aa6755c66f12c19bb3448dc9b5c8abb9cc28  (PR=3619  ,  Filename=packages-installed-in-user-libraries.md  ,  Dirpath=docs\advanced-analytics\r\  ,  MergeCommitSha40=aecf422ca2289b2a417147eb402921bb8530d969) -->



No entanto, isso nunca funciona ao executar soluções R no SQL Server, porque os pacotes de R devem ser instalados em uma biblioteca de padrão específico que está associada com a instância.

Se o pacote não estiver instalado na biblioteca padrão, você poderá receber esse erro ao tentar chamar o pacote:

*Erro em library(xxx): não há nenhum pacote chamado 'nome do pacote'*

Também é uma prática de desenvolvimento incorreta para instalar pacotes de R necessários para uma biblioteca de usuário personalizada, pois isso poderá resultar em erros se uma solução é executada por outro usuário que não tem acesso para o local da biblioteca.

**Como instalar pacotes de R em uma biblioteca acessível**


**Para o SQL Server 2016**

Use a biblioteca de pacote associada à instância. Para obter detalhes, consulte [pacotes R instalados com o SQL Server--installing-and-managing-r-packages.md)

**Para o SQL Server de 2017**

SQL Server fornece recursos para ajudá-lo a gerenciar várias versões de pacote e fornecer aos usuários permissões para pacotes individuais, sem exigir que os usuários tenham acesso de sistema de arquivos.

Para obter detalhes sobre como configurar uma biblioteca compartilhada de pacote e atribuir usuários a funções, consulte [gerenciamento de pacotes R para SQL Server--r-package-management-for-sql-server-r-services.md.)




&nbsp;

&nbsp;

---

<a name="TitleNum_8"/>

### <a name="8-nbsp-provision-a-virtual-machine-for-machine-learning-on-azurerprovision-the-r-server-only-sql-server-2016-enterprise-vm-on-azuremd"></a>8. &nbsp;[Provisionar uma máquina virtual para o aprendizado de máquina do Azure](r/provision-the-r-server-only-sql-server-2016-enterprise-vm-on-azure.md)

*Atualizado em: 2017-10-31* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([anterior](#TitleNum_7) | [próxima](#TitleNum_9))

<!-- Source markdown line 132.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 16439b4a8f5f4218edfcd746ed20ccbc8263dabc 1b3a8a7d1ceceaa459b3fd5640da26859df8d80b  (PR=3748  ,  Filename=provision-the-r-server-only-sql-server-2016-enterprise-vm-on-azure.md  ,  Dirpath=docs\advanced-analytics\r\  ,  MergeCommitSha40=262e3cf5df2448bb6b532c0549c3d72daefe5a96) -->



|Nome| Comentários|
|----|----|----|
| **SQL Server 2016**| ***  |
|SQL Server 2016 SP1 Enterprise no Windows|Serviços de R para análises avançadas integrados.|
|BYOL SQL Server 2016 SP1 Enterprise no Windows Server |Serviços de R para análises avançadas integrados. |
|Uma licença gratuita: SQL Server 2016 SP1 Developer no Windows Server 2016 |Serviços de R para análises avançadas integrados. |
| Máquina Virtual de ciência de dados - 2012 do Windows|Contém ferramentas populares de ciência de dados, incluindo Microsoft R Server Developer Edition, SQL Server 2016 Developer edition, a distribuição Anaconda Python, edição de desenvolvedor Julia Pro e blocos de anotações do Jupyter r.|
| Máquina Virtual de ciência de dados - Windows 2016|Inclui o SQL Server 2016 Developer Edition, com suporte para análise de R no banco de dados.|
|**SQL Server 2017**| ***   |
|SQL Server 2017 Enterprise Windows Server 2016| Serviços de aprendizado de máquina com suporte de linguagem Python e R.|
|BYOL SQL Server 2017 Enterprise Windows Server 2016|Serviços de aprendizado de máquina com suporte de linguagem Python e R.|
| Licença do gratuita do SQL Server: SQL Server 2017 Developer no Windows Server|Serviços de aprendizado de máquina com suporte de linguagem Python e R.|
| **Outro**| *** |
| Servidor SQL Server 2017 corporativa de aprendizado de máquina|Semelhante à imagem do SQL Server 2016 Enterprise, mas contém a versão autônoma do servidor de aprendizado de máquina e tem o núcleo de ScaleR e funcionalidade operacionalização otimizado para ambientes Windows.|
| Servidor de aprendizado de máquina para Windows|Contém a versão autônoma do servidor de aprendizado de máquina, com recursos de operacionalização otimizados para ambientes do Windows.|



&nbsp;

&nbsp;

---

<a name="TitleNum_9"/>

### <a name="9-nbsp-revoscalerrrevoscaler-overviewmd"></a>9. &nbsp;[RevoScaleR](r/revoscaler-overview.md)

*Atualizado em: 2017-11-30* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([anterior](#TitleNum_8) | [próxima](#TitleNum_10))

<!-- Source markdown line 18.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 92f2dfa2e75037a932415881c55d2fd37fc6847a c6e9f17f2df82447b18beff41769ae3ebfbed562  (PR=4150  ,  Filename=revoscaler-overview.md  ,  Dirpath=docs\advanced-analytics\r\  ,  MergeCommitSha40=578bd1c2760866ddeb3523f830cfc3cb6b4ab9af) -->




RevoScaleR é um pacote de funções de aprendizado de máquina, fornecido pela Microsoft, que oferece suporte a ciência de dados em grande escala.

+ Suportam a funções de importação de dados, transformação de dados, resumo, visualização e análise.

+ _Em escala_ significa que as operações podem ser executadas em grandes conjuntos de dados, em paralelo e distribuídas em sistemas de arquivos. Os algoritmos podem operar em conjuntos de dados que não cabem na memória, usando o agrupamento e pelos resultados de remontagem quando operações forem concluídas.

+ RevoScaleR fornece muitas melhorias em funções de R de software livre. Há funções de RevoScaleR correspondente a muitas das funções de base R mais populares. Funções de RevoScaleR são indicadas com um **rx** ou **Rx** prefixo para torná-los mais fáceis de identificar.

+ RevoScaleR serve como uma plataforma para ciência de dados distribuído. Por exemplo, você pode usar as transformações e contextos de computação RevoScaleR com os algoritmos de arte em [MicrosoftML](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-the-microsoftml-package). Você também pode usar [rxExec](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxexec) para executar funções básicas de R em paralelo.

Para obter exemplos de RevoScaleR em ação, consulte esses blogs:

+ [Criar e implantar um modelo de previsão usando R e SQL Server](https://microsoft.github.io/sql-ml-tutorials/R/rentalprediction/)

+ [Previsões de um milhão por segundo, com o servidor de aprendizado de máquina](https://blogs.msdn.microsoft.com/mlserver/2017/10/15/1-million-predictionssec-with-machine-learning-server-web-service/)

+ [Prevendo dicas táxi usando MicrosoftML](https://blogs.msdn.microsoft.com/microsoftrservertigerteam/2017/01/17/predicting-nyc-taxi-tips-using-microsoftml/)

+ [Otimização de desempenho com rxExec](https://blogs.msdn.microsoft.com/microsoftrservertigerteam/2016/11/14/performance-optimization-when-using-rxexec-to-parallelize-algorithms/)

**Como obter o RevoScaleR**




&nbsp;

&nbsp;

---

<a name="TitleNum_10"/>

### <a name="10-nbsp-enable-or-disable-r-package-management-for-sql-serverrr-package-how-to-enable-or-disablemd"></a>10. &nbsp;[Habilitar ou desabilitar o gerenciamento de pacotes de R para o SQL Server](r/r-package-how-to-enable-or-disable.md)

*Atualizado em: 2017-11-30* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([anterior](#TitleNum_9) | [próxima](#TitleNum_11))

<!-- Source markdown line 60.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 5f846cd7d601459a95e694ada41e9fc5285f3de9 83a4a84adf47670c7fd4599f889f27ec3c219708  (PR=4150  ,  Filename=r-package-how-to-enable-or-disable.md  ,  Dirpath=docs\advanced-analytics\r\  ,  MergeCommitSha40=578bd1c2760866ddeb3523f830cfc3cb6b4ab9af) -->



    If you do not specify a user, the current security context is used.

3. Repita o comando para cada banco de dados em que os pacotes devem ser instalados.

4.  Para verificar se as novas funções foram criadas com êxito, no SQL Server Management Studio, clique em banco de dados, expanda **segurança**e expanda **funções de banco de dados**.

    Você também pode executar uma consulta em sys. database_principals como o seguinte:

```sql
    SELECT pr.principal_id, pr.name, pr.type_desc,
        pr.authentication_type_desc, pe.state_desc,
        pe.permission_name, s.name + '.' + o.name AS ObjectName
    FROM sys.database_principals AS pr
    JOIN sys.database_permissions AS pe
        ON pe.grantee_principal_id = pr.principal_id
    JOIN sys.objects AS o
        ON pe.major_id = o.object_id
    JOIN sys.schemas AS s
        ON o.schema_id = s.schema_id;
```

4.  Depois que o recurso foi habilitado, qualquer usuário com as permissões apropriadas pode usar o [criar biblioteca externa](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql) instrução T-SQL para adicionar pacotes. Para obter um exemplo de como isso funciona, consulte [instalar outros pacotes no SQL Server](r/install-additional-r-packages-on-sql-server.md).

**<a name="bkmk_disable"></a>Desabilitar o gerenciamento de pacote**




&nbsp;

&nbsp;

---

<a name="TitleNum_11"/>

### <a name="11-nbsp-set-up-a-data-science-client-for-use-with-sql-serverrset-up-a-data-science-clientmd"></a>11. &nbsp;[Configurar um cliente de ciência de dados para uso com o SQL Server](r/set-up-a-data-science-client.md)

*Atualizado em: 2017-11-01* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([anterior](#TitleNum_10) | [próxima](#TitleNum_12))

<!-- Source markdown line 52.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 f674f5d329211e4c7d8dc464bd70f1cdef633350 8c65fc96c04f32d1e4777870774a11f9fd2ee219  (PR=3765  ,  Filename=set-up-a-data-science-client.md  ,  Dirpath=docs\advanced-analytics\r\  ,  MergeCommitSha40=dc67a9c744441f9d556e98fb9a4daf4414060360) -->



    For setup information, see [How to install R Tools for Visual Studio](https://docs.microsoft.com/visualstudio/rtvs/installation).

    To configure RTVS to use your Microsoft R client libraries, see [About Microsoft R Client](https://docs.microsoft.com/machine-learning-server/r-client/what-is-microsoft-r-client)

+ 2017 do Visual Studio

    Até mesmo a edição Community gratuita inclui a carga de trabalho de ciência de dados, que instala os modelos de projeto para R, Python e F #.

    Baixar o Visual Studio de [este site](https://www.visualstudio.com/vs/).

+ RStudio

    Se você preferir usar o RStudio, algumas etapas adicionais serão necessárias para usar as bibliotecas de RevoScaleR:

    - Instale o cliente do Microsoft R para obter os pacotes necessários e bibliotecas.
    - Atualize o caminho de R para usar o tempo de execução do Microsoft R.

    Para obter mais informações, consulte [cliente R - configurar seu IDE](https://docs.microsoft.com/machine-learning-server/r-client/what-is-microsoft-r-client#step-2-configure-your-ide).

**Configurar seu IDE**


+ Ferramentas de R para o Visual Studio

    Consulte [este site](https://docs.microsoft.com/visualstudio/rtvs/getting-started-with-r) para obter alguns exemplos de como criar e depurar R projetos usando ferramentas de R para Visual Studio.

+ 2017 do Visual Studio

    Se você instalar o cliente do Microsoft R ou R Server **antes de** instalar o Visual Studio, as bibliotecas de R Server são detectadas automaticamente e usadas para o caminho de biblioteca. Se você não tiver instalado as bibliotecas de RevoScaleR, do **ferramentas R** menu, selecione **instalar o cliente de R**.

**Executar R no SQL Server**


Este exemplo usa o Visual Studio 2017 Community Edition, com a carga de trabalho de ciência de dados instalada.

1. Do **arquivo** menu, selecione **novo** e, em seguida, selecione **projeto**.

2. -Mão painel contém uma lista de modelos pré-instalado. Clique em **R**e selecione **R projeto**. No **nome** , digite `dbtest` e clique em **Okey**.



&nbsp;

&nbsp;

---

<a name="TitleNum_12"/>

### <a name="12-nbsp-set-up-sql-server-machine-learning-services-in-databaserset-up-sql-server-r-services-in-databasemd"></a>12. &nbsp;[Configurar serviços de aprendizado de máquina do SQL Server (no banco de dados)](r/set-up-sql-server-r-services-in-database.md)

*Atualizado em: 2017-11-16* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([anterior](#TitleNum_11) | [próxima](#TitleNum_13))

<!-- Source markdown line 111.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 4d355f6494b417dd90dce3943e7176eaece7336e 20bddb8ffd4cf3774b812a7376c70b95ccc57e92  (PR=3980  ,  Filename=set-up-sql-server-r-services-in-database.md  ,  Dirpath=docs\advanced-analytics\r\  ,  MergeCommitSha40=06bb91d138a4d6395c7603a2d8f99c69a20642d3) -->



   + Serviços do Mecanismo de Banco de Dados
   + R Services (no banco de dados)

7. Quando a instalação for concluída, reinicie o computador.


**<a name="bkmk2017top"></a>Instale os serviços de aprendizado de máquina do SQL Server de 2017 (no banco de dados)**


> [!div class="checklist"]
> * Instalar o mecanismo de banco de dados e recursos de aprendizado de máquina
> * Necessárias etapas de pós-instalação: habilitar o aprendizado de máquina e reiniciar
> * Etapas de pós-instalação opcionais: adicionar regras de firewall, os usuários de adicionar, alterar ou configurar contas de serviço, configurar um cliente de ciência de dados remotos.

**Introdução**

1. Executar …! NCLUIR-NotShown – ssNoVersion –. /.. instalação /Includes/ssNoVersion-MD.MD]).

2. Sobre o **instalação** guia, selecione **instalação autônoma do novo SQL Server ou adicionar recursos a uma instalação existente**.

     ! [Instalar serviços de aprendizado de máquina (In-Database)--media/2017setup-installation-page-mlsvcs.png "Iniciar a instalação do mecanismo de banco de dados com serviços de aprendizado de máquina")

3. Sobre o **seleção de recursos** , selecione as seguintes opções:

    + Selecione **serviços do mecanismo de banco de dados**. O mecanismo de banco de dados é necessário em cada instância que usa o aprendizado de máquina.

    + Selecione **Services (no banco de dados) de aprendizado de máquina**. Esta opção instala o suporte para uso no banco de dados de R. Depois de selecionar essa opção, você pode selecionar a idioma de aprendizado de máquina. Você pode selecionar apenas R, ou você pode adicionar o R e Python.

    ! [Recurso de serviços de aprendizado de máquina selection--media/2017setup-features-page-mls-rpy.png "Selecione esses recursos para R Services no banco de dados")

    Se você não selecionar opções de idioma de R ou Python, o Assistente de instalação instala apenas o framework de extensibilidade, que inclui a barra inicial do SQL Server confiável e não instala todos os componentes específicos do idioma.  Em geral, recomendamos que você instale pelo menos um idioma inicial. No entanto, você pode usar essa opção se você pretende usar imediatamente o processo de ligação para atualizar a componentes de aprendizado de máquina. Para obter mais informações, consulte [SqlBindR de uso para atualizar uma instância de R Services--use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md).



&nbsp;

&nbsp;

---

<a name="TitleNum_13"/>

### <a name="13-nbsp-unattended-installation-of-machine-learning-services-in-databaserunattended-installs-of-sql-server-r-servicesmd"></a>13. &nbsp;[Instalação autônoma dos serviços de aprendizado de máquina (no banco de dados)](r/unattended-installs-of-sql-server-r-services.md)

*Atualizado em: 2017-11-01* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([anterior](#TitleNum_12) | [próxima](#TitleNum_14))

<!-- Source markdown line 75.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 ad203c90adff3f515b5f16472fad9753be7a421d 6925a9276bcd4a80babc7504de50400f1a5a2940  (PR=3765  ,  Filename=unattended-installs-of-sql-server-r-services.md  ,  Dirpath=docs\advanced-analytics\r\  ,  MergeCommitSha40=dc67a9c744441f9d556e98fb9a4daf4414060360) -->



O exemplo a seguir mostra os argumentos necessários para executar um silencioso, autônomo a instalação de serviços de máquina do SQL Server de 2017 (no banco de dados) com a linguagem Python adicionada.

```
Setup.exe /q /ACTION=Install /FEATURES=SQLENGINE,ADVANCEDANALYTICS, SQL_INST_MPY /INSTANCENAME=MSSQLSERVER /SECURITYMODE=SQL /SAPWD="%password%" /SQLSYSADMINACCOUNTS="<username>" /IACCEPTSQLSERVERLICENSETERMS /IACCEPTPYTHONOPENLICENSETERMS
```

Observe os sinalizadores necessários para Python no SQL Server 2017:

+ `ADVANCEDANALYTICS`
+ `SQL_INST_MPY`
+ `IACCEPTPYTHONOPENLICENSETERMS`

**Instalar o R e Python em uma instância nomeada**


O exemplo a seguir mostra os argumentos necessários para executar um silencioso, autônomo a instalação de serviços de máquina do SQL Server de 2017 (no banco de dados) em uma instância nomeada. Idiomas R e Python são adicionados.

```
Setup.exe /q /ACTION=Install /FEATURES=SQLENGINE,ADVANCEDANALYTICS, SQL_INST_MR, SQL_INST_MPY /INSTANCENAME=MSSQLSERVER.ServerName /SECURITYMODE=SQL /SAPWD="%password%" /SQLSYSADMINACCOUNTS="<username>" /IACCEPTSQLSERVERLICENSETERMS /IACCEPTROPENLICENSETERMS /IACCEPTPYTHONOPENLICENSETERMS
```

**<a name="OldInstall"></a>Instalação de linha de comando para o SQL Server 2016**


O exemplo a seguir mostra os argumentos necessários para executar um silencioso, autônomo instalação do SQL Server 2016 com a linguagem R adicionada.



&nbsp;

&nbsp;

---

<a name="TitleNum_14"/>

### <a name="14-nbsp-step-3-explore-and-visualize-the-datatutorialssqldev-py3-explore-and-visualize-the-datamd"></a>14. &nbsp;[Etapa 3: explorar e visualizar os dados](tutorials/sqldev-py3-explore-and-visualize-the-data.md)

*Atualizado em: 2017-11-30* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([anterior](#TitleNum_13))

<!-- Source markdown line 66.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 47edcfbd8da7cf1ea1ad03a05f86d3cd26014827 674a7c7d0e8290fc91970ed2aeda3b97d5165d75  (PR=4150  ,  Filename=sqldev-py3-explore-and-visualize-the-data.md  ,  Dirpath=docs\advanced-analytics\tutorials\  ,  MergeCommitSha40=578bd1c2760866ddeb3523f830cfc3cb6b4ab9af) -->



    Class 4: `tip_amount` > $20

**Criar gráficos usando Python no T-SQL**


Em geral, o desenvolvimento de uma solução de ciência de dados inclui intensiva exploração e visualização de dados. Como visualização é uma ferramenta poderosa para entender a distribuição dos dados e exceções, o Python fornece muitos pacotes para visualização de dados. O **matplotlib** módulo é uma das bibliotecas mais populares para visualização e inclui muitas funções para a criação de histogramas, gráficos de dispersão, gráficos de caixa e outros gráficos de exploração de dados.

Nesta seção, você aprenderá como trabalhar com gráficos usando procedimentos armazenados. Em vez de abrir a imagem no servidor, você armazena o objeto de Python `plot` como **varbinary** dados e, em seguida, gravar que para um arquivo que pode ser compartilhado ou exibidos em outro lugar.

**Criar um gráfico como dados varbinary**


O **revoscalepy** módulo incluído com os serviços de aprendizado de máquina do SQL Server 2017 oferece suporte a recursos semelhantes do **RevoScaleR** pacote r.  Este exemplo usa o equivalente a Python `rxHistogram` para plotar um histograma com base em dados de um...! NCLUIR-NotShown – tsql:... /.. consulta /Includes/TSQL-MD.MD]).

O procedimento armazenado retorna um Python serializado `figure` objeto como um fluxo de **varbinary** dados. Não é possível exibir os dados binários diretamente, mas você pode usar o código Python no cliente para desserializar e exibir os dados e, em seguida, salve o arquivo de imagem em um computador cliente.

1. Criar o procedimento armazenado _SerializePlots_, se o script do PowerShell já não fez isso.

    - A variável `@query` define o texto da consulta `SELECT tipped FROM nyctaxi_sample`, que é passado para o bloco de código Python como o argumento para a variável de entrada de script, `@input_data_1`.
    - O script de Python é bastante simple: **matplotlib** `figure` objetos são usados para fazer o gráfico de histograma e dispersão, e esses objetos, em seguida, são serializados usando o `pickle` biblioteca.







## <a name="similar-articles"></a>Artigos Semelhantes

<!--  HOW TO:
    Refresh this file's line items with the latest 'Count-in-Similars*' content.
    Then run Run-533-*.BAT
    2017-12-02  23:00pm
-->

Esta seção lista artigos muito semelhantes a artigos atualizados recentemente em outras áreas de assunto, em nosso repositório público GitHub.com: [MicrosoftDocs/sql-docs](https://github.com/MicrosoftDocs/sql-docs/).

#### <a name="subject-areas-which-do-have-new-or-recently-updated-articles"></a>Áreas de assunto que têm artigos novos ou atualizados recentemente

- [Novo + atualizado (3 + 14): **Advanced Analytics para o SQL** documentos](../advanced-analytics/new-updated-advanced-analytics.md)
- [Novo + atualizado (1 + 0): documentos do **Analysis Services para SQL**](../analysis-services/new-updated-analysis-services.md)
- [Novo + atualizado (87 + 0): **Analytics Platform System para SQL** documentos](../analytics-platform-system/new-updated-analytics-platform-system.md)
- [Novo + atualizado (5 + 4): **conectar-se ao SQL** documentos](../connect/new-updated-connect.md)
- [Novo + atualizado (0 + 1): **mecanismo de banco de dados do SQL** documentos](../database-engine/new-updated-database-engine.md)
- [Novo + atualizado (2 + 2): **Integration Services para SQL** documentos](../integration-services/new-updated-integration-services.md)
- [Novo + atualizado (10 + 9): **Linux para o SQL** documentos](../linux/new-updated-linux.md)
- [Novo + atualizado (2 + 4): **bancos de dados relacionais do SQL** documentos](../relational-databases/new-updated-relational-databases.md)
- [Novo + atualizados (4 + 2): **Reporting Services para SQL** documentos](../reporting-services/new-updated-reporting-services.md)
- [Novo + atualizado (0 + 1): **exemplos para SQL** documentos](../sample/new-updated-sample.md)
- [Novo + atualizado (21 + 0): **Studio de operações SQL** documentos](../sql-operations-studio/new-updated-sql-operations-studio.md)
- [Novo + atualizado (5 + 1): **Microsoft SQL Server** documentos](../sql-server/new-updated-sql-server.md)
- [Novo + atualizado (0 + 1): documentos do **SSDT (SQL Server Data Tools)**](../ssdt/new-updated-ssdt.md)
- [Novo + atualizado (1 + 0): **Migration Assistant SSMA (SQL Server)** documentos](../ssma/new-updated-ssma.md)
- [Novo + atualizado (0 + 1): documentos do **SSMS (SQL Server Management Studio)**](../ssms/new-updated-ssms.md)
- [Novo + atualizado (0 + 2): **Transact-SQL** documentos](../t-sql/new-updated-t-sql.md)

#### <a name="subject-areas-which-have-no-new-or-recently-updated-articles"></a>Áreas de assunto que não têm nenhum artigo novo ou atualizado recentemente

- [Novo + atualizado (0 + 0): **dados Migration Assistant (DMA) para o SQL** documentos](../dma/new-updated-dma.md)
- [Novo + atualizado (0 + 0): documentos do **ADO (ActiveX Data Objects) para SQL**](../ado/new-updated-ado.md)
- [Novo + atualizado (0 + 0): documentos do **Data Quality Services para SQL**](../data-quality-services/new-updated-data-quality-services.md)
- [Novo + atualizado (0 + 0): documentos de **Extensões DMX (Data Mining) para SQL**](../dmx/new-updated-dmx.md)
- [Novo + Atualizado (0+0): documentos sobre o **MDS (Master Data Services) para SQL**](../master-data-services/new-updated-master-data-services.md)
- [Novo + atualizado (0 + 0): documentos de **Expressão MDX para SQL**](../mdx/new-updated-mdx.md)
- [Novo + atualizado (0 + 0): documentos do **ODBC (Open Database Connectivity) para SQL**](../odbc/new-updated-odbc.md)
- [Novo + atualizado (0 + 0): documentos do **PowerShell para SQL**](../powershell/new-updated-powershell.md)
- [Novo + Atualizado (0 + 0): documentos de **Ferramentas para SQL**](../tools/new-updated-tools.md)
- [Novo + atualizado (0 + 0): documentos do **XQuery para SQL**](../xquery/new-updated-xquery.md)


