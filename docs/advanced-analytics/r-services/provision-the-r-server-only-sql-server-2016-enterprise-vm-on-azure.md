---
title: "Provisionar a m&#225;quina virtual do R Server Only SQL Server 2016 Enterprise no Azure | Microsoft Docs"
ms.custom: ""
ms.date: "12/22/2016"
ms.prod: "r-server"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: c8826df7-aa67-4768-baa9-bdc875c4a766
caps.latest.revision: 12
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 5
---
# Provisionar a m&#225;quina virtual do R Server Only SQL Server 2016 Enterprise no Azure

A máquina virtual do R Server Only SQL Server 2016 Enterprise é uma nova opção para a configuração rápida e fácil de um ambiente de servidor para dar suporte a soluções R. Esta máquina virtual do Azure foi pré-configurada com o Microsoft R Server (autônomo). 

Esta nova máquina virtual substitui a RRE para máquina virtual do Windows disponível anteriormente no Azure Marketplace. 

Esta máquina virtual também inclui o DeployR Enterprise para a implantação de análise de linguagem R dentro de aplicativos e sistemas de back-end. Para obter mais informações, consulte [Sobre a implantação da linguagem R](https://msdn.microsoft.com/microsoft-r/deployr-about).


## Provisionar a máquina virtual do R Server

Se você estiver usando máquinas virtuais do Azure pela primeira vez, recomendamos que você consulte este artigo para obter mais informações sobre como usar o portal e configurar uma máquina virtual.
[Máquinas virtuais – Introdução](https://azure.microsoft.com/documentation/learning-paths/virtual-machines/)

Para criar a máquina virtual do Servidor R do Microsoft Azure Marketplace 
1. Clique em **Máquinas virtuais**, e na caixa de pesquisa, digite *Servidor R*.
2. Selecione **R Server Only SQL Server 2016 Enterprise**
3. Continue provisionando a máquina virtual conforme descrito neste artigo: [https://azure.microsoft.com/documentation/articles/virtual-machines-windows-hero-tutorial/](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-windows-hero-tutorial/) 
7. Depois que a máquina virtual tiver sido criada e estiver em execução, clique no botão **Conectar** para abrir uma conexão e fazer logon na nova máquina.
8. Quando você se conectar, o **Gerenciador de Servidores** é aberto por padrão, mas não é necessária nenhuma configuração adicional de servidor. Feche o **Gerenciador de Servidores** para acessar a área de trabalho e prossiga com as próximas etapas:
    + Instalando ferramentas de R adicionais ou ferramentas de desenvolvimento
    + Configurando o DeployR  

Para localizar a máquina virtual do Servidor R no portal clássico do Azure
1. Clique em **Máquinas virtuais** e, em seguida, clique em **NOVA**.
2. No painel **Novo**, **Computação** e **Máquina virtual** já devem estar selecionados. 
3. Clique em **Da galeria** para localizar a imagem da máquina virtual. Você pode digitar *servidor R* na caixa de pesquisa ou clique em **Microsoft** e, em seguida, role para baixo até ver **R Server Only SQL Server 2016 Enterprise**.


## Instalar as ferramentas de R
Por padrão, o Microsoft R Server inclui todas as ferramentas R instaladas com uma instalação básica do R, incluindo o RTerm e o RGui. Um atalho para o RGui foi adicionado à área de trabalho, se você deseja começar a usar o R imediatamente.

No entanto, instale outras ferramentas de R, como RStudio, Ferramentas de R para o Visual Studio ou o cliente do Microsoft R. Consulte os links a seguir para obter instruções e locais de download:
+ [Ferramentas de R para o Visual Studio](https://www.visualstudio.com/features/rtvs-vs.aspx)
+ [Cliente do Microsoft R](https://msdn.microsoft.com/microsoft-r/install-r-client-windows)
+ [RStudio para Windows](https://www.rstudio.com/products/rstudio/download/)

Depois de instalar essas ferramentas, certifique-se de apontar suas ferramentas para bibliotecas do R Server.

## Usando o DeployR na máquina Virtual

É preciso seguir mais algumas etapas para usar a instância do DeployR instalada nesta máquina virtual. 

Para configurar a instância do DeployR:

1. Na máquina virtual, abra o **utilitário do administrador do DeployR**.
2. Defina a senha de administrador do DeployR conforme descrito aqui: [etapas pós-instalação](https://msdn.microsoft.com/microsoft-r/deployr-install-on-windows)
3. Defina o contexto do DeployR Web. Para obter mais informações, consulte [Instalação do DeployR Admin na nuvem](https://msdn.microsoft.com/microsoft-r/deployr-admin-install-in-cloud) 
4. Abra as portas apropriadas na máquina virtual, conforme descrito aqui: [Configurando pontos de extremidade do Azure](https://msdn.microsoft.com/microsoft-r/deployr-admin-install-in-cloud#configuring-azure-endpoints) 
4. Atualize o Firewall do Windows conforme descrito aqui: [Atualizando o firewall](https://msdn.microsoft.com/microsoft-r/deployr-admin-install-in-cloud#updating-the-firewall) 

## Acessando dados em uma conta de armazenamento do Azure 

Quando você precisar usar os dados da sua conta de armazenamento do Azure, há várias opções para acessá-los ou movê-los:


+ Copie os dados da sua conta de armazenamento para o sistema de arquivos locais usando um utilitário, como o [AzCopy](https://azure.microsoft.com/documentation/articles/storage-use-azcopy/#copy-files-in-azure-file-storage-with-azcopy-preview-version-only). 

+ Adicione os arquivos a um compartilhamento de arquivos em sua conta de armazenamento e, em seguida, monte o compartilhamento de arquivos como uma unidade de rede na sua máquina virtual.  Para obter mais informações, consulte [Montando arquivos do Azure](https://azure.microsoft.com/documentation/articles/storage-dotnet-how-to-use-files/). 

## Usando dados de uma conta do ADLS (Azure Data Lake Storage)

Você poderá ler dados do armazenamento do ADLS usando o ScaleR se você fizer referência à conta de armazenamento da mesma forma que você faria com o sistema de arquivos HDFS, usando o webHDFS.  Para obter mais informações, consulte este [guia de instalação](http://go.microsoft.com/fwlink/?LinkId=723452).

## Recursos

Você pode encontrar mais informações sobre o Microsoft R na biblioteca MSDSN: [R Server e Escala R](https://msdn.microsoft.com/microsoft-r)  


Consulte estes recursos adicionais para saber mais sobre o R em geral: 
+ [DataCamp](http://www.datacamp.com) Oferece um curso introdutório e intermediário gratuito em R e um curso sobre como trabalhar com Big Data usando o Revolution R.
+ [Stack Overflow](http://www.stackoverflow.com) Um bom recurso para perguntas sobre programação R e ferramentas ML. 
+ [Cross Validated](https://stats.stackexchange.com/) Site de perguntas sobre problemas de estatísticas no aprendizado de máquina.
+ [Arquivos da lista de correspondência da Ajuda do R](https://www.r-project.org/mail.html) Bom recurso de informações históricas. 
+ [Site MRAN](https://mran.microsoft.com/documents/getting-started/) Muitos outros recursos do R.  

## Consulte também
[SQL Server R Services](https://msdn.microsoft.com/library/mt604845.aspx)
