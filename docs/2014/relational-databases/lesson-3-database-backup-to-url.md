---
title: 'Lição 4: Criar um banco de dados no armazenamento do Windows Azure | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: a9ae1501-b614-49d3-b975-6569da8350b2
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 7361cb5d0e68cfa3f45f46d7f99d68c88c1a556b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66090816"
---
# <a name="lesson-4-create-a-database-in-windows-azure-storage"></a>Lição 4: Criar um banco de dados no Armazenamento do Microsoft Azure
  Nesta lição, você aprenderá a criar um banco de dados usando o recurso de arquivos de dados do SQL Server no Microsoft Azure. Observe que antes desta lição, você deverá concluir as lições 1, 2 e 3. A lição 3 é uma etapa muito importante, pois você precisa armazenar informações sobre o contêiner de armazenamento do Windows Azure, e seu nome de política e chave de SAS associados no repositório de credenciais do SQL Server antes da lição 4.  
  
 Para cada contêiner de armazenamento usado por um arquivo de dados ou de log, você deve criar uma Credencial do SQL Server cujo nome corresponda ao caminho do contêiner. Em seguida, você pode criar um novo banco de dados no Armazenamento do Windows Azure.  
  
 Esta lição supõe que você já concluiu as seguintes etapas:  
  
-   Você tem uma conta de Armazenamento do Windows Azure.  
  
-   Você criou um contêiner na sua conta de Armazenamento do Windows Azure.  
  
-   Você criou uma política em um contêiner com direitos de leitura, gravação e lista. Você também gerou uma chave de SAS.  
  
-   Você criou uma credencial do SQL Server no computador de origem.  
  
 Para criar um banco de dados no Windows Azure usando o recurso de arquivos de dados do SQL Server no Armazenamento do Windows Azure, siga estas etapas:  
  
1.  Conecte-se ao SQL Server Management Studio.  
  
2.  No Pesquisador de Objetos, conecte-se à instância do Mecanismo de Banco de Dados instalado.  
  
3.  Na barra de ferramentas Padrão, clique em Nova Consulta.  
  
4.  Copie e cole o exemplo a seguir na janela de consulta, e modifique conforme necessário. Observe que o campo FILENAME faz referência ao caminho do URI do arquivo de banco de dados no contêiner de armazenamento e deve iniciar com https.  
  
    ```  
  
    --Create a database that uses a SQL Server credential    
    CREATE DATABASE TestDB1    
    ON   
    (NAME = TestDB1_data,   
       FILENAME = 'https://teststorageaccnt.blob.core.windows.net/testcontainer/TestDB1Data.mdf')   
     LOG ON   
    (NAME = TestDB1_log,   
        FILENAME = 'https://teststorageaccnt.blob.core.windows.net/testcontainer/TestDB1Log.ldf')   
    GO  
  
    ```  
  
     Adicione alguns dados ao banco de dados.  
  
    ```  
  
    USE TestDB1;   
    GO   
    CREATE TABLE Table1 (Col1 int primary key, Col2 varchar(20));   
    GO   
    INSERT INTO Table1 (Col1, Col2) VALUES (1, 'string1'), (2, 'string2');   
    GO  
  
    ```  
  
5.  Para ver o novo TestDB1 no SQL Server local, atualize os bancos de dados no Pesquisador de Objetos.  
  
6.  Da mesma forma, para ver o banco de dados recém-criado na conta de armazenamento, conecte-se à conta de armazenamento através do SQL Server Management Studio (SSMS). Para obter informações sobre como se conectar a um Armazenamento do Windows Azure usando o SQL Server Management Studio, siga essas etapas:  
  
    1.  Primeiro, obtenha as informações da conta de armazenamento. Faça logon no Portal de Gerenciamento. Em seguida, clique em **armazenamento** e escolha sua conta de armazenamento. Quando uma conta de armazenamento for selecionada, clique em **gerenciar chaves de acesso** na parte inferior da página. Isso abre uma janela de caixa de diálogo similar:  
  
         ![SQL 14 CTP2](../tutorials/media/ss-was-tutlesson-4-6-1.gif "SQL 14 CTP2")  
  
    2.  Cópia de **nome da conta de armazenamento** e **chave de acesso primária** valores para o **conectar-se ao armazenamento do Windows Azure** janela da caixa de diálogo no SSMS. Em seguida, clique em **Connect**. Isso colocará as informações sobre contêineres da conta de armazenamento no SSMS, conforme mostrado na seguinte captura de tela:  
  
         ![SQL 14 CTP2](../tutorials/media/ss-was-tutlesson-4-6-2.gif "SQL 14 CTP2")  
  
 A captura de tela a seguir demonstra o novo banco de dados criado no ambiente local e do Armazenamento do Windows Azure.  
  
 ![SQL 14 CTP2](../tutorials/media/ss-was-tutlesson-4-6-2b.gif "SQL 14 CTP2")  
  
 **Observação:** Se houver alguma referência ativa aos arquivos de dados em um contêiner, qualquer tentativa de excluir a credencial associada do SQL Server falhará. Da mesma forma, se já houver uma concessão em um arquivo de banco de dados específico em um blob e você quiser excluí-lo, primeiro você precisa interromper a concessão no blob. Para interromper a concessão, você pode usar [Lease Blob](https://msdn.microsoft.com/library/azure/ee691972.aspx).  
  
 Usando esse novo recurso, você pode configurar o SQL Server de modo que qualquer instrução CREATE DATABASE assuma como padrão um banco de dados habilitado para nuvem. Em outras palavras, você pode definir locais de dados e log padrão nas propriedades de instância do SQL Server Management Studio Server para que, a qualquer momento que criar um banco de dados, todos os arquivos de banco de dados (.mdf, .ldf) sejam criados como blobs de página no Armazenamento do Windows Azure.  
  
 Para criar um banco de dados no Armazenamento do Windows Azure usando a interface do usuário do SQL Server Management Studio, execute estas etapas:  
  
1.  No Pesquisador de Objetos, conecte-se a uma instância do Mecanismo de Banco de Dados do SQL Server e expanda-a.  
  
2.  Clique com o botão direito do mouse em Bancos de Dados e clique em Novo Banco de Dados.  
  
3.  Na janela da caixa de diálogo Novo Banco de Dados, digite um nome de banco de dados.  
  
4.  Altere os valores padrão dos arquivos de dados primários e de log de transações, na grade de arquivos de banco de dados, clique na célula apropriada e digite o novo valor. Além disso, especifique o caminho para o local do arquivo. Em Caminho, digite o caminho da URL do contêiner de armazenamento, como `https://teststorageaccnt.blob.core.windows.net/testcontainer/`. Em Nome do Arquivo, digite os nomes de arquivo físicos dos arquivos de banco de dados (.mdf, .ldf).  
  
     ![SQL 14 CTP2](../tutorials/media/ss-was-tutlesson-4-6-4.gif "SQL 14 CTP2")  
  
     Para obter mais informações, consulte [adicionar dados ou arquivos de Log para um banco de dados](databases/add-data-or-log-files-to-a-database.md).  
  
5.  Mantenha todos os outros valores padrão.  
  
6.  Clique em OK.  
  
 Para ver o novo TestDB1 no SQL Server local, atualize os bancos de dados no Pesquisador de Objetos. Da mesma forma, para ver o banco de dados recém-criado na conta de armazenamento, conecte-se à conta de armazenamento através do SQL Server Management Studio (SSMS), conforme explicado anteriormente nessa lição.  
  
 **Próxima lição:**  
  
 [Lição 5. &#40;Opcional&#41; criptografar o banco de dados usando TDE](../relational-databases/lesson-4-restore-database-to-virtual-machine-from-url.md)  
  
  
