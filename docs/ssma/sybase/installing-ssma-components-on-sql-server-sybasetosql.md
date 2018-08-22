---
title: Instalar os componentes do SSMA no SQL Server (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 5ad9e12c-2cdb-4dd2-8703-05a23242d19d
caps.latest.revision: 10
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: c6090d5e24f7ba6fe6c06546f5f432a3c8eaa4ab
ms.sourcegitcommit: 603d2e588ac7b36060fa0cc9c8621ff2a6c0fcc7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/14/2018
ms.locfileid: "40394794"
---
# <a name="installing-ssma-components-on-sql-server-sybasetosql"></a>Instalar os componentes do SSMA no SQL Server (SybaseToSQL)
Além de instalar o SSMA, para usar a migração de dados do lado servidor, você também deve instalar componentes no computador que está executando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Esses componentes incluem o pacote de extensão do SSMA, que dá suporte à migração de dados e provedores do Sybase para habilitar a conectividade de servidor para servidor.  
  
## <a name="ssma-for-sybase-extension-pack"></a>SSMA para Sybase extensão Pack  
O pacote de extensão do SSMA adiciona os bancos de dados **sysdb** e **ssmatesterdb_syb**, para a instância especificada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O **sysdb** banco de dados contém as tabelas e procedimentos armazenados que são necessárias para migrar dados. O **ssmatester_syb** banco de dados contém o esquema **ssma_sybase_utilities**, em que os objetos (tabelas, gatilhos, modos de exibição) usados pelo componente do testador do SSMA foram criados.  
  
Além disso, quando você migra dados a serem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o SSMA cria [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] trabalhos do agente quando o mecanismo de migração de dados do lado servidor é usado para migrar os dados.  
  
### <a name="installing-the-extension-pack"></a>Instalar o pacote de extensão  
Você pode instalar o pacote de extensão a qualquer momento antes de migrar dados para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!IMPORTANT]  
> Para instalar o pacote de extensão, você deve ser um membro da função de servidor sysadmin na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
**Para instalar o pacote de extensão**  
  
1.  Copie o SSMA para o pacote de extensão do Sybase. *n*. Install.exe, onde *n* é o número de compilação, no computador que está executando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
2.  Clique duas vezes no SSMA para o pacote de extensão do Sybase. *n*. Install.exe.  
  
3.  Na página de boas-vinda, clique em **próxima**.  
  
4.  Na página Contrato de licença de usuário final, leia o contrato de licença. Se você concordar, selecione a **aceito os termos do contrato de licença** caixa de seleção e, em seguida, clique em **próxima**.  
  
5.  Na página Escolha o tipo de instalação, clique em **típica**.  
  
6.  Na página pronto para instalar, clique em **instalar**.  
  
7.  Sobre o página a primeira etapa de instalação concluído, clique em **próxima**.  
  
    Uma nova caixa de diálogo será exibida, em que você selecione a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para a instalação do pacote de extensão.  
  
8.  Selecione a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] onde você será migrando bancos de dados do ASE e, em seguida, clique em **próxima**.  
  
    A instância padrão tem o mesmo nome que o computador. Instâncias nomeadas serão seguidas por uma barra invertida e o nome da instância.  
  
9. Na página de parâmetros de Conexão, selecione o método de autenticação e, em seguida, clique em **próxima**.  
  
    Autenticação do Windows usarão suas credenciais do Windows para tentar fazer logon na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se você selecionar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticação, você deve inserir um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nome de logon e senha.  
  
10. Na página Gerenciar servidor, selecione **instalar utilitários de banco de dados** *n*, onde *n* é o número de versão e, em seguida, clique em **Avançar**.  
  
    O **sysdb** banco de dados é criado e os procedimentos armazenados são criados no banco de dados.  
  
    Se **instalar o banco de dados do testador** opção estiver marcada o testador **ssmatesterdb_syb** banco de dados será criado.  
  
11. Para instalar os utilitários para outra instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], selecione **retornar instâncias**e, em seguida, clique em **próximo**. Ou, para sair do assistente, clique em **sair**.  
  
### <a name="sql-server-database-objects"></a>Objetos de banco de dados do SQL Server  
Depois de instalar o pacote de extensão, você será um, consulte um **ssma_syb.bcp_migration_packages** na tabela a **sysdb** banco de dados. Você também verá os seguintes procedimentos armazenados:  
  
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
  
Sempre que você migra dados para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o SSMA cria um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] trabalho do agente. Esses trabalhos são nomeados **pacote de migração de dados {GUID} ssma_syb**e são visíveis na [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nó do agente de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] na pasta Jobs.  
  
## <a name="sybase-providers"></a>Provedores do Sybase  
Quando você migra dados de ASE [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]migram os dados do SQL Azure, diretamente entre o ASE e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]do SQL Azure. Ele não passa pelo SSMA porque isso seria mais lento de migração de dados.  
  
### <a name="installing-the-sybase-providers"></a>Instalando os provedores do Sybase  
As instruções a seguir fornecem as etapas básicas de instalação para instalação de provedores do Sybase. As instruções exatas variarão dependendo da versão do programa de instalação do Sybase.  
  
> [!IMPORTANT]  
> Antes de executar o programa de instalação, verifique se você não está violando as seus contratos de licenciamento.  
  
1.  Execute o programa de instalação de ASE do Sybase.  
  
2.  Selecione a instalação personalizada.  
  
3.  Na página seleção de recursos, selecione os provedores de dados ODBC, OLE DB e ADO.NET.  
  
4.  Verifique se os recursos selecionados e, em seguida, clique em **concluir** para instalar o provedor de dados.  
  
## <a name="see-also"></a>Consulte também  
[Instalar o SSMA para Sybase cliente &#40;SybaseToSQL&#41;](../../ssma/sybase/installing-ssma-for-sybase-client-sybasetosql.md)  
[Migrando bancos de dados do Sybase ASE para o SQL Server – BD SQL do Azure &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  
