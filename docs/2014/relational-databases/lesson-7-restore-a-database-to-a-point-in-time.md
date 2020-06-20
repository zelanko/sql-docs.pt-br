---
title: 'Lição 8: Restaurar um banco de dados no armazenamento do Azure | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: a9f99670-e1de-441e-972c-69faffcac17a
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: b500c2c9a2e725577ac542b738f2ea6a536cfe34
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85024939"
---
# <a name="lesson-8-restore-a-database-to-azure-storage"></a>Lição 8: Restaurar um banco de dados no Armazenamento do Microsoft Azure
  Nesta lição, você aprenderá a criar um arquivo de backup localmente e, em seguida, restaurá-lo no armazenamento do Azure. Observe que você pode ter seu banco de dados no local ou em uma máquina virtual no Azure. Para acompanhar esta lição, você não precisará concluir as lições 4, 5, 6 e 7.  
  
 Esta lição supõe que você já concluiu as seguintes etapas:  
  
-   Você tem uma conta de armazenamento do Azure.  
  
-   Você criou um contêiner em sua conta de armazenamento do Azure.  
  
-   Você criou uma política em um contêiner com direitos de leitura, gravação e lista. Você também gerou uma chave de SAS.  
  
-   Você criou uma credencial do SQL Server no computador de origem com base na Assinatura de Acesso Compartilhado.  
  
-   Você criou um banco de dados no computador de origem.  
  
 Para restaurar um banco de dados no armazenamento do Azure, você pode seguir estas etapas:  
  
1.  No computador de origem, inicie o SQL Server Management Studio.  
  
2.  Quando conectado ao banco de dados recém-criado, abra a janela de consulta. Execute a seguinte instrução:  
  
    ```sql  
  
    USE TestDB3Restore;   
    GO   
    BACKUP DATABASE TestDB3Restore   
    TO DISK = 'C:\BACKUP\TestDB3Restore.Bak'   
       WITH FORMAT,   
       NAME = 'Full Backup of TestDB3Restore'   
    GO  
  
    ```  
  
3.  Depois, copie e execute as seguintes instruções na janela Consulta.  
  
    ```sql  
  
    USE master;   
    GO   
    RESTORE DATABASE TestDB3Restore    
    FROM DISK = 'C:\BACKUP\TestDB3Restore.bak'    
    WITH REPLACE,   
    MOVE 'TestDB3Restore' TO 'https://teststorageaccnt.blob.core.windows.net/testcontainrestore/TestDB3Restore.mdf',     
    MOVE 'TestDB3Restore_log' TO 'https://teststorageaccnt.blob.core.windows.net/testcontainrestore/TestDB3Restore_log.ldf';   
    GO  
  
    ```  
  
     No final dessa etapa, o contêiner listará os dados (.mdf) e os arquivos (.ldf) no Portal de Gerenciamento.  
  
 Para restaurar um banco de dados com arquivos de log e de logs apontando para o armazenamento do Azure usando SQL Server Management Studio interface do usuário, execute estas etapas:  
  
1.  No Pesquisador de **objetos**, clique no nome do servidor para expandir a árvore de servidores.  
  
2.  Expanda **bancos**de dados e, em seguida, selecione o seu Database.  
  
3.  Clique com o botão direito do mouse no banco de dados, aponte para **Tarefas**e clique em **Restaurar**.  
  
4.  Na página **geral** , na seção **restaurar** origem, clique em dispositivo de **origem** .  
  
5.  Clique no botão procurar da caixa de texto dispositivo de **origem** , que abre a caixa de diálogo **selecionar dispositivos de backup** .  
  
6.  Na caixa de texto mídia de backup, selecione **arquivo**e clique no botão **Adicionar** para localizar o arquivo de backup (. bak). Clique em **OK**.  
  
7.  Clique em **arquivos** na primeira página.  
  
8.  Na seção **restaurar arquivos de banco de dados** como, em campo **restaurar como** , digite o seguinte:  
  
     Para arquivo de dados, digite: `https://teststorageaccnt.blob.core.windows.net/testrestoressms/TestRESSMS.mdf` . Para arquivo de log, digite: `https://teststorageaccnt.blob.core.windows.net/testrestoressms/TestRESSMS_log.ldf` .  
  
     ![SQL 14 CTP2](../tutorials/media/ss-was-tutlesson-8-8.gif "SQL 14 CTP2")  
  
9. Clique em **OK**.  
  
 Quando a restauração for feita, faça logon no Portal de Gerenciamento. Você verá os arquivos .mdf e .ldf no contêiner da seguinte maneira:  
  
 ![SQL 14 CTP2](../tutorials/media/ss-was-tutlesson-8-9.gif "SQL 14 CTP2")  
  
 **Próxima lição:**  
  
 [Lição 9. Restaurar um banco de dados do armazenamento do Azure](../relational-databases/lesson-8-restore-as-new-database-from-log-backup.md)  
  
  
