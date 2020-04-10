---
title: SqlDependency em um aplicativo ASP.NET
description: Demonstra como usar notificações de consulta em um aplicativo ASP.NET.
ms.date: 08/15/2019
dev_langs:
- csharp
ms.assetid: ff226ce3-f6b5-47a1-8d22-dc78b67e07f5
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-kaywon
ms.openlocfilehash: 403346644d04839d1b24acd2d90e18226a951d90
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80918674"
---
# <a name="sqldependency-in-an-aspnet-application"></a>SqlDependency em um aplicativo ASP.NET

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

O exemplo nesta seção mostra como usar <xref:Microsoft.Data.SqlClient.SqlDependency> indiretamente, utilizando o objeto ASP.NET <xref:System.Web.Caching.SqlCacheDependency>. O objeto <xref:System.Web.Caching.SqlCacheDependency> usa um <xref:Microsoft.Data.SqlClient.SqlDependency> para escutar notificações e atualizar corretamente o cache.  
  
> [!NOTE]
>  O código de exemplo pressupõe que você habilitou notificações de consulta executando os scripts em [Habilitar as notificações de consulta](enable-query-notifications.md).  
  
## <a name="about-the-sample-application"></a>Sobre o aplicativo de exemplo  
O aplicativo de exemplo usa uma página da Web ASP.NET para exibir informações sobre o produto no banco de dados do SQL Server **AdventureWorks** em um controle <xref:System.Web.UI.WebControls.GridView>. Quando a página é carregada, o código grava a hora atual em um controle <xref:System.Web.UI.WebControls.Label>. Ele define um objeto <xref:System.Web.Caching.SqlCacheDependency> e as propriedades no objeto <xref:System.Web.Caching.Cache> para armazenar os dados do cache por até três minutos. O código se conecta ao banco de dados e recupera os dados. Quando a página é carregada e o aplicativo está em execução, o ASP.NET recuperará os dados do cache, que você pode verificar observando que a hora na página não é alterada. Se os dados que estão sendo monitorados forem alterados, o ASP.NET invalidará o cache e preencherá novamente o controle `GridView` com os dados atualizados, atualizando a hora exibida no controle `Label`.  
  
## <a name="creating-the-sample-application"></a>Criar o aplicativo de exemplo  
Siga estas etapas para criar e executar o aplicativo de exemplo:  
  
1. Criar um site do ASP.NET.  
  
2. Adicione um <xref:System.Web.UI.WebControls.Label> e um controle <xref:System.Web.UI.WebControls.GridView> à página Default.aspx.  
  
3. Abra o módulo de classe da página e adicione as seguintes diretivas:  
  
    ```csharp  
    using Microsoft.Data.SqlClient;  
    using System.Web.Caching;  
    ```  
  
4. Adicione o seguinte código no evento `Page_Load` da página:  
  
    [!code-csharp[DataWorks SqlDependency_Start#1](~/../sqlclient/doc/samples/SqlDependency_Start.cs#1)]
  
5. Adicione dois métodos auxiliares, `GetConnectionString` e `GetSQL`. A cadeia de conexão definida usa segurança integrada. Você precisará verificar se a conta que está usando tem as permissões de banco de dados necessárias e se o banco de dados de exemplo, **AdventureWorks**, tem notificações habilitadas.
  
    [!code-csharp[DataWorks SqlDependency_Start#2](~/../sqlclient/doc/samples/SqlDependency_Start.cs#2)]
  
### <a name="testing-the-application"></a>Testando o aplicativo  
O aplicativo armazenará em cache os dados exibidos no formulário da Web e os atualizará a cada três minutos se não houver atividade. Se ocorrer uma alteração no banco de dados, o cache será atualizado imediatamente. Execute o aplicativo no Visual Studio, que carrega a página para o navegador. O tempo de atualização do cache exibido indica quando o cache foi atualizado pela última vez. Aguarde três minutos e atualize a página, fazendo ocorrer um evento de postback. Observe que a hora exibida na página foi alterada. Se você atualizar a página em menos de três minutos, a hora exibida na página permanecerá a mesma.  
  
Agora atualize os dados no banco de dados, usando um comando UPDATE Transact-SQL e atualize a página. A hora exibida agora indica que o cache foi atualizado com os novos dados do banco de dados. Observe que, embora o cache seja atualizado, a hora exibida na página não é alterada até que ocorra um evento de postback.  
  
## <a name="next-steps"></a>Próximas etapas
- [Notificações de consulta no SQL Server](query-notifications-sql-server.md)
