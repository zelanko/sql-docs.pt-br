---
title: Instalando os componentes do SSMA em SQL Server (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 10/01/2019
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Installign the Extension Pack
- SQL Server Database Objects
ms.assetid: 33070e5f-4e39-4b70-ae81-b8af6e4983c5
author: Shamikg
ms.author: Shamikg
manager: shamikg
ms.openlocfilehash: 1f0cea859e9465eebefebc061ee51107dc7844aa
ms.sourcegitcommit: fd3e81c55745da5497858abccf8e1f26e3a7ea7d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2019
ms.locfileid: "71713308"
---
# <a name="installing-ssma-components-on-sql-server-oracletosql"></a>Instalando os componentes do SSMA em SQL Server (OracleToSQL)

Além de instalar o SSMA, você também deve instalar componentes no computador que está executando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Esses componentes incluem o pacote de extensão do SSMA, que dá suporte à migração de dados e aos provedores Oracle para habilitar a conectividade de servidor para servidor.  
  
## <a name="ssma-for-oracle-extension-pack"></a>Pacote de extensão do SSMA para Oracle

O pacote de extensão do SSMA adiciona os bancos de dados **sysdb** e **ssmatesterdb** à instância especificada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O banco de dados **sysdb** contém as tabelas e os procedimentos armazenados necessários para migrar dados e as funções definidas pelo usuário que emulam funções do sistema Oracle. O banco de dados **ssmatesterdb** contém as tabelas e os procedimentos exigidos pelo componente testador.  
  
Além disso, quando você migra dados para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o SSMA cria trabalhos de agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] quando o mecanismo de migração de dados do servidor é usado para migrar os dados.  
  
### <a name="prerequisites"></a>Pré-requisitos

Antes de instalar os componentes de servidor do SSMA para Oracle no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], verifique se o sistema atende aos seguintes requisitos:  
  
- a instância [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está instalada. O SSMA não dá suporte ao SQL Server 2008 Express Edition.
  
- [!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows Installer 3,1 ou uma versão posterior.  
  
- O provedor de cliente Oracle ou o provedor de OLE DB para Oracle e a conectividade com o banco de dados Oracle que você deseja migrar. Você pode instalar provedores da mídia de produto Oracle ou do site da Oracle.  
  
- O serviço navegador [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve estar em execução durante a instalação. Isso é usado para popular uma lista das instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no assistente de instalação. Você pode desabilitar o serviço de navegador [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] após a instalação.  
  
    > [!NOTE]  
    > Se o serviço navegador [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] estiver em execução, mas você ainda não vir uma lista de instâncias na instalação, deverá desbloquear a porta UDP 1434. Você pode usar o Firewall do Windows para desbloquear temporariamente a porta ou pode desabilitar o Firewall do Windows temporariamente. Você também pode ter que desabilitar temporariamente o software antivírus. Certifique-se de habilitar firewalls e software antivírus após a instalação.  
  
### <a name="installing-the-extension-pack"></a>Instalando o pacote de extensão

Você pode instalar o pacote de extensão a qualquer momento antes de migrar dados para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!IMPORTANT]  
> Para instalar o pacote de extensão, você deve ser membro da função de servidor **sysadmin** na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
**Para instalar o pacote de extensão**
  
1. Se você ainda não fez isso, Extraia todos os arquivos do arquivo zip do SSMA.  
  
    Dependendo da versão do WinZip que você tem, você pode clicar duas vezes no arquivo ou clicar com o botão direito do mouse no arquivo e, em seguida, selecionar **extrair tudo** ou **abrir no WinZip**. Siga as instruções na interface do usuário do WinZip para extrair os arquivos.  
  
2. Copie o **pacote de extensão do SSMA para Oracle. *n*. Install. exe** (em que *n* é o número da compilação) no computador que está executando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
3. Clique duas vezes em **pacote de extensão do SSMA para Oracle. *n*. Install. exe**.  
  
4. Na página de **boas-vindas** , selecione **Avançar**.  
  
5. Na página **contrato de licença de usuário final** , leia o contrato de licença. Se você concordar, marque a caixa de seleção **eu aceito os termos do contrato de licença** e, em seguida, selecione **Avançar**.  
  
6. Na página **escolher tipo de instalação** , selecione **típica**.  
  
7. Na página **Pronto para Instalar** , selecione **Instalar**.  
  
8. Na página **concluir a primeira etapa da instalação** , selecione **Avançar**.  
  
    Uma nova caixa de diálogo será exibida, na qual você seleciona a instância de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para a instalação do pacote de extensão.  
  
9. Selecione a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para a qual você migrará os esquemas Oracle e, em seguida, selecione **Avançar**.  
  
    A instância padrão tem o mesmo nome que o computador. As instâncias nomeadas serão seguidas por uma barra invertida e o nome da instância.  
  
10. Na página conexão, selecione o método de autenticação e, em seguida, selecione **Avançar**.  
  
    A autenticação do Windows usará suas credenciais do Windows para tentar entrar na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se você selecionar a autenticação [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], deverá inserir um nome de logon e uma senha do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
11. Na página seguinte, selecione **instalar utilitários banco de dados** *n*, em que *n* é o número de versão e, em seguida, selecione **Avançar**.  
  
    O banco de dados **sysdb** é criado e as funções definidas pelo usuário e os procedimentos armazenados são criados nesse banco de dados.  
  
    Se a opção **instalar banco de dados do Tester** estiver marcada, o banco de dados **ssmatesterdb** do testador será criado.  
  
12. Para instalar os utilitários em outra instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], selecione **Sim**e, em seguida, selecione **Avançar**, ou para sair do assistente, selecione **não**.  
  
13. Em [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou usando o utilitário sqlcmd, execute o seguinte script para habilitar o CLR:  
  
    ```
    sp_configure 'clr enabled', 1  
    GO  
    RECONFIGURE  
    GO  
    ```

    Se o CLR não estiver habilitado, você receberá o seguinte erro quando o SSMA se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
    O SSMA não pôde recuperar as informações de versão do assembly do pacote de extensão. Reinstale o pacote de extensão no servidor de banco de dados.  
  
### <a name="sql-server-database-objects"></a>SQL Server objetos de banco de dados  

Depois de instalar o pacote de extensão, uma tabela **_migration_packages ssma_oracle. bcp** aparece no banco de dados **sysdb** .

Sempre que você migra dados para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o SSMA cria um trabalho de agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Esses trabalhos são chamados de **pacote de migração de dados ssma_oracle {GUID}** e são visíveis no nó de agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] na pasta trabalhos.  
  
## <a name="see-also"></a>Confira também

[Instalando o SSMA para &#40;Oracle Client OracleToSQL&#41;](../../ssma/oracle/installing-ssma-for-oracle-client-oracletosql.md)  
[Migrando bancos de dados Oracle para &#40;SQL Server OracleToSQL&#41;](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)  
