---
title: "Introdu&#231;&#227;o ao SQL Server R Services | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "12/07/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "get-started-article"
ms.assetid: 5b28a663-effe-41f6-9bda-eda95f0c6943
caps.latest.revision: 34
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 32
---
# Introdu&#231;&#227;o ao SQL Server R Services
 Um fluxo de trabalho típico da criação de uma solução de análise avançada é iniciado pela exploração de dados e pela modelagem preditiva, enquanto o cientista de dados desenvolve os modelos e scripts R que comprovam a eficácia da tarefa em questão. Depois que os modelos e os scripts estão prontos, eles podem ser implantados em produção e integrados a aplicativos novos ou existentes.   
  
O SQL Server R Services foi desenvolvido para ajudar você a concluir essas tarefas de ciência de dados. Você pode continuar a trabalhar com as suas ferramentas SQL ou R favoritas, mas é possível escalar a análise para bilhões de registros sem nenhum hardware adicional, aumentar o desempenho e evitar movimentações de dados desnecessárias. Agora você pode colocar seu código R em produção sem precisar reescrevê-lo em outra linguagem. Ele também facilita o uso de R para cálculos estatísticos que podem ser difíceis de implementar usando SQL. Ao mesmo tempo, você pode aproveitar a eficiência do SQL Server para obter o máximo em desempenho usando recursos como os índices columnstore e o mecanismo de banco de dados na memória.  
  
As seções a seguir fornecem uma visão geral de alto nível de alguns fluxos de trabalho de análise típico e como habilitá-los com o SQL Server R Services.  

> [!TIP] Veja este tutorial para uma introdução rápida. Você saberá como uma empresa de aluguel de equipamentos de esqui pode usar o aprendizado de máquina para prever futuras locações e agendar a equipe para atender à demanda.
> 
> [Compilar um aplicativo inteligente com o SQL Server e R](https://www.microsoft.com/sql-server/developer-get-started/r)


  
-   **Desenvolver**  
  
     Os cientistas de dados normalmente usam R para explorar dados e criar modelos de previsão de sua estação de trabalho usando uma IDE de R de sua escolha. O cientista de dados itera o teste e ajusta até que um bom modelo de previsão seja obtido. 
     
     Os componentes do cliente do [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] fornece aos cientistas de dados todas as ferramentas necessárias para testes e para desenvolvimento. Essas ferramentas incluem o tempo de execução de R, a biblioteca de kernel de matemática da Intel para melhorar o desempenho de operações padrão de R e um conjunto avançados de pacotes de R que dão suporte à execução do código R no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
     Os cientistas de dados podem se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e transferir os dados para o cliente para análise local, como de costume. No entanto, uma solução melhor é usar as APIs **ScaleR** para enviar por push os cálculos para o computador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], evitando uma movimentação de dados cara e insegura.  
  
     Para desenvolver soluções de R, os cientistas de dados podem usar qualquer IDE baseado no Windows com suporte a R, incluindo [Ferramentas de R para o Visual Studio ou RStudio](https://www.visualstudio.com/features/rtvs-vs.aspx).  
 
    ![rsql_keyscenario2](../../advanced-analytics/r-services/media/rsql-keyscenario2.PNG) 
 
     Para saber mais, confira [Data Exploration and Predictive Modeling with R](../../advanced-analytics/r-services/data-exploration-and-predictive-modeling-with-r.md).  

  
-   **Otimizar**  
  
     Ao analisar grandes conjuntos de dados com R, os cientistas de dados geralmente se deparam com problemas de desempenho e escala, porque a implementação de tempo de execução comum é de thread único e pode acomodar apenas os conjuntos de dados que se ajustam à memória disponível no computador local. Para obter um melhor desempenho e trabalhar com mais dados, o cientista de dados pode usar as APIs **ScaleR** fornecidas como parte do [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]. O pacote **RevoScaleR** contém implementações de algumas das funções R mais populares, reprojetadas para oferecer paralelismo e escala. O pacote também inclui funções que aumentam ainda mais o desempenho e a escala enviando por push cálculos para o computador [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], que geralmente tem muito mais memória e eficiência computacional.  
  
     Para saber mais, confira [Data Exploration and Predictive Modeling with R](../../advanced-analytics/r-services/data-exploration-and-predictive-modeling-with-r.md).  
  
-   **Implantar**  
  
     Depois de o script R ou o modelo estar pronto para uso em produção, o desenvolvedor de banco de dados pode inserir o código ou o modelo em procedimentos armazenados e invocar o código salvo de um aplicativo. Armazenar e executar código R do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] traz muitos benefícios: você pode usar a interface conveniente do [!INCLUDE[tsql](../../includes/tsql-md.md)] e todos os cálculos ocorrem no banco de dados, evitando movimentação desnecessária de dados. Você pode usar o [!INCLUDE[tsql](../../includes/tsql-md.md)] para gerar pontuações de um modelo de previsão em produção ou retornar gráficos gerados por R e apresentá-los em um aplicativo, como [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
     Para otimizar ainda mais o código R inserido em procedimentos armazenados do sistema, é recomendado usar as APIs do pacote [ScaleR](https://msdn.microsoft.com/microsoft-r/rserver/rserver-scaler-getting-started), que podem operar em grandes conjuntos de dados. Esses pacotes dão suporte à execução no banco de dados, para computação de vários segmentos, com vários núcleos e vários processos.  
  
     Quando você precisa implantar o código R em produção, o [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] fornece o melhor dos mundos de R e SQL. Você pode usar R para cálculos estatísticos difíceis de implementar usando SQL, mas aproveitar a eficiência do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para obter o máximo em desempenho usando recursos como os índices columnstore e o mecanismo de banco de dados na memória.  
  
    ![rsql_keyscenario1](../../advanced-analytics/r-services/media/rsql-keyscenario1.PNG)  
  
     Para obter mais informações, consulte [Operacionalização do código R](../../advanced-analytics/r-services/operationalizing-your-r-code.md).  
 
 > [!TIP] Saiba mais sobre como integrar o SQL Server com a ciência de dados neste livro, disponível como um download gratuito da Microsoft Virtual Academy: [Data Science with Microsoft SQL Server 2016](https://mva.microsoft.com/ebooks/) (Ciência de dados com o Microsoft SQL Server 2016)

-   **Gerenciar e monitorar**  
  
     O [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] usa uma nova arquitetura de extensibilidade que mantém o mecanismo de banco de dados seguro e isola as sessões de R. Você também tem controle sobre os usuários que podem executar scripts R, e você pode especificar quais bancos de dados podem ser acessados pelo código R. Você pode controlar a quantidade de recursos alocados ao tempo de execução de R, para evitar que cálculos muito intensos prejudiquem o desempenho geral do servidor.  
  
     Quando os trabalhos de R são executados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], você também pode controlar e auditar os dados usados por analistas ou agendar trabalhos e criar fluxos de trabalho que contêm scripts R, exatamente como faria com outros procedimentos armazenados.  
  
     Para obter mais informações, consulte [Managing and Monitoring R Solutions](../../advanced-analytics/r-services/managing-and-monitoring-r-solutions.md).  
  
  
-   **Integrar**  
  
     Não é necessário gastar seu orçamento de TI fazendo suas ferramentas empresariais trabalharem com alguns ambientes de tempo de execução R externo. Você pode trabalhar no ambiente familiar do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], e desenvolver fluxos de trabalho integrados e soluções de relatórios usando [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] e [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
     Para obter mais informações, consulte [Criando fluxos de trabalho que usam R no SQL Server](../../advanced-analytics/r-services/creating-workflows-that-use-r-in-sql-server.md).  
  
  
## <a name="how-do-i-get-it"></a>Como posso obtê-lo?  
   
  
+   **Instalar o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] ou posterior e habilitar o R Services (No banco de dados)**  
  
    [Configurar o SQL Server R Services &#40;No banco de dados&#41;](../../advanced-analytics/r-services/set-up-sql-server-r-services-in-database.md).  
  
  
-   **Configurar uma estação de trabalho cliente**  
  
     [Configurar um cliente de ciência de dados](../../advanced-analytics/r-services/set-up-a-data-science-client.md)  
   
> [!TIP]   
>   
> Precisa criar um servidor para trabalhos em R, mas não precisa do SQL Server? Experimente o [Microsoft R Server](https://msdn.microsoft.com/library/mt674874.aspx).  
  
## <a name="how-to-run-r-code-using-sql-server-r-services"></a>Como executar código R usando o SQL Server R Services  
 Após a conclusão da instalação, você poderá executar o código R no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] inserindo R nos procedimentos armazenados do [!INCLUDE[tsql](../../includes/tsql-md.md)] ou escrevendo scripts R ad hoc que funcionam com os dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Saiba como chamar o R de uma instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] e retornar resultados no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]  
  
     [Usando código do R no Transact-SQL](../../advanced-analytics/r-services/using-r-code-in-transact-sql-sql-server-r-services.md)  
  
-   Entenda o fluxo completo para criar uma solução de análise avançada e para implantá-la usando o SQL Server R Services  
  
     [Passo a passo de ponta a ponta sobre a ciência de dados](../../advanced-analytics/r-services/data-science-end-to-end-walkthrough.md)  
  
-   Saiba como usar o pacote do RevoScaleR para análise de alto desempenho e escalonável e como enviar por push os cálculos de R para o computador do SQL Server  
  
     [Aprofundamento da ciência de dados: usando os pacotes RevoScaleR](../../advanced-analytics/r-services/data-science-deep-dive-using-the-revoscaler-packages.md)  
  
-   Insira o script R em funcionamento nos procedimentos armazenados do [!INCLUDE[tsql](../../includes/tsql-md.md)] para que você possa chamar modelos para previsão, treinar modelos novamente ou obter previsões de aplicativos  
  
     [Análise avançada no banco de dados para desenvolvedores do SQL](../../advanced-analytics/r-services/in-database-advanced-analytics-for-sql-developers-tutorial.md)  
  
-   Use o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] e as ferramentas relacionadas de business intelligence na pilha do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para automatizar processos de aprendizado de máquina. A preparação de dados e os relatórios podem ser automatizados usando o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]; exiba plotagens do R juntamente com outros relatórios usando o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ou Power View.  
  
+ Mais exemplos, incluindo modelos de solução e código R de exemplo  
   [SQL Server R Services Tutorials](../../advanced-analytics/r-services/sql-server-r-services-tutorials.md).  
  
## <a name="see-also"></a>Consulte também  
 [SQL Server R Services](../../advanced-analytics/r-services/sql-server-r-services.md)   
 [Introdução ao Microsoft R Server &#40;autônomo&#41;](../../advanced-analytics/r-services/getting-started-with-microsoft-r-server-standalone.md)  
  
  