---
title: Instalando o SSMA para Sybase (SybaseToSQL) | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 8d5a4ce6-b747-46e3-9184-645d56e8b35c
caps.latest.revision: 6
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 432a31ae12c1d3fc091893de332a72a5da1c4fc3
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="installing-ssma--for-sybase-sybasetosql"></a>Instalando o SSMA para Sybase (SybaseToSQL)
[!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]SSMA (Migration Assistant) para Sybase consiste em um aplicativo cliente que você usa para executar uma migração do Sybase Adaptive Server Enterprise (ASE) para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou do SQL Azure. Ele também contém um pacote de extensão que oferece suporte à migração de dados e o uso das funções do sistema ASE em seus bancos de dados migrados.  
  
Você pode instalar o aplicativo cliente no computador do qual você executará as etapas de migração. Você deve instalar os arquivos de pacote de extensão no computador que está executando [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] onde os bancos de dados migrados serão hospedados.  
  
## <a name="upgrading-ssma-for-sybase"></a>Atualizando o SSMA para Sybase  
Se você quiser atualizar para uma versão posterior do SSMA for Sybase, você deve primeiro desinstalar o cliente e o pacote de extensão do servidor e, em seguida, instale a versão mais recente.  
  
Se você abrir um projeto de uma versão anterior do SSMA for Sybase, SSMA perguntará se você deseja converter o projeto para a versão mais recente. Você deve clicar em **Sim** para trabalhar com o projeto na versão mais recente do SSMA.  
  
## <a name="contents"></a>Sumário  
  
|Tópico|Description|  
|---------|---------------|  
|[Instalando o SSMA para Sybase cliente &#40; SybaseToSQL &#41;](../../ssma/sybase/installing-ssma-for-sybase-client-sybasetosql.md)|Fornece informações sobre e instruções para instalar o cliente do SSMA.|  
|[Instalando componentes do SSMA SQL Server &#40; SybaseToSQL &#41;](../../ssma/sybase/installing-ssma-components-on-sql-server-sybasetosql.md)|Fornece informações e instruções para instalar o pacote de extensão em instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].|  
|[Removendo o SSMA para Sybase componentes &#40; SybaseToSQL &#41;](../../ssma/sybase/removing-ssma-for-sybase-components-sybasetosql.md)|Fornece instruções para desinstalar o cliente do pacote de programa e a extensão.|  
  
## <a name="see-also"></a>Consulte também  
[Migrando Sybase ASE bancos de dados do SQL Server - banco de dados SQL do Azure &#40; SybaseToSQL &#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  

