---
title: Removendo os componentes do SSMA para MySQL (MySQLToSql) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Uninstalling, Extension pack
- Uninstalling, SSMA for MySQL client
ms.assetid: 87cdbd49-a0c9-4b00-8a93-34188b18d11a
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 3a5d6d1234cc294cc8e8cdd163ce8a9bd6ac3e3f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67929380"
---
# <a name="removing-the-ssma-for-mysql-components-mysqltosql"></a>Remover os componentes do SSMA para MySQL (MySQLToSql)
Quando terminar de migrar bancos de dados do MySQL para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]o, talvez você queira desinstalar os componentes do SSMA. Você pode desinstalar os componentes do cliente a qualquer momento. No entanto, se você desinstalar o pacote [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de extensões do, o SSMA não dará mais suporte à migração de dados do MySQL para o banco de dado de destino (SQL Server/SQL Azure) usando o mecanismo de migração de dados do lado do servidor.  
  
## <a name="uninstalling-the-ssma-for-mysql-client"></a>Desinstalando o cliente SSMA para MySQL  
Você pode desinstalar o SSMA usando **Adicionar ou remover programas**.  
  
**Para desinstalar o SSMA**  
  
1.  No Painel de Controle, abra **Adicionar ou Remover Programas**.  
  
2.  Selecione **Assistente de migração do Microsoft SQL Server para MySQL**e clique em **remover**.  
  
3.  Para confirmar que deseja desinstalar o SSMA, clique em **Sim**.  
  
## <a name="uninstalling-the-extension-pack"></a>Desinstalando o pacote de extensão  
Você pode remover o pacote de extensão usando **Adicionar ou remover programas**.  
  
**Para desinstalar o pacote de extensão**  
  
1.  No Painel de Controle, abra **Adicionar ou Remover Programas**.  
  
2.  Selecione **Assistente de migração do Microsoft SQL Server para o pacote de extensão MySQL**e clique em **remover**.  
  
3.  Para confirmar que deseja desinstalar o pacote de extensão, clique em **Sim**.  
  
4.  Na página instâncias com scripts de banco de dados de utilitários, selecione uma instância e clique em **Avançar**.  
  
5.  Na página parâmetros de conexão, selecione o método de autenticação e clique em **Avançar**.  
  
    A autenticação do Windows usará suas credenciais do Windows para tentar fazer logon na instância [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]do. Se você selecionar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticação, deverá inserir um nome [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de logon e uma senha.  
  
6.  Na página operação concluída, clique em **OK**.  
  
7.  Na página concluir, clique em **sair**.  
  
Após a conclusão do processo de desinstalação, você pode confirmar se os objetos no esquema **sysdb. ssma_MySQL** e, possivelmente, o banco de dados **sysdb** inteiro, foram removidos [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]usando o. No entanto, se você usar outros produtos do SSMA, eles também usarão o banco de dados **sysdb** . Se o banco de dados existir e você tiver certeza de que não há outros bancos de dados referenciados para os objetos nesse banco de dados, você poderá desanexar o banco.  
  
## <a name="see-also"></a>Consulte Também  
[Instalando o cliente SSMA para MySQL &#40;MySQLToSQL&#41;](../../ssma/mysql/installing-ssma-for-mysql-client-mysqltosql.md)  
[Instalar os componentes do SSMA no SQL Server](installing-ssma-components-on-sql-server-mysqltosql.md)  
  
