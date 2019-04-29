---
title: Atualizar um banco de dados utilizando Desanexar e Anexar (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- database attaching [SQL Server]
- upgrading databases
- database upgrades [SQL Server]
- database detaching [SQL Server]
- detaching databases [SQL Server]
- attaching databases [SQL Server]
ms.assetid: 99f66ed9-3a75-4e38-ad7d-6c27cc3529a9
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 290454026cc87819bf9ffcf73329bb562e3dc5a4
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62916750"
---
# <a name="upgrade-a-database-using-detach-and-attach-transact-sql"></a>Atualizar um banco de dados utilizando Desanexar e Anexar (Transact-SQL)
  Este tópico descreve como usar operações de desanexação e anexação para atualizar um banco de dados do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Depois de ser anexado ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], o banco de dados estará disponível imediatamente e, em seguida, será atualizado.  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Limitações e restrições](#Restrictions)  
  
     [Recomendações](#Recommendations)  
  
-   **Para atualizar um banco de dados do SQL Server:**  
  
     [Usando operações de anexação e desanexação](#SSMSProcedure)  
  
-   **Acompanhamento:**  [Depois de atualizar um banco de dados do SQL Server](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Restrictions"></a> Limitações e restrições  
  
-   Os bancos de dados de sistema não podem ser anexados.  
  
-   Anexe e desanexe a desabilitação do encadeamento de propriedades de bancos de dados ao definir sua opção **encadeamento de propriedades de bancos de dados** como 0. Para obter informações sobre como habilitar o encadeamento, veja [Opção cross db ownership chaining de configuração de servidor](../../database-engine/configure-windows/cross-db-ownership-chaining-server-configuration-option.md).  
  
-   Quando anexar um banco de dados replicado que foi copiado em vez de desanexado:  
  
    -   Se você anexar o banco de dados a uma versão atualizada da mesma instância do servidor, será necessário executar **sp_vupgrade_replication** para atualizar a replicação após a conclusão da operação de anexação. Para obter mais informações, veja [sp_vupgrade_replication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-vupgrade-replication-transact-sql).  
  
    -   Se você anexar o banco de dados a uma instância de servidor diferente (independentemente da versão), deverá executar **sp_removedbreplication** para remover a replicação após a conclusão da operação de anexação. Para obter mais informações, veja [sp_removedbreplication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql).  
  
###  <a name="Recommendations"></a> Recomendações  
 Não é recomendável anexar ou restaurar bancos de dados de origem desconhecida ou não confiável. Esses bancos de dados podem conter um código mal-intencionado que pode executar um código [!INCLUDE[tsql](../../includes/tsql-md.md)] inesperado ou provocar erros modificando o esquema ou a estrutura física do banco de dados. Antes de usar um banco de dados de origem desconhecida ou não confiável, execute [DBCC CHECKDB](/sql/t-sql/database-console-commands/dbcc-checkdb-transact-sql) no banco de dados, em um servidor que não seja de produção. Além disso, examine o código, como procedimentos armazenados ou outro código definido pelo usuário, no banco de dados.  
  
##  <a name="SSMSProcedure"></a> Para atualizar um banco de dados usando desanexar e anexar  
  
1.  Desanexe o banco de dados. Para obter mais informações, veja [Desanexar um banco de dados](detach-a-database.md).  
  
2.  Opcionalmente, mova o arquivo ou arquivos de banco de dados desanexados e o arquivo ou arquivos de log.  
  
     Você deverá mover os arquivos de log junto com os arquivos de dados, mesmo se pretender criar novos arquivos de log. Em alguns casos, reanexar um banco de dados exige seus arquivos de log existentes. Portanto, mantenha todos os arquivos de log desanexados até que o banco de dados seja anexado com êxito sem eles.  
  
    > [!NOTE]  
    >  Se você tentar anexar o banco de dados sem especificar o arquivo de log, a operação de anexação procurará o arquivo de log em seu local original. Se ainda existir uma cópia original do log nesse local, essa cópia será anexada. Para evitar a utilização do arquivo de log original, especifique o caminho do novo arquivo de log ou remova a cópia original do arquivo de log (depois de copiá-la para o novo local).  
  
3.  Anexe os arquivos copiados à instância do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Para obter mais informações, consulte [Attach a Database](attach-a-database.md).  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir atualiza uma cópia de um banco de dados de uma versão anterior do SQL Server. As instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] são executadas em uma janela do Editor de Consultas conectada à instância do servidor à qual está anexado.  
  
1.  Desanexe o banco de dados executando as seguintes instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] :  
  
    ```  
    USE master;  
    GO  
    EXEC sp_detach_db @dbname = N'MyDatabase';  
    GO  
    ```  
  
2.  Usando o método de sua escolha, copie os arquivos de dados e log no novo local.  
  
    > [!IMPORTANT]  
    >  Para um banco de dados de produção, coloque o banco de dados e o log de transações em discos separados.  
  
     Para copiar arquivos pela rede para um disco ou um computador remoto, utilize o nome UNC (Convenção Universal de Nomenclatura) do local remoto. Um nome UNC possui o formato **\\\\**_Servername_**\\**_Sharename_**\\**_Path_**\\**_Filename_. Assim como ocorre com a gravação de arquivos no disco rígido local, deverão ser concedidas, à conta do usuário utilizada pela instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], as permissões apropriadas exigidas para ler ou gravar em um arquivo no disco remoto.  
  
3.  Anexe o banco de dados movido e, opcionalmente, seu log executando a seguinte instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] :  
  
    ```  
    USE master;  
    GO  
    CREATE DATABASE MyDatabase   
        ON (FILENAME = 'C:\MySQLServer\MyDatabase.mdf'),  
        (FILENAME = 'C:\MySQLServer\Database.ldf')  
        FOR ATTACH;  
    GO  
    ```  
  
     No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], um banco de dados anexado recentemente não fica imediatamente visível no Pesquisador de Objetos. Para exibir o banco de dados, no Pesquisador de Objetos, clique em **Exibir** e depois em **Atualizar**. Quando o nó **Bancos de Dados** for expandido no Pesquisador de Objetos, o banco de dados recentemente anexado será exibido na lista de bancos de dados.  
  
##  <a name="FollowUp"></a> Acompanhamento: Depois de atualizar um banco de dados do SQL Server  
 Se o banco de dados tiver índices de texto completo, o processo de atualização importará, redefinirá ou recriará esses índices, dependendo da configuração da propriedade de servidor **upgrade_option** . Se a opção de atualização for definida como importar (**upgrade_option** = 2) ou recriar (**upgrade_option** = 0), os índices de texto completo permanecerão indisponíveis durante a atualização. Dependendo da quantidade de dados a serem indexados, a importação pode levar várias horas, e a recriação pode ser até dez vezes mais demorada. Lembre-se também de que, quando a opção de atualização estiver definida para importar, os índices de texto completo associados serão recriados se um catálogo de texto completo não estiver disponível. Para alterar a configuração da propriedade de servidor **upgrade_option** , use [sp_fulltext_service](/sql/relational-databases/system-stored-procedures/sp-fulltext-service-transact-sql).  
  
### <a name="database-compatibility-level-after-upgrade"></a>Nível de compatibilidade do banco de dados após a atualização  
 Se o nível de compatibilidade de um banco de dados de usuário for 100 ou mais alto antes da atualização, ele permanecerá o mesmo depois da atualização. Se o nível de compatibilidade for 90 ou inferior antes da atualização, no banco de dados atualizado, o nível de compatibilidade será definido como 100, que é o nível de compatibilidade mais baixo com suporte no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Para obter mais informações, veja [Nível de compatibilidade de ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-compatibility-level).  
  
### <a name="managing-metadata-on-the-upgraded-server-instance"></a>Gerenciando metadados na instância do servidor atualizado  
 Quando você anexa um banco de dados à outra instância do servidor, para oferecer uma utilização consistente aos usuários e aplicativos, pode ser necessário recriar alguns, ou todos os metadados, para o banco de dados, como logons, trabalhos e permissões, na outra instância do servidor. Para obter mais informações, consulte [Gerenciar metadados ao disponibilizar um banco de dados em outra instância do servidor &#40;SQL Server&#41;](manage-metadata-when-making-a-database-available-on-another-server.md).  
  
### <a name="service-master-key-and-database-master-key-encryption-changes-from-3des-to-aes"></a>A Chave mestra de serviço e a Criptografia de Chave Mestra de Banco de dados é alterada de 3DES para AES  
 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e versões posteriores usam o algoritmo de criptografia AES para proteger a SMK (chave mestra de serviço) e a DMK (chave mestra de banco de dados). O AES é um algoritmo de criptografia mais novo que o 3DES usado em versões anteriores. Quando um banco de dados é anexado ou restaurado pela primeira vez a uma nova instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], uma cópia da chave mestra de banco de dados (criptografada pela chave mestra de serviço) ainda não está armazenada no servidor. Você deve usar a instrução `OPEN MASTER KEY` para descriptografar a chave mestra do banco de dados (DMK). Uma vez que a DMK foi descriptografada, você tem a opção de permitir a descriptografia automática futuramente usando a instrução `ALTER MASTER KEY REGENERATE` para fornecer ao servidor uma cópia da DMK criptografada com a SMK. Quando um banco de dados for atualizado de uma versão anterior, a DMK deverá ser regenerada para usar o algoritmo AES mais recente. Para obter mais informações sobre como regenerar a DMK, veja [ALTER MASTER KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-master-key-transact-sql). O tempo necessário para regenerar a chave DMK para atualizar o AES depende do número de objetos protegidos pela DMK. É necessário regenerar a chave DMK para atualizar o AES somente uma vez, isso não tem impacto sobre regenerações futuras como parte de uma estratégia de rotação de chave.  
  
  
