---
title: Instalar os componentes do SSMA no SQL Server (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Installign the Extension Pack
- SQL Server Database Objects
ms.assetid: 33070e5f-4e39-4b70-ae81-b8af6e4983c5
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: 2041901a851ca755b1079535ccbf763472ec7bc4
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47853354"
---
# <a name="installing-ssma-components-on-sql-server-oracletosql"></a>Instalar os componentes do SSMA no SQL Server (OracleToSQL)
Além de instalar o SSMA, você também deve instalar componentes no computador que está executando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Esses componentes incluem o pacote de extensão do SSMA, que dá suporte à migração de dados e provedores da Oracle para habilitar a conectividade de servidor para servidor.  
  
## <a name="ssma-for-oracle-extension-pack"></a>SSMA para o pacote de extensão do Oracle  
O pacote de extensão do SSMA adiciona os bancos de dados **sysdb** e **ssmatesterdb**, para a instância especificada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O banco de dados **sysdb** contém as tabelas e procedimentos armazenados que são necessárias para migrar dados e as funções definidas pelo usuário que emulam funções do sistema Oracle. O **ssmatesterdb** banco de dados contém as tabelas e procedimentos necessários para o componente de testador.  
  
Além disso, quando você migra dados a serem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o SSMA cria [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] trabalhos do agente quando o mecanismo de migração de dados do lado servidor é usado para migrar os dados.  
  
### <a name="prerequisites"></a>Prerequisites  
Antes de instalar o SSMA para componentes do servidor Oracle em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], certifique-se de que o sistema atende aos seguintes requisitos:  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instância está instalada. O SSMA não oferece suporte para o SQL Server 2008 Express Edition.  
  
-   [!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows Installer 3.1 ou posterior.  
  
-   O provedor de cliente Oracle ou o provedor OLE DB para Oracle e conectividade de banco de dados Oracle que você deseja migrar. Você pode instalar provedores da mídia do produto Oracle ou site da Oracle.  
  
-   O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] serviço do navegador deve ser executado durante a instalação. Isso é usado para preencher uma lista das instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no Assistente de instalação. Você pode desabilitar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] serviço navegador após a instalação.  
  
    > [!NOTE]  
    > Se o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] navegador estiver em execução, mas você ainda não vir uma lista de instâncias na instalação, você deve desbloquear a porta UDP 1434. Você pode usar o Firewall do Windows para desbloquear temporariamente a porta, ou você pode desativar temporariamente o Firewall do Windows. Você também terá que desabilitar temporariamente o software antivírus. Certifique-se de habilitar o software antivírus e firewalls depois da instalação.  
  
### <a name="installing-the-extension-pack"></a>Instalar o pacote de extensão  
Você pode instalar o pacote de extensão a qualquer momento antes de migrar dados para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!IMPORTANT]  
> Para instalar o pacote de extensão, você deve ser um membro do **sysadmin** função de servidor na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
**Para instalar o pacote de extensão**  
  
1.  Se você ainda não fez isso, extraia todos os arquivos do arquivo Zip do SSMA.  
  
    Dependendo da versão do WinZip você tem, você pode clique duas vezes no arquivo, ou o arquivo com o botão direito e selecione **extrair tudo** ou **abrir no WinZip**. Siga as instruções na interface do usuário WinZip para extrair os arquivos.  
  
2.  Copie o SSMA para o pacote de extensão do Oracle. *n*. Install.exe, onde *n* é o número de compilação, no computador que está executando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
3.  Clique duas vezes no SSMA para o pacote de extensão do Oracle. *n*. Install.exe.  
  
4.  Na página de boas-vinda, clique em **próxima**.  
  
5.  Na página Contrato de licença de usuário final, leia o contrato de licença. Se você concordar, selecione a **aceito os termos do contrato de licença** caixa de seleção e, em seguida, clique em **próxima**.  
  
6.  Na página Escolha o tipo de instalação, clique em **típica**.  
  
7.  Na página pronto para instalar, clique em **instalar**.  
  
8.  Sobre o página a primeira etapa de instalação concluído, clique em **próxima**.  
  
    Uma nova caixa de diálogo será exibida, em que você selecione a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para a instalação do pacote de extensão.  
  
9. Selecione a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] onde você irá ser migrando esquemas Oracle e, em seguida, clique em **próxima**.  
  
    A instância padrão tem o mesmo nome que o computador. Instâncias nomeadas serão seguidas por uma barra invertida e o nome da instância.  
  
10. Na página de conexão, selecione o método de autenticação e, em seguida, clique em **próxima**.  
  
    Autenticação do Windows usarão suas credenciais do Windows para tentar fazer logon na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se você selecionar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticação, você deve inserir um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nome de logon e senha.  
  
11. Na próxima página, selecione **instalar utilitários de banco de dados** *n*, onde *n* é o número de versão e, em seguida, clique em **Avançar**.  
  
    O **sysdb** banco de dados é criado e as funções definidas pelo usuário e procedimentos armazenados são criados no banco de dados.  
  
    Se **instalar o banco de dados do testador** opção estiver marcada o testador **ssmatesterdb** banco de dados será criado.  
  
12. Para instalar os utilitários para outra instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], selecione **Yes**e, em seguida, clique em **próximo**. Ou, para sair do assistente, clique em **não**.  
  
13. No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou usando o utilitário sqlcmd, execute o seguinte script para habilitar o CLR:  
  
    ```  
    sp_configure 'clr enabled', 1  
    GO  
    RECONFIGURE  
    GO  
    ```  
    Se o CLR não estiver habilitado, você receberá o seguinte erro quando o SSMA se conecta ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
    O SSMA não foi possível recuperar as informações de versão de assembly de pacote de extensão. Reinstale o pacote de extensão no servidor de banco de dados.  
  
### <a name="sql-server-database-objects"></a>Objetos de banco de dados do SQL Server  
Depois de instalar o pacote de extensão, você será um, consulte um **ssma_oracle.bcp_migration_packages** tabela, um **ssma_oracle.db_storage** tabela e um **ssma_oracle.db_error_list** na tabela o **sysdb** banco de dados. Você também verá muitos procedimentos armazenados e funções definidas pelo usuário na **ssma_oracle** esquema.  
  
Sempre que você migra dados para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o SSMA cria um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] trabalho do agente. Esses trabalhos são nomeados **pacote de migração de dados {GUID} ssma_oracle**e são visíveis na [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nó do agente de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] na pasta Jobs.  
  
## <a name="see-also"></a>Consulte também  
[Instalar o SSMA para cliente Oracle &#40;OracleToSQL&#41;](../../ssma/oracle/installing-ssma-for-oracle-client-oracletosql.md)  
[Migrando do Oracle bancos de dados para o SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)  
  
