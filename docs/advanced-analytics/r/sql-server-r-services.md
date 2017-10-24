---
title: "Serviços de aprendizado de máquina do SQL Server | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 08/20/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: ba1dea65-40ea-484a-b767-53680c954934
caps.latest.revision: 38
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: e8c384b7fba553175767aaf7c439207771b31e6b
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="sql-server-machine-learning-services"></a>Serviços de SQL Server Machine Learning

  Serviços do aprendizado de máquina 2017 SQL Server (anteriormente SQL Server 2016 R Services) fornece uma plataforma para desenvolvimento e implantação de aplicativos inteligentes que descobrem novas informações. Você pode usar a linguagem R avançada e poderosa e os diversos pacotes da comunidade para criar modelos e gerar previsões usando seus dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .
  
  Como o aprendizado de máquina está integrado com [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], você pode manter a análise próxima aos dados e eliminar os custos e os riscos de segurança associados à movimentação de dados.
  
SQL Server oferece suporte a linguagem R de software livre com um conjunto abrangente de ferramentas e tecnologias que oferecem melhor desempenho, segurança, confiabilidade e capacidade de gerenciamento. Você pode implantar soluções R usando ferramentas SQL familiares e convenientes, e seus aplicativos de produção podem chamar o tempo de execução de R e recuperar previsões e visuais usando [!INCLUDE[tsql](../../includes/tsql-md.md)]. Você também pode obter o [Microsoft R](https://docs.microsoft.com/r-server/r-reference/revoscaler/revoscaler) bibliotecas para melhorar a escala e o desempenho de suas soluções de R, incluindo RevoScaleR, revoscalepy e MicrososftML.
  
Você pode instalar componentes de cliente e de servidor através da instalação do SQL Server.
  
## <a name="machine-learning-in-sql-server-2017"></a>No SQL Server 2017 de aprendizado de máquina

+ Instalar **serviços de aprendizado de máquina (no banco de dados)** durante [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instalação para habilitar a execução segura de scripts de R ou Python no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] computador.
  
    Quando você seleciona esse recurso, as extensões são instaladas no mecanismo de banco de dados para permitir a execução de código escrito em R ou Python. Um novo serviço é criado, o [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)], para gerenciar as comunicações entre os tempos de execução externas e a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instância.
  
+ Instalar **aprendizado de máquina do Microsoft Server (autônomo)** em um computador separado, se você não precisa usar o SQL Server como o contexto de computação. Servidor de aprendizado de máquina inclui a mesmo componentes, além de pacote mrsdeploy escalonável e distribuído a execução de trabalhos de aprendizado de máquina como um serviço web de aprendizado de máquina.
  
+    Instalar [Microsoft R cliente](https://docs.microsoft.com/r-server/r-client/what-is-microsoft-r-client) em computadores remotos para desenvolver soluções que podem ser implantados para o SQL Server ou ao servidor de aprendizado de máquina no Windows, Linux ou Hadoop.

## <a name="machine-learning-in-sql-server-2016"></a>No SQL Server 2016 de aprendizado de máquina

+ Instalar **R Services (no banco de dados)** durante a instalação do SQL Server 2016 para permitir a execução segura de scripts de R no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] computador.
  
    Quando você seleciona esse recurso, você recebe a capacidade de executar script R usando o SQL Server como o contexto de computação, ou para executar o script de R em um procedimento armazenado.
  
+   Instalar **Microsoft R Server (autônomo)** da instalação do SQL Server 2016 para configurar os componentes de R em um computador separado que você usa para soluções developin R.


## <a name="which-type-of-machine-learning-service-do-i-need"></a>O tipo de serviço de aprendizado de máquina é necessário?

+ Se você precisa executar seu código R [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], usando procedimentos armazenados ou usando a instância do SQL Server como o contexto de computação, você deve instalar [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] conforme descrito [aqui](../../advanced-analytics/r-services/set-up-sql-server-r-services-in-database.md).

+ Aprendizado de máquina do Microsoft Server (autônomo) é uma opção separada projetada para usar o [Microsoft R](https://docs.microsoft.com/r-server/r-reference/introducing-r-server-r-package-reference) e [relacionados bibliotecas Python](../python/what-is-revoscalepy.md) em um computador com Windows que não esteja executando o SQL Server. No entanto, ele, requerem uma licença de Enterprise Edition do SQL Server.
    
    É recomendável que você instale o Microsoft máquina de aprendizado Server (autônomo) em um laptop ou outro computador remoto usado para desenvolvimento e use esse computador para criar e testar soluções de aprendizado de máquina que podem ser implantadas facilmente a uma instância de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que está executando serviços de aprendizado de máquina \(no banco de dados\) ou outro contexto de computação tem suporte.
  
    Você também pode usar o **mrsdeploy** pacote instalado com o servidor de aprendizado de máquina para publicar e distribuir os trabalhos de R e Python como um serviço web.

## <a name="additional-resources"></a>Recursos adicionais

+ [Introdução ao SQL Server R Services](../../advanced-analytics/r/getting-started-with-sql-server-r-services.md)
 
    Descreve os cenários comuns de usos do R com o SQL Server

+ [Configurar o SQL Server R Services no Banco de Dados](../../advanced-analytics/r/set-up-sql-server-r-services-in-database.md)

    Instalar componentes de banco de dados associado e R como parte da instalação do SQL Server
  
+ [Tutoriais do SQL Server R](../../advanced-analytics/tutorials/sql-server-r-tutorials.md)

    Saiba como criar fontes de dados do SQL Server no seu código R e como usar contextos de computação remota. Outros tutoriais destinados a desenvolvedores SQL demonstram como treinar e implantar um modelo de R no SQL Server.

