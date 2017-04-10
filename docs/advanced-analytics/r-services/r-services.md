---
title: "R Services | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "12/20/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 341e80f5-3b59-4122-bbaa-969d7904297d
caps.latest.revision: 21
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 20
---
# R Services
  O Microsoft R Services oferece duas plataformas de servidor para integrar a popular linguagem R de software livre a aplicativos de negócios: **SQL Server R Services (no Banco de Dados)**, para integração ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], e **Microsoft R Server**.  
  
-   **R Services (no Banco de Dados)**  
  
     A meta do [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] é permitir processos de desenvolvimento, de implantação e de operacionalização rápidos de soluções do R baseadas na plataforma [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e em serviços relacionados.  
  
     O [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] leva a computação para os dados, permitindo que o R seja executado no mesmo computador que o banco de dados. Ele inclui um serviço de banco de dados que é executado fora do processo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e se comunica com segurança com o tempo de execução do R. É possível treinar os modelos do R, gerar gráficos do R, realizar a pontuação e mover dados com facilidade entre o R e o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Cientistas de dados que testam e desenvolvem soluções podem se comunicar com o servidor por meio de um computador de desenvolvimento remoto para executar o código R no servidor e implantar as soluções concluídas no SQL Server inserindo chamadas no R em procedimentos armazenados.  
  
     Este download inclui uma distribuição da linguagem R de software livre, bem como o ScaleR, um conjunto de pacotes do R escalonáveis e de alto desempenho. Ele também inclui provedores para conectividade mais fácil e rápida, com todas as tecnologias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
     Para obter mais informações, consulte [SQL Server R Services](../../advanced-analytics/r-services/sql-server-r-services.md). Para obter cenários de exemplo, consulte [Tutoriais do SQL Server R Services](../../advanced-analytics/r-services/sql-server-r-services-tutorials.md).  
  
-   **Microsoft R Server**  
  
     Este sistema de servidor autônomo oferece suporte a soluções R distribuídas e escalonáveis em várias plataformas e usando várias fontes de dados empresariais, inclusive Linux, Hadoop e Teradata.  
  
     Para obter mais informações, consulte [Microsoft R Server (MSDN)](https://msdn.microsoft.com/microsoft-r/index).  
  
## <a name="related-technologies"></a>Tecnologias relacionadas  
 A Microsoft fornece amplo suporte para o ecossistema de linguagem R de software livre, incluindo ferramentas, provedores, pacotes de R aprimorados e ambientes de desenvolvimento integrado.  
  
-   **Ferramentas de R para o Visual Studio**  
  
     O Visual Studio fornece um ambiente de desenvolvimento completo para a linguagem R. O plug-in inclui editor, janela interativa, plotagem, depurador e muito mais. Você pode usar linguagens .NET de R ou invocar R do .NET por meio de bibliotecas de software livre, como R.NET e rClr.  
  
     Para obter mais informações, consulte [Ferramentas do R para Visual Studio](https://www.visualstudio.com/vs/rtvs/).  
  
-   **R no Azure Machine Learning**  
  
     Crie seu próprio espaço de trabalho no Estúdio de Aprendizado de Máquina do Azure , onde você pode acessar mais de 400 pacotes R pré-carregados. Crie e treine modelos para implantar como um serviço Web ou grave scripts personalizados para transformar dados. Crie seus próprios pacotes de R e carregue-os no Azure para executar como módulos personalizados e publicar soluções no [Marketplace do Aprendizado de Máquina](http://datamarket.azure.com/browse/data?category=machine-learning).  
  
     Para obter mais informações, consulte [Estender seu experimento com o R](https://docs.microsoft.com/azure/machine-learning/machine-learning-extend-your-experiment-with-r) e [Criar módulos do R personalizados no Azure Machine Learning](https://docs.microsoft.com/azure/machine-learning/machine-learning-custom-r-modules).  
  
-   **Máquinas virtuais de ciência de dados**  
  
     É possível implantar uma versão pré-instalada e pré-configurada do [!INCLUDE[rsql_platform](../../includes/rsql-platform-md.md)] no Microsoft Azure, facilitando a introdução à exploração de dados e modelagem imediatamente na nuvem, sem a necessidade de um sistema local totalmente configurado.  
  
     O Azure Marketplace contém várias máquinas virtuais que dão suporte à ciência de dados:
     + A **Máquina Virtual de Ciência de Dados da Microsoft** é configurada com o Microsoft R Server, bem como o Python (distribuição Anaconda), um servidor de bloco de notas Jupyter, o Visual Studio Community Edition, o Power BI Desktop, o SDK do Azure e o SQL Server Express Edition. 
     + O **Microsoft R Server 2016 para Linux** contém a última versão do R Server (versão 9.0.1). VMs separadas estão disponíveis para CentOS versão 7.2 e Ubuntu versão 16.04. 
     + A máquina virtual do **R Server Only SQL Server 2016 Enterprise** inclui um instalador autônomo para o R Server 9.0.1 que dá suporte ao novo modelo de licenciamento do Ciclo de Vida de Software Moderno.
 

## <a name="see-also"></a>Consulte também  
[Introdução ao SQL Server R Services](../../advanced-analytics/r-services/getting-started-with-sql-server-r-services.md) 

[Introdução ao Microsoft R Server](../../advanced-analytics/r-services/getting-started-with-microsoft-r-server-standalone.md)  

 [Instalar o Mecanismo de Banco de Dados do SQL Server](../../database-engine/install-windows/install-sql-server-database-engine.md)  
  
  