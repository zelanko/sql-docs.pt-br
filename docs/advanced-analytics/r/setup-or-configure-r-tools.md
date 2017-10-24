---
title: Instalar ou configurar as Ferramentas de R | Microsoft Docs
ms.custom: 
ms.date: 01/20/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 7c04ae30-d391-4369-9742-d2b275e14c0d
caps.latest.revision: 9
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: a3baf97a960d7e8f950bb6e9cd251550f4c4b942
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="setup-or-configure-r-tools"></a>Instalar ou configurar as Ferramentas de R
  O Microsoft R Server fornece todas as bibliotecas de R da base, um conjunto de pacotes de ScaleR e ferramentas padrão do R de que você precisa para desenvolver e testar o código R. No entanto, se você quiser usar um ambiente de desenvolvimento dedicado do R, existem vários disponíveis, incluindo muitas ferramentas gratuitas.  
  
## <a name="basic-r-tools"></a>Ferramentas básicas de R  
 Ferramentas adicionais não são necessárias em uma instalação do Microsoft R Server, porque todas as ferramentas padrão do R que são incluídas em uma *instalação base* do R são instaladas por padrão.

-   **RTerm**: uma ferramenta de linha de comando para execução de scripts R 
  
-   **RGui.exe**: um editor interativo simples de R. Os argumentos de linha de comando são os mesmos para RGui.exe e RTerm. 
  
-   **RScript**: uma ferramenta de linha de comando para executar scripts R no modo de lote.  

Para localizar essas ferramentas, encontre o local da biblioteca de R. Isso varia, dependendo de você ter instalado somente o SQL Server R Services ou ter instalado R Server (Autônomo) também. Para obter mais informações, consulte [O que é instalado e em que local encontrar os pacotes do R](https://msdn.microsoft.com/library/mt695941(sql.130).aspx#Anchor_1)

Em seguida, procure na pasta `..\R_SERVER\bin\x64`.  

> [!TIP]  
>  Precisa de ajuda com as ferramentas de R? A documentação está incluída, na pasta de instalação `C:\Program Files\Microsoft SQL Server\R_SERVER\doc` e em `C:\Program Files\Microsoft SQL Server\R_SERVER\doc\manual`.  
>   
>  Ou então, basta abrir **RGui**, clicar em **Ajuda** e selecionar uma das opções.  

## <a name="microsoft-r-client"></a>Cliente do Microsoft R

O Microsoft R Client é um download gratuito que permite que você desenvolva soluções de R que podem ser facilmente executadas no Microsoft R Server ou no SQL Server R Services. Essa opção é fornecida para ajudar a cientistas de dados que podem não ter acesso ao R Server (disponível no Enterprise Edition) a desenvolver soluções que usam ScaleR. 

Se você usar um ambiente de desenvolvimento R diferente, por exemplo, as Ferramentas do R para Visual Studio ou RStudio, para usar o ScaleR você deverá especificar que o Microsoft R Client seja usado como o executável do R. Isso lhe dá acesso completo ao pacote de RevoScaleR e outros recursos do Microsoft R Server, embora o desempenho seja limitado.

Você também pode usar as ferramentas fornecidas no R Client, por exemplo, RGui e RTerm, para executar scripts ou escrever e executar código R ad hoc.

[Instalar o Microsoft R Client](https://msdn.microsoft.com/microsoft-r/r-client-install)
  
##  <a name="bkmk_RTools"></a> Ferramentas do R para Visual Studio  

 Para conveniência ao trabalhar com bancos de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], considere o uso de [!INCLUDE[rsql_rtvs](../../includes/rsql-rtvs-md.md)] como seu ambiente de desenvolvimento. O[!INCLUDE[rsql_rtvs](../../includes/rsql-rtvs-md.md)] é um suplemento gratuito do Visual Studio que funciona em todas as edições do Visual Studio. O Visual Studio também dá suporte à integração de Python e F #.  

 Para obter instruções de instalação, consulte [como instalar as ferramentas de R para Visual Studio](https://docs.microsoft.com/visualstudio/rtvs/installation).

> [!TIP]
> Antes de instalar quaisquer novos pacotes, verifique qual tempo de execução do R está sendo usado por padrão. Se você não fizer isso, terá um risco muito grande de instalar novos pacotes do R para um local da biblioteca padrão e, em seguida, não conseguir encontrá-los do R Server!


## <a name="rstudio"></a>RStudio

Se você preferir usar o RStudio, algumas etapas adicionais serão necessárias para usar as bibliotecas de RevoScaleR:
- Instale o Microsoft R Server ou Microsoft R Client para obter os pacotes e bibliotecas necessários.
- Atualize o caminho do R para usar o tempo de execução do R Server.

Para obter mais informações, consulte [Configurar o IDE](https://msdn.microsoft.com/microsoft-r/r-client-get-started#step-2-configure-your-ide).


## <a name="see-also"></a>Consulte também  
 [Criar um R Server autônomo](../../advanced-analytics/r-services/create-a-standalone-r-server.md)   
 [Introdução ao Microsoft R Server &#40;autônomo&#41;](../../advanced-analytics/r-services/getting-started-with-microsoft-r-server-standalone.md)  
  
  

