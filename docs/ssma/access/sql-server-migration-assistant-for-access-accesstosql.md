---
title: Assistente de Migração do SQL Server para acesso (AccessToSQL) | Microsoft Docs
description: Saiba mais sobre o SSMA para acesso e siga as instruções passo a passo para migrar bancos de dados do Access para o SQL Server ou o Azure SQL Database.
ms.prod: sql
ms.custom: ''
ms.date: 10/10/2019
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 40c1eb02-26b2-44ba-969d-6c430c61c281
author: Jtoland
ms.author: Jtoland
manager: murato
ms.openlocfilehash: 2e4ce80a111efcf978da55cab280205b08acdd1f
ms.sourcegitcommit: 59cda5a481cfdb4268b2744edc341172e53dede4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/02/2020
ms.locfileid: "84292931"
---
# <a name="sql-server-migration-assistant-for-access-accesstosql"></a>Assistente de Migração do SQL Server para acesso (AccessToSQL)

[!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]O assistente de migração (SSMA) para acesso é uma ferramenta para a migração de bancos de dados do [!INCLUDE[msCoName](../../includes/msconame_md.md)] Acesse as versões de 97 a 2010 para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012, [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014, [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016, [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2017 no Windows e Linux, [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2019 no Windows e no Linux ou no [!INCLUDE[msCoName](../../includes/msconame_md.md)] banco de dados SQL do Azure. O SSMA para Access converte objetos de banco de dados do Access [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou objetos do banco de dados SQL do Azure, carrega esses objetos no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] banco de dados SQL do Azure e, em seguida, migra-os do Access para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou do Azure SQL Database.
  
Esta documentação apresenta o SSMA para o Access e fornece instruções passo a passo para migrar bancos de dados do Access para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou o Azure SQL Database e informações sobre problemas que podem ocorrer após a migração.  
  
## <a name="contents"></a>Sumário  
  
|Seção|Description|
|-----------|---------------|
|[Novidades do SSMA para Access](https://msdn.microsoft.com/a24d3fc0-6911-4bfa-828a-197abf222e02)|Lista as alterações em versões do SSMA.|  
|[Instalando o Assistente de Migração do SQL Server para acesso](installing-sql-server-migration-assistant-for-access-accesstosql.md)|Lista os pré-requisitos para instalar o SSMA, o procedimento para instalar e licenciar o SSMA e um link para a versão mais recente.|  
|[Introdução com Assistente de Migração do SQL Server para acesso &#40;AccessToSQL&#41;](../../ssma/access/getting-started-with-sql-server-migration-assistant-for-access-accesstosql.md)|Apresenta o SSMA e sua interface do usuário.|  
|[Preparando bancos de dados do Access para migração](preparing-access-databases-for-migration-accesstosql.md)|Descreve como preparar seus bancos de dados do Access para conversão para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] /SQL Azure.|  
|[Migrando bancos de dados do Access para SQL Server](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)|Fornece uma visão geral do processo de conversão e informações detalhadas sobre cada etapa no processo.|  
|[Vinculando aplicativos de acesso a SQL Server](linking-access-applications-to-sql-server-azure-sql-db-accesstosql.md)|Descreve como usar seus aplicativos do Access existentes com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|  
|[Referência da interface do usuário](user-interface-reference-accesstosql.md)|Contém a documentação das caixas de diálogo do SSMA.|  
|[Trabalhar com o console do SSMA para Access](working-with-ssma-for-access-console-accesstosql.md)|Contém documentação sobre o aplicativo de console do SSMA|  
|[Obtendo assistência do SSMA para acesso](https://go.microsoft.com/fwlink/?LinkID=708538&clcid=0x409)|Fornece informações sobre como obter assistência adicional.|  
