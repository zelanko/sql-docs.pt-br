---
title: "Configurar ou configurar as ferramentas de R | Microsoft Docs"
ms.custom: ""
ms.date: "01/20/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 7c04ae30-d391-4369-9742-d2b275e14c0d
caps.latest.revision: 9
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 8
---
# Configurar ou configurar as ferramentas de R
  Microsoft R Server fornece todas as bibliotecas R base, pacotes R de escala e ferramentas padrão do R que você precisa para desenvolver e testar o código R. No entanto, se você quiser usar um ambiente de desenvolvimento dedicado R, existem vários disponíveis, incluindo várias ferramentas gratuitas.  
  
## <a name="basic-r-tools"></a>Ferramentas básicas de R  
 Ferramentas adicionais não são necessárias em uma instalação do servidor do Microsoft R, porque R padrão das ferramentas que são incluídos em um *base instalação* de R são instalados por padrão.

-   **RTerm**: uma ferramenta de linha de comando para execução de scripts de R 
  
-   **RGui.exe**: um simple editor interativo de R. Os argumentos de linha de comando são os mesmos para RGui.exe e RTerm. 
  
-   **RScript**: uma ferramenta de linha de comando para executar R scripts no modo de lote.  

Por padrão, essas ferramentas são instaladas nas seguintes pastas:
- SQL Server 2016: `C:\Program Files\Microsoft SQL Server\130\R_SERVER\bin\x64`  
- SQL Server vNext: `C:\Program Files\Microsoft SQL Server\140\R_SERVER\bin\x64`  

> [!TIP]  
>  Precisa de mais ajuda? Documentação para as ferramentas de R pode ser encontrada na pasta de instalação: `C:\Program Files\Microsoft SQL Server\R_SERVER\doc` e em `C:\Program Files\Microsoft SQL Server\R_SERVER\doc\manual`.  
>   
>  Ou, basta abrir **RGui**, clique em **Ajuda**, e selecione uma das opções.  

## <a name="microsoft-r-client"></a>Cliente do Microsoft R

O cliente do Microsoft R é um download gratuito que permite que você desenvolva soluções R que podem ser facilmente executadas no Microsoft R Server ou no SQL Server R Services.

Normalmente, você instala um ambiente de desenvolvimento R diferente, como as ferramentas de R para o Visual Studio ou RStudio e, em seguida, especifica que o Microsoft R Client seja usado como o executável de R. Isso lhe dá acesso completo para o pacote de RevoScaleR e outros recursos do Microsoft R Server.

Você também pode usar ferramentas conhecidas, como RGui e RTerm para executar scripts ou escrever e executar código R ad hoc.

[Instalar o cliente Microsoft R](https://msdn.microsoft.com/microsoft-r/r-client-install)
  
##  <a name="a-namebkmkrtoolsa-r-tools-for-visual-studio"></a> Ferramentas de R para Visual Studio  

 Para conveniência ao trabalhar com [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bancos de dados, considere o uso de [!INCLUDE[rsql_rtvs](../../includes/rsql-rtvs-md.md)] como seu ambiente de desenvolvimento. [!INCLUDE[rsql_rtvs](../../includes/rsql-rtvs-md.md)] é um suplemento gratuito do Visual Studio que funciona em todas as edições do Visual Studio. Visual Studio também fornece suporte para a integração de Python e F #.  

Para obter mais informações, consulte [VisualStudio.com](https://www.visualstudio.com/vs/rtvs/).

 Esta seção descreve como instalar o [!INCLUDE[rsql_rtvs](../../includes/rsql-rtvs-md.md)] usando o livre Community Edition do Visual Studio.  
  
#### <a name="install-visual-studio"></a>Instale o Visual Studio  
  
1.  O Community edition gratuita do Visual Studio está disponível para download nesta página: [Visual Studio Community](http://visualstudio.com/products/visual-studio-community-vs.aspx)  
  
2.  Quando o download for concluído, clique em **executar** e selecione os componentes a serem instalados.  
  
     Se você fizer uma instalação personalizada, observe que os componentes do Microsoft Web Developer são necessários.  
  
3.  Escolha a **geral** configuração por enquanto. Quando você instala o [!INCLUDE[rsql_rtvs](../../includes/rsql-rtvs-md.md)], você terá que toption para mudar para um layout personalizado para o desenvolvimento de R.  

#### <a name="add-the-r-tools"></a>Adicionar as ferramentas de R

Após a instalação do Visual Studio, as extensões estão disponíveis para R, Python e muitos outros idiomas por meio de **opções** menu.

4. Clique em ferramentas na barra de menus e selecione **extensões e atualizações**.

5. No final da instalação, ferramentas de R detectará as versões do tempo de execução do R que estão disponíveis no computador e perguntam se você deseja alterar seu ambiente de desenvolvimento para usar o tempo de execução de R para Microsoft R Server ou o tempo de execução de R para o cliente do Microsoft R.

Se a instalação detectar o tempo de execução do servidor R que você deseja usar, você pode alterá-lo manualmente a qualquer momento usando o **opções** menu. Para obter mais informações, consulte [Configurar o IDE](https://msdn.microsoft.com/microsoft-r/r-client-get-started#step-2-configure-your-ide).

## <a name="rstudio"></a>RStudio

Se você preferir usar o RStudio, siga estas etapas adicionais para usar as bibliotecas de RevoScaleR:
- Instale o Microsoft R Server ou Microsoft R Client para obter os pacotes necessários e as bibliotecas.
- Atualize o caminho R para usar o tempo de execução de R apropriado.

Para obter mais informações, consulte [Configurar o IDE](https://msdn.microsoft.com/microsoft-r/r-client-get-started#step-2-configure-your-ide).


## <a name="see-also"></a>Consulte também  
 [Criar um servidor de R autônomo](../../advanced-analytics/r-services/create-a-standalone-r-server.md)   
 [Introdução ao servidor Microsoft R & #40. Autônomos e 41;](../../advanced-analytics/r-services/getting-started-with-microsoft-r-server-standalone.md)  
  
  