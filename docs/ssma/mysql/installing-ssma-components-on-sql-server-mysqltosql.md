---
title: Instalando componentes do SSMA no SQL Server (MySQLToSql) | Microsoft Docs
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- SSMA extension pack, Installation
ms.assetid: 6772d0c5-258f-4d7b-afb0-b5f810e71af1
caps.latest.revision: 9
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 9544fb62402871b9a93284df88e0082f62fec582
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="installing-ssma-components-on-sql-server-mysqltosql"></a>Instalar os componentes do SSMA no SQL Server (MySQLToSql)
Além de instalar o SSMA, você também deve instalar componentes no computador que está executando [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Esses componentes incluem o pacote de extensão do SSMA, que dá suporte à migração de dados e provedores do MySQL para habilitar a conectividade de servidor para servidor.  
  
## <a name="ssma-for-mysql-extension-pack"></a>SSMA para o pacote de extensão do MySQL  
O pacote de extensão do SSMA adiciona um banco de dados, **sysdb**, a instância especificada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Este banco de dados contém tabelas e procedimentos armazenados que são necessárias para migrar os dados.  
  
Além disso, quando você migra dados para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], cria o SSMA [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] trabalhos do Agent, quando o mecanismo de migração de dados do lado servidor é usado para migrar os dados.  
  
### <a name="prerequisites"></a>Pré-requisitos  
Antes de instalar o SSMA para componentes do servidor MySQL em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], certifique-se de que o computador atende aos seguintes requisitos:  
  
-   [!INCLUDE[msCoName](../../includes/msconame_md.md)]Windows Installer 3.1 ou posterior.  
  
-   O provedor de cliente do MySQL e conectividade com o banco de dados MySQL que você deseja migrar. Você pode instalar provedores da mídia de produto do MySQL ou site do MySQL.  
  
-   O [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] serviço de navegador deve ser executado durante a instalação. Isso é usado para preencher uma lista das instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] no Assistente de instalação. Você pode desabilitar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] serviço de navegador após a instalação.  
  
    > [!NOTE]  
    > Se o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] navegador estiver em execução, mas você ainda não vir uma lista de instâncias na instalação, você deve desbloquear a porta UDP 1434. Você pode usar o Firewall do Windows para desbloquear temporariamente a porta, ou você pode desativar temporariamente o Firewall do Windows. Você também terá que desabilitar temporariamente o software antivírus. Certifique-se de habilitar o software antivírus e firewalls depois da instalação.  
  
### <a name="installing-the-extension-pack"></a>Instalando o pacote de extensão  
Você pode instalar o pacote de extensão a qualquer momento antes de migrar dados para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
> [!IMPORTANT]  
> Para instalar o pacote de extensão, você deve ser um membro do **sysadmin** a função de servidor na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
**Para instalar o pacote de extensão**  
  
1.  Copie o SSMA para o pacote de extensão do MySQL. *n*. Install.exe, onde  *n*  é o número de compilação para o computador que está executando [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
2.  Clique duas vezes o SSMA para o pacote de extensão do MySQL. *n*. Install.exe.  
  
3.  Na caixa de diálogo de boas-vindas, clique em **próximo**.  
  
4.  Na caixa de diálogo Contrato de licença de usuário final, leia o contrato de licença. Se você concordar, selecione o **aceito os termos do contrato de licença** caixa de seleção e, em seguida, clique em **próximo**.  
  
5.  Na caixa de diálogo Escolher tipo de instalação, clique em **típica**.  
  
6.  Em pronto para a caixa de diálogo de instalação, clique em **instalar**.  
  
7.  Sobre a caixa de diálogo da primeira etapa de instalação concluída, clique em **próximo**.  
  
    Uma nova caixa de diálogo será exibida, em que você selecionar a instância de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] para a instalação do pacote de extensão.  
  
8.  Selecione a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] onde você será migrar esquemas do MySQL e, em seguida, clique em **próximo**.  
  
    A instância padrão tem o mesmo nome que o computador. Instâncias nomeadas serão seguidas por uma barra invertida e o nome da instância.  
  
9. Na caixa de diálogo de conexão, selecione o método de autenticação e, em seguida, clique em **próximo**.  
  
    Autenticação do Windows usará as credenciais do Windows para tentar fazer logon instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Se você selecionar [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] autenticação, você deve inserir um [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] nome de logon e senha.  
  
10. Na próxima caixa de diálogo, selecione **instalar utilitários de banco de dados**  *n* , onde  *n*  é o número de versão e, em seguida, clique em **próximo**.  
  
    O **sysdb** banco de dados é criado com as tabelas e procedimentos armazenados necessários para a migração de dados (usando o mecanismo de migração de dados do lado servidor) são criados no banco de dados.  
  
11. Para instalar os utilitários para outra instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], selecione **Sim**e, em seguida, clique em **próximo**. Ou, para sair do assistente, clique em **não**.  
  
## <a name="see-also"></a>Consulte também  
[Instalando o SSMA para MySQL cliente &#40; MySQLToSQL &#41;](../../ssma/mysql/installing-ssma-for-mysql-client-mysqltosql.md)  
[Migrando bancos de dados MySQL para o SQL Server - banco de dados SQL do Azure &#40; MySQLToSql &#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
  

