---
title: Determinar se o Mecanismo de Banco de Dados está instalado e foi iniciado | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- SQL Server, determining if installed
- verifying Database Engine installation
- viewing Database Engine installation
- installed Database Engine verification [SQL Server]
ms.assetid: babb02e4-3521-4b75-b5df-e09205594375
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 6fce171575cf2383c308c3992126c784ca3691d5
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48115716"
---
# <a name="determine-whether-the-database-engine-is-installed-and-started"></a>Determinar se o Mecanismo de Banco de Dados está instalado e iniciado
  Uma instalação bem sucedida do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] instala arquivos no sistema de arquivos, cria entradas no Registro e instala várias ferramentas. Este tópico descreve como determinar se o [!INCLUDE[ssDE](../../includes/ssde-md.md)] está instalado e iniciado no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Configuration Manager  
  
#### <a name="how-to-view-and-start-the-database-engine-by-using-sql-server-configuration-manager"></a>Como exibir e iniciar o Mecanismo de Banco de Dados usando o SQL Server Configuration Manager  
  
1.  Clique em **Iniciar**, aponte para **Todos os Programas**, aponte para **Microsoft SQL Server**, aponte para **Ferramentas de Configuração**e clique em **SQL Server Configuration Manager**.  
  
     Se você não tiver essas entradas no menu **Iniciar** , significa que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não está instalado corretamente. Execute a Instalação para instalar o [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)].  
  
2.  No **SQL Server Configuration Manager**, no painel esquerdo, clique em **Serviços do SQL Server**. O painel direito lista vários serviços relacionados ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se o [!INCLUDE[ssDE](../../includes/ssde-md.md)] estiver instalado, o serviço do [!INCLUDE[ssDE](../../includes/ssde-md.md)] estará listado como **SQL Server (MSSQLSERVER)** , se for a instância padrão, ou como **SQL Server (**\<*instance_name*>**)**, se o [!INCLUDE[ssDE](../../includes/ssde-md.md)] estiver instalado como uma instância nomeada. A menos que o nome da instância seja alterado, o [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] é instalado como uma instância nomeada denominada **SQLEXPRESS**. Um ícone de triângulo verde indica que o [!INCLUDE[ssDE](../../includes/ssde-md.md)] está em execução. Um ícone de quadrado vermelho indica que o [!INCLUDE[ssDE](../../includes/ssde-md.md)] está parado.  
  
3.  Para iniciar o [!INCLUDE[ssDE](../../includes/ssde-md.md)], no painel direito, clique com o botão direito do mouse em [!INCLUDE[ssDE](../../includes/ssde-md.md)]e clique em **Iniciar**.  
  
> [!NOTE]  
>  Durante a instalação, o usuário pode selecionar um local no qual instalar os arquivos de programa e os arquivos de banco de dados. Se o usuário aceitar o local padrão, os arquivos serão instalados em [!INCLUDE[ssInstallPath](../../includes/ssinstallpath-md.md)] e em C:\Arquivos de Programas\Microsoft SQL Server\MSSQL.*x*, em que *x* é um número.  
  
  
