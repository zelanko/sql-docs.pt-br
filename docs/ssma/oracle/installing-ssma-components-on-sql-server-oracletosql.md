---
title: Instalando os componentes do SSMA em SQL Server (OracleToSQL) | Microsoft Docs
description: Saiba como instalar o pacote de extensão do SSMA e os provedores Oracle no computador que executa o SQL Server para dar suporte à conversão de banco de dados Oracle.
ms.prod: sql
ms.custom: ''
ms.date: 11/16/2020
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Installing the extension pack
- SQL Server Database Objects
ms.assetid: 33070e5f-4e39-4b70-ae81-b8af6e4983c5
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 64850d1a701491f0dc5817576a568fdc3ebc2483
ms.sourcegitcommit: 82b92f73ca32fc28e1948aab70f37f0efdb54e39
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/18/2020
ms.locfileid: "94870090"
---
# <a name="installing-ssma-components-on-sql-server-oracletosql"></a>Instalando os componentes do SSMA em SQL Server (OracleToSQL)

Além de instalar o SSMA, você também deve instalar componentes no computador que está executando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Esses componentes incluem o pacote de extensão do SSMA, que dá suporte à migração de dados e aos provedores Oracle para habilitar a conectividade de servidor para servidor.

## <a name="ssma-for-oracle-extension-pack"></a>Pacote de extensão do SSMA para Oracle

O pacote de extensão do SSMA implanta procedimentos armazenados estendidos e adiciona os bancos de dados **sysdb** e **ssmatesterdb** à instância especificada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Os procedimentos armazenados estendidos fornecem a funcionalidade necessária para emular recursos e behaiov da Oracle, enquanto o banco de dados **sysdb** contém as tabelas e os procedimentos armazenados necessários para migrar os dados. O banco de dados **ssmatesterdb** contém as tabelas e os procedimentos exigidos pelo componente testador (se instalado).

Além disso, quando você migra dados para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SSMA cria trabalhos do Agent quando o mecanismo de migração de dados do servidor é usado para migrar os dados.

### <a name="prerequisites"></a>Pré-requisitos

Antes de instalar os componentes de servidor do SSMA para Oracle [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , verifique se o sistema atende aos seguintes requisitos:

- [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a instância está instalada.
- [!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows Installer 3,1 ou uma versão posterior.
- A [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort_md.md)] versão 4.7.2 ou posterior. Você pode obtê-lo no [centro de desenvolvedores .NET Framework](https://go.microsoft.com/fwlink/?LinkId=48882).
- O provedor de OLE DB para Oracle (se estiver usando o OLE DB) e a conectividade com o banco de dados Oracle que você deseja migrar. Você pode instalar provedores da mídia de produto Oracle ou do site da Oracle.
- O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] serviço navegador deve estar em execução durante a instalação. Isso é usado para preencher uma lista das instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no assistente de instalação do. Você pode desabilitar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] serviço navegador após a instalação.

  > [!NOTE]
  > Se o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] serviço navegador estiver em execução, mas você ainda não vir uma lista de instâncias na instalação, deverá desbloquear a porta UDP 1434. Você pode usar o Firewall do Windows para desbloquear temporariamente a porta ou pode desabilitar o Firewall do Windows temporariamente. Você também pode ter que desabilitar temporariamente o software antivírus. Certifique-se de habilitar firewalls e software antivírus após a instalação.

### <a name="installing-the-extension-pack"></a>Instalando o pacote de extensão

Você pode instalar o pacote de extensão a qualquer momento antes de migrar dados para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .

> [!IMPORTANT]
> Para instalar o pacote de extensão, você deve ser membro da função de servidor **sysadmin** na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .

Para instalar o pacote de extensão:

1. Copie **SSMAforOracleExtensionPack_ *n*. msi** (em que *n* é o número da compilação) para o computador que está executando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .
2. Clique duas vezes em **SSMAforOracleExtensionPack_ *n*. msi**.
3. Na página **Bem-vindo** , clique em **Avançar**.
4. Na página **contrato de licença de usuário final** , leia o contrato de licença. Se você concordar, selecione aceito **a opção de contrato** e clique em **Avançar**.
5. Na página **escolher tipo de instalação** , selecione **típica**.
6. Na página **Pronto para Instalar** , selecione **Instalar**.
7. Na página **concluir a primeira etapa da instalação** , selecione **Avançar**.
  
   Uma nova caixa de diálogo é exibida. Selecione o tipo de pacote de extensão.
  
8. Selecione o tipo de instalação desejado e clique em **Avançar**.

   > [!IMPORTANT]
   > A opção remota deve ser usada somente ao instalar o pacote de extensão em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] execução no Linux ou no destino [!INCLUDE[ssAzureMi](../../includes/ssazuremi_md.md)] . [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] as instalações em execução no Windows devem ter sempre o pacote de extensão instalado localmente. [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] e o Azure Synapse Analytics não dão suporte ao pacote de extensão.

   Se você estiver instalando o pacote de extensão em uma [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instância local, a próxima página permitirá que você escolha uma instância local do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] à qual você migrará os esquemas Oracle. Escolha uma instância na lista suspensa e, em seguida, selecione **Avançar**.

   A instância padrão tem o mesmo nome que o computador. As instâncias nomeadas serão seguidas por uma barra invertida e o nome da instância.

9. Na página conexão, selecione o método de autenticação e, em seguida, selecione **Avançar**.

   A autenticação do Windows usará suas credenciais do Windows para tentar entrar na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Se você selecionar autenticação de servidor, deverá inserir um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nome de logon e uma senha.

10. A próxima etapa exige que você defina a senha para uma chave mestra que será usada para criptografar os dados confidenciais armazenados no banco de dados do pacote de extensão durante a migração de dado do lado do servidor. Forneça uma senha forte e clique em **Avançar**.

11. Na página seguinte, selecione **instalar utilitários banco de *dados n* e instalar bibliotecas de pacotes de extensão**, em que *n* é o número de versão. Se você planeja usar o recurso de testador, marque a caixa de seleção **instalar banco de dados do testador** e, em seguida, selecione **Avançar**.

    O banco de dados **sysdb** é criado com as tabelas e os procedimentos armazenados necessários para a migração de data (o uso do mecanismo de migração de dados do lado do servidor) são criados nesse banco.

    Se a opção **instalar banco de dados do Tester** estiver marcada, o banco de dados **ssmatesterdb** será criado.

12. Depois que a instalação for concluída, será exibido um prompt perguntando se você deseja instalar o banco de dados de utilitários em outra instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , selecione **Sim** e, em seguida, selecione **Avançar**, ou para sair do assistente, selecione **não** e, em seguida, selecione **sair**.

13. No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou usando o `sqlcmd` Utilitário do, execute o script a seguir para habilitar o CLR:

    ```sql
    sp_configure 'clr enabled', 1
    GO
    RECONFIGURE
    GO
    ```

    Se o CLR não estiver habilitado, você receberá o seguinte erro quando o SSMA se conectar a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] :

    > O SSMA não pôde recuperar as informações de versão do assembly do pacote de extensão. Reinstale o pacote de extensão no servidor de banco de dados.

### <a name="sql-server-database-objects"></a>SQL Server objetos de banco de dados

Depois de instalar o pacote de extensão, uma tabela **_migration_packages ssma_oracle. bcp** aparece no banco de dados **sysdb** .

Sempre que você migra dados para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o, o SSMA cria um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] trabalho do Agent. Esses trabalhos são nomeados **ssma_oracle pacote de migração de dados {GUID}** e ficam visíveis no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nó agente do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] na pasta trabalhos.

Além disso, os procedimentos armazenados estendidos a seguir serão adicionados ao banco de dados **mestre** :

- `xp_ora2ms_exec2`
- `xp_ora2ms_exec2_ex`
- `xp_ora2ms_versioninfo2`

## <a name="see-also"></a>Veja também

- [Instalando o SSMA para cliente Oracle](../../ssma/oracle/installing-ssma-for-oracle-client-oracletosql.md)
- [Migrando Bancos de Dados Oracle para o SQL Server](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)
