---
title: Provisionar a VM do SQL Server 2016 Enterprise somente do R Server no Azure | Microsoft Docs
ms.custom: 
ms.date: 06/05/2017
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
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: a3bfca0753984f09220d8ca4e4f6933c949daf2b
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="advanced-analytics-virtual-machines-on-azure"></a>Máquinas virtuais de análise avançada no Azure

Máquinas virtuais no Azure são uma opção conveniente para configurar rapidamente um ambiente de servidor completo para soluções de aprendizado de máquina. Este tópico lista algumas imagens de máquinas virtuais que contêm o R Server, SQL Server com o aprendizado de máquina ou outras ferramentas de ciência de dados da Microsoft.

> [!TIP]
> É recomendável que você use a nova versão do portal do Azure e o Azure Marketplace. Algumas imagens não estão disponíveis ao procurar a Galeria do Azure no portal clássico.

O Azure Marketplace contém várias máquinas virtuais que oferecem suporte a ciência de dados. Essa lista não se destina a ser abrangente, mas forneça somente os nomes de imagens que incluem serviços, para facilitar a descoberta de aprendizado de máquina do Microsoft R Server ou SQL Server.

## <a name="how-to-provision-a-vm"></a>Como provisionar uma máquina virtual

Se você for novo no uso de máquinas virtuais do Azure, recomendamos que você consulte estes artigos para obter mais informações sobre como usar o portal e configurar uma máquina virtual.

+ [Máquinas virtuais – Introdução](https://azure.microsoft.com/documentation/learning-paths/virtual-machines/)
+ [Guia de Introdução com máquinas virtuais do Windows](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-windows-hero-tutorial/)

### <a name="find-an-image"></a>Localizar uma imagem

1. No painel do Azure, clique em **Marketplace**.

    - Clique em **Intelligence e análise** ou **bancos de dados**, e, em seguida, digite "R" o **filtro** controle para ver uma lista de máquinas virtuais do servidor de R.
    - Outros possíveis cadeias de caracteres para o **filtro** controle são *ciência de dados* e *aprendizado de máquina*
    - Use o caractere curinga % na pesquisa para localizar nomes VM que contêm uma cadeia de caracteres de destino, como *R* ou *Julia*.

2. Para obter o R Server para Windows, selecione **R Server somente SQL Server 2016 Enterprise**.
  
    [R Server](https://msdn.microsoft.com/microsoft-r/rserver-whats-new) é licenciado como um recurso do SQL Server Enterprise Edition, mas a versão 9.1. é instalado como um servidor autônomo e atendidas na política de suporte do ciclo de vida modernos.

3. Depois que a máquina virtual tiver sido criada e estiver em execução, clique no botão **Conectar** para abrir uma conexão e fazer logon na nova máquina.

4. Depois de se conectar, você precisará instalar ferramentas de R adicionais ou ferramentas de desenvolvimento.

### <a name="install-additional-r-tools"></a>Instalar ferramentas de R adicionais

Por padrão, o Microsoft R Server inclui todas as ferramentas R instaladas com uma instalação básica do R, incluindo o RTerm e o RGui. Um atalho para o RGui foi adicionado à área de trabalho, se você deseja começar a usar o R imediatamente.

No entanto, você pode desejar instalar ferramentas de R adicionais, como RStudio, as ferramentas de R para Visual Studio (RTVS) ou o cliente do Microsoft R. Consulte os links a seguir para obter instruções e locais de download:
+ [Ferramentas de R para o Visual Studio](https://docs.microsoft.com/visualstudio/rtvs/installation)
+ [Cliente do Microsoft R](https://msdn.microsoft.com/microsoft-r/install-r-client-windows)
+ [RStudio para Windows](https://www.rstudio.com/products/rstudio/download/)

Após a conclusão da instalação, verifique se o local de tempo de execução de R padrão foi alterado para que todas as ferramentas de desenvolvimento de R usem as bibliotecas do Microsoft R Server.

### <a name="configure-server-for-web-services"></a>Configurar o servidor para serviços web

Se a máquina virtual inclui o R Server, será necessário realizar configuração adicional para usar a implantação do serviço Web, a execução remota ou aproveitar o R Server como um servidor de implantação em sua organização. Para obter instruções, consulte [Configurar R Server para operacionalização](https://msdn.microsoft.com/microsoft-r/operationalize/configuration-initial).

> [!NOTE]
> Configuração adicional não é necessária se você quiser apenas para usar os pacotes como RevoScaleR ou MicrosoftML.

## <a name="r-server-images"></a>Imagens de servidor de R

### <a name="microsoft-data-science-virtual-machine"></a>Máquina virtual de ciência de dados da Microsoft

Vem configurado com o Microsoft R Server, bem como Python (distribuição Anaconda), um servidor de notebook Jupyter, Visual Studio Community Edition, Power BI Desktop, o SDK do Azure e SQL Server Express edition.

A versão do Windows é executado no Windows Server 2012 e contém várias ferramentas especiais para modelagem e análise, incluindo CNTK e mxnet, pacotes R populares, como xgboost e Vowpal Wabbit.

### <a name="linux-data-science-virtual-machine"></a>Máquina de Virtual de ciência de dados do Linux

Também contém ferramentas populares para atividades de desenvolvimento e ciência dados, incluindo Microsoft R Open, Microsoft R Server Developer Edition, Anaconda Python e Jupyter blocos de anotações Python, R e Julia.

Esta imagem VM foi atualizada recentemente para incluir JupyterHub, software livre que permite o uso por vários usuários, por meio de métodos de autenticação diferentes, incluindo autenticação de conta local do sistema operacional e autenticação de conta do Github. JupyterHub é uma opção particularmente útil se você deseja executar uma classe de treinamento e deseja que todos os alunos para compartilhar o mesmo servidor, mas use anotações separadas e diretórios.

Imagens são fornecidas para Ubuntu, Centos e Centos CSP.

### <a name="r-server-only-sql-server-2016-enterprise"></a>R Server somente SQL Server 2016 Enterprise

Esta máquina virtual inclui um instalador autônomo para [R Server 9.1.](https://msdn.microsoft.com/microsoft-r/rserver-whats-new) que suporta o novo modelo de licenciamento do ciclo de vida do Software moderno.

 R Server também está disponível nas imagens para CentOS Linux versão 7.2, versão do Linux RedHat 7.2 e Ubuntu 16.04.

 > [!NOTE]
 > Essas máquinas virtuais substituem a **RRE para máquina virtual do Windows** disponível anteriormente no Azure Marketplace.

## <a name="sql-server-images"></a>Imagens do SQL Server

Para usar o R Services (no banco de dados) ou serviços de aprendizado de máquina, você deve instalar uma das máquinas do SQL Server Enterprise ou Developer edition virtual e adicione a serviço, aprendizado de máquina, conforme descrito aqui: [instalando o SQL Server R Services em um Máquina Virtual do Azure](../../advanced-analytics/r-services/installing-sql-server-r-services-on-an-azure-virtual-machine.md).

> [!NOTE]
> Atualmente, os serviços de aprendizado de máquina não têm suporte nas máquinas virtuais Linux para 2017 do SQL Server ou no banco de dados do SQL Azure. Você deve usar o SQL Server 2016 SP1 ou SQL Server 2017 para Windows.

A máquina de Virtual de ciência de dados também inclui o SQL Server 2016 com o recurso de serviços de R já está habilitado.


## <a name="other-vms"></a>Outras VMs

### <a name="deep-learning-toolkit-for-the-data-science-virtual-machine"></a>Profundo Kit de ferramentas de aprendizado de máquina de Virtual de ciência de dados

Esta máquina virtual contém a mesma máquina aprendizado ferramentas disponíveis na máquina Virtual de ciência de dados, mas com as versões GPU do mxnet, CNTK, TensorFlow e Keras. Essa imagem pode ser usada apenas em instâncias de série de GPU N do Azure. 

O Kit de ferramentas de aprendizado também fornece um conjunto de exemplo profundo soluções que usam a GPU, incluindo o reconhecimento de imagem no banco de dados de 10 CIFAR e um exemplo de reconhecimento de caracteres no banco de dados MNIST de aprendizado. Instâncias GPU estão disponíveis atualmente no Centro Sul dos EUA, Leste dos EUA, Europa Ocidental e Sudeste da Ásia.

> [!IMPORTANT]
> As instâncias de GPU só estão disponíveis no Centro-Sul dos EUA no momento.


## <a name="frequently-asked-questions"></a>Perguntas frequentes

### <a name="can-i-install-a-virtual-machine-with-sql-server-2017"></a>Pode instalar uma máquina virtual com o SQL Server 2017?

Imagens estão disponíveis que contêm 2017 CTP 2.0 do SQL Server para ambientes Linux, mas esses ambientes atualmente não dão suporte a serviços de aprendizado de máquina. 

Uma máquina de virtual baseado no Windows para o SQL Server de 2017 Enterprise Edition que inclui serviços de aprendizado de máquina estará disponível após o lançamento. 

Como alternativa, você pode usar a imagem do SQL Server 2016 e atualize sua instância do R, conforme descrito aqui: [atualizar uma instância usando SqlBindR](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md). 

Ou crie uma máquina virtual e baixar a visualização do CTP 2.0 do [SQL Server 2017](https://www.microsoft.com/sql-server/sql-server-2017).

### <a name="how-do-i-access-data-in-an-azure-storage-account"></a>Como acessar os dados em uma conta de Armazenamento do Azure?

Quando você precisar usar os dados da sua conta de armazenamento do Azure, há várias opções para acessá-los ou movê-los:

+ Copie os dados da sua conta de armazenamento para o sistema de arquivos locais usando um utilitário, como o [AzCopy](https://azure.microsoft.com/documentation/articles/storage-use-azcopy/#copy-files-in-azure-file-storage-with-azcopy-preview-version-only). 

+ Adicione os arquivos a um compartilhamento de arquivos em sua conta de armazenamento e, em seguida, monte o compartilhamento de arquivos como uma unidade de rede na sua máquina virtual.  Para obter mais informações, consulte [Montando arquivos do Azure](https://azure.microsoft.com/documentation/articles/storage-dotnet-how-to-use-files/). 

### <a name="how-do-i-use-data-from-azure-data-lake-storage-adls"></a>Como usar o dados do Armazenamento Azure Data Lake (ADLS)?

Você pode ler dados do armazenamento ADLS usando o RevoScaleR, se você fizer referência a conta de armazenamento no sistema de arquivos da mesma maneira que faria com um HDFS usando webHDFS.  Para obter mais informações, consulte este artigo: [R usando para executar operações de sistema de arquivos no repositório Azure Data Lake](https://blogs.msdn.microsoft.com/microsoftrservertigerteam/2017/03/14/using-r-to-perform-filesystem-operations-on-azure-data-lake-store/).

## <a name="see-also"></a>Consulte também

[SQL Server R Services](https://msdn.microsoft.com/library/mt604845.aspx)


