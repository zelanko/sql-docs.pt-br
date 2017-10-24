---
title: "Provisionar uma máquina virtual para o aprendizado de máquina do Azure | Microsoft Docs"
ms.custom: 
ms.date: 10/16/2017
ms.prod: r-server
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: c8826df7-aa67-4768-baa9-bdc875c4a766
caps.latest.revision: 12
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 8cc1fcfdeae8742a93916dfb08c9db1215f88721
ms.openlocfilehash: 7cb9e069fc3b537f8aab9d048a152435ad0cc6ac
ms.contentlocale: pt-br
ms.lasthandoff: 10/17/2017

---
# <a name="provision-a-virtual-machine-for-machine-learning-on-azure"></a>Provisionar uma máquina virtual para o aprendizado de máquina do Azure

Máquinas virtuais no Azure são uma opção conveniente para configurar rapidamente um ambiente de servidor completo para soluções de aprendizado de máquina. Este artigo lista algumas imagens de máquinas virtuais que contêm o R Server, o servidor de aprendizado de máquina ou o SQL Server com o aprendizado de máquina.

Essa lista não se destina a ser abrangente, mas forneça somente os nomes de imagens que estão relacionadas ao servidor de aprendizado de máquina ou serviços de aprendizado de máquina do SQL Server, para facilitar a descoberta.

> [!TIP]
> É recomendável que você use a nova versão do portal do Azure e o Azure Marketplace. Algumas imagens não estão disponíveis ao procurar a Galeria do Azure no portal clássico.

## <a name="how-to-provision-a-virtual-machine"></a>Como provisionar uma máquina virtual

Se você for novo no uso de máquinas virtuais do Azure, recomendamos que você consulte estes artigos para obter mais informações sobre como usar o portal e configurar uma máquina virtual.

+ [Máquinas virtuais – Introdução](https://azure.microsoft.com/documentation/learning-paths/virtual-machines/)
+ [Guia de Introdução com máquinas virtuais do Windows](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-hero-tutorial/)

## <a name="find-a-machine-learning-image"></a>Localizar uma imagem de aprendizado de máquina

1. No portal do Azure (portal.azure.com), clique em **máquinas virtuais**, ou clique em **novo**.

2. Localize a caixa de pesquisa na parte superior da página, você pode usar para filtrar recursos por nome. 

3. Digite "R Server" (ou "ML Server") o **filtro** controle para ver uma lista de recursos relacionados. Clique em **pesquisar no Marketplace** para ver as máquinas virtuais.

    > [!TIP]
    > 
    > Outras cadeias de caracteres possíveis para o controle de filtro são "ciência de dados" e "aprendizado de máquina".
    > 
    > Use o `%` curinga na pesquisa para localizar os nomes de máquinas virtuais. Por exemplo, você pode digitar `"`% % Julia` or `%R %'.

4. Para obter o R Server para Windows, selecione **R Server somente SQL Server 2016 Enterprise**.
  
    [R Server](https://msdn.microsoft.com/microsoft-r/rserver-whats-new) é licenciado como um recurso do SQL Server Enterprise Edition, mas a versão 9.1 é instalado como um servidor autônomo e será atendido na política de suporte do ciclo de vida modernos.

    > [!NOTE] 
    > 
    > Isso se encaixam, procure a versão de uma nova máquina virtual que inclui 2017 do SQL Server e o 9.2.1 versão do servidor de aprendizado de máquina.
    > Até lá, você pode atualizar a versão do SQL Server instalada nesta máquina virtual usando a Central de instalação do SQL Server e escolhendo a opção de atualização. Para obter mais informações, consulte [atualizar o SQL Server usando o Assistente de instalação](https://docs.microsoft.com/sql/database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup).

5. Depois que a máquina virtual foi criada e está em execução, clique no **conectar** botão para abrir uma conexão e fazer logon no novo computador.

5. Depois de se conectar, você pode instalar o pacote de R adicional, ou sua ferramenta de desenvolvimento preferencial.

### <a name="install-additional-r-tools"></a>Instalar ferramentas de R adicionais

Por padrão, o Microsoft R Server inclui todas as ferramentas R instaladas com uma instalação básica do R, incluindo o RTerm e o RGui. Um atalho para RGui também foi adicionado à área de trabalho.

No entanto, você pode desejar instalar ferramentas de R adicionais, como RStudio, ferramentas de R para Visual Studio (RTVS) ou o cliente do Microsoft R. Consulte os links a seguir para obter instruções e locais de download:

+ [Ferramentas de R para o Visual Studio](https://docs.microsoft.com/visualstudio/rtvs/installation)
+ [Cliente do Microsoft R](https://msdn.microsoft.com/microsoft-r/install-r-client-windows)
+ [RStudio para Windows](https://www.rstudio.com/products/rstudio/download/)

Após a conclusão da instalação, verifique se o local de tempo de execução de R padrão foi alterado para que todas as ferramentas de desenvolvimento de R usem as bibliotecas do Microsoft R Server.

### <a name="configure-r-server-to-support-web-services"></a>Configurar o R Server para dar suporte a serviços web

Configuração adicional é necessária para usar a implantação do serviço da web, a execução remota, ou que utilizam o R Server como um servidor de implantação em sua organização. Para obter instruções, consulte [Configurando R Server para colocar a análise em](https://docs.microsoft.com/machine-learning-server/install/operationalize-r-server-one-box-config).

> [!NOTE]
> Configuração adicional não é necessária se você quiser apenas para usar os pacotes como RevoScaleR ou MicrosoftML.

## <a name="other-virtual-machines"></a>Outras máquinas virtuais

As imagens a seguir estão disponíveis no Azure Marketplace e incluem totalmente configuradas ferramentas de aprendizado de máquina, mas não necessariamente incluem SQL Server.

### <a name="data-science-virtual-machine"></a>Máquina de Virtual de ciência de dados

Esta imagem é pré-configurado com o Microsoft R Server, bem como Python (distribuição Anaconda), um servidor de notebook Jupyter, Visual Studio Community Edition, Power BI Desktop, o SDK do Azure e SQL Server Express edition.

A versão do Windows é executado no Windows Server 2012 e contém várias ferramentas especiais para modelagem e análise, incluindo [CNTK](https://www.microsoft.com/cognitive-toolkit/), [mxNet](https://mxnet.incubator.apache.org/), e pacotes de R popular como **xgboost**.

Edições de Linux são fornecidas para Ubuntu, Centos e Centos CSP e contêm muitas ferramentas populares para atividades de desenvolvimento e a ciência de dados.

Para obter mais informações, consulte [Introdução ao Azure ciência da máquina Virtual de dados para Linux e Windows](https://docs.microsoft.com/azure/machine-learning/data-science-virtual-machine/provision-vm).

Esta imagem foi atualizada recentemente para incluir: 

+ Suporte para Julia, a linguagem de ciência de dados escalonáveis, poderosos do futuro 
+ JupyterHub, que é uma opção útil quando você deseja executar uma classe de treinamento e deseja que todos os alunos para compartilhar o mesmo servidor, mas use anotações separadas e diretórios.

Para obter mais informações sobre ferramentas com suporte e estruturas de aprendizado de máquina, consulte [conhecer sua máquina de Virtual de ciência de dados](https://docs.microsoft.com/azure/machine-learning/data-science-virtual-machine/dsvm-tools-overview)

### <a name="r-server-virtual-machines"></a>Máquinas virtuais do servidor de R

Além de **R Server somente SQL Server 2016 Enterprise** imagem, você pode obter as máquinas virtuais autônomas que contêm o R Server. Imagens estão disponíveis para CentOS Linux versão 7.2, versão do Linux RedHat 7.2 e Ubuntu 16.04.

Para obter mais informações, consulte [Server de aprendizado de máquina na nuvem](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-in-the-cloud)

 > [!NOTE]
 > Essas máquinas virtuais substituem a **RRE para máquina virtual do Windows** disponível anteriormente no Azure Marketplace.

### <a name="sql-server-virtual-machines"></a>Máquinas virtuais do SQL Server

Há duas opções para usar no Azure de aprendizado de máquina do SQL Server:

+ Obtenha uma das imagens de máquina virtual que inclui o SQL Server R Services pré-instalado.
+ Criar uma máquina virtual do Azure e instalar o SQL Server Enterprise ou Developer edition usando sua própria chave de licença. 
  
    Em seguida, execute a instalação novamente para adicionar e habilitar a serviço, aprendizado de máquina, conforme descrito aqui: [instalando o SQL Server R Services em uma máquina virtual do Azure](../r/installing-sql-server-r-services-on-an-azure-virtual-machine.md).
+ Crie um banco de dados do SQL do Azure usando uma camada de serviço que pode oferecer suporte ao aprendizado de máquina e usar o novo recurso de R Services atualmente na visualização. Para obter mais informações, consulte [Azure SQL DB](../r/using-r-in-azure-sql-database.md).

> [!NOTE]
> Atualmente, serviços de aprendizado de máquina do SQL Server não tem suporte nas máquinas virtuais Linux para 2017 do SQL Server. No entanto, você pode executar a pontuação em um modelo treinado usando a função PREVER T-SQL. Para obter mais informações, consulte [pontuação nativo no SQl Server](../sql-native-scoring.md). 

### <a name="virtual-machines-for-deep-learning"></a>Máquinas virtuais para o aprendizado 

Anteriormente, fornecidos pela Microsoft o Kit de ferramentas de aprendizado profunda para dados ciência da máquina Virtual, que você pode adicionar a uma Data ciência da máquina Virtual existente. Este Kit de ferramentas agora é substituída pela máquina profunda aprendizado Virtual, que contém as ferramentas de aprendizado populares:

+ Edições de GPU do aprendizado estruturas, como Microsoft cognitivas Toolkit, TensorFlow, Keras e Caffe
+ Drivers internos de GPU
+ Uma coleção de ferramentas para processamento de texto e imagem
+ Ferramentas de desenvolvimento empresarial, como o Microsoft R Server Developer Edition, Python Anaconda, blocos de anotações do Jupyter Python e R
+ Ferramentas de desenvolvimento do Python, R, SQL Server e muito mais
+ Exemplos de ponta a ponta para imagem e compreensão de texto

A máquina Virtual de aprendizado detalhada está disponível no Windows 2016 ou plataformas Ubuntu Linux. Para obter mais informações, consulte [estruturas de aprendizado e AI](https://docs.microsoft.com/azure/machine-learning/data-science-virtual-machine/dsvm-deep-learning-ai-frameworks).

> [!IMPORTANT]
> 
> Implantando a máquina virtual requer que as imagens de máquina virtual de série de GPU NC do Azure, que estão disponíveis em regiões do Azure limitados. Para obter informações sobre disponibilidade, consulte [produtos disponíveis por região](https://azure.microsoft.com/en-us/regions/services/). Quando você provisiona a máquina virtual, certifique-se de usar **HDD** como o tipo de disco, não **SSD**.

## <a name="frequently-asked-questions"></a>Perguntas frequentes

Esta seção contém algumas perguntas comuns sobre máquinas virtuais da Microsoft de aprendizado de máquina.

### <a name="can-i-install-a-virtual-machine-with-sql-server-2017"></a>Pode instalar uma máquina virtual com o SQL Server 2017?

Uma máquina de virtual baseado no Windows para o SQL Server de 2017 Enterprise Edition que inclui serviços de aprendizado de máquina estará disponível em breve. Procure anúncios nesses sites blogs:

+ [Inteligência de Cortana e aprendizado de máquina](https://blogs.technet.microsoft.com/machinelearning/)
+ [Dentro da plataforma de dados](https://blogs.technet.microsoft.com/dataplatforminsider/)

### <a name="how-do-i-access-data-in-an-azure-storage-account"></a>Como acessar os dados em uma conta de Armazenamento do Azure?

Quando você precisar usar os dados da sua conta de armazenamento do Azure, há várias opções para acessá-los ou movê-los:

+ Copie os dados da sua conta de armazenamento para o sistema de arquivos locais usando um utilitário, como o [AzCopy](https://azure.microsoft.com/documentation/articles/storage-use-azcopy/#copy-files-in-azure-file-storage-with-azcopy-preview-version-only). 

+ Adicione os arquivos a um compartilhamento de arquivos em sua conta de armazenamento e, em seguida, monte o compartilhamento de arquivos como uma unidade de rede na sua máquina virtual.  Para obter mais informações, consulte [Montando arquivos do Azure](https://azure.microsoft.com/documentation/articles/storage-dotnet-how-to-use-files/). 

### <a name="how-do-i-use-data-from-azure-data-lake-storage-adls"></a>Como usar o dados do Armazenamento Azure Data Lake (ADLS)?

Você pode ler dados do armazenamento ADLS usando o RevoScaleR, se você fizer referência a conta de armazenamento no sistema de arquivos da mesma maneira que faria com um HDFS usando webHDFS.  Para obter mais informações, consulte este artigo: [R usando para executar operações de sistema de arquivos no repositório Azure Data Lake](https://blogs.msdn.microsoft.com/microsoftrservertigerteam/2017/03/14/using-r-to-perform-filesystem-operations-on-azure-data-lake-store/).



