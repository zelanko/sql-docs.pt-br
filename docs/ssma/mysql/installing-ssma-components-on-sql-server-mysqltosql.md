---
title: Instalando os componentes do SSMA em SQL Server (MySQLToSql) | Microsoft Docs
description: Instale os componentes no servidor que executa SQL Server para dar suporte à conversão de banco de dados MySQL com o SSMA, incluindo o pacote de extensão do SSMA e provedores de MySQL.
ms.prod: sql
ms.custom: ''
ms.date: 07/14/2020
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- SSMA extension pack, Installation
ms.assetid: 6772d0c5-258f-4d7b-afb0-b5f810e71af1
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 9b598915222610470bc9cf2e618cea65d725c5fb
ms.sourcegitcommit: fd7b268a34562d70d46441f689543ecce7df2e4d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/16/2020
ms.locfileid: "86411269"
---
# <a name="installing-ssma-components-on-sql-server-mysqltosql"></a>Instalando os componentes do SSMA em SQL Server (MySQLToSql)

Além de instalar o SSMA, você também deve instalar componentes no computador que está executando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Esses componentes incluem o pacote de extensão do SSMA, que dá suporte à migração de dados e provedores de MySQL para habilitar a conectividade de servidor para servidor.

## <a name="ssma-for-mysql-extension-pack"></a>Pacote de extensão do SSMA para MySQL

O pacote de extensão do SSMA adiciona um banco de dados, **sysdb**, à instância especificada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Esse banco de dados contém as tabelas e os procedimentos armazenados que são necessários para migrar os dados.

Além disso, quando você migra dados para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o, o SSMA cria [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] trabalhos do Agent quando o mecanismo de migração de dados do servidor é usado para migrar os dados.

### <a name="prerequisites"></a>Pré-requisitos

Antes de instalar os componentes do SSMA para servidor MySQL no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , verifique se o computador atende aos seguintes requisitos:

- [!INCLUDE[msCoName](../../includes/msconame_md.md)]Windows Installer 3,1 ou uma versão posterior.
- A [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort_md.md)] versão 4.7.2 ou posterior. Você pode obtê-lo no [centro de desenvolvedores .NET Framework](https://go.microsoft.com/fwlink/?LinkId=48882).
- O provedor do cliente MySQL e a conectividade com o banco de dados MySQL que você deseja migrar. Você pode instalar provedores da mídia de produto do MySQL ou do site MySQL.
- O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] serviço navegador deve estar em execução durante a instalação. Isso é usado para preencher uma lista das instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no assistente de instalação do. Você pode desabilitar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] serviço navegador após a instalação.  

  > [!NOTE]
  > Se o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] serviço navegador estiver em execução, mas você ainda não vir uma lista de instâncias na instalação, deverá desbloquear a porta UDP 1434. Você pode usar o Firewall do Windows para desbloquear temporariamente a porta ou pode desabilitar o Firewall do Windows temporariamente. Você também pode ter que desabilitar temporariamente o software antivírus. Certifique-se de habilitar firewalls e software antivírus após a instalação.

### <a name="installing-the-extension-pack"></a>Instalando o pacote de extensão

Você pode instalar o pacote de extensão a qualquer momento antes de migrar dados para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .

> [!IMPORTANT]
> Para instalar o pacote de extensão, você deve ser membro da função de servidor **sysadmin** na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .

Para instalar o pacote de extensão:

1. Copie o SSMA para **SSMAforMySQLExtensionPack_*n*. msi**, em que *n* é o número de Build, para o computador que está executando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .
2. Clique duas vezes em **SSMAforMySQLExtensionPack_*n*. msi**.
3. Na caixa de diálogo de **boas-vindas** , clique em **Avançar**.
4. Na caixa de diálogo **contrato de licença de usuário final** , leia o contrato de licença. Se você concordar, selecione a opção **aceito o contrato** e clique em **Avançar**.
5. Na caixa de diálogo **escolher tipo de instalação** , clique em **típico**.
6. Na caixa de diálogo **pronto para instalar** , clique em **instalar**.
7. Na caixa de diálogo **concluir a primeira etapa da instalação** , clique em **Avançar**.

   Uma nova caixa de diálogo será exibida, na qual você seleciona a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para a instalação do pacote de extensão.
  
8. Selecione a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] onde você migrará os esquemas do MySQL e clique em **Avançar**.
  
   A instância padrão tem o mesmo nome que o computador. As instâncias nomeadas serão seguidas por uma barra invertida e o nome da instância.

9. Na página conexão, selecione o método de autenticação e clique em **Avançar**.
  
    A autenticação do Windows usará suas credenciais do Windows para tentar fazer logon na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Se você selecionar autenticação de servidor, deverá inserir um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nome de logon e uma senha.

10. A próxima etapa exige que você defina a senha para uma chave mestra que será usada para criptografar os dados confidenciais armazenados no banco de dados do pacote de extensão durante a migração de dado do lado do servidor. Forneça uma senha forte e clique em **Avançar**.

11. Na próxima caixa de diálogo, selecione **instalar utilitários banco de dados *n* e instalar bibliotecas de pacotes de extensão**, em que *n* é o número de versão e clique em **Avançar**.

    O banco de dados **sysdb** é criado com as tabelas e os procedimentos armazenados necessários para a migração de data (o uso do mecanismo de migração de dados do lado do servidor) são criados nesse banco.

12. Para instalar os utilitários em outra instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , selecione **Sim**e clique em **Avançar**. Ou, para sair do assistente, clique em **não**.

## <a name="see-also"></a>Confira também

- [Instalando SSMA para cliente do MySQL](../../ssma/mysql/installing-ssma-for-mysql-client-mysqltosql.md)
- [Migrando bancos de dados MySQL para SQL Server-BD SQL do Azure](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)
