---
title: "Novidades no SQL Server R Services | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "01/20/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 6aff043a-8b37-4f3f-9827-10a671e1ad1c
caps.latest.revision: 36
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 35
---
# Novidades no SQL Server R Services
  O [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] é um recurso do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] e do SQL Server vNext que dá suporte à ciência de dados de escala corporativa.  R é a linguagem de programação mais popular para análise avançada e oferece um conjunto incrivelmente rico de pacotes e uma comunidade de desenvolvedores vibrante e em rápido crescimento. O [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] ajuda você a adotar a linguagem R de software livre extremamente popular em sua empresa. 
  
 > [!TIP]Já tem o SQL Server 2016 R Services?
 > Agora, você pode instalar a versão mais recente do Microsoft R Server em suas instâncias 2016, para ter acesso a atualizações mais frequentes para componentes do R. Para saber mais, veja [Microsoft R Server 9.0.1](https://msdn.microsoft.com/microsoft-r/rserver-whats-new).  

## <a name="whats-new-in-sql-server-vnext"></a>Novidades no SQL Server vNext
  
+ Apresentando o pacote **MicrosoftML**

   O MicrosoftML é um novo pacote de aprendizado de máquina para o R desenvolvido pelas equipes do Microsoft R Server e de Ciência de Dados da Microsoft. O MicrosoftML oferece maior velocidade, desempenho e escala para lidar com um grande corpus de dados de texto e dados categóricos altamente dimensionais em modelos do R com apenas algumas linhas de código. Além disso, os clientes do Microsoft R Server terão acesso aos cinco aprendizes rápidos e altamente precisos incluídos no Azure Machine Learning. 
   
   Para obter mais informações, consulte [Usando o pacote MicrosoftML com o SQL Server R Services](../../advanced-analytics/r-services/using-the-microsoftml-package-with-sql-server-r-services.md).
   
+ Gerenciamento de pacotes mais fácil para os cientistas de dados

  Você não precisa mais depender do administrador de banco de dados para instalar os pacotes do R necessários para o SQL Server. As novas funções de instalação e desinstalação do pacote no **RevoScaleR** permitem que você instale e atualize pacotes com facilidade no R Services por meio de um computador cliente. 
  
  Para o administrador de banco de dados, as novas funções são incluídas no [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] para gerenciar as permissões associadas aos pacotes, tanto no nível de instância quanto de banco de dados. 
  
  Para obter mais informações, consulte [Gerenciamento de pacotes do R para o SQL Server R Services](../../advanced-analytics/r-services/r-package-management-for-sql-server-r-services.md). 
     
+ Novas funções no **RevoScaleR** para leitura e gravação de objetos de modelo do R

  O RevoScaleR agora inclui novas funções de serialização e um formato de armazenamento de modelos mais compacto, para acelerar a velocidade do carregamento e da leitura de um modelo. 
  
  Para obter mais informações, consulte [Salvar e carregar objetos do R no SQL Server usando o ODBC](../../advanced-analytics/r-services/save-and-load-r-objects-from-sql-server-using-odbc.md). 

+ Pacote **sqlrutils** para integração mais fácil do SQL

  Esse pacote do R ajuda você a gerar a chamada de procedimento armazenado SQL para o código R. Os procedimentos armazenados SQL gerados poderão, em seguida, ser usados no SQL Server R Services. São fornecidos exemplos para ajudá-lo a consolidar o código R em uma função que pode ser parametrizada em um procedimento armazenado SQL.
  
  Para obter mais informações, consulte [Gerando um procedimento armazenado do R para o código do R usando o pacote sqlrutils](../../advanced-analytics/r-services/generating-an-r-stored-procedure-for-r-code-using-the-sqlrutils-package.md). 
  

+ Pacote **olapR** para uma conexão fácil com o SSAS

   Esse novo pacote fornece uma nova dimensão de conectividade para o R e o SQL Server Analysis Services, facilitando o uso de dados OLAP para análise no R. Execute consultas MDX existentes e retorne um quadro de dados do R ou crie instruções MDX simples definindo eixos de cubo e segmentações no código R. 
   
   Para obter mais informações, consulte [Usando dados de cubos OLAP no R](../../advanced-analytics/r-services/using-data-from-olap-cubes-in-r.md).
   

  
## <a name="features-in-sql-server-2016-r-services-and-sql-server-vnext"></a>Recursos do SQL Server 2016 R Services e SQL Server vNext  
  
- O pacote **RevoScaleR** para o aprendizado de máquina rápido e paralelizável com o R.

-   Dá suporte a logons SQL e à autenticação integrada do Windows.  
    
-   Melhorias de desempenho significativas, incluindo otimização dos processos Satélite do SQL, que se conectam ao R e ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], suporte para paginação de dados para permitir o uso de um alto volume de dados, bem como streaming para permitir o processamento rápido de bilhões de linhas. 
  
-   Use pools de recursos do SQL Server para gerenciar a memória usada pelos processos do R. Para obter mais informações, consulte [CREATE EXTERNAL RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-resource-pool-transact-sql.md).  
  

### <a name="tools-and-setup"></a>Ferramentas e instalação

-   Fácil instalação de todos os componentes. O assistente de instalação do SQL Server pode instalar o **SQL Server R Services (no Banco de Dados)** ou o **Microsoft R Server (Autônomo)**.   Ao executar o assistente de instalação, escolha R Services se estiver configurando uma instância do SQL Server e R Server (Autônomo) se estiver configurando uma estação de trabalho de ciência de dados.   Para obter mais informações sobre as opções de configuração, consulte [Instalar o SQL Server R Services &#40;no Banco de Dados&#41;](../../advanced-analytics/r-services/set-up-sql-server-r-services-in-database.md) ou [Criar um R Server autônomo](../../advanced-analytics/r-services/create-a-standalone-r-server.md).  

-   Caso você não precise usar dados no SQL Server, considere o uso do [!INCLUDE[rsql_platform](../../includes/rsql-platform-md.md)], que é executado em uma ampla variedade de plataformas e que oferece escala corporativa e desempenho para a linguagem R popular de software livre. [!INCLUDE[rsql_platform](../../includes/rsql-platform-md.md)]. Para obter detalhes, consulte [R Server &#40;Autônomo&#41;](../../advanced-analytics/r-services/r-server-standalone.md) ou [Introducing Microsoft R Server](https://msdn.microsoft.com/microsoft-r/rserver) (Apresentando o Microsoft R Server) no MSDN.

- Para atualizar a instância do SQL Server 2016 para usar o Microsoft R Server 9.0.1, use o [utilitário SqlBindR.exe](https://msdn.microsoft.com/library/mt791781.aspx).  

- O [Cliente do Microsoft R](https://msdn.microsoft.com/microsoft-r/r-client-install) é um ambiente do R gratuito que inclui todas as ferramentas e bibliotecas necessárias para criar soluções do R executadas no R Services ou no R Server.  

-   As Ferramentas do R para Visual Studio são um plug-in gratuito para o Visual Studio com suporte avançado para o R, incluindo as janelas de variáveis padrão e interativas do R, IntelliSense para funções do R, depuração e Markdown do R, completas com a exportação para Word e HTML.  Para obter mais informações, consulte [Ferramentas do R para Visual Studio](https://www.visualstudio.com/vs/rtvs/).  

## <a name="learn-more"></a>Saiba mais
  
-  Os recursos estão disponíveis para cientistas de dados que desejam saber mais sobre a integração do SQL Server e para desenvolvedores do SQL que desejam criar soluções do R usando o T-SQL e o ambiente já conhecido do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. 
   + [Tutoriais do SQL Server R Services](https://msdn.microsoft.com/library/mt591993.aspx)
   + [Livro eletrônico gratuito: Data Science with SQL Server 2016](https://mva.microsoft.com/ebooks/) (Ciência de dados com o SQL Server 2016)
 
+ Se você precisar de soluções prontas, os [modelos de aprendizado de máquina](https://blogs.technet.microsoft.com/machinelearning/2016/03/23/machine-learning-templates-with-sql-server-2016-r-services/) desenvolvidos pela equipe de ciência de dados da Microsoft demonstram soluções práticas para tarefas analíticas comuns, como manutenção preditiva e prevenção contra variação.
 

  
## <a name="see-also"></a>Consulte também  
[Novidades do SQL Server vNext](../../sql-server/what-s-new-in-sql-server-vnext.md)
  