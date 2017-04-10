---
title: "Configurar um cliente de ci&#234;ncia de dados | Microsoft Docs"
ms.custom: ""
ms.date: "02/10/2017"
ms.prod: "r-server"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: d15ee956-918f-40e0-b986-2bf929ef303a
caps.latest.revision: 14
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 10
---
# Configurar um cliente de ci&#234;ncia de dados
  Depois de configurar uma instância do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] instalando o **R Services (no Banco de Dados)**, recomendamos configurar um ambiente de desenvolvimento do R com capacidade de se conectar ao servidor para implantação e execução remotas. 
  
  O ambiente de cliente deve incluir o Microsoft R Open, bem como os pacotes RevoScaleR adicionais que dão suporte à execução distribuída do R no SQL Server.  Há várias maneiras pelas quais é possível instalar esses pacotes:
  
+ Instale o [Cliente do Microsoft R](http://aka.ms/rclient/download).
+ Instale o Microsoft R Server. Obtenha o Microsoft R Server por meio da instalação do SQL Server ou de um instalador autônomo. Para obter mais informações, consulte [Criar um R Server autônomo](../../advanced-analytics/r-services/create-a-standalone-r-server.md) ou [Introdução ao R Server](https://msdnstage.redmond.corp.microsoft.com/en-us/microsoft-r/rserver?branch=r-server-nov16-dev).

 Para obter mais informações sobre como usar o Cliente do Microsoft R para se conectar ao SQL Server usando os pacotes ScaleR, consulte [Introdução ao ScaleR](https://msdn.microsoft.com/microsoft-r/scaler-getting-started#).  
  
 Para obter um passo a passo detalhado sobre como se conectar a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para a execução remota de código R, consulte este tutorial: [Aprofundamento da ciência de dados: Usando os pacotes RevoScaleR](../../advanced-analytics/r-services/data-science-deep-dive-using-the-revoscaler-packages.md).  
  
## <a name="see-also"></a>Consulte também  
 [Configurar o SQL Server R Services &#40;no Banco de Dados&#41;](../../advanced-analytics/r-services/set-up-sql-server-r-services-in-database.md)  
  
  