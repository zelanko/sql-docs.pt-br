---
title: Removendo o SSMA para componentes do MySQL (MySQLToSql) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Uninstalling, Extension pack
- Uninstalling, SSMA for MySQL client
ms.assetid: 87cdbd49-a0c9-4b00-8a93-34188b18d11a
caps.latest.revision: 10
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: db4762c702597b197aad75a8aee2b2987c11c581
ms.sourcegitcommit: 8aa151e3280eb6372bf95fab63ecbab9dd3f2e5e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/05/2018
ms.locfileid: "34776752"
---
# <a name="removing-the-ssma-for-mysql-components-mysqltosql"></a>Removendo o SSMA para componentes do MySQL (MySQLToSql)
Quando terminar de migrar bancos de dados do MySQL para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], talvez você queira desinstalar componentes do SSMA. Você pode desinstalar os componentes do cliente a qualquer momento. No entanto, se você desinstalar o pacote de extensão de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] , em seguida, SSMA não oferecerá suporte a migração de dados do MySQL para dados de destino (SQL Server/SQL Azure) usando o mecanismo de migração de dados do servidor.  
  
## <a name="uninstalling-the-ssma-for-mysql-client"></a>Desinstalando o SSMA para cliente do MySQL  
Você pode desinstalar o SSMA usando **adicionar ou remover programas**.  
  
**Para desinstalar o SSMA**  
  
1.  No painel de controle, abra **adicionar ou remover programas**.  
  
2.  Selecione **Microsoft SQL Server Migration Assistant para MySQL**e, em seguida, clique em **remover**.  
  
3.  Para confirmar que você deseja desinstalar o SSMA, clique em **Sim**.  
  
## <a name="uninstalling-the-extension-pack"></a>Desinstalar o pacote de extensão  
Você pode remover o pacote de extensão usando **adicionar ou remover programas**.  
  
**Para desinstalar o pacote de extensão**  
  
1.  No painel de controle, abra **adicionar ou remover programas**.  
  
2.  Selecione **Microsoft SQL Server Migration Assistant para o pacote de extensão do MySQL**e, em seguida, clique em **remover**.  
  
3.  Para confirmar que você deseja desinstalar o pacote de extensão, clique em **Sim**.  
  
4.  Em instâncias com página de utilitários Scripts de banco de dados, selecione uma instância e, em seguida, clique em **próximo**.  
  
5.  Na página de parâmetros de Conexão, selecione o método de autenticação e, em seguida, clique em **próximo**.  
  
    Autenticação do Windows usará as credenciais do Windows para tentar fazer logon instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Se você selecionar [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] autenticação, você deve inserir um [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] nome de logon e senha.  
  
6.  Na página concluir a operação, clique em **Okey**.  
  
7.  Na página conclusão, clique em **saída**.  
  
Depois que o processo de desinstalação for concluído, você pode confirmar que os objetos no **sysdb.ssma_MySQL** esquema e, possivelmente, todo o **sysdb** banco de dados, foi removido usando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)]. No entanto, se você usar outros produtos do SSMA, eles também usam o **sysdb** banco de dados. Se o banco de dados existe e você tiver certeza de que nenhum outro banco de dados fazem referência aos objetos nesse banco de dados, é possível desanexar o banco de dados.  
  
## <a name="see-also"></a>Consulte também  
[Instalando o SSMA para MySQL cliente &#40;MySQLToSQL&#41;](../../ssma/mysql/installing-ssma-for-mysql-client-mysqltosql.md)  
[Instalar os componentes do SSMA no SQL Server](http://msdn.microsoft.com/en-us/6772d0c5-258f-4d7b-afb0-b5f810e71af1)  
  
