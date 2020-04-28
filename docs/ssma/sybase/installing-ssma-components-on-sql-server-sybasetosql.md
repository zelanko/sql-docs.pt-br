---
title: Instalando os componentes do SSMA em SQL Server (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 5ad9e12c-2cdb-4dd2-8703-05a23242d19d
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 1fbc3a8f74b21bd5a53bdd874b5c41ef522e29f6
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68029013"
---
# <a name="installing-ssma-components-on-sql-server-sybasetosql"></a>Instalar os componentes do SSMA no SQL Server (SybaseToSQL)
Além de instalar o SSMA, para usar a migração de dados do servidor, você também deve instalar componentes no computador que está [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]executando o. Esses componentes incluem o pacote de extensão do SSMA, que dá suporte à migração de dados e aos provedores de Sybase para habilitar a conectividade de servidor para servidor.  
  
## <a name="ssma-for-sybase-extension-pack"></a>Pacote de extensão do SSMA para Sybase  
O pacote de extensão do SSMA adiciona os bancos de dados, **sysdb** e **ssmatesterdb_syb**, à instância especificada [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]do. O banco de dados **sysdb** contém as tabelas e os procedimentos armazenados que são necessários para migrar o dado. O banco de dados **ssmatester_syb** contém o **ssma_sybase_utilities**de esquema, no qual os objetos (tabelas, gatilhos, modos de exibição) usados pelo componente de testador do SSMA são criados.  
  
Além disso, quando você migra dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]para o, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SSMA cria trabalhos do Agent quando o mecanismo de migração de dados do servidor é usado para migrar os dados.  
  
### <a name="installing-the-extension-pack"></a>Instalando o pacote de extensão  
Você pode instalar o pacote de extensão a qualquer momento antes de migrar dados para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]o.  
  
> [!IMPORTANT]  
> Para instalar o pacote de extensão, você deve ser membro da função de servidor sysadmin na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
**Para instalar o pacote de extensão**  
  
1.  Copie o pacote de extensão do SSMA para Sybase. *n*. Install. exe, em que *n* é o número de Build, para o computador que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]está executando o.  
  
2.  Clique duas vezes em pacote de extensão do SSMA para Sybase. *n*. Install. exe.  
  
3.  Na página de Boas-vindas, clique em **Avançar**.  
  
4.  Na página contrato de licença de usuário final, leia o contrato de licença. Se você concordar, marque a caixa de seleção **eu aceito os termos do contrato de licença** e clique em **Avançar**.  
  
5.  Na página escolher tipo de instalação, clique em **típico**.  
  
6.  Na página pronto para instalar, clique em **instalar**.  
  
7.  Na página concluir a primeira etapa da instalação, clique em **Avançar**.  
  
    Uma nova caixa de diálogo será exibida, na qual você seleciona a instância [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] do para a instalação do pacote de extensão.  
  
8.  Selecione a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] onde você migrará bancos de dados ase e clique em **Avançar**.  
  
    A instância padrão tem o mesmo nome que o computador. As instâncias nomeadas serão seguidas por uma barra invertida e o nome da instância.  
  
9. Na página parâmetros de conexão, selecione o método de autenticação e clique em **Avançar**.  
  
    A autenticação do Windows usará suas credenciais do Windows para tentar fazer logon na instância [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]do. Se você selecionar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticação, deverá inserir um nome [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de logon e uma senha.  
  
10. Na página Gerenciar servidor, selecione **instalar utilitários banco de dados** *n*, em que *n* é o número de versão e clique em **Avançar**.  
  
    O banco de dados **sysdb** é criado e os procedimentos armazenados são criados nesse banco de dados.  
  
    Se a opção **instalar banco de dados do testador** estiver marcada, o testador **ssmatesterdb_syb** banco de dados será criado.  
  
11. Para instalar os utilitários em outra instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], selecione **retornar para instâncias**e clique em **Avançar**. Ou, para sair do assistente, clique em **sair**.  
  
### <a name="sql-server-database-objects"></a>SQL Server objetos de banco de dados  
Depois de instalar o pacote de extensão, você verá uma tabela **ssma_syb. bcp_migration_packages** no banco de dados **sysdb** . Você também verá os seguintes procedimentos armazenados:  
  
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
  
Toda vez que você migra dados para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]o, o SSMA [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cria um trabalho do Agent. Esses trabalhos são nomeados **ssma_syb pacote de migração de dados {GUID}** e ficam visíveis [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no nó agente [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] do na pasta trabalhos.  
  
## <a name="sybase-providers"></a>Provedores de Sybase  
Ao migrar dados do ASE para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]o/SQL Azure, os dados são migrados diretamente entre [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]o ase e o/SQL Azure. Ele não passa pelo SSMA porque isso tornaria a migração de dados mais lenta.  
  
### <a name="installing-the-sybase-providers"></a>Instalando os provedores de Sybase  
As instruções a seguir fornecem as etapas básicas de instalação para a instalação de provedores do Sybase. As instruções exatas serão diferentes dependendo da versão do programa de instalação do Sybase.  
  
> [!IMPORTANT]  
> Antes de executar o programa de instalação, verifique se você não está violando seus contratos de licenciamento.  
  
1.  Execute o programa de instalação do Sybase ASE.  
  
2.  Selecione instalação personalizada.  
  
3.  Na página seleção de recursos, selecione os provedores de dados ODBC, OLE DB e ADO.NET.  
  
4.  Verifique os recursos selecionados e clique em **concluir** para instalar o provedor de dados.  
  
## <a name="see-also"></a>Consulte Também  
[Instalação do SSMA for Sybase Client &#40;SybaseToSQL&#41;](../../ssma/sybase/installing-ssma-for-sybase-client-sybasetosql.md)  
[Migrando bancos de dados do Sybase ASE para o SQL Server-BD SQL do Azure &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  
