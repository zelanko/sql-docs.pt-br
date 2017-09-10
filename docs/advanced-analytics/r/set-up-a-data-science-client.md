---
title: "Configurar um cliente de ciência de dados | Microsoft Docs"
ms.custom: 
ms.date: 02/10/2017
ms.prod: r-server
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d15ee956-918f-40e0-b986-2bf929ef303a
caps.latest.revision: 14
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 0661b2fcf9b23d3c81cb0d80f0424d87dbde7ef8
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="set-up--a-data-science-client"></a>Set Up  a Data Science Client
  Depois de configurar uma instância do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] instalando o **R Services (no Banco de Dados)**, recomendamos configurar um ambiente de desenvolvimento do R com capacidade de se conectar ao servidor para implantação e execução remotas. 
  
  Esse ambiente deve incluir os pacotes ScaleR e pode opcionalmente incluir um ambiente de desenvolvimento do cliente.
  
 ## <a name="where-to-get-scaler"></a>Onde obter o ScaleR 
  
  O ambiente de cliente deve incluir o Microsoft R Open, bem como os pacotes RevoScaleR adicionais que dão suporte à execução distribuída do R no SQL Server.  Há várias maneiras pelas quais é possível instalar esses pacotes:
  
+ Instale o [Cliente do Microsoft R](http://aka.ms/rclient/download). Instruções de instalação adicionais são fornecidas aqui: [Introdução ao Microsoft R Client](https://msdn.microsoft.com/microsoft-r/r-client-get-started)
+ Instale o Microsoft R Server. Você pode obter o Microsoft R Server por meio da instalação do SQL Server ou usando o novo Windows Installer autônomo. Para obter mais informações, consulte [Criar um R Server autônomo](../../advanced-analytics/r-services/create-a-standalone-r-server.md) e [Introdução ao R Server](https://msdn.microsoft.com/microsoft-r/rserver).

Se você tiver um contrato de licenciamento do R Server, recomendamos o uso do Microsoft R Server (Autônomo), para evitar limitações em threads de processamento de R e nos dados na memória.


## <a name="how-to-set-up-the-r-development-environment"></a>Como configurar o ambiente de desenvolvimento de R

Você pode usar qualquer ambiente de desenvolvimento de R de sua escolha que seja compatível com o Windows. 

+ As Ferramentas do R para Visual Studio dão suporte à integração com o Microsoft R Open
+ O RStudio é um ambiente gratuito popular  

Após a instalação, você precisará reconfigurar seu ambiente para usar as bibliotecas Microsoft R Open por padrão, caso contrário, você não terá acesso às bibliotecas ScaleR. Para obter mais informações, consulte [Introdução ao Microsoft R Client](http://msdn.microsoft.com/microsoft-r/r-client-get-started).
 
## <a name="more-resources"></a>Mais recursos
  
 Para obter um passo a passo detalhado sobre como se conectar a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para a execução remota de código R, consulte este tutorial: [Aprofundamento da ciência de dados: Usando os pacotes RevoScaleR](../../advanced-analytics/r-services/data-science-deep-dive-using-the-revoscaler-packages.md).  
 

Para começar a usar o Microsoft R Client e os pacotes de ScaleR com o SQL Server, consulte [Introdução ao ScaleR](https://msdn.microsoft.com/microsoft-r/scaler-getting-started#).  
  
## <a name="see-also"></a>Consulte também  
 [Configurar o SQL Server R Services &#40;no Banco de Dados&#41;](../../advanced-analytics/r-services/set-up-sql-server-r-services-in-database.md)  
  
  

