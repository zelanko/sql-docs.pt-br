---
title: Instalando o SSMA para SAP ASE (SybaseToSQL) | Microsoft Docs
description: Use estes artigos para instalar, atualizar e desinstalar o Assistente de Migração do SQL Server para SAP ASE, que inclui um aplicativo cliente e um pacote de extensão.
ms.custom: ''
ms.date: 11/29/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 8d5a4ce6-b747-46e3-9184-645d56e8b35c
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 302225b3339f779bbcf138ce0c6ee2e3ee24adf8
ms.sourcegitcommit: 59cda5a481cfdb4268b2744edc341172e53dede4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/02/2020
ms.locfileid: "84292894"
---
# <a name="installing-ssma-for-sap-ase-sybasetosql"></a>Instalando o SSMA para SAP ASE (SybaseToSQL)
[!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]O Assistente de Migração (SSMA) para SAP Adaptive Server Enterprise (ASE) consiste em um aplicativo cliente que você usa para executar uma migração do SAP ASE para o ou para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] banco de dados SQL do Azure. Ele também contém um pacote de extensão que dá suporte à migração de dados e ao uso de funções de sistema ASE em seus bancos de dados migrados.  
  
Instale o aplicativo cliente no computador do qual você planeja executar as etapas de migração. Instale os arquivos do pacote de extensão no computador que está sendo executado [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no qual os bancos de dados migrados devem ser hospedados.  
  
## <a name="upgrading-ssma-for-sap-ase"></a>Atualizando o SSMA para SAP ASE  
Se você quiser atualizar para uma versão posterior do SSMA para SAP ASE, primeiro você deve desinstalar o cliente e o pacote de extensão do servidor. Em seguida, instale a versão mais recente.  
  
Se você abrir um projeto de uma versão anterior do SSMA para SAP ASE, o SSMA perguntará se você deseja converter o projeto para a versão mais recente. Clique em **Sim** para trabalhar com o projeto na versão mais recente do SSMA.  
  
## <a name="contents"></a>Sumário  
  
|Artigo|Descrição|  
|---------|---------------|  
|[Instalando o cliente do SSMA para SAP ASE &#40;SybaseToSQL&#41;](../../ssma/sybase/installing-ssma-for-sybase-client-sybasetosql.md)|Fornece informações e instruções para instalar o cliente do SSMA para SAP ASE.|  
|[Instalando os componentes do SSMA em SQL Server &#40;SybaseToSQL&#41;](../../ssma/sybase/installing-ssma-components-on-sql-server-sybasetosql.md)|Fornece informações e instruções para instalar o pacote de extensão em instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|  
|[Removendo os componentes do SSMA para SAP ASE &#40;SybaseToSQL&#41;](../../ssma/sybase/removing-ssma-for-sybase-components-sybasetosql.md)|Fornece instruções para desinstalar o programa cliente e o pacote de extensão.|  
  
## <a name="see-also"></a>Veja também  
[Migrar bancos de dados do SAP ASE para o SQL Server-Azure SQL Database &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
