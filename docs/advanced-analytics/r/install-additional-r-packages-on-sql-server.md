---
title: Instalar pacotes R adicionais no SQL Server | Microsoft Docs
ms.date: 02/20/2018
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 21456462-e58a-44c3-9d3a-68b4263575d7
caps.latest.revision: 
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: On Demand
ms.openlocfilehash: a328b07027f61f50df7e3ca2b6ac12b92508688b
ms.sourcegitcommit: c08d665754f274e6a85bb385adf135c9eec702eb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/28/2018
---
# <a name="install-additional-r-packages-on-sql-server"></a>Instalar pacotes R adicionais no SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artigo descreve como instalar novos pacotes de R em uma instância do SQL Server onde o aprendizado de máquina está habilitado.

Há vários métodos para instalar novos pacotes de R, dependendo de qual versão do SQL Server que você tem e se o servidor tem acesso à internet.

+ [Instalar novos pacotes usando ferramentas de R, com acesso à internet](#bkmk_rInstall)

    Use comandos de R convencionais para instalar os pacotes da Internet. Este é o método mais simples, mas requer acesso administrativo.

    **Aplica-se a:**[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)][!INCLUDE[rsql-productname-md](../../includes/rsql-productname-md.md)].     Também é necessário para instâncias de [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] [!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)] onde o gerenciamento de pacotes por meio de DDLs não foi habilitado.

+ [Instalar novos pacotes de R em um servidor com **sem** acesso à internet](#bkmk_offlineInstall)

    Se o servidor não tiver acesso à internet, algumas etapas adicionais são necessárias para preparar os pacotes. Esta seção descreve como preparar os arquivos necessários para a instalação do pacote e suas dependências.

+ [Instalar pacotes usando a instrução Criar biblioteca externa](#bkmk_createlibrary) 

    A instrução Criar biblioteca externa é fornecida no SQL Server 2017, para possibilitar que um DBA criar uma biblioteca de pacote sem executar código R ou Python diretamente. No entanto, esse método requer que você preparar todos os pacotes necessários com antecedência.  

    **Aplica-se a:** [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] [!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)]; outras restrições são aplicáveis  

## <a name="bkmk_rInstall"></a> Instalar novos pacotes de R usando a Internet

Você pode usar ferramentas padrão de R para instalar novos pacotes em uma instância do SQL Server 2016 ou 2017 do SQL Server. Esse processo exige que você é um administrador no computador.

> [!IMPORTANT] 
> Certifique-se de instalar os pacotes para a biblioteca padrão que está associada com a instância atual. Nunca instale pacotes em um diretório de usuário.

Este procedimento descreve como você pode instalar pacotes usando RGui; No entanto, você pode usar o RTerm ou qualquer outra R ferramenta de linha que dá suporte ao acesso com privilégios elevados.

### <a name="install-a-package-using-rgui-or-rterm"></a>Instalar um pacote usando RGui ou RTerm

1. Navegue até a pasta no servidor em que as bibliotecas de R para a instância estão instaladas.

  **Instância padrão**

    SQL Server 2017: `C:\Program Files\MSSQL14.MSSQLSERVER\R_SERVICES\bin\x64`
    
    SQL Server 2016: `C:\Program Files\MSSQL13.MSSQLSERVER\R_SERVICES\bin\x64`

  **Instância nomeada**

    SQL Server 2017: `C:\Program files\MSSQL14.<instanceName>\R_SERVICES\bin\x64`
    
    SQL Server 2016: `C:\Program files\MSSQL13.<instanceName>\R_SERVICES\bin\x64`

  Se você tiver usado a associação para atualizar a componentes de aprendizado de máquina, o caminho pode ter alterado. Sempre verifique o caminho da instância antes de instalar novos pacotes. 

2. RGui.exe e selecione **executar como administrador**.

    Se você não tiver as permissões necessárias, contate o administrador de banco de dados e fornecer uma lista dos pacotes que você precisa.

3. Na linha de comando, se você souber o nome do pacote, você pode digitar: `install.packages("the_package-name")` aspas duplas são necessárias para o nome do pacote.

4. Quando for solicitado para um site de espelhamento, selecione qualquer local que é conveniente para seu local.

5. Se o pacote de destino depender de outros pacotes, o instalador de R automaticamente baixa as dependências e as instala para você.

6. Para cada instância em que você precisa usar o pacote, execute a instalação separadamente. Pacotes não podem ser compartilhados entre instâncias.

## <a name = "bkmk_offlineInstall"></a> Instalação offline usando ferramentas de R

Para instalar pacotes de R em um servidor que não tem acesso à internet, você deve:

+ Analise as dependências com antecedência.
+ Baixe o pacote de destino para um computador com acesso à Internet.
+ Baixe os pacotes necessários no mesmo computador e colocar todos os pacotes em um arquivo único pacote.
+ Compacte o arquivo se ele não ainda estiver em formato compactado.
+ Copie o arquivo de pacote para um local no servidor.
+ Instale o pacote de destino, especificando o arquivo como origem.

> [!IMPORTANT] 
> > Certifique-se de que você analisar todas as dependências e baixar **todos os** pacotes necessários **antes de** iniciando a instalação. É recomendável [miniCRAN](https://mran.microsoft.com/package/miniCRAN) para esse processo. Este pacote de R usa uma lista de pacotes que você deseja instalar, analisa as dependências e obtém todos os arquivos compactados para você. miniCRAN, em seguida, cria um único repositório que você pode copiar para o computador do servidor.
> 
> Para obter detalhes, consulte [criar um repositório de pacote local usando miniCRAN](create-a-local-package-repository-using-minicran.md)

Este procedimento pressupõe que você preparou todos os pacotes que você precisa, em formato compactado e está pronto para copiá-los para o servidor.

1. Copie o pacote compactado arquivo ou de vários pacotes, o repositório completo que contém todos os pacotes no compactado formato para um local que o servidor possa acessar.

2. Abra a pasta no servidor em que as bibliotecas de R para a instância são instaladas. Por exemplo, se você estiver usando o prompt de comando do Windows, navegue até o diretório onde estão localizados RTerm.Exe ou RGui.exe.

  **Instância padrão**

    SQL Server 2017: `C:\Program Files\MSSQL14.MSSQLSERVER\R_SERVICES\bin\x64`
    
    SQL Server 2016: `C:\Program Files\MSSQL13.MSSQLSERVER\R_SERVICES\bin\x64`

  **Instância nomeada**

    SQL Server 2017: `C:\Program files\MSSQL14.<instanceName>\R_SERVICES\bin\x64`
    
    SQL Server 2016: `C:\Program files\MSSQL13.<instanceName>\R_SERVICES\bin\x64`

3. Clique com botão direito no RGui ou o prompt de comando e selecione **executar como administrador**.

4. Execute o comando de R `install.packages` e especifique o pacote ou o nome do repositório e o local dos arquivos compactados.

    ```R
    install.packages("C:\\Temp\\Downloaded packages\\mynewpackage.zip", repos=NULL)
    ```

    Esse comando extrai o pacote R `mynewpackage` de seu arquivo compactado local, supondo que você salvou a cópia no diretório `C:\Temp\Downloaded packages`e instala o pacote no computador local. Se o pacote tiver quaisquer dependências, o instalador verifica se os pacotes existentes na biblioteca. Se você tiver criado um repositório que inclui as dependências, o instalador instalará os pacotes necessários também.

    Se os pacotes necessários não estão presentes na biblioteca de instância e não podem ser encontrados em arquivos compactados, a instalação do pacote de destino falha.

## <a name="bkmk_createlibrary"></a> Use uma instrução DDL para instalar um pacote 

No SQL Server de 2017, você pode usar o [criar biblioteca externa](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql) instrução para adicionar um pacote ou conjunto de pacotes para uma instância ou um banco de dados específico. Esta instrução DDL e as funções de banco de dados de suporte são destinadas para facilitar a instalação e o gerenciamento de pacotes por um BA sem a necessidade de usar ferramentas de R ou Python.

Esse processo requer alguma preparação, em comparação com a instalação de pacotes usando os métodos de R ou Python convencionais.

+ Todos os pacotes devem ser disponível como um local compactado do arquivo, em vez de download da internet.

    Se você não tiver acesso ao sistema de arquivos no servidor, você também pode passar um pacote completo como uma variável, usando um formato binário. Para obter mais informações, consulte [criar biblioteca externa](../../t-sql/statements/create-external-library-transact-sql.md).

+ A instrução falhará se pacotes requeridos não estão disponíveis. Você deve analisar as dependências do pacote que você deseja instalar e certifique-se de que os pacotes são carregados para o servidor e o banco de dados. É recomendável usar **miniCRAN** ou **igraph** para análise de dependências de pacotes.

### <a name="prepare-the-packages-in-archive-format"></a>Prepare os pacotes no formato de arquivo

1. Se você estiver instalando um único pacote, baixe o pacote em formato compactado. 

2. Se o pacote exige que todos os outros pacotes, você deve verificar se os pacotes necessários estão disponíveis. Você pode usar miniCRAN para analisar o pacote de destino e identificar todas as suas dependências. 

3. Copie os arquivos compactados ou miniCRAN repositório que contém todos os pacotes em uma pasta local no servidor.

4. Abra um **consulta** janela, usando uma conta com privilégios administrativos.

5. Execute a instrução T-SQL `CREATE EXTERNAL LIBRARY` para carregar a coleção de pacote compactado para o banco de dados.

    Por exemplo, a instrução a seguir nomes como a origem do pacote um repositório de miniCRAN que contém o **randomForest** pacote, juntamente com suas dependências. 

    ```R
    CREATE EXTERNAL LIBRARY randomForest
    FROM (CONTENT = 'C:\Temp\Rpackages\randomForest_4.6-12.zip')
    WITH (LANGUAGE = 'R');
    ```

    Você não pode usar um nome arbitrário; o nome da biblioteca externa deve ter o mesmo nome que você pretende usar ao carregar ou chamar o pacote.

6. Se a biblioteca é criada com êxito, você pode executar o pacote no SQL Server, chamando-o dentro de um procedimento armazenado.
    
    ```SQL
    EXEC sp_execute_external_script
    @language =N'R',
    @script=N'
    library(randomForest)'
    ```

### <a name="known-issues-with-create-external-library"></a>Problemas conhecidos com criar biblioteca externa

Criar biblioteca externa é suportada sob estas condições:

+ Você está instalando um único pacote sem dependências.
+ Você está instalando pacotes com dependências e preparar todos os pacotes com antecedência. 

A instrução DDL falhará se dependências do pacote estão ausentes. Por exemplo, o processo de instalação é conhecido falha nesses casos:

+ Você instalou um pacote que possui dependências de segundo nível e a análise não estender pacotes de segundo nível. Por exemplo, você deseja instalar **gglot2**e identificar todos os pacotes listados no manifesto; no entanto, esses pacotes tinham outras dependências que não foram instaladas.
+ Você instalou um conjunto de pacotes que exigem diferentes versões de um pacote de suporte e seu servidor tiver a versão errada.

## <a name="package-installation-tips"></a>Dicas de instalação do pacote

Esta seção fornece dicas variadas e perguntas comuns relacionadas à instalação do pacote de R no SQL Server.

###  <a name="packageVersion"></a> Obter a versão correta do pacote e o formato

Há várias origens de pacotes de R, como o CRAN e Bioconductor. O site oficial da linguagem R (<https://www.r-project.org/>) lista vários desses recursos. Muitos pacotes são publicados no GitHub, onde é possível obter o código-fonte. Por fim, talvez tenha recebido pacotes R desenvolvidos por alguém de sua empresa, ou você tiver um pacote personalizado que você tenha escrito.

Independentemente da origem, antes de tentar instalar o pacote, verifique se você obteve o formato binário para a plataforma Windows. 

### <a name="bkmk_zipPreparation"></a> Baixe o pacote como um arquivo compactado

Para instalação em um servidor sem acesso à internet, você deve baixar uma cópia do pacote no formato de um arquivo compactado para instalação offline. **Não descompacte o pacote.**

Por exemplo, o procedimento a seguir descreve agora para obter a versão correta do [FISHalyseR](http://bioconductor.org/packages/release/bioc/html/FISHalyseR.html) pacote da Bioconductor, supondo que o computador tem acesso à internet.

1.  Na lista **Arquivos de Pacote** , localize a versão **Binário do Windows** .

2.  Clique no link para o. Arquivo ZIP e selecione **Salvar destino como**.

3.  Navegue até a pasta local onde os pacotes compactados são armazenados e clique em **salvar**.

    Esse processo cria uma cópia local do pacote. 

4. Se você receber um erro de download, tente um site diferente do espelho.

5. Depois que o arquivo de pacote foi baixado, você pode instalar o pacote ou copiar o pacote compactado em um servidor que não tenha acesso à internet.

> [!TIP]
> Se por engano, você instalar o pacote em vez de baixar os binários, uma cópia do arquivo compactado baixado também serão salvos em seu computador. Observe as mensagens de status que o pacote for instalado, para determinar o local do arquivo. Você pode copiar o arquivo compactado para o servidor que não tem acesso à internet.
> 
> No entanto, quando você obter pacotes usando esse método, as dependências não são incluídas. 

### <a name="bkmk_packageDependencies"></a> Obter pacotes necessários

Pacotes de R com frequência dependem de vários pacotes, alguns dos quais podem não estar disponíveis na biblioteca R padrão usada pela instância. Às vezes, um pacote exige uma versão diferente de um pacote dependente que já está instalado.

Se você precisar instalar vários pacotes, ou para garantir que todas as pessoas em sua organização obtém o tipo correto de pacote e versão, é recomendável que você use o [miniCRAN](https://mran.microsoft.com/package/miniCRAN) pacote para analisar a cadeia de dependência completa. minicRAN cria um repositório local que pode ser compartilhado entre vários usuários ou computadores. Para obter mais informações, consulte [criar um repositório de pacote local usando miniCRAN](create-a-local-package-repository-using-minicran.md).


### <a name="know-which-library-you-are-using-for-installation"></a>Saber qual biblioteca que você está usando para instalação

Se você modificou anteriormente o ambiente R no computador, antes de instalar qualquer coisa, pausar um momento e certifique-se de que a variável de ambiente R `.libPath` usa apenas um caminho.

Esse caminho deve apontar para a pasta R_SERVICES para a instância. Para obter mais informações, consulte [pacotes R instalados com o SQL Server](installing-and-managing-r-packages.md).

### <a name="side-by-side-installation-with-r-server"></a>Instalação lado a lado com o servidor de R

Se você tiver instalado o Microsoft Machine Learning Server (autônomo) além de serviços de aprendizado de máquina do SQL Server, o computador deve ter instalações separadas do R para cada um, com as duplicatas de todas as bibliotecas e ferramentas de R.

Pacotes que estão instalados para a biblioteca R_SERVER são usados apenas pelo Microsoft R Server e não podem ser acessados pelo SQL Server. Certifique-se de usar o `R_SERVICES` biblioteca ao instalar os pacotes que você deseja usar no SQL Server.

### <a name="how-to-determine-which-packages-are-already-installed"></a>Como determinar quais pacotes já estão instalados?

 Consulte [pacotes R instalados com o SQL Server](installing-and-managing-r-packages.md)