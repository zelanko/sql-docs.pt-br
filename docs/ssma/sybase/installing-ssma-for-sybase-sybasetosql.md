---
title: Instalando o SSMA para SAP ASE (SybaseToSQL) | Microsoft Docs
ms.custom: 
ms.date: 11/29/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 8d5a4ce6-b747-46e3-9184-645d56e8b35c
caps.latest.revision: "6"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 282dacb356df5a7956e9f30852193b54f37961e7
ms.sourcegitcommit: c41e1bf5a53e96855b4424de4e0897153070bb28
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/28/2017
---
# <a name="installing-ssma-for-sap-ase-sybasetosql"></a>Instalando o SSMA para SAP ASE (SybaseToSQL)
[!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]SSMA (Migration Assistant) para o SAP Adaptive Server Enterprise (ASE) consiste em um aplicativo cliente que você usa para realizar uma migração do SAP ASE para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou banco de dados do SQL Azure. Ele também contém um pacote de extensão que oferece suporte à migração de dados e o uso das funções do sistema ASE em seus bancos de dados migrados.  
  
Instale o aplicativo cliente no computador do qual você planeja executar as etapas de migração. Instalar os arquivos de pacote de extensão no computador que está executando [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] no qual os bancos de dados migrados devem ser hospedadas.  
  
## <a name="upgrading-ssma-for-sap-ase"></a>Atualizando o SSMA para SAP ASE  
Se você quiser atualizar para uma versão posterior do SSMA para SAP ASE, primeiro você deve desinstalar o cliente e o pacote de extensão do servidor. Em seguida, instale a versão mais recente.  
  
Se você abrir um projeto de uma versão anterior do SSMA para SAP ASE, SSMA perguntará se você deseja converter o projeto para a versão mais recente. Clique em **Sim** para trabalhar com o projeto na versão mais recente do SSMA.  
  
## <a name="contents"></a>Sumário  
  
|Artigo|Description|  
|---------|---------------|  
|[Instalando o SSMA para SAP ASE cliente &#40; SybaseToSQL &#41;](../../ssma/sybase/installing-ssma-for-sybase-client-sybasetosql.md)|Fornece informações sobre e instruções para instalar o SSMA para cliente SAP ASE.|  
|[Instalando componentes do SSMA SQL Server &#40; SybaseToSQL &#41;](../../ssma/sybase/installing-ssma-components-on-sql-server-sybasetosql.md)|Fornece informações e instruções para instalar o pacote de extensão em instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].|  
|[Removendo o SSMA para componentes do SAP ASE &#40; SybaseToSQL &#41;](../../ssma/sybase/removing-ssma-for-sybase-components-sybasetosql.md)|Fornece instruções para desinstalar o cliente do pacote de programa e a extensão.|  
  
## <a name="see-also"></a>Consulte também  
[Migrando SAP ASE bancos de dados para o SQL Server - banco de dados SQL do Azure &#40; SybaseToSQL &#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
