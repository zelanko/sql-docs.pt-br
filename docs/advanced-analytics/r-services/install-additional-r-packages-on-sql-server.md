---
title: "Instalar pacotes R adicionais no SQL Server | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "11/08/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 21456462-e58a-44c3-9d3a-68b4263575d7
caps.latest.revision: 16
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 16
---
# Instalar pacotes R adicionais no SQL Server
Este tópico descreve como instalar novos pacotes de R para uma instância de [!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)] em um computador que tenha acesso à Internet.

## <a name="1-locate-the-windows-binaries-in-zip-file-format"></a>1. Localizar os binários do Windows no formato de arquivo ZIP

Pacotes R têm suporte em várias plataformas. Certifique-se de que o pacote que você deseja instalar tem um formato binário para a plataforma Windows. Caso contrário, o pacote baixado não funcionará.

Por exemplo, para obter o pacote [FISHalyseR](http://bioconductor.org/packages/release/bioc/html/FISHalyseR.html) da Bioconductor:  
  
1.  Na lista **Arquivos de Pacote** , localize a versão **Binário do Windows** .  
  
2.  Clique com o botão direito do mouse no link do arquivo .ZIP e selecione  **Salvar destino como**.  
  
3.  Navegue até a pasta local onde os pacotes compactados foram armazenados e clique em **Salvar**.  
  
 Esse processo cria uma cópia local do pacote. Você pode instalar o pacote, ou copie o pacote compactado para um servidor que não tem acesso à Internet.  
  
  
## <a name="2-open-the-default-r-package-library-for-sql-server-r-services"></a>2. Abra a biblioteca de pacote padrão R para serviços do SQL Server R 

Navegue até a pasta no servidor onde os pacotes de R associados ao [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] foram instalados. É importante que você instale pacotes da biblioteca padrão que é associado à instância atual. 

Para obter instruções sobre como localizar essa biblioteca, consulte [Instalando e Gerenciando pacotes de R](../../advanced-analytics/r-services/installing-and-managing-r-packages.md).

   Para cada instância onde você executará um pacote, você deve instalar uma cópia separada dos pacotes. Atualmente os pacotes não podem ser compartilhados entre instâncias.
     
  
## <a name="3-open-an-administrative-command-prompt"></a>3. Abra um prompt de comando administrativo 

Abra R como administrador.  Você pode fazer isso usando o comando de Windows p, ropt, ou usando um dos utilitários R.
  
### <a name="using-the-windows-command-prompt"></a>Usando o prompt de comando do Windows 

1. Abra um prompt de comando do Windows como administrador e navegue até o diretório onde estão localizados os arquivos RTerm.Exe ou RGui.exe.  
  
    Em uma instalação padrão, esse é o diretório **\bin** de R. Por exemplo, em [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], as ferramentas de R estão localizadas aqui: 

    **Instância padrão**

     `C:\Program Files\MSSQL13.MSSQLSERVER\R_SERVICES\bin` 
 
     **Instância nomeada**
   
     `C:\Program files\MSSQL13.<instanceName>\R_SERVICES\bin\x64`  
  
2. Execute **R.Exe**.  
  
### <a name="using-the-r-commandline-utilities"></a>Como usar os utilitários de linha de comando de R. 
  
1. Use o Windows Explorer para navegar até o diretório que contém as ferramentas de R.  
  
2. Clique com botão direito **RGui.exe** ou **RTerm.exe**, e selecione **Executar como administrador**.  
## <a name="4-install-the-package"></a>4. Instalar o pacote

O comando para instalar o pacote R depende se você receber o pacote da Internet ou de um arquivo compactado local.  
  
### <a name="install-package-from-internet"></a>Instale o pacote da Internet  
  
1.  Em geral, use o seguinte comando para instalar um novo pacote de CRAN ou um dos sites de espelho.  
  
    ```  
    install.packages("target_package_name")  
    ```
    
    Observe que as aspas duplas são sempre obrigatórias para o nome do pacote.

2.  Para especificar a biblioteca onde o pacote deve ser instalado, use um comando como este para definir a localização da biblioteca:
    
    ```  
    lib.SQL <- "C:\\Program Files\\Microsoft SQL Server\\MSSQL13.MSSQLSERVER\\R_SERVICES\\library"    
    ```

    Observe que para [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], atualmente biblioteca apenas um pacote é permitida. Não instalar pacotes em uma biblioteca de usuário, ou você não poderá executar o pacote de [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)].   
     
3.  Após a definição a localização da biblioteca, a instrução a seguir instala o pacote de e1070 popular para a biblioteca de pacote usada pelos serviços de R.  
  
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
  
### <a name="manual-package-installation-or-installing-on-computer-with-no-internet-access"></a>Instalação manual ou instalar no computador sem acesso à Internet 

1. Se o pacote que você pretende instalar tem dependências, obtenha os pacotes necessários antecipadamente e adicioná-los para a pasta com outro pacote de arquivos compactado.

    > [!TIP]
    > 
    > É recomendável que você configure um repositório local usando [miniCRAN](https://mran.revolutionanalytics.com/package/miniCRAN/) se você precisar oferecer suporte à instalação offline frequente dos pacotes de R.  
  
2.  No prompt de comando de R, digite o seguinte comando para especificar o caminho e o nome do pacote para instalação:  
   
    ```  
    install.packages("C:\\Temp\\Downloaded packages\\mynewpackage.zip", repos=NULL)  
    ``` 
     
    Este comando extrai o pacote R de seu arquivo compactado local, supondo que você salvou a cópia no diretório `C:\Temp\Downloaded packages`, e instala o pacote (com suas dependências) para a biblioteca de R no computador local.  
  
3.  Se você modificou anteriormente o ambiente R no computador, você deve garantir que a variável de ambiente R `.libPath` usa apenas um caminho, que aponta para a pasta R_SERVICES para a instância.  
  
> [!NOTE]
> Se você tiver instalado o Microsoft R servidor (autônomo) além de serviços do SQL Server R, seu computador terá uma instalação separada de R com todas as bibliotecas e ferramentas de R. Pacotes que estão instalados para a biblioteca R_SERVER são usados apenas pelo Microsoft R Server e não pode ser acessados por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
> 
>  Certifique-se de usar a biblioteca R_SERVICES ao instalar os pacotes que você deseja usar no SQL Server.

  
## <a name="see-also"></a>Consulte também  
 [Configurar serviços do SQL Server R &40; no banco de dados &41;](../../advanced-analytics/r-services/set-up-sql-server-r-services-in-database.md)  
  
  