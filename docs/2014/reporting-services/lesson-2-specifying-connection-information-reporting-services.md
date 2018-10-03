---
title: 'Lição 2: Especificando informações de conexão (Reporting Services) | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 54405a3a-d7fa-4d95-8963-9aa224e5901e
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 75022350450358c22c53851939faa2ae7b10c8e0
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48200036"
---
# <a name="lesson-2-specifying-connection-information-reporting-services"></a>Lição 2: Especificando informações sobre conexão (Reporting Services)
  Depois de adicionar um relatório ao projeto Tutorial, é necessário definir uma *fonte de dados*, que são informações de conexão usadas pelo relatório para acessar dados de um banco de dados relacional, banco de dados multidimensional ou outro recurso.  
  
 Nesta lição, você usará o banco de dados de exemplo do [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] como a fonte de dados. Este tutorial assume que esse banco de dados está localizado em uma instância padrão do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../includes/ssde-md.md)] instalada no computador local.  
  
### <a name="to-set-up-a-connection"></a>Para configurar uma conexão  
  
1.  No painel **Dados do Relatório** , clique em **Nova** e em **Fonte de Dados…**.  
  
    > [!NOTE]  
    >  Se o painel **Dados do Relatório** não estiver visível, no menu **Exibir** , clique em **Dados do Relatório**.  
  
2.  Na **nome**, tipo [!INCLUDE[ssSampleDBUserInputNonLocal](../includes/sssampledbuserinputnonlocal-md.md)].  
  
3.  Garanta que a opção **Conexão inserida** está selecionada.  
  
4.  Em **Tipo**, selecione **Microsoft SQL Server**.  
  
5.  Em **Cadeia de conexão**, digite o seguinte:  
  
    ```  
    Data source=localhost; initial catalog=AdventureWorks2012  
    ```  
  
     Esta cadeia de conexão assume que o [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], o servidor de relatório e o banco de dados [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] estão instalados no computador local e que você tem permissão para fazer logon no banco de dados [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] .  
  
    > [!NOTE]  
    >  Se estiver usando o [!INCLUDE[ssExpress](../includes/ssexpress-md.md)] com Serviços Avançados ou uma instância nomeada, a cadeia de conexão deverá incluir informações da instância:  
    >   
    >  `Data source=localhost\SQLEXPRESS; initial catalog=AdventureWorks2012`  
    >   
    >  Para obter mais informações sobre cadeias de caracteres de conexão, consulte [conexões de dados, fontes de dados e cadeias de caracteres de Conexão no Reporting Services](data-connections-data-sources-and-connection-strings-in-reporting-services.md) e [caixa de diálogo de propriedades de fonte de dados, geral](data-source-properties-dialog-box-general.md).  
  
6.  Clique em **Credenciais** no painel esquerdo e clique em **Usar Autenticação do Windows (segurança integrada)**.  
  
7.  [!INCLUDE[clickOK](../includes/clickok-md.md)] fonte de dados [!INCLUDE[ssSampleDBnormal](../includes/sssampledbnormal-md.md)] é adicionado para o **dados de relatório** painel.  
  
## <a name="next-task"></a>Próxima tarefa  
 Você definiu uma conexão com o banco de dados de exemplo [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] com êxito. Em seguida, você criará o relatório. Consulte [Lição 3: Definindo um conjunto de dados para o relatório de tabela &#40;Reporting Services&#41;](lesson-3-defining-a-dataset-for-the-table-report-reporting-services.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Conexões de dados, fontes de dados e cadeias de conexão no Reporting Services](data-connections-data-sources-and-connection-strings-in-reporting-services.md)  
  
  
