---
title: Removendo o SSMA para componentes do Oracle (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-oracle
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology:
- sql-ssma
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Uninstalling the Extension Pack
ms.assetid: 8b527a56-4e52-487a-9ac9-2320388e6d7d
caps.latest.revision: 6
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.workload: Inactive
ms.openlocfilehash: f55d809746dc5782a8d591cd6e85322394035cb2
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
---
# <a name="removing-ssma--for-oracle-components-oracletosql"></a>Removendo o SSMA para componentes do Oracle (OracleToSQL)
Quando terminar de migrar bancos de dados do Oracle para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], talvez você queira desinstalar componentes do SSMA. Você pode desinstalar os componentes do cliente a qualquer momento. No entanto, você deve desinstalar o pacote de extensão de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] , a menos que seus bancos de dados migrados não usam funções no **ssma_oracle** esquema do **sysdb** banco de dados.  
  
## <a name="uninstalling-the-ssma-for-oracle-client"></a>Desinstalando o SSMA para cliente Oracle  
Você pode desinstalar o SSMA usando **adicionar ou remover programas**.  
  
**Para desinstalar o SSMA**  
  
1.  No painel de controle, abra **adicionar ou remover programas**.  
  
2.  Selecione  **[!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o Assistente de migração para Oracle**e, em seguida, clique em **remover**.  
  
3.  Para confirmar que você deseja desinstalar o SSMA, clique em **Sim**.  
  
## <a name="uninstalling-the-extension-pack"></a>Desinstalar o pacote de extensão  
Se você tiver certeza de seus bancos de dados migrados não usam objetos de **sysdb.ssma_oracle** esquema, você pode remover o pacote de extensão usando **adicionar ou remover programas**.  
  
**Para desinstalar o pacote de extensão**  
  
1.  No painel de controle, abra **adicionar ou remover programas**.  
  
2.  Selecione **Microsoft SQL Server Migration Assistant para o pacote de extensão do Oracle**e, em seguida, clique em **remover**.  
  
3.  Para confirmar que você deseja desinstalar o pacote de extensão, clique em **Sim**.  
  
4.  Em instâncias com página de utilitários Scripts de banco de dados, selecione uma instância e, em seguida, clique em **próximo**.  
  
5.  Na página de parâmetros de Conexão, selecione o método de autenticação e, em seguida, clique em **próximo**.  
  
    Autenticação do Windows usará as credenciais do Windows para tentar fazer logon instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Se você selecionar [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] autenticação, você deve inserir um [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] nome de logon e senha.  
  
6.  Na página concluir a operação, clique em **Okey**.  
  
7.  Na página conclusão, clique em **saída**.  
  
Após a desinstalação, você pode confirmar que os objetos no **sysdb.ssma_oracle** esquema e, possivelmente, todo o **sysdb** banco de dados, foi removido usando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)]. No entanto, se você usar outros produtos do SSMA, eles também usam o **sysdb** banco de dados. Se o banco de dados existe e você tiver certeza de que nenhum outro banco de dados fazem referência a objetos no banco de dados, é possível desanexar o banco de dados.  
  
## <a name="see-also"></a>Consulte também  
[Instalando o SSMA para cliente Oracle &#40;OracleToSQL&#41;](../../ssma/oracle/installing-ssma-for-oracle-client-oracletosql.md)  
[Instalando componentes do SSMA no SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/installing-ssma-components-on-sql-server-oracletosql.md)  
  
