---
title: Desinstalar instância existente
description: Este artigo descreve como desinstalar uma instância autônoma do SQL Server, o que também prepara o sistema para que você possa reinstalar o SQL Server.
ms.custom: seo-lt-2019
ms.date: 12/13/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- removing instances of SQL Server
- uninstalling instances of SQL Server
- removing SQL Server
- instances of SQL Server, uninstalling
- uninstalling SQL Server
ms.assetid: 3c64b29d-61d7-4b86-961c-0de62261c6a1
author: cawrites
ms.author: chadam
ms.openlocfilehash: 16522114fb7e02517ec7385b6b7c73aa90b4b6b0
ms.sourcegitcommit: 5a1ed81749800c33059dac91b0e18bd8bb3081b1
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/23/2020
ms.locfileid: "96127488"
---
# <a name="uninstall-an-existing-instance-of-sql-server-setup"></a>Desinstalar uma instância existente do SQL Server (Instalação)
[!INCLUDE [SQL Server Windows Only - ASDBMI ](../../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  Este artigo descreve como desinstalar uma instância autônoma do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Seguindo as etapas deste artigo, você também prepara o sistema para que seja possível reinstalar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 > [!NOTE]
 > Para desinstalar um cluster de failover do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , use a função Remover Nó fornecida na instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para remover cada nó individualmente. Para obter mais informações, consulte [Adicionar ou remover nós em um cluster de failover do SQL Server &#40;Instalação&#41;](../../sql-server/failover-clusters/install/add-or-remove-nodes-in-a-sql-server-failover-cluster-setup.md)  

## <a name="considerations"></a>Considerações

- Para desinstalar o SQL Server, você deve ser um administrador local com permissões para fazer logon como um serviço. 
- Se o computador tiver a quantidade *mínima* de memória física necessária, aumente o tamanho do arquivo de paginação para duas vezes a quantidade de memória física. Memória virtual insuficiente pode resultar em uma remoção incompleta do SQL Server. 
- Em um sistema com várias instâncias do SQL Server, o serviço SQL Server Browser é desinstalado somente quando a última instância de SQL Server é removida. O serviço SQL Server Browser pode ser removido manualmente de **Programas e Recursos** no **Painel de Controle**. 
- Desinstalar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] exclui os arquivos de dados tempdb que foram adicionados durante o processo de instalação. Os arquivos com um padrão de nome tempdb_mssql_*.ndf serão excluídos se eles existirem no diretório de banco de dados do sistema. 
  

  
## <a name="prepare"></a>Preparar  
  
1.  **Faça backup dos dados.** Crie [backups completos](../../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md) de todos os bancos de dados, incluindo bancos de dados do sistema, ou copie manualmente os arquivos .mdf e .ldf para um local separado. O banco de dados **mestre** contém todas as informações de nível de sistema para o servidor, tais como logons e esquemas. O banco de dados **msdb** contém informações de trabalho, tais como trabalhos do SQL Server Agent, histórico de backup e planos de manutenção. Para obter mais informações sobre bancos de dados do sistema, confira [Bancos de dados do sistema](../../relational-databases/backup-restore/back-up-and-restore-of-system-databases-sql-server.md). 
  
    Os arquivos que você deve salvar incluem os arquivos de banco de dados a seguir:  

    * master.mdf
    * msdbdata.mdf
    * Tempdb.mdf
    * mastlog.ldf
    * msdblog.ldf
    * Templog.ldf
    * model.mdf
    * Mssqlsystemresource.mdf
    * ReportServer[$InstanceName]
    * modellog.ldf
    * Mssqlsystemresource.ldf
    * ReportServer[$InstanceName]TempDB

    > [!NOTE]
    > Os bancos de dados do ReportServer estão incluídos com o SQL Server Reporting Services.   

 
1.  **Interromper todos** **os serviços do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].** É recomendável interromper todos os serviços do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] antes de desinstalar os componentes do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Conexões ativas podem impedir a desinstalação com êxito.  
  
1.  **Use uma conta que tenha as permissões apropriadas.** Faça logon no servidor usando a conta de serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou usando uma conta que tenha permissões equivalentes. Por exemplo, é possível fazer logon no servidor com uma conta que seja membro do grupo Administradores local.  
  
## <a name="uninstall"></a>Desinstalar 

# <a name="windows-10--2016-"></a>[Windows 10 / 2016 +](#tab/Windows10)

Para desinstalar o SQL Server do Windows 10, Windows Server 2016, Windows Server 2019 e posteriores, siga estas etapas: 

1. Para iniciar o processo de remoção, navegue até **Configurações** no menu iniciar e escolha **Aplicativos**. 
1. Procure por `sql` na caixa de pesquisa. 
1. Selecione **Microsoft SQL Server (Versão) (Bit)** . Por exemplo, `Microsoft SQL Server 2017 (64-bit)`.
1. Selecionar **Desinstalar**.
 
    ![Desinstalar o SQL Server](media/uninstall-an-existing-instance-of-sql-server-setup/uninstall-sql-server-windows-10.png)

1. Selecione **Remover** no pop-up da caixa de diálogo SQL Server para iniciar o assistente de instalação do Microsoft SQL Server. 

    ![Remover o SQL Server](media/uninstall-an-existing-instance-of-sql-server-setup/remove-sql-2017.png)
  
1.  Na página **Selecionar Instância**, use a caixa suspensa para especificar uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a ser removida ou especifique a opção para remover somente os recursos compartilhados e as ferramentas de gerenciamento do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para continuar, selecione **Avançar**.  
  
1.  Na página **Selecionar Recursos**, especifique os recursos a serem removidos da instância especificada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
1.  Na página **Pronto para Desinstalar** , examine a lista de componentes e de recursos que serão desinstalados. Clique em **Remover** para começar a desinstalação  
 
1. Atualize a janela **Aplicativos e Recursos** para verificar se a instância do SQL Server foi removida com êxito e determinar quais, se houver, componentes do SQL Server ainda existem. Remova esses componentes dessa janela também, se preferir. 

# <a name="windows-2008---2012-r2"></a>[Windows 2008 – 2012 R2](#tab/windows2012)

Para desinstalar o SQL Server do Windows Server 2008, Windows Server 2012 e Windows 2012 R2, siga estas etapas: 

1. Para iniciar o processo de remoção, navegue até o **Painel de Controle** e, em seguida, selecione **Programas e Recursos**.
1. Clique com o botão direito do mouse em **Microsoft SQL Server (Versão) (Bit)** e selecione **Desinstalar**. Por exemplo, `Microsoft SQL Server 2012 (64-bit)`.  
  
    ![Desinstalar o SQL Server](media/uninstall-an-existing-instance-of-sql-server-setup/uninstall-sql-server-windows-2012.png)

1. Selecione **Remover** no pop-up da caixa de diálogo SQL Server para iniciar o assistente de instalação do Microsoft SQL Server. 

    ![Remover o SQL Server](media/uninstall-an-existing-instance-of-sql-server-setup/remove-sql-2012.png)
  
1.  Na página **Selecionar Instância**, use a caixa suspensa para especificar uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a ser removida ou especifique a opção para remover somente os recursos compartilhados e as ferramentas de gerenciamento do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para continuar, selecione **Avançar**.  
  
1.  Na página **Selecionar Recursos**, especifique os recursos a serem removidos da instância especificada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
1.  Na página **Pronto para Desinstalar** , examine a lista de componentes e de recursos que serão desinstalados. Clique em **Remover** para começar a desinstalação  
 
1. Atualize a janela **Programas e Recursos** para verificar se a instância do SQL Server foi removida com êxito e determinar quais, se houver, componentes do SQL Server ainda existem. Remova esses componentes dessa janela também, se preferir. 

---

  
## <a name="in-the-event-of-failure"></a>Em caso de falha  

Se o processo de remoção falhar, examine os [arquivos de log da instalação do SQL Server](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md) para determinar a causa raiz. 

O artigo da base de conhecimento [Como identificar problemas de instalação do SQL Server nos arquivos de log da instalação](https://support.microsoft.com/kb/955396/en-us) pode auxiliar na investigação. Embora seja para o SQL Server 2008, a metodologia descrita é aplicável a todas as versões do SQL Server. 

  
## <a name="see-also"></a>Consulte Também  
 [Exibir e ler arquivos de log da Instalação do SQL Server](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)  
  
  
