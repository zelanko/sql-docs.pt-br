---
title: Remover o SSMA para componentes do Oracle (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Uninstalling the Extension Pack
ms.assetid: 8b527a56-4e52-487a-9ac9-2320388e6d7d
caps.latest.revision: 6
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: a301770224db68e0f812650ce87c15a3f2e5f7bf
ms.sourcegitcommit: 603d2e588ac7b36060fa0cc9c8621ff2a6c0fcc7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/14/2018
ms.locfileid: "40396208"
---
# <a name="removing-ssma--for-oracle-components-oracletosql"></a>Remover componentes do SSMA para Oracle (OracleToSQL)
Quando você terminar de migrar bancos de dados do Oracle para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], talvez você queira desinstalar os componentes do SSMA. Você pode desinstalar os componentes do cliente a qualquer momento. No entanto, você não deve desinstalar o pacote de extensão de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , a menos que seus bancos de dados migrados não usam funções na **ssma_oracle** esquema dos **sysdb** banco de dados.  
  
## <a name="uninstalling-the-ssma-for-oracle-client"></a>Desinstalando o SSMA para cliente Oracle  
Você pode desinstalar o SSMA usando **adicionar ou remover programas**.  
  
**Para desinstalar o SSMA**  
  
1.  No painel de controle, abra **adicionar ou remover programas**.  
  
2.  Selecione  **[!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Assistente de migração para o Oracle**e, em seguida, clique em **remover**.  
  
3.  Para confirmar que você deseja desinstalar o SSMA, clique em **Sim**.  
  
## <a name="uninstalling-the-extension-pack"></a>Desinstalando o pacote de extensão  
Se você tiver certeza seus bancos de dados migrados não usam objetos na **sysdb.ssma_oracle** esquema, você pode remover o pacote de extensão usando **adicionar ou remover programas**.  
  
**Para desinstalar o pacote de extensão**  
  
1.  No painel de controle, abra **adicionar ou remover programas**.  
  
2.  Selecione **Microsoft SQL Server Migration Assistant para o pacote de extensão do Oracle**e, em seguida, clique em **remover**.  
  
3.  Para confirmar que você deseja desinstalar o pacote de extensão, clique em **Sim**.  
  
4.  Nas instâncias com página de Scripts de banco de dados de utilitários, selecione uma instância e, em seguida, clique em **próxima**.  
  
5.  Na página de parâmetros de Conexão, selecione o método de autenticação e, em seguida, clique em **próxima**.  
  
    Autenticação do Windows usarão suas credenciais do Windows para tentar fazer logon na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se você selecionar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticação, você deve inserir um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nome de logon e senha.  
  
6.  Na página de operação concluída, clique em **Okey**.  
  
7.  Na página concluir, clique em **Exit**.  
  
Após a desinstalação, você pode confirmar que os objetos na **sysdb.ssma_oracle** esquema e, possivelmente, todo **sysdb** banco de dados, foi removido usando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. No entanto, se você usar outros produtos do SSMA, eles também usam o **sysdb** banco de dados. Se o banco de dados existe e tem certeza de que nenhum outro banco de dados fazem referência a objetos neste banco de dados, é possível desanexar o banco de dados.  
  
## <a name="see-also"></a>Consulte também  
[Instalar o SSMA para cliente Oracle &#40;OracleToSQL&#41;](../../ssma/oracle/installing-ssma-for-oracle-client-oracletosql.md)  
[Instalar os componentes do SSMA no SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/installing-ssma-components-on-sql-server-oracletosql.md)  
  
