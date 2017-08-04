---
title: "Acessar dados para as operações do DQS | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- data-quality-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 88dfb9ea-6321-4eaf-b9e4-45d36ef048f6
caps.latest.revision: 15
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: a03861b1706667657461ecf95196fc6cb3501d2f
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="access-data-for-the-dqs-operations"></a>Acessar dados para as operações do DQS
  Para usar seus dados de origem para operações do [!INCLUDE[ssDQSnoversion](../../includes/ssdqsnoversion-md.md)] (DQS) e exportar seus dados processados, você pode adotar um destes procedimentos:  
  
-   Copiar seus dados de origem em uma tabela/exibição no banco de dados DQS_STAGING_DATA e, depois, usá-los em operações do DQS. Você também pode exportar os dados processados para uma nova tabela no banco de dados DQS_STAGING_DATA. Para isso, sua conta de usuário do Windows deve ter acesso de leitura/gravação ao banco de dados DQS_STAGING_DATA.  
  
-   Use seu próprio banco de dados como os dados de origem em operações do DQS e destino para exportar os dados processados. Para fazer isso, verifique se o banco de dados está na mesma instância do SQL Server que os bancos de dados do Data Quality Server. Caso contrário, o banco de dados não estará disponível no cliente Data Quality para operações do DQS. Além disso, sua conta de usuário do Windows deve ter acesso ao banco de dados DQS_STAGING_DATA para exportar os resultados compatíveis porque eles são exportados em duas fases: primeiro, os resultados compatíveis são exportados para as tabelas temporárias no banco de dados DQS_STAGING_DATA e, em seguida, são movidos para a tabela no banco de dados de destino.  
  
## <a name="prerequisites"></a>Pré-requisitos  
  
-   Você precisa ter concluído a instalação do [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] executando o arquivo DQSInstaller.exe. Para obter mais informações, consulte [Executar o DQSInstaller.exe para concluir a instalação do Data Quality Server](../../data-quality-services/install-windows/run-dqsinstaller-exe-to-complete-data-quality-server-installation.md).  
  
-   Sua conta de usuário do Windows deve ser um membro da função de servidor fixa apropriada (como securityadmin, serveradmin ou sysadmin) na instância do mecanismo de banco de dados para conceder/modificar o acesso ao logon do SQL em bancos de dados.  
  
### <a name="to-grant-readwrite-access-to-a-user-on-the-dqsstagingdata-database"></a>Para conceder acesso de leitura/gravação a um Usuário no banco de dados DQS_STAGING_DATA  
  
1.  Inicie o Microsoft SQL Server Management Studio.  
  
2.  No Microsoft SQL Server Management Studio, expanda sua instância do SQL Server, expanda **Segurança**e, depois, expanda **Logons**.  
  
3.  Clique com o botão direito do mouse em um logon do SQL e clique em **Propriedades**.  
  
4.  Na caixa de diálogo **Propriedades de Logon** , clique na página **Mapeamento de Usuário** no painel esquerdo.  
  
5.  No painel direito, marque a caixa de seleção na coluna **Mapa** do banco de dados **DQS_STAGING_DATA** e selecione as seguintes funções no painel **Associação à função de banco de dados para: DQS_STAGING_DATA** :  
  
    -   **db_datareader**: ler dados de tabelas/exibições.  
  
    -   **db_datawriter**: adicionar, excluir ou alterar dados em tabelas.  
  
    -   **db_ddladmin**: criar, modificar ou excluir tabelas/exibições.  
  
6.  Na caixa de diálogo **Propriedades** , clique em **OK** para aplicar as alterações.  
  
## <a name="next-steps"></a>Próximas etapas  
 Tente realizar operações do DQS que acessam o banco de dados como fonte de dados para a operação DQS e, em seguida, exportam os dados processados para o banco de dados.  
  
## <a name="see-also"></a>Consulte também  
 [Instalar o Data Quality Services](../../data-quality-services/install-windows/install-data-quality-services.md)  
  
  
