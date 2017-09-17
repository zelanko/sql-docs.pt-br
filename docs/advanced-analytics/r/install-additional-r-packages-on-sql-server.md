---
title: Instalar pacotes de R adicionais no SQL Server | Microsoft Docs
ms.custom:
- SQL2016_New_Updated
ms.date: 11/08/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 21456462-e58a-44c3-9d3a-68b4263575d7
caps.latest.revision: 16
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: adc0e5fc229547632759c5702e98d87f4b71cbb3
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="install-additional-r-packages-on-sql-server"></a>Instalar pacotes R adicionais no SQL Server
Este tópico descreve como instalar novos pacotes de R em uma instância do [!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)] em um computador que tenha acesso à Internet.

## <a name="1-locate-the-windows-binaries-in-zip-file-format"></a>1. Localizar os binários do Windows no formato de arquivo ZIP

Os pacotes de R têm suporte em várias plataformas. Certifique-se de que o pacote que você deseja instalar tenha um formato binário para a plataforma Windows. Caso contrário, o pacote baixado não funcionará.

Por exemplo, para obter o pacote [FISHalyseR](http://bioconductor.org/packages/release/bioc/html/FISHalyseR.html) da Bioconductor:  
  
1.  Na lista **Arquivos de Pacote** , localize a versão **Binário do Windows** .  
  
2.  Clique com o botão direito do mouse no link do arquivo .ZIP e selecione  **Salvar destino como**.  
  
3.  Navegue até a pasta local onde os pacotes compactados foram armazenados e clique em **Salvar**.  
  
 Esse processo cria uma cópia local do pacote. Em seguida, você pode instalar o pacote ou copiar o pacote compactado para um servidor que não tenha acesso à Internet.  
  
  
## <a name="2-open-the-default-r-package-library-for-sql-server-r-services"></a>2. Abra a biblioteca padrão do pacote do R para SQL Server R Services 

Navegue até a pasta no servidor em que os pacotes de R associados ao [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] foram instalados. É importante que você instale pacotes na biblioteca padrão que está associada à instância atual. 

Para obter instruções sobre como localizar essa biblioteca, consulte [Instalar e gerenciar pacotes de R](../../advanced-analytics/r-services/installing-and-managing-r-packages.md).

   Para cada instância em que você executará um pacote, é necessário instalar uma cópia separada dos pacotes. Atualmente os pacotes não podem ser compartilhados entre instâncias.
     
  
## <a name="3-open-an-administrative-command-prompt"></a>3. Abrir um prompt de comando administrativo 

Abra R como administrador.  Você pode fazer isso usando o prompt de comando do Windows ou usando um dos utilitários de R.
  
### <a name="using-the-windows-command-prompt"></a>Usando o prompt de comando do Windows 

1. Abra um prompt de comando do Windows como administrador e navegue até o diretório em que estão localizados os arquivos RTerm.Exe ou RGui.exe.  
  
    Em uma instalação padrão, esse é o diretório **\bin** de R. Por exemplo, no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], as ferramentas de R estão localizadas aqui: 

    **Instância padrão**

     `C:\Program Files\MSSQL13.MSSQLSERVER\R_SERVICES\bin` 
 
     **Instância nomeada**
   
     `C:\Program files\MSSQL13.<instanceName>\R_SERVICES\bin\x64`  
  
2. Execute **R.Exe**.  
  
### <a name="using-the-r-command-line-utilities"></a>Como usar os utilitários de linha de comando de R. 
  
1. Use o Windows Explorer para navegar até o diretório que contém as ferramentas de R.  
  
2. Clique com o botão direito do mouse em **RGui.exe** ou **RTerm.exe** e selecione **Executar como administrador**.  
## <a name="4-install-the-package"></a>4. Instalar o pacote

O comando de R para instalar o pacote depende de se você obteve o pacote da Internet ou de um arquivo compactado local.  
  
### <a name="install-package-from-internet"></a>Instalar o pacote da Internet  
  
1.  Em geral, você usa o seguinte comando para instalar um novo pacote do CRAN ou de um dos locais de espelhamento.  
  
    ```  
    install.packages("target_package_name")  
    ```
    
    Observe que as aspas duplas são sempre obrigatórias para o nome do pacote.

2.  Para especificar a biblioteca em que o pacote deverá ser instalado, use um comando como este para definir a localização da biblioteca:
    
    ```  
    lib.SQL <- "C:\\Program Files\\Microsoft SQL Server\\MSSQL13.MSSQLSERVER\\R_SERVICES\\library"    
    ```

    Observe que para o [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], somente uma biblioteca de pacote é permitida atualmente. Não instale pacotes em uma biblioteca de usuário ou você não poderá executar o pacote no [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)].   
     
3.  Após a definição da localização da biblioteca, a instrução a seguir instala o pacote e1070 popular na biblioteca de pacote usada pelo R Services.  
  
    ```  
    install.packages("e1071", lib = lib.SQL)  
    ```  
  
4.  Você receberá uma solicitação por um local de espelhamento a partir do qual obterá o pacote. Selecione qualquer local de espelhamento conveniente ao seu local.  
  
    Para obter uma lista dos espelhos CRAN atuais, confira [este site](https://cran.r-project.org/mirrors.html).  
  
    > [!TIP]  
    >  Para evitar ter que selecionar um local de espelhamento sempre que adicionar um novo pacote, configure seu ambiente de desenvolvimento R para usar sempre o mesmo repositório.  
    >   
    >  Para fazer isso, edite o arquivo de configurações global de R, o .Rprofile, e adicione a seguinte linha:  
    >   
    >  `options(repos=structure(c(CRAN="<mirror site URL>")))`  
    >   
    >  Para obter informações detalhadas sobre as preferências e sobre outros arquivos carregados no momento da inicialização do tempo de execução de R, execute este comando em um console R:  
    >   
    >  `?Startup`  
  
5.  Se o pacote de destino depender de outros pacotes, o instalador de R baixará automaticamente as dependências e as instalará para você.  
  
### <a name="manual-package-installation-or-installing-on-computer-with-no-internet-access"></a>Instalação manual ou instalar em computador sem acesso à Internet 

1. Se o pacote que você pretende instalar tem dependências, obtenha os pacotes necessários antecipadamente e adicione-os à pasta com outro pacote de arquivos compactados.

    > [!TIP]
    > 
    > É recomendável que você configure um repositório local usando [miniCRAN](https://mran.revolutionanalytics.com/package/miniCRAN/) se você precisar dar suporte à instalação offline frequente de pacotes de R.  
  
2.  No prompt de comando de R, digite o seguinte comando para especificar o caminho e o nome do pacote para instalação:  
   
    ```  
    install.packages("C:\\Temp\\Downloaded packages\\mynewpackage.zip", repos=NULL)  
    ``` 
     
    Esse comando extrai o pacote R de seu arquivo compactado local, supondo que você tenha salvo a cópia no diretório `C:\Temp\Downloaded packages`, e instala o pacote (com suas dependências) na biblioteca R no computador local.  
  
3.  Se você modificou anteriormente o ambiente do R no computador, é necessário garantir que a variável de ambiente de R `.libPath` use apenas um caminho, que aponta para a pasta R_SERVICES da instância.  
  
> [!NOTE]
> Se você instalou o Microsoft R Server (autônomo) além do SQL Server R Services, seu computador terá uma instalação separada do R, com todas as bibliotecas e ferramentas de R. Os pacotes que estão instalados na biblioteca R_SERVER são usados apenas pelo Microsoft R Server e não pode ser acessados pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
> 
>  Certifique-se de usar a biblioteca R_SERVICES ao instalar os pacotes que você deseja usar no SQL Server.

  
## <a name="see-also"></a>Consulte também  
 [Configurar o SQL Server R Services &#40;no Banco de Dados&#41;](../../advanced-analytics/r-services/set-up-sql-server-r-services-in-database.md)  
  
  

