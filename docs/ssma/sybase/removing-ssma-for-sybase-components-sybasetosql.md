---
title: Removendo o SSMA para Sybase componentes (SybaseToSQL) | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: aec09593-17d9-4ec2-ac56-3cd8851406fd
caps.latest.revision: "6"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: dadcc8384871ceaebd0151859f4017c88ed6a219
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="removing-ssma-for-sybase-components-sybasetosql"></a>Removendo o SSMA para Sybase componentes (SybaseToSQL)
Quando terminar de migrar bancos de dados do Sybase Adaptive Server Enterprise (ASE) para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], talvez você queira desinstalar componentes do SSMA. Você pode desinstalar os componentes do cliente a qualquer momento, mas você não deve desinstalar o pacote de extensão de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] , a menos que você tiver certeza de que seus bancos de dados migrados não usam funções no **ssma_syb** esquema do **sysdb** banco de dados.  
  
## <a name="uninstalling-the-ssma-for-sybase-client"></a>Desinstalando o SSMA para Sybase cliente  
Você pode desinstalar o SSMA usando **adicionar ou remover programas**.  
  
**Para desinstalar o SSMA**  
  
1.  No painel de controle, abra **adicionar ou remover programas**.  
  
2.  Selecione **Microsoft SQL Server Migration Assistant para Sybase**e, em seguida, clique em **remover**.  
  
3.  Para confirmar que você deseja desinstalar o SSMA, clique em **Sim**.  
  
## <a name="uninstalling-the-extension-pack"></a>Desinstalar o pacote de extensão  
Se você tiver certeza de seus bancos de dados migrados não usam objetos de **sysdb.ssma_syb** esquema, você pode remover o pacote de extensão usando **adicionar ou remover programas**.  
  
Para desinstalar o pacote de extensão  
  
1.  No painel de controle, abra **adicionar ou remover programas**.  
  
2.  Selecione **Microsoft SQL Server Migration Assistant para o pacote de extensão do Sybase**e, em seguida, clique em **remover**.  
  
3.  Para confirmar que você deseja desinstalar o pacote de extensão, clique em **Sim**.  
  
4.  Em instâncias com página de Scripts de banco de dados de utilitários, clique em **próximo**.  
  
5.  Na página de parâmetros de Conexão, selecione o método de autenticação e, em seguida, clique em **próximo**.  
  
    Autenticação do Windows usará as credenciais do Windows para tentar fazer logon instância do SQL Server. Se você selecionar a autenticação do SQL Server, você deve inserir um nome de logon do SQL Server e uma senha.  
  
6.  Na página concluir a operação, clique em **Okey**.  
  
7.  Na página conclusão, clique em **saída**.  
  
Após a desinstalação, você pode confirmar que o **sysdb.ssma_syb** esquema e, possivelmente, todo o **sysdb** banco de dados, foi removido usando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)]. No entanto, se você usar outros produtos do SSMA, eles também usam o **sysdb** banco de dados. Se o banco de dados existe e você tiver certeza de que nenhum outro banco de dados fazem referência a objetos no banco de dados, é possível desanexar o banco de dados.  
  
## <a name="see-also"></a>Consulte também  
[Instalando o SSMA para Sybase cliente &#40; SybaseToSQL &#41;](../../ssma/sybase/installing-ssma-for-sybase-client-sybasetosql.md)  
[Instalando componentes do SSMA SQL Server &#40; SybaseToSQL &#41;](../../ssma/sybase/installing-ssma-components-on-sql-server-sybasetosql.md)  
  
