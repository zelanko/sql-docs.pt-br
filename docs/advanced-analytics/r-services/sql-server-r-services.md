---
title: "SQL Server R Services | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "12/16/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: ba1dea65-40ea-484a-b767-53680c954934
caps.latest.revision: 38
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 36
---
# SQL Server R Services
  [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] fornece uma plataforma para desenvolvimento e implantação de aplicativos inteligentes que descobrem novas informações. Você pode usar a linguagem R avançada e poderosa e os diversos pacotes da comunidade para criar modelos e gerar previsões usando seus dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Como o [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] integra a linguagem R com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], você pode manter a análise próxima aos dados e eliminar os custos e os riscos de segurança associados à movimentação de dados.  
  
 O [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] dá suporte à linguagem R de software livre com um conjunto abrangente de ferramentas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e tecnologias que oferecem melhor desempenho, segurança, confiabilidade e capacidade de gerenciamento. Você pode implantar soluções R usando ferramentas familiares e convenientes, e seus aplicativos de produção podem chamar o tempo de execução de R e recuperar previsões e visuais usando o [!INCLUDE[tsql](../../includes/tsql-md.md)]. Você também pode obter as bibliotecas [ScaleR](https://msdn.microsoft.com/microsoft-r/scaler/scaler) para melhorar a escala e o desempenho das soluções de R.  
  
Você pode instalar componentes de cliente e de servidor através da instalação do SQL Server.  
  
+   **R Services (In-Database):** instale este recurso durante a instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para permitir a execução segura de scripts de R no computador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
     Quando você seleciona esse recurso, extensões são instaladas no mecanismo de banco de dados para dar suporte à execução de scripts de R e um novo serviço é criado, o [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)], para gerenciar as comunicações entre o tempo de execução de R e a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
+   **Microsoft R Server (Autônomo):** Uma distribuição de software livre R combinada com pacotes proprietários que dão suporte ao processamento paralelo e outros aprimoramentos de desempenho. O R Services (no banco de dados) e o Microsoft R Server (Autônomo) incluem o tempo de execução e os pacotes de R básicos, além das bibliotecas **ScaleR** para conectividade e desempenho aprimorados. 
  
+    O [Cliente do Microsoft R](https://msdn.microsoft.com/microsoft-r/index#mrc) está disponível como um instalador separado e gratuito.  Você pode usar o Cliente do Microsoft R para desenvolver soluções que podem ser implantadas no R Services em execução no SQL Server ou no Microsoft R Server em execução no Windows, no Teradata ou no Hadoop. 
     

  > [!NOTE] Se precisar executar o código R no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], lembre-se de instalar o [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] conforme descrito [aqui](../../advanced-analytics/r-services/set-up-sql-server-r-services-in-database.md).
  >  
  > O Microsoft R Server \(Autônomo\) é uma opção separada, projetada para usar as bibliotecas ScaleR em um computador Windows que não esteja executando o SQL Server. 
>   
>  No entanto, se você tiver a Enterprise Edition, recomendamos que você instale o Microsoft R Server \(Autônomo\) em um laptop ou outro computador usado para o desenvolvimento do R, a fim de criar soluções do R que possam ser facilmente implantadas em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que executa o R Services \(no Banco de Dados\).
  
## <a name="additional-resources"></a>Recursos adicionais  
  
 [Introdução ao SQL Server R Services](../../advanced-analytics/r-services/getting-started-with-sql-server-r-services.md)   
 Descreve cenários comuns para usos de R com o SQL Server.  
  
[Configurar o SQL Server R Services no Banco de Dados](../../advanced-analytics/r-services/set-up-sql-server-r-services-in-database.md)  
Instalar o R e os componentes associados de banco de dados como parte da instalação do SQL Server.  
  
[Tutoriais do SQL Server R Services](../../advanced-analytics/r-services/sql-server-r-services-tutorials.md)  
Saiba como criar fontes de dados do SQL Server no seu código R e como usar contextos de computação remota. Outros tutoriais destinados a desenvolvedores SQL demonstram como treinar e implantar um modelo de R no SQL Server.  
  
## <a name="see-also"></a>Consulte também  
  
 [Introdução ao Microsoft R Server &#40;autônomo&#41;](../../advanced-analytics/r-services/getting-started-with-microsoft-r-server-standalone.md)  
 
 [Configurar um R Server Autônomo](../../advanced-analytics/r-services/create-a-standalone-r-server.md) 
  