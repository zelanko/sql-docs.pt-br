---
title: "Criar um reposit&#243;rio de pacote Local usando miniCRAN | Microsoft Docs"
ms.custom: ""
ms.date: "05/27/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 27f2a1ce-316f-4347-b206-8a1b9eebe90b
caps.latest.revision: 4
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 4
---
# Criar um reposit&#243;rio de pacote Local usando miniCRAN
Este tópico descreve como você pode criar um repositório de pacotes de R local usando o pacote R **miniCRAN**. 

Porque [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] instâncias normalmente estão localizadas em um servidor que não tem conectividade com a Internet, o método padrão de instalação de pacotes de R (o comando R `install.packages()`) podem não funcionar, pois o instalador do pacote não é possível acessar CRAN ou quaisquer outros sites de espelho.

Há duas opções para instalar pacotes de um compartilhamento local ou o repositório:

+ Use o pacote miniCRAN para criar um repositório local dos pacotes, você precisa, então instala deste repositório. Este tópico descreve o método miniCRAN.

+ Baixe os pacotes necessários e suas dependências, como arquivos zip e salvá-los em uma pasta local e, em seguida, copie essa pasta para o [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] computador. Para obter mais informações sobre o método de cópia manual, consulte [instalar pacotes adicionais no SQL Server](../../advanced-analytics/r-services/install-additional-r-packages-on-sql-server.md).


## Etapa 1. Instalar miniCRAN e baixar pacotes 


1. Instale o pacote de miniCRAN em um computador que tenha acesso à Internet.

   ~~~~
   # Install miniCRAN ---------------------------------------------------

   if(!require("miniCRAN")) install.packages("miniCRAN")
   if(!require("igraph")) install.packages("igraph")
   library(miniCRAN)

   # Define the package source: a CRAN mirror, or an MRAN snapshot
   CRAN_mirror <- c(CRAN = "https://mran.microsoft.com/snapshot/2016-04-01")

   # Define the local download location
   local_repo <- "~/miniCRAN"
   ~~~~

2. Baixar ou instalar os pacotes que necessários para este computador. Isso criará a estrutura de pastas que você precisa copiar os pacotes para o [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] mais tarde.

   ~~~~
   # List the packages you need 
   # Do not specify dependencies
   pkgs_needed <- c("ggplot2", "ggdendro")
   ~~~~

3. Copiar o repositório miniCRAN na biblioteca R_SERVICES na [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] instância.

## Etapa 2. Instalar os pacotes no computador do SQL Server 

4. Sobre o [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] computador, execute o comando R  `install.packages()`. Você pode usar uma das ferramentas de R são instaladas com o [!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)], como Rgui.exe, ou você pode executar o comando como parte de uma [!INCLUDE[tsql_md](../../includes/tsql-md.md)] procedimento armazenado.
5. No prompt para especificar um repositório, selecione a pasta que contém os arquivos que você acabou de copiar; ou seja, o repositório local miniCRAN.

   ~~~~
   pkgs_needed <- c("ggplot2", "ggdendro")
   local_repo  <- "~/miniCRAN"
   
   .libPaths()[1]
   "C:/Program Files/Microsoft SQL Server/130/R_SERVER/library"

   lib <- .libPaths()[1]

   install.packages(pkgs_needed, 
                 repos = file.path("file://", normalizePath(local_repo, winslash = "/")),
                 lib = lib,
                 type = "win.binary",
                 dependencies = TRUE
                 )
   ~~~~

6. Verificar se os pacotes foram instalados ao executar esse código R.
   ~~~~
   installed.packages()
   ~~~~



## Confirmações

A fonte dessas informações é neste artigo, Andre de Vries, que também desenvolveu o pacote miniCRAN. Para obter detalhes e uma explicação completa, consulte  [como instalar o R pacotes em uma instância do SQL Server 2016 off-line](http://blog.revolutionanalytics.com/2016/05/minicran-sql-server.html)