---
title: Instalando componentes do SSMA no SQL Server (OracleToSQL) | Microsoft Docs
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
- Installign the Extension Pack
- SQL Server Database Objects
ms.assetid: 33070e5f-4e39-4b70-ae81-b8af6e4983c5
caps.latest.revision: 7
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.workload: Inactive
ms.openlocfilehash: 9dc0fbc22cedb1c7aa7d4ac3bd342c6acb91ba88
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
---
# <a name="installing-ssma-components-on-sql-server-oracletosql"></a>Instalar os componentes do SSMA no SQL Server (OracleToSQL)
Além de instalar o SSMA, você também deve instalar componentes no computador que está executando [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Esses componentes incluem o pacote de extensão do SSMA, que dá suporte à migração de dados e provedores da Oracle para habilitar a conectividade de servidor para servidor.  
  
## <a name="ssma-for-oracle-extension-pack"></a>SSMA para o pacote de extensão do Oracle  
O pacote de extensão do SSMA adiciona os bancos de dados, **sysdb** e **ssmatesterdb**, a instância especificada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. O banco de dados **sysdb** contém as tabelas e procedimentos armazenados que são necessárias para migrar dados e as funções definidas pelo usuário que emulam funções do sistema Oracle. O **ssmatesterdb** banco de dados contém tabelas e procedimentos necessários para o componente Tester.  
  
Além disso, quando você migra dados para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], cria o SSMA [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] trabalhos de agente quando o mecanismo de migração de dados do lado servidor é usado para migrar os dados.  
  
### <a name="prerequisites"></a>Prerequisites  
Antes de instalar o SSMA para componentes de servidor Oracle em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], certifique-se de que o sistema atende aos seguintes requisitos:  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] instância está instalada. O SSMA não oferece suporte para o SQL Server 2008 Express Edition.  
  
-   [!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows Installer 3.1 ou posterior.  
  
-   O provedor de cliente Oracle ou o provedor OLE DB para Oracle e conectividade com o banco de dados Oracle que você deseja migrar. Você pode instalar provedores da mídia do produto Oracle ou site da Oracle.  
  
-   O [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] serviço de navegador deve ser executado durante a instalação. Isso é usado para preencher uma lista das instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] no Assistente de instalação. Você pode desabilitar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] serviço de navegador após a instalação.  
  
    > [!NOTE]  
    > Se o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] navegador estiver em execução, mas você ainda não vir uma lista de instâncias na instalação, você deve desbloquear a porta UDP 1434. Você pode usar o Firewall do Windows para desbloquear temporariamente a porta, ou você pode desativar temporariamente o Firewall do Windows. Você também terá que desabilitar temporariamente o software antivírus. Certifique-se de habilitar o software antivírus e firewalls depois da instalação.  
  
### <a name="installing-the-extension-pack"></a>Instalando o pacote de extensão  
Você pode instalar o pacote de extensão a qualquer momento antes de migrar dados para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
> [!IMPORTANT]  
> Para instalar o pacote de extensão, você deve ser um membro do **sysadmin** a função de servidor na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
**Para instalar o pacote de extensão**  
  
1.  Se você ainda não fez isso, extraia todos os arquivos do arquivo Zip do SSMA.  
  
    Dependendo da versão do WinZip tiver, você poderá duas vezes no arquivo, ou clique no arquivo e selecione **extrair tudo** ou **abrir no WinZip**. Siga as instruções na interface do usuário WinZip para extrair os arquivos.  
  
2.  Copie o SSMA para o pacote de extensão do Oracle. *n*. Install.exe, onde *n* é o número de compilação para o computador que está executando [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
3.  Clique duas vezes o SSMA para o pacote de extensão do Oracle. *n*. Install.exe.  
  
4.  Na página de boas-vinda, clique em **próximo**.  
  
5.  Na página Contrato de licença de usuário final, leia o contrato de licença. Se você concordar, selecione o **aceito os termos do contrato de licença** caixa de seleção e, em seguida, clique em **próximo**.  
  
6.  Na página Escolha o tipo de instalação, clique em **típica**.  
  
7.  Na página pronto para instalar, clique em **instalar**.  
  
8.  Sobre a página a primeira etapa de instalação concluída, clique em **próximo**.  
  
    Uma nova caixa de diálogo será exibida, em que você selecionar a instância de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] para a instalação do pacote de extensão.  
  
9. Selecione a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] onde você será migrar esquemas Oracle e, em seguida, clique em **próximo**.  
  
    A instância padrão tem o mesmo nome que o computador. Instâncias nomeadas serão seguidas por uma barra invertida e o nome da instância.  
  
10. Na página de conexão, selecione o método de autenticação e, em seguida, clique em **próximo**.  
  
    Autenticação do Windows usará as credenciais do Windows para tentar fazer logon instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Se você selecionar [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] autenticação, você deve inserir um [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] nome de logon e senha.  
  
11. Na página seguinte, selecione **instalar utilitários de banco de dados** *n*, onde *n* é o número de versão e, em seguida, clique em **próximo**.  
  
    O **sysdb** banco de dados é criado e as funções definidas pelo usuário e procedimentos armazenados são criados no banco de dados.  
  
    Se **instalar o banco de dados Tester** opção estiver marcada o testador **ssmatesterdb** banco de dados será criado.  
  
12. Para instalar os utilitários para outra instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], selecione **Sim**e, em seguida, clique em **próximo**. Ou, para sair do assistente, clique em **não**.  
  
13. Em [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] ou usando o utilitário sqlcmd, execute o script a seguir para habilitar o CLR:  
  
    ```  
    sp_configure 'clr enabled', 1  
    GO  
    RECONFIGURE  
    GO  
    ```  
    Se o CLR não está habilitado, você receberá o seguinte erro quando o SSMA se conecta ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]:  
  
    O SSMA não foi possível recuperar as informações de versão de assembly de pacote de extensão. Reinstale o pacote de extensão no servidor de banco de dados.  
  
### <a name="sql-server-database-objects"></a>Objetos de banco de dados do SQL Server  
Depois de instalar o pacote de extensão, você será um, consulte um **ssma_oracle.bcp_migration_packages** tabela, uma **ssma_oracle.db_storage** tabela e um **ssma_oracle.db_error_list** tabela o **sysdb** banco de dados. Você também verá muitos procedimentos armazenados e funções definidas pelo usuário no **ssma_oracle** esquema.  
  
Toda vez que você migra dados para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], SSMA cria um [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] trabalho do agente. Esses trabalhos são nomeados **ssma_oracle pacote de migração de dados {GUID}** e são visíveis no [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] nó do agente de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] na pasta Jobs.  
  
## <a name="see-also"></a>Consulte também  
[Instalando o SSMA para cliente Oracle &#40;OracleToSQL&#41;](../../ssma/oracle/installing-ssma-for-oracle-client-oracletosql.md)  
[Bancos de dados Oracle migrando para o SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)  
  
