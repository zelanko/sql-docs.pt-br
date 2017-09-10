---
title: "Introdução ao Microsoft R Server (autônomo) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: r-server
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 52347d0d-ce60-4bb8-98d2-6163e87716b0
caps.latest.revision: 21
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: fc7874c6900474c7c2f3d927183616b2f5e69699
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="getting-started-with-microsoft-r-server-standalone"></a>Introdução ao servidor Microsoft R (autônomo)
  O Microsoft R Server (autônomo) ajuda você a trazer a linguagem de software livre de R para a empresa, a fim de habilitar soluções analíticas de alto desempenho e integração com outros aplicativos de negócios.  

  
## <a name="install-microsoft-r-server"></a>Instalar o Microsoft R Server 

A forma como você instala o Microsoft R Server depende de se você precisa usar dados do SQL Server em seus aplicativos. Se esse for o caso, você deverá instalar usando a instalação do SQL Server. Se você não usará dados do SQL Server ou não precisa executar código de R no banco de dados, você pode usar tanto a instalação do SQL Server quanto o novo instalador autônomo.
 
 
+ Instale o Microsoft R Server (autônomo) através da instalação do SQL Server. Uma instância separada dos binários do R é criada para o R Server e a instância é licenciada por meio da política de suporte do SQL Server Enterprise Edition. Para obter mais informações, consulte [Criar um R Server autônomo](../../advanced-analytics/r-services/create-a-standalone-r-server.md).  

+ Use o novo Windows Installer autônomo para criar uma nova instância do Microsoft R Server que usa a política de suporte moderna de ciclo de vida de software da Microsoft. Para obter mais informações, consulte [Executar Microsoft R Server para Windows](https://msdn.microsoft.com/microsoft-r/rserver-install-windows).

+ Se você tem uma instância existente do R Server (autônomo) ou do R Services que deseja atualizar, é necessário baixar e executar também o instalador baseado no Windows para a atualização. Para obter mais informações, consulte [Executar Microsoft R Server para Windows](https://msdn.microsoft.com/microsoft-r/rserver-install-windows).
  
## <a name="install-additional-r-tools"></a>Instalar ferramentas adicionais de R  

 Recomendamos o [Microsoft R Client](http://aka.ms/rclient/download) gratuito (download).  

 Você também pode usar seu ambiente de desenvolvimento preferido de R para desenvolver soluções para o SQL Server R Services ou Microsoft R Server. Para obter detalhes, consulte [Instalar ou configurar as Ferramentas de R](../../advanced-analytics/r-services/setup-or-configure-r-tools.md). 
 

### <a name="location-of-r-server-binaries"></a>Local dos binários do R Server

Dependendo do método usado para instalar o Microsoft R Server, o local padrão será diferente. Antes de começar a usar seu ambiente de desenvolvimento favorito, verifique o local em que você instalou as bibliotecas de R:

+ Microsoft R Server instalado usando o novo Windows Installer

  `C:\Program Files\Microsoft\R Server\R_SERVER`

+ R Server (autônomo) instalado por meio da instalação do SQL Server

  `C:\Program Files\Microsoft SQL Server\130\R_SERVER`

+ R Services (no banco de dados)

  `C:\Program Files\Microsoft SQL Server\<instance_name>\R_SERVICES`
      
## <a name="start-using-r-on-microsoft-r-server"></a>Começar a usar o R no Microsoft R Server  

 Depois que você configurou os componentes de servidor e configurou seu IDE do R para usar os binários do R Server, você pode começar a desenvolver sua solução usando as novas APIs, como o pacote RevoScaleR, o MicrosoftML e o olapR.
    
Para começar com o R Server, consulte este guia na biblioteca do MSDN: [R Server – Introdução](https://msdn.microsoft.com/microsoft-r/microsoft-r-get-started-node)   
  
-   [ScaleR](https://msdn.microsoft.com/microsoft-r/scaler-getting-started): explore esse conjunto de funções analíticas distribuíveis que proporciona alto desempenho e escala para as soluções de R. Inclui versões paralelizáveis de muitos dos pacotes mais populares de modelagem do R, como clustering k-means, árvores de decisão e florestas de decisão, bem como as ferramentas para a manipulação de dados. Para obter mais informações, consulte [Explorar R e ScaleR em 25 funções](https://msdn.microsoft.com/microsoft-r/microsoft-r-getting-started-tutorial)  
    
- [MicrosoftML](https://msdn.microsoft.com/library/mt790482.aspx): o pacote MicrosoftML é um conjunto de novos algoritmos de aprendizado de máquina e de transformações, que são rápidos e escalonáveis e que foram desenvolvidos na Microsoft. Para obter mais informações, consulte [Funções do MicrosoftML](https://msdn.microsoft.com/microsoft-r/microsoftml/microsoftml).
  


  
## <a name="see-also"></a>Consulte também  
 [Introdução ao SQL Server R Services](../../advanced-analytics/r-services/getting-started-with-sql-server-r-services.md)  
  
  

