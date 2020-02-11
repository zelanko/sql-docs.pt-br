---
title: Instalando o SSMA para SAP ASE (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/29/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 8d5a4ce6-b747-46e3-9184-645d56e8b35c
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 91a4dfcf8add3900c51e33a6e40fa874ce9f9798
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68028968"
---
# <a name="installing-ssma-for-sap-ase-sybasetosql"></a>Instalando o SSMA para SAP ASE (SybaseToSQL)
[!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]O Assistente de Migração (SSMA) para SAP Adaptive Server Enterprise (ASE) consiste em um aplicativo cliente que você usa para executar uma migração do SAP ASE para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o ou para o banco de dados SQL do Azure. Ele também contém um pacote de extensão que dá suporte à migração de dados e ao uso de funções de sistema ASE em seus bancos de dados migrados.  
  
Instale o aplicativo cliente no computador do qual você planeja executar as etapas de migração. Instale os arquivos do pacote de extensão no computador que está [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sendo executado no qual os bancos de dados migrados devem ser hospedados.  
  
## <a name="upgrading-ssma-for-sap-ase"></a>Atualizando o SSMA para SAP ASE  
Se você quiser atualizar para uma versão posterior do SSMA para SAP ASE, primeiro você deve desinstalar o cliente e o pacote de extensão do servidor. Em seguida, instale a versão mais recente.  
  
Se você abrir um projeto de uma versão anterior do SSMA para SAP ASE, o SSMA perguntará se você deseja converter o projeto para a versão mais recente. Clique em **Sim** para trabalhar com o projeto na versão mais recente do SSMA.  
  
## <a name="contents"></a>Conteúdo  
  
|Artigo|DESCRIÇÃO|  
|---------|---------------|  
|[Instalando o cliente do SSMA para SAP ASE &#40;SybaseToSQL&#41;](../../ssma/sybase/installing-ssma-for-sybase-client-sybasetosql.md)|Fornece informações e instruções para instalar o cliente do SSMA para SAP ASE.|  
|[Instalando os componentes do SSMA em SQL Server &#40;SybaseToSQL&#41;](../../ssma/sybase/installing-ssma-components-on-sql-server-sybasetosql.md)|Fornece informações e instruções para instalar o pacote de extensão em instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|[Removendo os componentes do SSMA para SAP ASE &#40;SybaseToSQL&#41;](../../ssma/sybase/removing-ssma-for-sybase-components-sybasetosql.md)|Fornece instruções para desinstalar o programa cliente e o pacote de extensão.|  
  
## <a name="see-also"></a>Confira também  
[Migrar bancos de dados do SAP ASE para o SQL Server-Azure SQL Database &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
