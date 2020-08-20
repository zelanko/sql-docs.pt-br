---
description: Remover componentes do SSMA para Oracle (OracleToSQL)
title: Removendo o SSMA for Oracle Components (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Uninstalling the Extension Pack
ms.assetid: 8b527a56-4e52-487a-9ac9-2320388e6d7d
author: nahk-ivanov
ms.author: alexiva
manager: alexiva
ms.openlocfilehash: 263d04b401146ce2975a810b084e4957f1daf718
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88492376"
---
# <a name="removing-ssma--for-oracle-components-oracletosql"></a>Remover componentes do SSMA para Oracle (OracleToSQL)
Quando terminar de migrar bancos de dados do Oracle para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , talvez você queira desinstalar os componentes do SSMA. Você pode desinstalar os componentes do cliente a qualquer momento. No entanto, você não deve desinstalar o pacote de extensão de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , a menos que os bancos de dados migrados não usem mais funções no esquema de **ssma_oracle** do **sysdb** .  
  
## <a name="uninstalling-the-ssma-for-oracle-client"></a>Desinstalando o cliente SSMA para Oracle  
Você pode desinstalar o SSMA usando **Adicionar ou remover programas**.  
  
**Para desinstalar o SSMA**  
  
1.  No Painel de Controle, abra **Adicionar ou Remover Programas**.  
  
2.  Selecione ** [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Assistente de migração para Oracle**e clique em **remover**.  
  
3.  Para confirmar que deseja desinstalar o SSMA, clique em **Sim**.  
  
## <a name="uninstalling-the-extension-pack"></a>Desinstalando o pacote de extensão  
Se você tiver certeza de que os bancos de dados migrados não usam objetos no esquema **sysdb. ssma_oracle** , você poderá remover o pacote de extensão usando **Adicionar ou remover programas**.  
  
**Para desinstalar o pacote de extensão**  
  
1.  No Painel de Controle, abra **Adicionar ou Remover Programas**.  
  
2.  Selecione **Assistente de migração do Microsoft SQL Server para o pacote de extensão Oracle**e clique em **remover**.  
  
3.  Para confirmar que deseja desinstalar o pacote de extensão, clique em **Sim**.  
  
4.  Na página instâncias com scripts de banco de dados de utilitários, selecione uma instância e clique em **Avançar**.  
  
5.  Na página parâmetros de conexão, selecione o método de autenticação e clique em **Avançar**.  
  
    A autenticação do Windows usará suas credenciais do Windows para tentar fazer logon na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Se você selecionar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticação, deverá inserir um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nome de logon e uma senha.  
  
6.  Na página operação concluída, clique em **OK**.  
  
7.  Na página concluir, clique em **sair**.  
  
Após a desinstalação, você pode confirmar se os objetos no esquema **sysdb. ssma_oracle** e, possivelmente, o banco de dados **sysdb** inteiro, foram removidos usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] . No entanto, se você usar outros produtos do SSMA, eles também usarão o banco de dados **sysdb** . Se o banco de dados existir e você tiver certeza de que não há outros bancos de dados de referência a objetos nesse banco, você poderá desanexar o banco de dados.  
  
## <a name="see-also"></a>Consulte Também  
[Instalação do SSMA para Oracle Client &#40;OracleToSQL&#41;](../../ssma/oracle/installing-ssma-for-oracle-client-oracletosql.md)  
[Instalando os componentes do SSMA em SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/installing-ssma-components-on-sql-server-oracletosql.md)  
  
