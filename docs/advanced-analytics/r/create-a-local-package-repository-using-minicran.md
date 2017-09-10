---
title: "Criar um repositório de pacote local usando o miniCRAN | Microsoft Docs"
ms.custom: 
ms.date: 03/30/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 27f2a1ce-316f-4347-b206-8a1b9eebe90b
caps.latest.revision: 4
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: e8af93b3e132290eef4b43da568b9381ff8e5a04
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="create-a-local-package-repository-using-minicran"></a>Criar um repositório de pacote local usando o miniCRAN
Este tópico descreve como é possível criar um repositório local de pacotes de R usando o pacote **miniCRAN**. 

Como as instâncias [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] normalmente estão localizadas em um servidor que não tem conectividade com a Internet, talvez o método padrão de instalação de pacotes de R (o comando `install.packages()` do R) não funcione, porque o instalador do pacote não pode acessar o CRAN ou quaisquer outros locais de espelho.

Há duas opções para instalar pacotes de um compartilhamento local ou do repositório:

+ Use o pacote miniCRAN para criar um repositório local dos pacotes necessários, em seguida, instale desse repositório. Este tópico descreve o método miniCRAN.

+ Baixe os pacotes necessários e suas dependências, como arquivos zip e salve-os em uma pasta local e, em seguida, copie essa pasta para o computador [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]. Para obter mais informações sobre o método de cópia manual, consulte [Install Additional Packages on SQL Server (Instalar pacotes adicionais no SQL Server)](../../advanced-analytics/r-services/install-additional-r-packages-on-sql-server.md).


## <a name="step-1-install-minicran-and-download-packages"></a>Etapa 1. Instalar o miniCRAN e baixar pacotes 


1. Instale o pacote miniCRAN em um computador que tenha acesso à Internet.

   ~~~~
   # Install miniCRAN and igraph

   if(!require("miniCRAN")) install.packages("miniCRAN")
   if(!require("igraph")) install.packages("igraph")
   library(miniCRAN)

   # Define the package source: a CRAN mirror, or an MRAN snapshot
   CRAN_mirror <- c(CRAN = "https://mran.microsoft.com/snapshot/2016-04-01")

   # Define the local download location
   local_repo <- "~/miniCRAN"
   ~~~~

2. Baixe ou instale os pacotes necessários para esse computador usando o seguinte script R. Isso criará a estrutura de pastas de que você precisa para copiar os pacotes para o [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] posteriormente.

   ~~~~
   # List the packages to get. Do not specify dependencies.
   pkgs_needed <- c("ggplot2", "ggdendro")
   # Plot the dependency graph 
   plot(makeDepGraph(pkgs_needed)) 
   
   # Create the local repo 
   pkgs_expanded <- pkgDep(pkgs_needed, repos = CRAN_mirror) 
   makeRepo(pkgs_expanded, path = local_repo, repos = CRAN_mirror, type = "win.binary", Rversion = "3.2") 

   # List local packages 
   pdb <- as.data.frame( 
     pkgAvail(local_repo, type = "win.binary", Rversion = "3.2"),  
     stringsAsFactors = FALSE) 
   head(pdb) 
   pdb$Package 
   pdb[, c("Package", "Version", "License")] 
   ~~~~


## <a name="step-2-copy-the-minicran-repository-to-the-sql-server-computer"></a>Etapa 2. Copie o repositório miniCRAN para o computador do SQL Server 

Copie o repositório miniCRAN para a biblioteca R_SERVICES na instância do [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)].

+ Para o SQL Server 2016, a pasta padrão é `C:/Program Files/Microsoft SQL Server/MSSQL13.MSSQLSERVER/R_SERVICES/library1`.
+ Para o SQL Server 2017, a pasta padrão é `C:/Program Files/Microsoft SQL Server/MSSQL14.MSSQLSERVER/R_SERVICES/library1`.

Se você tiver instalado o R Services usando uma instância nomeada, certifique-se de incluir o nome da instância no caminho para garantir que as bibliotecas sejam instaladas na instância correta. Por exemplo, se sua instância nomeada fosse RTEST02, o caminho padrão da instância nomeada seria: `C:\Program Files\Microsoft SQL Server\MSSQL13.RTEST02\R_SERVICES\library`.

Se você tiver instalado o SQL Server em uma unidade diferente ou tiver feito outras alterações no caminho de instalação, certifique-se de fazer essas alterações também.

## <a name="step-3-install-the-packages-on-sql-server-using-the-minicran-repository"></a>Etapa 3. Instalar os pacotes no SQL Server usando o repositório miniCRAN

No computador [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], abra uma linha de comando do R ou o RGUI como administrador. 
  
> [!TIP]
> Talvez você tenha várias bibliotecas do R no computador; portanto, para garantir que os pacotes sejam instalados na instância correta, use a cópia do RGUI ou do RTerm instalada com a instância específica em que você deseja instalar os pacotes.
  
Quando você for solicitado a especificar um repositório, selecione a pasta que contém os arquivos que você acabou de copiar; ou seja, o repositório local miniCRAN.

   ~~~~
   # Run this R code as administrator on the SQL Server computer 
   pkgs_needed <- c("ggplot2", "ggdendro") 
   local_repo  <- "~/miniCRAN" 

   # OPTIONAL: If you are not running R from the instance library as recommended, you must specify the path
   #   .libPaths()[1] 
   # "C:/Program Files/Microsoft SQL Server/MSSQL14.MSSQLSERVER/R_SERVICES/library " 
   # lib <- .libPaths()[1]
   
   install.packages(pkgs_needed,  
                    repos = file.path("file://", normalizePath(local_repo, winslash = "/")), 
                    lib = lib, 
                    type = "win.binary", 
                    dependencies = TRUE 
                    ) 
   installed.packages() 
   ~~~~

Verifique se os pacotes foram instalados.
   ~~~~
   installed.packages()
   ~~~~



## <a name="acknowledgements"></a>Confirmações

A fonte dessas informações é este artigo de Andre de Vries, que também desenvolveu o pacote miniCRAN. Para obter detalhes e um passo a passo completo, consulte [How to install R packages on an off-line SQL Server 2016 instance (Como instalar os pacotes de R em uma instância offline do SQL Server 2016)](http://blog.revolutionanalytics.com/2016/05/minicran-sql-server.html)

