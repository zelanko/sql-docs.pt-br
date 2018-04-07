---
title: Instalando componentes do SSMA no SQL Server (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-sybase
ms.reviewer: ''
ms.suite: sql
ms.technology:
- sql-ssma
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 5ad9e12c-2cdb-4dd2-8703-05a23242d19d
caps.latest.revision: 10
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 97c0e5dc529a6563212dc3ddedce5014ccfd463a
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/06/2018
---
# <a name="installing-ssma-components-on-sql-server-sybasetosql"></a>Instalar os componentes do SSMA no SQL Server (SybaseToSQL)
Além de instalar o SSMA, para usar a migração de dados do lado de servidor, você também deve instalar componentes no computador que está executando [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Esses componentes incluem o pacote de extensão do SSMA, que dá suporte à migração de dados e provedores do Sybase para habilitar a conectividade de servidor para servidor.  
  
## <a name="ssma-for-sybase-extension-pack"></a>SSMA para Sybase extensão Pack  
O pacote de extensão do SSMA adiciona os bancos de dados, **sysdb** e **ssmatesterdb_syb**, a instância especificada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. O **sysdb** banco de dados contém tabelas e procedimentos armazenados que são necessárias para migrar os dados. O **ssmatester_syb** banco de dados contém o esquema **ssma_sybase_utilities**, no qual os objetos (tabelas, gatilhos, modos de exibição) usados pelo componente tester SSMA são criados.  
  
Além disso, quando você migra dados para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], cria o SSMA [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] trabalhos de agente quando o mecanismo de migração de dados do lado servidor é usado para migrar os dados.  
  
### <a name="installing-the-extension-pack"></a>Instalando o pacote de extensão  
Você pode instalar o pacote de extensão a qualquer momento antes de migrar dados para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
> [!IMPORTANT]  
> Para instalar o pacote de extensão, você deve ser um membro da função de servidor sysadmin na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
**Para instalar o pacote de extensão**  
  
1.  Copie SSMA para Sybase extensão Pack. *n*. Install.exe, onde *n* é o número de compilação para o computador que está executando [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
2.  Clique duas vezes em SSMA para Sybase extensão Pack. *n*. Install.exe.  
  
3.  Na página de boas-vinda, clique em **próximo**.  
  
4.  Na página Contrato de licença de usuário final, leia o contrato de licença. Se você concordar, selecione o **aceito os termos do contrato de licença** caixa de seleção e, em seguida, clique em **próximo**.  
  
5.  Na página Escolha o tipo de instalação, clique em **típica**.  
  
6.  Na página pronto para instalar, clique em **instalar**.  
  
7.  Sobre a página a primeira etapa de instalação concluída, clique em **próximo**.  
  
    Uma nova caixa de diálogo será exibida, em que você selecionar a instância de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] para a instalação do pacote de extensão.  
  
8.  Selecione a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] onde você será migrar ASE bancos de dados e, em seguida, clique em **próximo**.  
  
    A instância padrão tem o mesmo nome que o computador. Instâncias nomeadas serão seguidas por uma barra invertida e o nome da instância.  
  
9. Na página de parâmetros de Conexão, selecione o método de autenticação e, em seguida, clique em **próximo**.  
  
    Autenticação do Windows usará as credenciais do Windows para tentar fazer logon instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Se você selecionar [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] autenticação, você deve inserir um [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] nome de logon e senha.  
  
10. Na página Gerenciar servidor, selecione **instalar utilitários de banco de dados** *n*, onde *n* é o número de versão e, em seguida, clique em **próximo**.  
  
    O **sysdb** banco de dados é criado e os procedimentos armazenados são criados no banco de dados.  
  
    Se **instalar o banco de dados Tester** opção estiver marcada o testador **ssmatesterdb_syb** banco de dados será criado.  
  
11. Para instalar os utilitários para outra instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], selecione **retornar instâncias**e, em seguida, clique em **próximo**. Ou, para sair do assistente, clique em **sair**.  
  
### <a name="sql-server-database-objects"></a>Objetos de banco de dados do SQL Server  
Depois de instalar o pacote de extensão, você será um, consulte um **ssma_syb.bcp_migration_packages** tabela o **sysdb** banco de dados. Você também verá os seguintes procedimentos armazenados:  
  
-   **bcp_clean_migration_data**  
  
-   **bcp_ensure_message_table**  
  
-   **bcp_insert_new_message**  
  
-   **bcp_post_process**  
  
-   **bcp_read_new_migration_messages**  
  
-   **bcp_save_migration_package**  
  
-   **bcp_smart_truncate**  
  
-   **bcp_start_migration_process**  
  
-   **get_jobstep_info**  
  
-   **stop_agent_process**  
  
Toda vez que você migra dados para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], SSMA cria um [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] trabalho do agente. Esses trabalhos são nomeados **ssma_syb pacote de migração de dados {GUID}**e são visíveis no [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] nó do agente de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] na pasta Jobs.  
  
## <a name="sybase-providers"></a>Provedores do Sybase  
Quando você migra dados de ASE para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]migra o SQL Azure, os dados diretamente entre ASE e [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]do SQL Azure. Ele não passa pelo SSMA porque isso seria mais lento de migração de dados.  
  
### <a name="installing-the-sybase-providers"></a>Instalando os provedores do Sybase  
As instruções a seguir fornecem as etapas básicas de instalação para instalar provedores de Sybase. As instruções exatas serão diferentes dependendo da versão do programa de instalação do Sybase.  
  
> [!IMPORTANT]  
> Antes de executar o programa de instalação, verifique se que não estão violando seus contratos de licenciamento.  
  
1.  Execute o programa de instalação do Sybase ASE.  
  
2.  Selecione Instalação personalizada.  
  
3.  Na página seleção de recursos, selecione os provedores de dados ODBC, OLE DB e ADO.NET.  
  
4.  Verifique se os recursos selecionados e, em seguida, clique em **concluir** para instalar o provedor de dados.  
  
## <a name="see-also"></a>Consulte também  
[Instalando o SSMA para Sybase cliente &#40;SybaseToSQL&#41;](../../ssma/sybase/installing-ssma-for-sybase-client-sybasetosql.md)  
[Migrando bancos de dados Sybase ASE para o SQL Server - banco de dados SQL do Azure &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  
