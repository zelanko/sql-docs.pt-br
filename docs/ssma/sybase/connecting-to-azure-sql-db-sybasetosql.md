---
title: Conectando-se ao BD SQL do Azure (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 9e77e4b0-40c0-455c-8431-ca5d43849aa7
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 10be1dc3652c944b9de08a01b0f4cdff5ae5849a
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "70176233"
---
# <a name="connecting-to-azure-sql-db-sybasetosql"></a>Conectar-se ao BD SQL do Azure (SybaseToSQL)
Para migrar bancos de dados Sybase para o BD SQL do Azure, você deve se conectar à instância de destino do banco de dados SQL do Azure. Quando você se conecta, o SSMA obtém metadados sobre todos os bancos de dados na instância do BD SQL do Azure e exibe os metadados do banco de dados no Gerenciador de metadados do BD SQL do Azure. O SSMA armazena informações da instância do banco de dados SQL do Azure à qual você está conectado, mas não armazena senhas.  
  
Sua conexão com o BD SQL do Azure permanece ativa até que você feche o projeto. Quando você reabrir o projeto, deverá se reconectar ao banco de BD SQL do Azure se quiser uma conexão ativa com o servidor. Você pode trabalhar offline até carregar objetos de banco de dados no BD SQL do Azure e migrá-los.  
  
Os metadados sobre a instância do BD SQL do Azure não são sincronizados automaticamente. Em vez disso, para atualizar os metadados no Gerenciador de metadados do BD SQL do Azure, você deve atualizar manualmente os metadados do BD SQL do Azure. Para obter mais informações, consulte a seção "sincronizando metadados do banco de dados SQL do Azure" mais adiante neste tópico.  
  
## <a name="required-azure-sql-db-permissions"></a>Permissões necessárias do banco de BD SQL do Azure  
A conta usada para se conectar ao BD SQL do Azure requer permissões diferentes dependendo das ações que a conta executa:  
  
1.  Para converter objetos Sybase em [!INCLUDE[tsql](../../includes/tsql-md.md)] sintaxe, atualizar metadados do BD SQL do Azure ou salvar a sintaxe convertida em scripts, a conta deve ter permissão para fazer logon na instância do BD SQL do Azure.  
  
2.  Para carregar objetos de banco de dados no BD SQL do Azure, o requisito mínimo de permissão é a associação na função de banco de dados **db_owner** no banco de dados de destino.  
  
## <a name="establishing-an-azure-sql-db-connection"></a>Estabelecendo uma conexão do BD SQL do Azure  
Antes de converter objetos de banco de dados Sybase para a sintaxe do BD SQL do Azure, você deve estabelecer uma conexão com a instância do banco de dados SQL do Azure onde você deseja migrar os bancos de  
  
Ao definir as propriedades de conexão, você também especifica o banco de dados em que os objetos e data serão migrados. Você pode personalizar esse mapeamento no nível de esquema do Sybase depois de se conectar ao banco de BD SQL do Azure. Para obter mais informações, consulte [mapeando esquemas do ase do Sybase para esquemas de SQL Server &#40;SybaseToSQL&#41;](../../ssma/sybase/mapping-sybase-ase-schemas-to-sql-server-schemas-sybasetosql.md)  
  
> [!WARNING]  
> Antes de tentar se conectar ao BD SQL do Azure, verifique se a instância do banco de BD SQL do Azure está em execução e pode aceitar conexões.  
  
**Para se conectar ao BD SQL do Azure**  
  
1.  No menu **arquivo** , selecione **conectar ao BD SQL do Azure**(essa opção é habilitada após a criação de um projeto).  
  
    Se você tiver se conectado anteriormente ao BD SQL do Azure, o nome do comando será **reconectado ao banco de BD SQL do Azure**  
  
2.  Na caixa de diálogo conexão, digite ou selecione o nome do servidor do banco de BD SQL do Azure.  
  
3.  Insira, selecione ou **procure** o nome do banco de dados.  
  
4.  Insira ou selecione o **nome de usuário**.  
  
5.  Insira a **senha**.  
  
6.  O SSMA recomenda a conexão criptografada com o banco de BD SQL do Azure.  
  
7.  Clique em **Conectar**.  
  
> [!IMPORTANT]  
> O SSMA para Sybase não oferece suporte à conexão com o banco de dados **mestre** no BD SQL do Azure.  
  
## <a name="synchronizing-azure-sql-db-metadata"></a>Sincronizando metadados do BD SQL do Azure  
Os metadados sobre os bancos de dados do Azure SQL DB não são atualizados automaticamente. Os metadados no Gerenciador de metadados do BD SQL do Azure são um instantâneo dos metadados quando você se conecta pela primeira vez ao BD SQL do Azure, ou na última vez que você atualizou os metadados manualmente. Você pode atualizar os metadados manualmente para todos os bancos de dados ou para qualquer banco de dados ou objeto de banco de dados individual.  
  
**Para sincronizar metadados**  
  
1.  Certifique-se de que você está conectado ao banco de BD SQL do Azure.  
  
2.  No Gerenciador de metadados do BD SQL do Azure, marque a caixa de seleção ao lado do banco de dados ou esquema de banco de dados que você deseja atualizar.  
  
    Por exemplo, para atualizar os metadados de todos os bancos de dados, selecione a caixa ao lado de bancos de dados.  
  
3.  Clique com o botão direito do mouse em bancos de dados ou em um esquema ou banco de dados individual e selecione **sincronizar com Banco de dados**.  
  
## <a name="next-step"></a>Próxima etapa  
A próxima etapa na migração depende de suas necessidades de projeto:  
  
-   Para personalizar o mapeamento entre esquemas do Sybase e os esquemas e bancos de dados do Azure SQL DB, consulte [mapeando esquemas do ase do Sybase para esquemas de SQL Server &#40;SybaseToSQL&#41;](../../ssma/sybase/mapping-sybase-ase-schemas-to-sql-server-schemas-sybasetosql.md)  
  
-   Para personalizar as opções de configuração para os projetos, consulte [definir opções de projeto &#40;SybaseToSQL&#41;](../../ssma/sybase/setting-project-options-sybasetosql.md)  
  
-   Para personalizar o mapeamento de tipos de dados de origem e de destino, consulte [mapeando Sybase ase e SQL Server tipos de dados &#40;SybaseToSQL&#41;](../../ssma/sybase/mapping-sybase-ase-and-sql-server-data-types-sybasetosql.md)  
  
-   Se você não precisar executar nenhuma dessas tarefas, poderá converter as definições de objeto do banco de dados Sybase em definições de objeto do BD SQL do Azure. Para obter mais informações, consulte [convertendo objetos de banco de dados do Sybase ASE &#40;SybaseToSQL&#41;](../../ssma/sybase/converting-sybase-ase-database-objects-sybasetosql.md)  
  
## <a name="see-also"></a>Consulte Também  
[Migrando bancos de dados do Sybase ASE para o SQL Server-BD SQL do Azure &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  
