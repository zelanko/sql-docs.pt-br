---
title: Instalando os componentes do SSMA em SQL Server (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/14/2020
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 5ad9e12c-2cdb-4dd2-8703-05a23242d19d
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 1c66255f57a69db0807ab1620cafd60444f296c8
ms.sourcegitcommit: 21bedbae28840e2f96f5e8b08bcfc794f305c8bc
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/06/2020
ms.locfileid: "87865384"
---
# <a name="installing-ssma-components-on-sql-server-sybasetosql"></a>Instalando os componentes do SSMA em SQL Server (SybaseToSQL)

Além de instalar o SSMA, para usar a migração de dados do servidor, você também deve instalar componentes no computador que está executando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Esses componentes incluem o pacote de extensão do SSMA, que dá suporte à migração de dados e aos provedores de Sybase para habilitar a conectividade de servidor para servidor.

## <a name="ssma-for-sybase-extension-pack"></a>Pacote de extensão do SSMA para Sybase

O pacote de extensão do SSMA adiciona os bancos de dados, **sysdb** e **ssmatesterdb_syb**, à instância especificada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . O banco de dados **sysdb** contém as tabelas e os procedimentos armazenados que são necessários para migrar o dado. O banco de dados **ssmatester_syb** contém o **ssma_sybase_utilities**de esquema, no qual os objetos (tabelas, gatilhos, modos de exibição) usados pelo componente de testador do SSMA são criados.

Além disso, quando você migra dados para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o, o SSMA cria [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] trabalhos do Agent quando o mecanismo de migração de dados do servidor é usado para migrar os dados.

### <a name="prerequisites"></a>Pré-requisitos

Antes de instalar os componentes do SSMA para servidor Sybase no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , verifique se o sistema atende aos seguintes requisitos:

- [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]a instância está instalada.
- [!INCLUDE[msCoName](../../includes/msconame_md.md)]Windows Installer 3,1 ou uma versão posterior.
- A [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort_md.md)] versão 4.7.2 ou posterior. Você pode obtê-lo no [centro de desenvolvedores .NET Framework](https://go.microsoft.com/fwlink/?LinkId=48882).
- O provedor Sybase OLE DB/ADO.Net/ODBC e a conectividade com o servidor de banco de dados do SAP ASE que contém os bancos que você deseja migrar. Você pode instalar provedores da mídia de produto SAP ASE. Para obter informações sobre conectividade, consulte [conectando-se ao Sybase ASE &#40;SybaseToSQL&#41;](../../ssma/sybase/connecting-to-sybase-ase-sybasetosql.md).
- O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] serviço navegador deve estar em execução durante a instalação. Isso é usado para preencher uma lista das instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no assistente de instalação do. Você pode desabilitar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] serviço navegador após a instalação.

  > [!NOTE]
  > Se o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] serviço navegador estiver em execução, mas você ainda não vir uma lista de instâncias na instalação, deverá desbloquear a porta UDP 1434. Você pode usar o Firewall do Windows para desbloquear temporariamente a porta ou pode desabilitar o Firewall do Windows temporariamente. Você também pode ter que desabilitar temporariamente o software antivírus. Certifique-se de habilitar firewalls e software antivírus após a instalação.

### <a name="installing-the-extension-pack"></a>Instalando o pacote de extensão

Você pode instalar o pacote de extensão a qualquer momento antes de migrar dados para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .

> [!IMPORTANT]
> Para instalar o pacote de extensão, você deve ser membro da função de servidor sysadmin na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .

Para instalar o pacote de extensão:

1. Copie **SSMAforSybaseExtensionPack_*n*. msi**, em que *n* é o número de Build, para o computador que está executando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .
2. Clique duas vezes em **SSMAforSybaseExtensionPack_*n*. msi**.
3. Na página de **Boas-vindas**, clique em **Avançar**.
4. Na página **contrato de licença de usuário final** , leia o contrato de licença. Se você concordar, selecione a opção **aceito o contrato** e clique em **Avançar**.
5. Na página **escolher tipo de instalação** , clique em **típico**.
6. Na página **Pronto para instalar**, clique em **Instalar**.
7. Na página **concluir a primeira etapa da instalação** , clique em **Avançar**.

   Uma nova caixa de diálogo será exibida, na qual você seleciona a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para a instalação do pacote de extensão.

8. Selecione a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] onde você migrará os bancos de dados do SAP ase e clique em **Avançar**.

   A instância padrão tem o mesmo nome que o computador. As instâncias nomeadas serão seguidas por uma barra invertida e o nome da instância.

9. Na página conexão, selecione o método de autenticação e clique em **Avançar**.

   A autenticação do Windows usará suas credenciais do Windows para tentar fazer logon na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Se você selecionar autenticação de servidor, deverá inserir um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nome de logon e uma senha.

10. A próxima etapa exige que você defina a senha para uma chave mestra que será usada para criptografar os dados confidenciais armazenados no banco de dados do pacote de extensão durante a migração de dado do lado do servidor. Forneça uma senha forte e clique em **Avançar**.

11. Na página seguinte, selecione **instalar utilitários banco de *dados n* e instalar bibliotecas de pacotes de extensão**, em que *n* é o número de versão. Se você planeja usar o recurso de testador, marque a caixa de seleção **instalar banco de dados do testador** e, em seguida, selecione **Avançar**.

    O banco de dados **sysdb** é criado com as tabelas e os procedimentos armazenados necessários para a migração de data (o uso do mecanismo de migração de dados do lado do servidor) são criados nesse banco.

    Se a opção **instalar banco de dados do Tester** estiver marcada, o banco de dados **ssmatesterdb_syb** será criado.

12. Depois que a instalação for concluída, será exibido um prompt perguntando se você deseja instalar o banco de dados de utilitários em outra instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , selecione **Sim**e, em seguida, selecione **Avançar**, ou para sair do assistente, selecione **não** e, em seguida, selecione **sair**.

### <a name="sql-server-database-objects"></a>SQL Server objetos de banco de dados

Depois de instalar o pacote de extensão, você verá uma tabela **ssma_syb. bcp_migration_packages** no banco de dados **sysdb** . Você também verá os seguintes procedimentos armazenados:

- `bcp_clean_migration_data`
- `bcp_ensure_message_table`
- `bcp_insert_new_message`
- `bcp_post_process`
- `bcp_read_new_migration_messages`
- `bcp_save_migration_package`
- `bcp_smart_truncate`
- `bcp_start_migration_process`
- `get_jobstep_info`
- `stop_agent_process`

Toda vez que você migra dados para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o, o SSMA cria um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] trabalho do Agent. Esses trabalhos são nomeados **ssma_syb pacote de migração de dados {GUID}** e ficam visíveis no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nó agente do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] na pasta trabalhos.  

## <a name="sybase-providers"></a>Provedores de Sybase

Quando você usa a migração de dados do lado do servidor para mover dados do SAP ASE para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o, os dados são migrados diretamente entre o SAP ase e o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Ele não passa pelo SSMA porque isso tornaria a migração de dados mais lenta.

### <a name="installing-the-sybase-providers"></a>Instalando os provedores de Sybase

As instruções a seguir fornecem as etapas básicas de instalação para a instalação de provedores do Sybase. As instruções exatas serão diferentes dependendo da versão do programa de instalação do Sybase.

> [!IMPORTANT]
> Antes de executar o programa de instalação, verifique se você não está violando seus contratos de licenciamento.

1. Execute o programa de instalação do Sybase ASE.
2. Selecione instalação personalizada.
3. Na página seleção de recursos, selecione os provedores de dados ODBC, OLE DB e ADO.NET.
4. Verifique os recursos selecionados e clique em **concluir** para instalar o provedor de dados.

## <a name="see-also"></a>Confira também

- [Instalando o SSMA para cliente Sybase](../../ssma/sybase/installing-ssma-for-sybase-client-sybasetosql.md)
- [Migrando bancos de dados de ASE do Sybase para o SQL Server-Azure SQL Database](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)
