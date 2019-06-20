---
title: Instalar o SSMA para SAP ASE (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/29/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 8d5a4ce6-b747-46e3-9184-645d56e8b35c
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: b859c3b9841945241ac0ec9c5238a479a5ba3343
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63302815"
---
# <a name="installing-ssma-for-sap-ase-sybasetosql"></a>Instalar o SSMA para SAP ASE (SybaseToSQL)
[!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SSMA (Migration Assistant) para o SAP Adaptive Server Enterprise (ASE) consiste em um aplicativo cliente que você usa para realizar uma migração do SAP ASE para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou banco de dados SQL. Ele também contém um pacote de extensão que oferece suporte à migração de dados e o uso das funções do sistema ASE em seus bancos de dados migrados.  
  
Instale o aplicativo cliente no computador do qual você planeja executar as etapas de migração. Instalar os arquivos de pacote de extensão no computador que está executando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no qual os bancos de dados migrados devem ser hospedadas.  
  
## <a name="upgrading-ssma-for-sap-ase"></a>Atualizando o SSMA para SAP ASE  
Se você quiser atualizar para uma versão posterior do SSMA para SAP ASE, você deve primeiro desinstalar o cliente e o pacote de extensão do servidor. Em seguida, instale a versão mais recente.  
  
Se você abrir um projeto de uma versão anterior do SSMA para SAP ASE, o SSMA perguntará se você deseja converter o projeto para a versão mais recente. Clique em **Sim** para trabalhar com o projeto na versão mais recente do SSMA.  
  
## <a name="contents"></a>Sumário  
  
|Artigo|Descrição|  
|---------|---------------|  
|[Instalar o SSMA para cliente do SAP ASE &#40;SybaseToSQL&#41;](../../ssma/sybase/installing-ssma-for-sybase-client-sybasetosql.md)|Fornece informações e instruções para instalar o SSMA para cliente do SAP ASE.|  
|[Instalar os componentes do SSMA no SQL Server &#40;SybaseToSQL&#41;](../../ssma/sybase/installing-ssma-components-on-sql-server-sybasetosql.md)|Fornece informações e instruções para instalar o pacote de extensão em instâncias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|[Remover o SSMA para componentes do SAP ASE &#40;SybaseToSQL&#41;](../../ssma/sybase/removing-ssma-for-sybase-components-sybasetosql.md)|Fornece instruções para desinstalar o cliente pack de programa e a extensão.|  
  
## <a name="see-also"></a>Confira também  
[Bancos de dados do SAP ASE migrando para o SQL Server - banco de dados SQL &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
