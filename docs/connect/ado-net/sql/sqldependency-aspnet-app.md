---
title: SqlDependency em um aplicativo ASP.NET
description: Demonstra como usar notificações de consulta de um aplicativo ASP.NET.
ms.date: 08/15/2019
dev_langs:
- csharp
ms.assetid: ff226ce3-f6b5-47a1-8d22-dc78b67e07f5
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: 2115d087d837118b99ee3ffded9cae0003b6d4e0
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 10/16/2019
ms.locfileid: "72451967"
---
# <a name="sqldependency-in-an-aspnet-application"></a>SqlDependency em um aplicativo ASP.NET

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[Download ADO.NET](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

O exemplo nesta seção mostra como usar <xref:Microsoft.Data.SqlClient.SqlDependency> indiretamente, aproveitando o objeto ASP.NET <xref:System.Web.Caching.SqlCacheDependency>. O objeto <xref:System.Web.Caching.SqlCacheDependency> usa uma <xref:Microsoft.Data.SqlClient.SqlDependency> para escutar notificações e atualizar corretamente o cache.  
  
> [!NOTE]
>  O código de exemplo pressupõe que você habilitou notificações de consulta executando os scripts em [habilitando notificações de consulta](enable-query-notifications.md).  
  
## <a name="about-the-sample-application"></a>Sobre o aplicativo de exemplo  
O aplicativo de exemplo usa uma única página da Web ASP.NET para exibir informações de produto do banco de dados **AdventureWorks** SQL Server em um controle de <xref:System.Web.UI.WebControls.GridView>. Quando a página é carregada, o código grava a hora atual em um controle de <xref:System.Web.UI.WebControls.Label>. Em seguida, ele define um objeto <xref:System.Web.Caching.SqlCacheDependency> e define as propriedades no objeto <xref:System.Web.Caching.Cache> para armazenar os dados de cache por até três minutos. O código, em seguida, se conecta ao banco de dados e os recupera. Quando a página for carregada e o aplicativo estiver em execução, o ASP.NET recuperará os dados do cache, que você pode verificar observando se a hora na página não é alterada. Se os dados que estão sendo monitorados forem alterados, o ASP.NET invalida o cache e preenche novamente o controle de `GridView` com dados atualizados, atualizando o tempo exibido no controle de `Label`.  
  
## <a name="creating-the-sample-application"></a>Criando o aplicativo de exemplo  
Siga estas etapas para criar e executar o aplicativo de exemplo:  
  
1. Crie um novo site do ASP.NET.  
  
2. Adicione um <xref:System.Web.UI.WebControls.Label> e um controle <xref:System.Web.UI.WebControls.GridView> à página default. aspx.  
  
3. Abra o módulo de classe da página e adicione as seguintes diretivas:  
  
    ```csharp  
    using Microsoft.Data.SqlClient;  
    using System.Web.Caching;  
    ```  
  
4. Adicione o seguinte código ao evento de `Page_Load` da página:  
  
    [!code-csharp[DataWorks SqlDependency_Start#1](~/../sqlclient/doc/samples/SqlDependency_Start.cs#1)]
  
5. Adicione dois métodos auxiliares, `GetConnectionString` e `GetSQL`. A cadeia de conexão definida usa segurança integrada. Você precisará verificar se a conta que você está usando tem as permissões de banco de dados necessárias e se o banco de dados de exemplo **AdventureWorks**tem notificações habilitadas.
  
    [!code-csharp[DataWorks SqlDependency_Start#2](~/../sqlclient/doc/samples/SqlDependency_Start.cs#2)]
  
### <a name="testing-the-application"></a>Testando o aplicativo  
O aplicativo armazena em cache os dados exibidos no formulário da Web e os atualiza a cada três minutos, se não houver atividade. Se ocorrer uma alteração no banco de dados, o cache será atualizado imediatamente. Execute o aplicativo no Visual Studio, que carrega a página no navegador. O tempo de atualização do cache exibido indica quando o cache foi atualizado pela última vez. Aguarde três minutos e, em seguida, atualize a página, fazendo com que ocorra um evento de postback. Observe que a hora exibida na página foi alterada. Se você atualizar a página em menos de três minutos, a hora exibida na página permanecerá a mesma.  
  
Agora, atualize os dados no banco de dado, usando um comando de atualização Transact-SQL e atualize a página. O tempo exibido agora indica que o cache foi atualizado com os novos dados do banco de dado. Observe que, embora o cache seja atualizado, a hora exibida na página não é alterada até que ocorra um evento de postback.  
  
## <a name="next-steps"></a>Próximas etapas
- [Notificações de consulta no SQL Server](query-notifications-sql-server.md)
