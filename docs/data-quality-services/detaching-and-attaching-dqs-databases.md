---
description: Desanexando e anexando bancos de dados do DQS
title: Desanexando e anexando bancos de dados do DQS
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 830e33bc-dd15-4f8e-a4ac-d8634b78fe45
author: swinarko
ms.author: sawinark
ms.openlocfilehash: 6d59c5c92b41176cfb6a664bdf1617c164d23d30
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88462110"
---
# <a name="detaching-and-attaching-dqs-databases"></a>Desanexando e anexando bancos de dados do DQS

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sqlserver.md)]

  Este tópico descreve como desanexar e anexar os bancos de dados do DQS.  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="limitations-and-restrictions"></a><a name="Limitations"></a> Limitações e restrições  
 Para obter uma lista de limitações e restrições, veja [Anexar e desanexar bancos de dados &#40;SQL Server&#41;](../relational-databases/databases/database-detach-and-attach-sql-server.md).  
  
###  <a name="prerequisites"></a><a name="Prerequisites"></a> Pré-requisitos  
  
-   Verifique se não há nenhuma atividade ou processo em execução no DQS. Isso pode ser verificado com o uso da tela **Monitoramento de atividade** . Para obter informações detalhadas sobre como trabalhar nessa tela, consulte [Monitor DQS Activities](../data-quality-services/monitor-dqs-activities.md).  
  
-   Verifique se não há usuários conectados no [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)].  
  
###  <a name="security"></a><a name="Security"></a> Segurança  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permissões  
  
-   Sua conta de usuário do Windows deve ser um membro da função de servidor fixa db_owner na instância do SQL Server para desanexar bancos de dados DQS.  
  
-   Sua conta de usuário do Windows deve ter a permissão CREATE DATABASE, CREATE ANY DATABASE ou ALTER ANY DATABASE para anexar um banco de dados.  
  
-   Você deve ter a função dqs_administrator no banco de dados DQS_MAIN para terminar as atividades em execução ou interromper os processos em execução no DQS.  
  
##  <a name="detach-dqs-databases"></a><a name="Detach"></a> Desanexar bancos de dados DQS  
 Quando você desanexa um banco de dados DQS usando o SQL Server Management Studio, os arquivos desanexados permanecem no computador e podem ser anexados novamente à mesma instância do SQL Server ou podem ser movidos para outro servidor e anexados lá. Os arquivos de banco de dados do DQS geralmente estão disponíveis no seguinte local no computador do Data Quality Services: C:\Program Files\Microsoft SQL Server\MSSQL13.*<Instance_Name>* \MSSQL\DATA.  
  
1.  Inicie o Microsoft SQL Server Management Studio e conecte-se à instância apropriada do SQL Server.  
  
2.  No Pesquisador de Objetos, expanda o nó **Bancos de Dados** .  
  
3.  Clique com o botão direito do mouse no banco de dados **DQS_MAIN** , aponte para **Tarefas**e clique em **Desanexar**. A caixa de diálogo **Desanexar Banco de Dados** é exibida.  
  
4.  Marque a caixa de seleção na coluna **Descartar** e clique em **OK** para desanexar o banco de dados DQS_MAIN.  
  
5.  Repita as etapas 3 e 4 com os bancos de dados DQS_PROJECTS e DQS_STAGING_DATA para desanexá-los.  
  
 Você também pode desanexar bancos de dados DQS usando as instruções Transact-SQL usando o procedimento armazenado sp_detach_db. Para obter mais informações sobre como desanexar bancos de dados usando instruções Transact-SQL, consulte [Using Transact-SQL](../relational-databases/databases/detach-a-database.md#TsqlProcedure) em [Detach a Database](../relational-databases/databases/detach-a-database.md).  
  
##  <a name="attach-dqs-databases"></a><a name="Attach"></a> Anexar bancos de dados DQS  
 Use as instruções a seguir para anexar um banco de dados DQS na mesma instância do SQL Server (de onde você desanexou) ou a uma instância diferente do SQL Server em que o [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] está instalado.  
  
1.  Inicie o Microsoft SQL Server Management Studio e conecte-se à instância apropriada do SQL Server.  
  
2.  No Pesquisador de Objetos, clique com o botão direito do mouse em **Bancos de Dados**e em **Anexar**. A caixa de diálogo **Anexar Bancos de Dados** é exibida.  
  
3.  Para especificar o banco de dados a ser anexado, clique em **Adicionar**. A caixa de diálogo **Localizar Arquivos de Banco de Dados** é exibida.  
  
4.  Selecione a unidade de disco onde o banco de dados reside e expanda a árvore do diretório para localizar e selecionar o arquivo .mdf do banco de dados. Por exemplo, para o banco de dados DQS_MAIN:  
  
    ```  
    C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\DATA\DQS_MAIN.mdf  
    ```  
  
5.  O painel **detalhes do banco de dados** (inferior) exibe os nomes dos arquivos a serem anexados. Para verificar ou alterar o nome do caminho de um arquivo, clique no botão **Procurar** ( ... ).  
  
6.  Clique em **OK** para anexar o banco de dados DQS_MAIN.  
  
7.  Repita as etapas 2 a 6 para os bancos de dados DQS_PROJECTS e DQS_STAGING_DATA para anexá-los.  
  
8.  Você também deve executar as instruções Transact-SQL na próxima etapa depois de restaurar o banco de dados DQS_MAIN, caso contrário, uma mensagem de erro será exibida quando você tentar se conectar ao Data Quality Server usando o aplicativo Cliente Data Quality, e você não puder se conectar. Porém, você não precisa executar as etapas 9 e 10 se tiver acabado de anexar o banco de dados DQS_PROJECTS ou DQS_STAGING_DATA e não o DQS_MAIN.  
  
     Para executar as instruções Transact-SQL, no Pesquisador de Objetos, clique com o botão direito do mouse no servidor e clique em **Nova Consulta**.  
  
9. Na janela Editor de Consultas, copie as seguintes instruções SQL:  
  
    ```sql  
    ALTER DATABASE [DQS_MAIN] SET TRUSTWORTHY ON;  
    EXEC sp_configure 'clr enabled', 1;  
    RECONFIGURE WITH OVERRIDE;  
    ALTER DATABASE [DQS_MAIN] SET ENABLE_BROKER;  
    ALTER AUTHORIZATION ON DATABASE::[DQS_MAIN] TO [##MS_dqs_db_owner_login##];  
    ALTER AUTHORIZATION ON DATABASE::[DQS_PROJECTS] TO [##MS_dqs_db_owner_login##];  
    ```  
  
10. Pressione F5 para executar as instruções. Consulte o painel Resultados para verificar se as instruções foram executadas com êxito. Você verá a seguinte mensagem: `Configuration option 'clr enabled' changed from 1 to 1. Run the RECONFIGURE statement to install.`  
  
11. Conecte-se ao Data Quality Server usando o Cliente Data Quality para verificar se é possível conectar-se com êxito.  
  
 Você também pode anexar bancos de dados DQS usando as instruções Transact-SQL. Para obter mais informações sobre como anexar bancos de dados usando instruções Transact-SQL, consulte [Using Transact-SQL](../relational-databases/databases/attach-a-database.md#TsqlProcedure) em [Attach a Database](../relational-databases/databases/attach-a-database.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Gerenciar bancos de dados do DQS](../data-quality-services/manage-dqs-databases.md)  
  
  
