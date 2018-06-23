---
title: 'Lição 8: Restaurar um banco de dados para o armazenamento do Windows Azure | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: a9f99670-e1de-441e-972c-69faffcac17a
caps.latest.revision: 7
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: ea9ec20e60fb879b17434e8fe4581d28b3d7a551
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36007481"
---
# <a name="lesson-8-restore-a-database-to-windows-azure-storage"></a>Lição 8: Restaurar um banco de dados para o Armazenamento do Windows Azure
  Nesta lição, você aprenderá a criar localmente um arquivo de backup e restaurá-lo para o Armazenamento do Windows Azure. Observe que você pode ter o banco de dados no local ou em uma máquina virtual no Windows Azure. Para acompanhar esta lição, você não precisará concluir as lições 4, 5, 6 e 7.  
  
 Esta lição supõe que você já concluiu as seguintes etapas:  
  
-   Você tem uma conta de Armazenamento do Windows Azure.  
  
-   Você criou um contêiner na sua conta de Armazenamento do Windows Azure.  
  
-   Você criou uma política em um contêiner com direitos de leitura, gravação e lista. Você também gerou uma chave de SAS.  
  
-   Você criou uma credencial do SQL Server no computador de origem com base na Assinatura de Acesso Compartilhado.  
  
-   Você criou um banco de dados no computador de origem.  
  
 Para restaurar um banco de dados para o Armazenamento do Windows Azure, siga estas etapas:  
  
1.  No computador de origem, inicie o SQL Server Management Studio.  
  
2.  Quando conectado ao banco de dados recém-criado, abra a janela de consulta. Execute a seguinte instrução:  
  
    ```tsql  
  
    USE TestDB3Restore;   
    GO   
    BACKUP DATABASE TestDB3Restore   
    TO DISK = 'C:\BACKUP\TestDB3Restore.Bak'   
       WITH FORMAT,   
       NAME = 'Full Backup of TestDB3Restore'   
    GO  
  
    ```  
  
3.  Depois, copie e execute as seguintes instruções na janela Consulta.  
  
    ```tsql  
  
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
  
 Para restaurar um banco de dados com os arquivos de dados e de log que apontam para o Armazenamento do Windows Azure usando a interface do usuário do SQL Server Management Studio, execute estas etapas:  
  
1.  Em **Pesquisador de objetos**, clique no nome do servidor para expandir a árvore do servidor.  
  
2.  Expanda **bancos de dados**e, selecione seu banco de dados.  
  
3.  Clique com o botão direito do mouse no banco de dados, aponte para **Tarefas**e clique em **Restaurar**.  
  
4.  No **geral** página, o **restaurar** seção de origem, clique em **fonte** dispositivo.  
  
5.  Clique no botão Procurar para o **fonte** caixa de texto do dispositivo, que abre o **Selecione dispositivos de Backup** caixa de diálogo.  
  
6.  Na caixa de texto mídia de Backup, selecione **arquivo**e clique no **adicionar** botão para localizar o arquivo de backup (. bak). Clique em **OK**.  
  
7.  Clique em **arquivos** na primeira página.  
  
8.  No **restaurar arquivos de banco de dados** como seção, no **restaurar como** , digite o seguinte:  
  
     Arquivo de dados, digite: `https://teststorageaccnt.blob.core.windows.net/testrestoressms/TestRESSMS.mdf`. Para o arquivo de log, digite: `https://teststorageaccnt.blob.core.windows.net/testrestoressms/TestRESSMS_log.ldf`.  
  
     ![SQL 14 CTP2](../tutorials/media/ss-was-tutlesson-8-8.gif "SQL 14 CTP2")  
  
9. Clique em **OK**.  
  
 Quando a restauração for feita, faça logon no Portal de Gerenciamento. Você verá os arquivos .mdf e .ldf no contêiner da seguinte maneira:  
  
 ![SQL 14 CTP2](../tutorials/media/ss-was-tutlesson-8-9.gif "SQL 14 CTP2")  
  
 **Próxima lição:**  
  
 [Lição 9. Restaurar um banco de dados por meio do Armazenamento do Microsoft Azure](../relational-databases/lesson-8-restore-as-new-database-from-log-backup.md)  
  
  