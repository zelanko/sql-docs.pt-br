---
title: "Determinar se o Mecanismo de Banco de Dados est&#225; instalado e iniciado | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "SQL Server, determinando se está instalado"
  - "verificando a instalação do Mecanismo de Banco de Dados"
  - "exibindo a instalação do Mecanismo de Banco de Dados"
  - "verificando se o Mecanismo de Banco de Dados está instalado [SQL Server]"
ms.assetid: babb02e4-3521-4b75-b5df-e09205594375
caps.latest.revision: 17
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 17
---
# Determinar se o Mecanismo de Banco de Dados est&#225; instalado e iniciado
  Uma instalação bem sucedida do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] instala arquivos no sistema de arquivos, cria entradas no Registro e instala várias ferramentas. Este tópico descreve como determinar se o [!INCLUDE[ssDE](../../includes/ssde-md.md)] está instalado e iniciado no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Configuration Manager  
  
#### Como exibir e iniciar o Mecanismo de Banco de Dados usando o SQL Server Configuration Manager  
  
1.  Clique em **Iniciar**, aponte para **Todos os Programas**, aponte para **Microsoft SQL Server**, aponte para **Ferramentas de Configuração** e clique em **SQL Server Configuration Manager**.  
  
     Se você não tiver essas entradas no menu **Iniciar**, significa que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não está instalado corretamente. Execute a Instalação para instalar o [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)].  
  
2.  No **SQL Server Configuration Manager**, no painel esquerdo, clique em **Serviços do SQL Server**. O painel direito lista vários serviços relacionados ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se o [!INCLUDE[ssDE](../../includes/ssde-md.md)] estiver instalado, o serviço do [!INCLUDE[ssDE](../../includes/ssde-md.md)] estará listado como **SQL Server (MSSQLSERVER)**, se for a instância padrão, ou como **SQL Server (**\<*instance_name*>**)**, se o [!INCLUDE[ssDE](../../includes/ssde-md.md)] estiver instalado como uma instância nomeada. A menos que o nome da instância seja alterado, o [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] é instalado como uma instância nomeada denominada **SQLEXPRESS**. Um ícone de triângulo verde indica que o [!INCLUDE[ssDE](../../includes/ssde-md.md)] está em execução. Um ícone de quadrado vermelho indica que o [!INCLUDE[ssDE](../../includes/ssde-md.md)] está parado.  
  
3.  Para iniciar o [!INCLUDE[ssDE](../../includes/ssde-md.md)], no painel direito, clique com o botão direito do mouse em [!INCLUDE[ssDE](../../includes/ssde-md.md)] e clique em **Iniciar**.  
  
> [!NOTE]  
>  Durante a instalação, o usuário pode selecionar um local no qual instalar os arquivos de programa e os arquivos de banco de dados. Se o usuário aceitar o local padrão, os arquivos serão instalados em [!INCLUDE[ssInstallPath](../../includes/ssinstallpath-md.md)] e em C:\Arquivos de Programas\Microsoft SQL Server\MSSQL.*x*, em que *x* é um número.  
  
  