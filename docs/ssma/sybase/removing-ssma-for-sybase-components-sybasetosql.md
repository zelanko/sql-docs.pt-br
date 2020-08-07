---
title: Removendo os componentes do SSMA para Sybase (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: aec09593-17d9-4ec2-ac56-3cd8851406fd
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 4ffa47be1f35e86d09c136e5aeca6c0811630ca5
ms.sourcegitcommit: e8f6c51d4702c0046aec1394109bc0503ca182f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/07/2020
ms.locfileid: "87930547"
---
# <a name="removing-ssma-for-sybase-components-sybasetosql"></a>Remover componentes SSMA para Sybase (SybaseToSQL)
Quando você terminar de migrar bancos de dados do Sybase Adaptive Server Enterprise (ASE) para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , talvez queira desinstalar os componentes do SSMA. Você pode desinstalar os componentes do cliente a qualquer momento, mas não deve desinstalar o pacote de extensão a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] menos que tenha certeza de que seus bancos de dados migrados não usam mais funções no esquema de **ssma_syb** do banco de dados **sysdb** .  
  
## <a name="uninstalling-the-ssma-for-sybase-client"></a>Desinstalando o cliente SSMA para Sybase  
Você pode desinstalar o SSMA usando **Adicionar ou remover programas**.  
  
**Para desinstalar o SSMA**  
  
1.  No Painel de Controle, abra **Adicionar ou Remover Programas**.  
  
2.  Selecione **Assistente de migração do Microsoft SQL Server para Sybase**e clique em **remover**.  
  
3.  Para confirmar que deseja desinstalar o SSMA, clique em **Sim**.  
  
## <a name="uninstalling-the-extension-pack"></a>Desinstalando o pacote de extensão  
Se você tiver certeza de que os bancos de dados migrados não usam objetos no esquema **sysdb. ssma_syb** , você poderá remover o pacote de extensão usando **Adicionar ou remover programas**.  
  
Para desinstalar o pacote de extensão  
  
1.  No Painel de Controle, abra **Adicionar ou Remover Programas**.  
  
2.  Selecione **Assistente de migração do Microsoft SQL Server para pacote de extensão Sybase**e clique em **remover**.  
  
3.  Para confirmar que deseja desinstalar o pacote de extensão, clique em **Sim**.  
  
4.  Na página instâncias com scripts de banco de dados de utilitários, clique em **Avançar**.  
  
5.  Na página parâmetros de conexão, selecione o método de autenticação e clique em **Avançar**.  
  
    A autenticação do Windows usará suas credenciais do Windows para tentar fazer logon na instância do SQL Server. Se você selecionar SQL Server autenticação, deverá inserir um nome de logon e uma senha de SQL Server.  
  
6.  Na página operação concluída, clique em **OK**.  
  
7.  Na página concluir, clique em **sair**.  
  
Após a desinstalação, você pode confirmar se o esquema **sysdb. ssma_syb** e, possivelmente, o banco de dados **sysdb** inteiro, foi removido usando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] . No entanto, se você usar outros produtos do SSMA, eles também usarão o banco de dados **sysdb** . Se o banco de dados existir e você tiver certeza de que não há outros bancos de dados de referência a objetos nesse banco, você poderá desanexar o banco de dados.  
  
## <a name="see-also"></a>Consulte Também  
[Instalação do SSMA for Sybase Client &#40;SybaseToSQL&#41;](../../ssma/sybase/installing-ssma-for-sybase-client-sybasetosql.md)  
[Instalando os componentes do SSMA em SQL Server &#40;SybaseToSQL&#41;](../../ssma/sybase/installing-ssma-components-on-sql-server-sybasetosql.md)  
  
