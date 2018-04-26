---
title: Assistente de migração do SQL Server para Access (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-access
ms.custom: ''
ms.date: 08/14/2017
ms.reviewer: ''
ms.suite: sql
ms.technology:
- sql-ssma
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 40c1eb02-26b2-44ba-969d-6c430c61c281
caps.latest.revision: 22
author: Shamikg
ms.author: Shamikg
manager: murato
ms.workload: On Demand
ms.openlocfilehash: a9634591b3f9d1c75bc64e89c363a38e4d6b1b7e
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
---
# <a name="sql-server-migration-assistant-for-access-accesstosql"></a>Assistente de migração do SQL Server para Access (AccessToSQL)
[!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] SSMA (Migration Assistant) para o acesso é uma ferramenta para migrar bancos de dados de [!INCLUDE[msCoName](../../includes/msconame_md.md)] acessar versões 97 através do 2010 para [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2005 / [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2008 / [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2012 / [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2014 / [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2016 / [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2017 no Windows e Linux (visualização) / [!INCLUDE[msCoName](../../includes/msconame_md.md)] banco de dados SQL do Azure. O SSMA para Access converte objetos de banco de dados do Access para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou objetos de banco de dados do SQL Azure, carrega os objetos em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou SQL Azure, e migra os dados do Access para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou SQL Azure.  
  
Esta documentação apresenta o SSMA para Access e fornece instruções passo a passo para migrar bancos de dados do Access para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou SQL Azure e obter informações sobre problemas que podem ocorrer após a migração.  
  
## <a name="contents"></a>Sumário  
  
|Seção|Description|  
|-----------|---------------|  
|[Novidades do SSMA para Access](http://msdn.microsoft.com/en-us/a24d3fc0-6911-4bfa-828a-197abf222e02)|Lista as alterações às versões do SSMA.|  
|[Instalando o Assistente de migração do SQL Server para Access](http://msdn.microsoft.com/en-us/dd50eebd-75df-4e0d-8c4d-88b511aae4c7)|Lista os pré-requisitos para a instalação do SSMA, o procedimento de instalação e licenciamento do SSMA e um link para a versão mais recente.|  
|[Introdução ao Assistente de migração do SQL Server para Access &#40;AccessToSQL&#41;](../../ssma/access/getting-started-with-sql-server-migration-assistant-for-access-accesstosql.md)|Apresenta o SSMA e sua interface do usuário.|  
|[Preparar bancos de dados do Access para a migração](http://msdn.microsoft.com/en-us/9b80a9e0-08e7-4b4d-b5ec-cc998d3f5114)|Descreve como preparar seus bancos de dados do Access para conversão em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] SQL Azure.|  
|[Migrando bancos de dados do Access para o SQL Server](http://msdn.microsoft.com/en-us/76a3abcf-2998-4712-9490-fe8d872c89ca)|Fornece uma visão geral do processo de conversão e informações detalhadas sobre cada etapa do processo.|  
|[Vinculando a aplicativos de acesso ao SQL Server](http://msdn.microsoft.com/en-us/82374ad2-7737-4164-a489-13261ba393d4)|Descreve como usar seus aplicativos existentes do Access com [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].|  
|[Referência da interface do usuário](http://msdn.microsoft.com/en-us/af24c303-4a41-449b-9c86-d6558a97e839)|Contém a documentação do SSMA para caixas de diálogo.|  
|[Trabalhar com o console do SSMA para Access](http://msdn.microsoft.com/en-us/ef94e843-9f88-45a2-86c4-a0af268738c4)|Contém a documentação sobre o aplicativo de Console SSMA|  
|[Obtendo assistência do SSMA para Access](http://go.microsoft.com/fwlink/?LinkID=708538&clcid=0x409)|Fornece informações sobre como obter assistência adicional.|  
  
