---
title: 'Lição 1: Criando um banco de dados do assinante de exemplo | Microsoft Docs'
ms.date: 05/30/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.assetid: 47a882b7-efe5-4ee6-bef4-06118eb56903
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 9cc144c8b19b2fa90e2cb867f980d9f0ad3a641b
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47813494"
---
# <a name="lesson-1-creating-a-sample-subscriber-database"></a>Lição 1: Criando um banco de dados do assinante de exemplo

Nesta lição do tutorial do [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] , você cria um banco de dados pequeno de “assinante” para armazenar dados de assinatura que serão usados por uma assinatura controlada por dados. Quando a assinatura é processada, o servidor de relatório recupera esses dados e os utiliza para personalizar a saída do relatório. Por exemplo, as linhas de dados incluem números de pedido específicos a serem usados para filtros e em quais formatos de arquivo os relatórios gerados estarão quando forem criados.  
  
Esta lição pressupõe que você esteja usando o [!INCLUDE[ssManStudioFull_md](../includes/ssmanstudiofull-md.md)] para criar um banco de dados do SQL Server.  
  
### <a name="to-create-a-sample-subscriber-database"></a>Para criar um banco de dados de assinantes de exemplo  
  
1.  Inicie o [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]e abra uma conexão com uma instância do [!INCLUDE[ssDEnoversion_md](../includes/ssdenoversion-md.md)].  
  
2.  Clique com o botão direito do mouse em Bancos de Dados e selecione **Novo Banco de Dados...**.  
  
3.  Na caixa de diálogo Novo Banco de Dados, em **Nome do Banco de Dados**, digite *Assinantes*. 
4. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
5.  Clique no botão **Nova Consulta** na barra de ferramentas.  
  
6.  Copie as seguintes instruções [!INCLUDE[tsql](../includes/tsql-md.md)] na consulta vazia:  
  
    ```  
    Use Subscribers  
    CREATE TABLE [dbo].[OrderInfo] (  
        [SubscriptionID] [int] NOT NULL PRIMARY KEY ,  
        [Order] [nvarchar] (20) NOT NULL,  
        [FileType] [bit],  
        [Format] [nvarchar] (20) NOT NULL ,  
    ) ON [PRIMARY]  
    GO  
  
    INSERT INTO [dbo].[OrderInfo] (SubscriptionID, [Order], FileType, Format)   
    VALUES ('1', 'so43659', '1', 'IMAGE')  
    INSERT INTO [dbo].[OrderInfo] (SubscriptionID, [Order], FileType, Format)   
    VALUES ('2', 'so43664', '1', 'MHTML')  
    INSERT INTO [dbo].[OrderInfo] (SubscriptionID, [Order], FileType, Format)   
    VALUES ('3', 'so43668', '1', 'PDF')  
    INSERT INTO [dbo].[OrderInfo] (SubscriptionID, [Order], FileType, Format)   
    VALUES ('4', 'so71949', '1', 'Excel')  
    GO  
    ```  
  
7.  Clique em **! Execute**  na barra de ferramentas.  
  
8.  Use uma instrução SELECT para verificar se há três linhas de dados. Por exemplo: `select * from OrderInfo`  
  
## <a name="next-steps"></a>Next Steps  
+ Você criou com êxito os dados de assinatura que controlarão a distribuição de relatórios e modificarão a saída de relatório para cada assinante. 
+ Em seguida, você modificará as propriedades de fonte de dados do relatório para usar credenciais armazenadas. 
+ Você também modificará o design do relatório para incluir um parâmetro que a assinatura usará com os dados do assinante. [Lição 2: Modificando as propriedades da fonte de dados do relatório](../reporting-services/lesson-2-modifying-the-report-data-source-properties.md).  

## <a name="next-steps"></a>Próximas etapas

[Criar uma assinatura controlada por dados](../reporting-services/create-a-data-driven-subscription-ssrs-tutorial.md)  
[Criar um banco de dados](../relational-databases/databases/create-a-database.md)  
[Criar um relatório de tabela básico](../reporting-services/create-a-basic-table-report-ssrs-tutorial.md)  

Ainda tem dúvidas? [Experimente perguntar no fórum do Reporting Services](http://go.microsoft.com/fwlink/?LinkId=620231)
