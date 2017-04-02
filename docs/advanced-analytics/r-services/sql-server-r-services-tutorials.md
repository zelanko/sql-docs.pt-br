---
title: "Tutoriais do SQL Server R Services | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/17/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to: 
  - "SQL Server 2016"
dev_langs: 
  - "R"
ms.assetid: 5ccc75f6-6703-47d9-b879-9a740569b45e
caps.latest.revision: 31
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 27
---
# Tutoriais do SQL Server R Services
Use esses tutoriais para saber mais sobre o [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] e os cenários de ciência de dados a que ele dá suporte, incluindo:

+ Desenvolver modelos em R e implantá-los no SQL Server
+ Operacionalizar código em R implantando uma solução em R desenvolvida por um cientista de dados em um servidor ou em outro ambiente de produção.
+ Mover dados entre R e o SQL Server
+ Como usar contextos de computação local e remoto
  

## <a name="a-namebkmkend-to-endadeveloping-an-end-to-end-advanced-analytics-solution"></a><a name="bkmk_end-to-end"></a>Desenvolvendo uma solução de análise avançada de ponta a ponta  

[Passo a passo de ponta a ponta sobre a ciência de dados](../../advanced-analytics/r-services/data-science-end-to-end-walkthrough.md) 

Tenha a experiência do processo de ciência de dados de ponta a ponta, da aquisição e análise de dados à pontuação. Aprenda a usar dados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e coloque seu modelo em operação, salvando-o no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
Importe o conjunto de dados de táxis de Nova York para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando o PowerShell e explore os dados usando R. 

Em seguida, crie um modelo preditivo e implante o modelo em R para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a fim de classificar o modo preditivo simples e em banheira. 

  
Este tutorial é destinado a pessoas que têm mais familiaridade com R, assim como ferramentas de desenvolvedor, tais como PowerShell e SQL Server Management Studio. Você deve ter acesso a um ambiente de desenvolvimento de R e familiaridade com comandos de R. 
  
## <a name="a-namebkmkdatascienceadata-science-deep-dive"></a><a name="bkmk_dataScience"></a>Aprofundamento da ciência de dados  

[Introdução ao RevoScaleR e ao SQL Server](http://go.microsoft.com/fwlink/?LinkID=691640&clcid=0x809)  

Este passo a passo é um bom começo para cientistas de dados ou desenvolvedores já familiarizados com a linguagem R, e que querem aprender sobre as funções e os pacotes de R avançados do Microsoft R pela Revolution Analytics. 

Você aprenderá como usar as funções nos pacotes ScaleR para mover dados entre R e SQL, e para alternar contextos de computação para se adequarem a uma tarefa específica. Você criará alguns modelos e gráficos e os moverá entre o ambiente de desenvolvimento e o SQL Server.  
  
Este tutorial destina-se a pessoas que utilizam o R e querem aprender sobre como o RevoScaleR e o SQL Server podem aprimorar a experiência de R.

## <a name="in-database-advanced-analytics-for-the-sql-developer"></a>Análise avançada no banco de dados para o desenvolvedor do SQL  
  
[Análise avançada no banco de dados para desenvolvedores do SQL &#40;Tutorial&#41;](../../advanced-analytics/r-services/in-database-advanced-analytics-for-sql-developers-tutorial.md)

Crie e implante uma solução completa de análise avançada usando o [!INCLUDE[tsql](../../includes/tsql-md.md)]. Este exemplo se concentra em como integrar a linguagem R de software livre ao mecanismo de banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Você aprenderá a encapsular o código R em um procedimento armazenado, salvar um modelo do R em um banco de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e fazer chamadas parametrizadas para o modelo do R para previsão. 
  
Este tutorial destina-se a desenvolvedores de SQL, desenvolvedores de aplicativos ou DBAs do SQL que darão suporte a soluções de R e querem saber como implantar modelos em R no SQL Server.  Nenhum ambiente de R é necessário; todo o código R é fornecido e você pode criar a solução completa usando apenas o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] e ferramentas familiares de business intelligence e de desenvolvimento do SQL.   

## <a name="use-r-services-in-an-application"></a>Usar serviços R em um aplicativo

[Compilar um aplicativo inteligente com o SQL Server e R](https://www.microsoft.com/sql-server/developer-get-started/r)

Neste tutorial, você aprenderá como uma empresa de aluguel de esqui pode usar o machine learning para prever o futuras locações, o que ajuda a equipe e plano de negócios a atender às demandas futuras.


## <a name="using-r-code-in-t-sql"></a>Usando o código R no T-SQL  

[Usando o código R no Transact-SQL &#40;SQL Server R Services&#41;](../../advanced-analytics/r-services/using-r-code-in-transact-sql-sql-server-r-services.md)  

Uma série de exemplos autônomos muito breves que demonstram a sintaxe básica do uso do R no [!INCLUDE[tsql](../../includes/tsql-md.md)]. 

Você aprenderá a chamar o tempo de execução de R do SQL, conhecerá as principais diferenças de tipos de dados entre R e SQL, encapsulará funções R no código SQL e executará um procedimento armazenado que salva a saída de R para uma tabela SQL.
  
Este tutorial é para as pessoas que são novas no R Services e querem aprender os fundamentos de como chamar o R usando o T-SQL. Nenhuma experiência com R é necessária. No entanto, você deve saber como usar o SQL Server Management Studio ou qualquer outra ferramenta que possa se conectar a um banco de dados e executar consultas simples de T-SQL.

  
## <a name="a-namebkmkprerequisitesaprerequisites"></a><a name="bkmk_Prerequisites"></a>Pré-requisitos
  
Para executar qualquer um destes tutoriais, você precisa baixar e instalar o **R Services (no banco de dados)** conforme descrito aqui:  [Instalar o SQL Server R Services](../../advanced-analytics/r-services/set-up-sql-server-r-services-in-database.md)

Depois de executar a instalação do SQL Server, não se esqueça destas etapas adicionais:
+ Habilitar o R Services executando *sp_configure*
+ Reiniciar o servidor
+ Verifique se o serviço que chama o tempo de execução do R tem as permissões necessárias
+ Verifique se o logon do SQL ou a conta de usuário do Windows que você usará para seu código R tem as permissões necessárias para se conectar ao servidor e seus bancos de dados

Se você tiver problemas, consulte este artigo que trata de alguns problemas comuns: [Upgrade and Installation of SQL Server R Services](../../advanced-analytics/r-services/upgrade-and-installation-faq-sql-server-r-services.md) (Atualização e instalação do SQL Server R Services)

Se ainda não tiver um ambiente de desenvolvimento de R preferido, você poderá instalar uma destas ferramentas para começar:

+ [Cliente do Microsoft R](https://msdn.microsoft.com/microsoft-r/r-client-get-started)
+ [Ferramentas de R para o Visual Studio](https://www.visualstudio.com/vs/rtvs/)

Observe que as bibliotecas de R padrão são suficientes para usar esses tutoriais; seu ambiente de desenvolvimento de R e o computador do SQL Server que executa o R devem ter os pacotes ScaleR da Microsoft. Para obter mais informações sobre o que há no Microsoft R, consulte este artigo: [Produtos Microsoft R](https://msdn.microsoft.com/microsoft-r/microsoft-r-getting-started#compare-prods).

## <a name="additional-resources"></a>Recursos adicionais

Quando tiver concluído estes tutoriais, use os links a seguir para exibir exemplos e cenários mais avançados.
  
### <a name="end-to-end-solution-templates-for-key-machine-learning-tasks"></a>Modelos de solução de ponta a ponta para as principais tarefas de aprendizado de máquina  

[Machine Learning Templates with SQL Server 2016 R Services](https://blogs.technet.microsoft.com/machinelearning/2016/03/23/machine-learning-templates-with-sql-server-2016-r-services/) (Modelos de aprendizado de máquina com o SQL Server 2016 R Services).  

A equipe do Microsoft Machine Learning forneceu um conjunto de modelos personalizáveis para ajudá-lo a promover uma solução de aprendizado de máquina para essas tarefas importantes de aprendizado de máquina:  
* Detecção de fraudes  
* Previsão de variação personalizada  
* Manutenção preditiva  
  
Todo o código T-SQL e R é fornecido, juntamente com instruções sobre como treinar e implantar um modelo de pontuação usando os procedimentos armazenados do SQL Server. 

### <a name="sample-data-and-sample-scripts"></a>Dados e scripts de exemplo  
Amostras do produto do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] estão disponíveis no Centro de Download da Microsoft. Para obter apenas as amostras do [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], selecione o arquivo zip e abra a pasta **Análise Avançada**.  Algumas das instruções são para versões anteriores, mas há uma demonstração de detecção de fraudes de seguros baseada na lei de Benford e uma explicação simples de um modelo preditivo em um conjunto de dados muito pequeno (o conjunto de dados Iris) que pode ser útil para demonstrações.
  
[Exemplos de produto do SQL Server 2016](https://www.microsoft.com/en-us/download/details.aspx?id=49502)  
### <a name="learn-more-about-r"></a>Saiba mais sobre o R  
Para saber mais sobre o R em geral, consulte um dos vários excelentes recursos listados aqui: [Recursos da linguagem R](http://revolutionanalytics.com/r-language-resources).  
  
Para obter mais informações sobre os pacotes do R fornecidos no [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], visite o  [site da Revolution Analytics](http://go.microsoft.com/fwlink/?LinkId=691541).  
  
Esta postagem de blog descreve o processo de usar os pacotes e as funções do R fornecidos pelo [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] para se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]e inclui o código de exemplo: [Usando o R no SQL Server](http://blog.revolutionanalytics.com/2015/10/previewing-using-revolution-r-enterprise-inside-sql-server.html).  
  
## <a name="see-also"></a>Consulte também  
[Introdução ao SQL Server R Services](../../advanced-analytics/r-services/getting-started-with-sql-server-r-services.md)  
[Recursos e tarefas do SQL Server R Services](../../advanced-analytics/r-services/sql-server-r-services-features-and-tasks.md)  
  
