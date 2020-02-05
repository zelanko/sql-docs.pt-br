---
title: Publicar um banco de dados (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
ms.assetid: 98b2914e-7147-40af-ba7d-87253bbe8bf9
author: stevestein
ms.author: sstein
ms.openlocfilehash: bbcec1ab749b87f37397f94425226e5f4f523132
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "72908517"
---
# <a name="publish-a-database-sql-server-management-studio"></a>Publicar um banco de dados (SQL Server Management Studio)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Você pode usar o **Assistente para Gerar e Publicar Scripts** para publicar um banco de dados inteiro ou objetos de banco de dados individuais em um provedor de hospedagem Web.  
  
> [!NOTE]  
>  A funcionalidade descrita neste tópico costumava ser fornecida pelo Assistente de Publicação do Banco de Dados. A funcionalidade de publicação foi adicionada ao Assistente para Gerar e Publicar Scripts; o Assistente de Publicação do Banco de Dados foi descontinuado.  
  
## <a name="generate-and-publish-scripts-wizard"></a>Assistente para Gerar e Publicar Scripts  
 O Assistente para Gerar e Publicar Scripts pode ser usado para publicar um banco de dados ou objetos de banco de dados selecionados em um provedor de hospedagem Web. Um provedor de hospedagem Web do SQL Server é uma interface de conectividade com um serviço Web. O serviço Web é criado usando o projeto dos Serviços de Publicação de Banco de dados do Conjunto de Ferramentas de Hospedagem do SQL Server no CodePlex. O serviço Web permite que clientes do hoster da Web publiquem com facilidade seus bancos de dados para o serviço usando o Assistente para Gerar e Publicar Scripts. Para obter mais informações sobre como baixar o Conjunto de Ferramentas de Hospedagem do SQL Server, consulte [SQL Server Database Publishing Services](https://go.microsoft.com/fwlink/?LinkId=142025)(em inglês).  
  
 O Assistente para Gerar e Publicar Scripts também pode ser usado para criar um script para transferir um banco de dados.  
  
#### <a name="to-publish-a-database-to-a-web-service"></a>Para publicar um banco de dados em um serviço Web  
  
1.  No Pesquisador de Objetos, expanda **Banco de Dados**, clique com o botão direito do mouse em um banco de dados, aponte para **Tarefas**e clique em **Gerar e Publicar Scripts**. Siga as etapas no assistente para executar scripts nos objetos de banco de dados para publicação.  
  
2.  Na página **Escolher Objetos** , selecione os objetos a serem publicados no serviço Web de hospedagem.  
  
3.  Na página **Definir Opções de Script** , selecione **Publicar no Serviço Web**.  
  
    1.  Na caixa **Provedor** , especifique o provedor para seu serviço Web. Se você não configurou um provedor de hospedagem Web, selecione **Gerenciar Provedores** e use a caixa de diálogo **Gerenciar Provedores** para configurar um provedor para seu serviço Web.  
  
    2.  Para especificar opções de publicação avançadas, selecione o botão **Avançado** na seção **Publicar no serviço Web** .  
  
4.  Na página **Resumo** , revise suas seleções. Clique em **Anterior** para alterar suas seleções. Clique em **Próximo** para publicar os objetos selecionados.  
  
5.  Na página **Salvar ou Publicar Scripts** , monitore o progresso da publicação.  

## <a name="see-also"></a>Consulte Também  
 [Gerar scripts &#40;SQL Server Management Studio&#41;](../../relational-databases/scripting/generate-scripts-sql-server-management-studio.md)   
 [Copiar bancos de dados para outros servidores](../../relational-databases/databases/copy-databases-to-other-servers.md)  
  
  
