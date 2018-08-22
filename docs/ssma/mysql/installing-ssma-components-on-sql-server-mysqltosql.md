---
title: Instalar os componentes do SSMA no SQL Server (MySQLToSql) | Microsoft Docs
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
- SSMA extension pack, Installation
ms.assetid: 6772d0c5-258f-4d7b-afb0-b5f810e71af1
caps.latest.revision: 9
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 5a5e64aca2b46e60a1fda93a9bde2f5b62c981fa
ms.sourcegitcommit: 603d2e588ac7b36060fa0cc9c8621ff2a6c0fcc7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/14/2018
ms.locfileid: "40395404"
---
# <a name="installing-ssma-components-on-sql-server-mysqltosql"></a>Instalar os componentes do SSMA no SQL Server (MySQLToSql)
Além de instalar o SSMA, você também deve instalar componentes no computador que está executando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Esses componentes incluem o pacote de extensão do SSMA, que dá suporte à migração de dados e provedores do MySQL para habilitar a conectividade de servidor para servidor.  
  
## <a name="ssma-for-mysql-extension-pack"></a>SSMA para o pacote de extensão do MySQL  
O pacote de extensão do SSMA adiciona um banco de dados **sysdb**, para a instância especificada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Este banco de dados contém as tabelas e procedimentos armazenados que são necessárias para migrar dados.  
  
Além disso, quando você migra dados a serem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o SSMA cria [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] trabalhos do Agent, quando o mecanismo de migração de dados do lado servidor é usado para migrar os dados.  
  
### <a name="prerequisites"></a>Prerequisites  
Antes de instalar o SSMA para componentes do servidor MySQL em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], certifique-se de que o computador atende aos seguintes requisitos:  
  
-   [!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows Installer 3.1 ou posterior.  
  
-   O provedor de cliente do MySQL e conectividade ao banco de dados MySQL que você deseja migrar. Você pode instalar provedores da mídia de produto do MySQL ou o site do MySQL.  
  
-   O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] serviço do navegador deve ser executado durante a instalação. Isso é usado para preencher uma lista das instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no Assistente de instalação. Você pode desabilitar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] serviço navegador após a instalação.  
  
    > [!NOTE]  
    > Se o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] navegador estiver em execução, mas você ainda não vir uma lista de instâncias na instalação, você deve desbloquear a porta UDP 1434. Você pode usar o Firewall do Windows para desbloquear temporariamente a porta, ou você pode desativar temporariamente o Firewall do Windows. Você também terá que desabilitar temporariamente o software antivírus. Certifique-se de habilitar o software antivírus e firewalls depois da instalação.  
  
### <a name="installing-the-extension-pack"></a>Instalar o pacote de extensão  
Você pode instalar o pacote de extensão a qualquer momento antes de migrar dados para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!IMPORTANT]  
> Para instalar o pacote de extensão, você deve ser um membro do **sysadmin** função de servidor na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
**Para instalar o pacote de extensão**  
  
1.  Copie o SSMA para o pacote de extensão do MySQL. *n*. Install.exe, onde *n* é o número de compilação, no computador que está executando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
2.  Clique duas vezes no SSMA para o pacote de extensão do MySQL. *n*. Install.exe.  
  
3.  Na caixa de diálogo de boas-vindas, clique em **próxima**.  
  
4.  Na caixa de diálogo de contrato de licença de usuário final, leia o contrato de licença. Se você concordar, selecione a **aceito os termos do contrato de licença** caixa de seleção e, em seguida, clique em **próxima**.  
  
5.  Na caixa de diálogo Escolher tipo de instalação, clique em **típica**.  
  
6.  Em pronto para a caixa de diálogo de instalação, clique em **instalar**.  
  
7.  Sobre o caixa de diálogo primeira etapa de instalação concluído, clique em **próxima**.  
  
    Uma nova caixa de diálogo será exibida, em que você selecione a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para a instalação do pacote de extensão.  
  
8.  Selecione a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] onde você irá ser migrando MySQL esquemas e, em seguida, clique em **próxima**.  
  
    A instância padrão tem o mesmo nome que o computador. Instâncias nomeadas serão seguidas por uma barra invertida e o nome da instância.  
  
9. Na caixa de diálogo de conexão, selecione o método de autenticação e, em seguida, clique em **próxima**.  
  
    Autenticação do Windows usarão suas credenciais do Windows para tentar fazer logon na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se você selecionar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticação, você deve inserir um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nome de logon e senha.  
  
10. Na próxima caixa de diálogo, selecione **instalar utilitários de banco de dados** *n*, onde *n* é o número de versão e, em seguida, clique em **Avançar**.  
  
    O **sysdb** banco de dados é criado com as tabelas e procedimentos armazenados necessários para a migração de dados (usando o mecanismo de migração de dados do lado servidor) são criados no banco de dados.  
  
11. Para instalar os utilitários para outra instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], selecione **Yes**e, em seguida, clique em **próximo**. Ou, para sair do assistente, clique em **não**.  
  
## <a name="see-also"></a>Consulte também  
[Instalar o SSMA para cliente do MySQL &#40;MySQLToSQL&#41;](../../ssma/mysql/installing-ssma-for-mysql-client-mysqltosql.md)  
[Migrando MySQL bancos de dados para o SQL Server – BD SQL do Azure &#40;MySQLToSql&#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
  
