---
title: "Provisionar uma máquina virtual para o aprendizado de máquina do Azure | Microsoft Docs"
ms.custom: 
ms.date: 10/31/2017
ms.prod: r-server
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: c8826df7-aa67-4768-baa9-bdc875c4a766
caps.latest.revision: "12"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.openlocfilehash: a57f9d0e392818ec1198f3d0a19106e9db9c7810
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="provision-a-virtual-machine-for-machine-learning-on-azure"></a>Provisionar uma máquina virtual para o aprendizado de máquina do Azure

Máquinas virtuais no Azure são uma opção conveniente para configurar rapidamente um ambiente de servidor completo para soluções de aprendizado de máquina.

Este artigo lista as imagens de máquina virtual que contêm o SQL Server com o aprendizado de máquina, bem como algumas VMs relacionadas.

Este artigo também fornece respostas para perguntas comuns sobre como modificar ou atualizar uma instância existente do SQL Server em uma máquina virtual.

+ [Lista de máquinas de virtuais atuais](#bkmk_list)

## <a name="provision-a-virtual-machine-with-sql-server-and-machine-learning"></a>Provisionar uma máquina virtual com o SQL Server e aprendizado de máquina

Se você for novo no uso de máquinas virtuais do Azure, recomendamos que você consulte estes artigos para obter mais informações sobre como usar o portal e configurar uma máquina virtual.

+ [Máquinas virtuais – Introdução](https://azure.microsoft.com/documentation/learning-paths/virtual-machines/)
+ [Guia de Introdução com máquinas virtuais do Windows](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-hero-tutorial/)

Certifique-se de usar a nova versão do portal do Azure ou o Azure Marketplace. Algumas imagens não estão disponíveis ao procurar a Galeria do Azure no portal clássico.

**Criar a máquina virtual**

1. Abra o portal do Azure: [portal.azure.com](https:portal.azure.com).

2. Clique em **máquinas virtuais**, ou clique em **novo**.

3. Clique em **Adicionar**.

4. Na caixa de pesquisa na parte superior da página, digite "Servidor de aprendizado de máquina" ou "SQL Server" para ver uma lista de máquinas de virtuais relacionadas.

5. Examine os requisitos e clique em **criar** para começar.

6. Depois que a máquina virtual foi criada e está em execução, clique no **conectar** botão para abrir uma conexão e fazer logon no novo computador.

5. Depois de se conectar, você pode instalar outros pacotes de R ou Python ou configurar sua ferramenta de desenvolvimento preferencial.

### <a name="connect-to-the-virtual-machine"></a>Conecte-se à máquina virtual

A maneira que um cliente se conecta ao SQL Server em execução em uma máquina virtual difere dependendo do local do cliente e a configuração de rede.

Para obter mais informações, consulte [conectar-se a uma máquina de virtual do SQL Server no Azure](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-connect).

## <a name="frequently-asked-questions"></a>Perguntas frequentes

Esta seção contém algumas perguntas comuns sobre máquinas virtuais da Microsoft de aprendizado de máquina.

### <a name="can-i-install-a-virtual-machine-with-sql-server-2017"></a>Pode instalar uma máquina virtual com o SQL Server 2017?

Uma máquina de virtual baseado no Windows para o SQL Server de 2017 Enterprise Edition que inclui serviços de aprendizado de máquina está disponível a partir de novembro de 2017. 

Para anúncios sobre novas máquinas de virtuais de ciência de dados, assista a esses sites de blog:

+ [Inteligência de Cortana e aprendizado de máquina](https://blogs.technet.microsoft.com/machinelearning/)
+ [Dentro da plataforma de dados](https://blogs.technet.microsoft.com/dataplatforminsider/)

### <a name="adding-sql-server-to-an-existing-virtual-machine"></a>Adicionar o SQL Server para uma máquina virtual existente

Além de criar uma máquina virtual usando uma imagem que já inclui o SQL Server aprendizado de máquina, você pode instalar o SQL Server em uma máquina virtual existente e habilitar a recursos de aprendizado de máquina. Recomendamos a edição Enterprise ou Developer, para evitar limitações de recursos. Instalação também requer que você use sua própria chave de licença.

Quando você executar a instalação, certifique-se de selecionar a recurso e pelo menos um idioma (R ou Python) de aprendizado de máquina. Algumas etapas adicionais são necessárias para habilitar os serviços de aprendizado de máquina para se comunicar com o SQL Server e permitem que a rede na máquina virtual.

Para obter mais informações, consulte [instalando o SQL Server R Services em uma máquina virtual do Azure](../r/installing-sql-server-r-services-on-an-azure-virtual-machine.md).

### <a name="using-machine-learning-in-azure-sql-database"></a>Usando o aprendizado de máquina no banco de dados do SQL Azure

A partir de ficar 2017, banco de dados do SQL Azure oferece suporte ao uso de R para treinar modelos e usá-los para previsão. 

Serviços de R no banco de dados está disponível como um recurso de visualização e tem algumas limitações em comparação com a edição no local do SQL Server. Para obter mais informações, consulte [Azure SQL DB](../r/using-r-in-azure-sql-database.md).

### <a name="can-i-upgrade-the-sql-server-version-on-a-virtual-machine"></a>Posso atualizar a versão do SQL Server em uma máquina virtual?

Embora as imagens do SQL Server 2016 suportam a R, se você quiser usar o Python, você pode atualizar para SQL Server 2017, o que também atualiza a outros componentes do aprendizado de máquina.

Para atualizar a versão do SQL Server está instalado, abra a Central de instalação do SQL Server na máquina virtual e selecione o **atualização** opção. Dependendo de qual máquina virtual criada, uma licença talvez seja necessária.

Para obter mais informações, consulte [atualizar o SQL Server usando o Assistente de instalação](https://docs.microsoft.com/sql/database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup).

### <a name="can-i-upgrade-just-the-machine-learning-components"></a>É possível atualizar apenas a componentes de aprendizado de máquina?

Quando novas atualizações são publicadas para RevoScaleR, MicrosoftML ou revoscalepy, você pode atualizar a componentes usados pelo SQL Server, usando um processo conhecido como de aprendizado de máquina _associação_. Isso não alterar a sua versão do SQL Server, mas a política de suporte para a instância.

Para obter mais informações, consulte [SqlBindR de uso para atualizar os componentes de aprendizado de máquina no SQL Server](../r/use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md).

### <a name="how-do-i-access-data-in-an-azure-storage-account"></a>Como acessar os dados em uma conta de Armazenamento do Azure?

Quando você precisar usar os dados da sua conta de armazenamento do Azure, há várias opções para acessá-los ou movê-los:

+ Copie os dados da sua conta de armazenamento para o sistema de arquivos locais usando um utilitário, como o [AzCopy](https://azure.microsoft.com/documentation/articles/storage-use-azcopy/#copy-files-in-azure-file-storage-with-azcopy-preview-version-only). 

+ Adicione os arquivos a um compartilhamento de arquivos em sua conta de armazenamento e, em seguida, monte o compartilhamento de arquivos como uma unidade de rede na sua máquina virtual. Para obter mais informações, consulte [Montando arquivos do Azure](https://azure.microsoft.com/documentation/articles/storage-dotnet-how-to-use-files/). 

### <a name="how-do-i-use-data-from-azure-data-lake-storage-adls"></a>Como usar o dados do Armazenamento Azure Data Lake (ADLS)?

Você pode ler dados do armazenamento ADLS usando o RevoScaleR, usando webHDFS para fazer referência a conta de armazenamento no sistema de arquivos da mesma maneira que faria com um HDFS. Para obter mais informações, consulte este artigo: [R usando para executar operações de sistema de arquivos no repositório Azure Data Lake](https://blogs.msdn.microsoft.com/microsoftrservertigerteam/2017/03/14/using-r-to-perform-filesystem-operations-on-azure-data-lake-store/).

### <a name="i-cant-find-the-rre-virtual-machine"></a>Não é possível localizar a máquina virtual RRE

O "RRE para máquina Virtual do Windows", que estava disponível anteriormente no Azure Marketplace foi substituído pela imagem "Machine Learning Server para Windows".

Imagens de servidor de aprendizado de máquina também estão disponíveis para CentOS Linux versão 7.2, versão do Linux RedHat 7.2 e Ubuntu 16.04.

Para obter mais informações, consulte [Server de aprendizado de máquina na nuvem](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-in-the-cloud)

### <a name="configuring-machine-learning-server-or-r-server-to-support-web-services"></a>Configurando o servidor de aprendizado de máquina ou R Server para dar suporte a serviços web

Se você usar uma máquina virtual que inclui o servidor de aprendizado de máquina, a configuração adicional pode ser necessária para usar a implantação do serviço da web, a execução remota, ou para usar a máquina virtual como um servidor de implantação em sua organização.

Para obter instruções, consulte [configurar servidor de aprendizado de máquina para colocar análise em](https://docs.microsoft.com/machine-learning-server/operationalize/configure-machine-learning-server-one-box).

Configuração adicional não é necessária se você quiser apenas para usar os pacotes como RevoScaleR ou MicrosoftML.

## <a name="bkmk_list"></a>Lista de máquinas virtuais

Atualmente, as seguintes máquinas virtuais estão disponíveis para o aprendizado de máquina com o SQL Server:

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
|Máquina de Virtual de ciência de dados |As edições de Linux incluem R Server. Máquinas virtuais do Linux que incluem 2017 do SQL Server não pode executar código R ou Python no SQL Server. No entanto, você pode executar a pontuação em um modelo treinado usando a função PREVER T-SQL. Para obter mais informações, consulte [pontuação nativo no SQl Server](../sql-native-scoring.md).|
