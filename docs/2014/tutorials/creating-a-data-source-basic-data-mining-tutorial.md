---
title: Criando uma fonte de dados (Tutorial de mineração de dados básico) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: d7107c32-69ed-49a8-9b6e-32753eebf42c
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: eb18bc37f63b74981fcccbcb889bd80dcb816d12
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63273158"
---
# <a name="creating-a-data-source-basic-data-mining-tutorial"></a>Criando uma fonte de dados (Tutorial de mineração de dados básico)
  Um *fonte de dados* é uma conexão de dados que é salvo e gerenciado no seu projeto e implantado em seu [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] banco de dados. A fonte de dados contém os nomes do servidor e o banco de dados em que a sua fonte de dados reside, além das demais propriedades de conexão necessárias.  
  
> [!IMPORTANT]  
>  O nome do banco de dados é [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)]. Se você ainda não instalou esse banco de dados, consulte o [Microsoft SQL Sample Databases](https://go.microsoft.com/fwlink/?LinkId=88417) página.  
  
### <a name="to-create-a-data-source"></a>Para criar uma fonte de dados  
  
1.  Na **Gerenciador de soluções**, clique com botão direito do **fontes de dados** pasta e selecione **nova fonte de dados**.  
  
2.  Sobre o **bem-vindo ao Assistente de fonte de dados** , clique em **próxima**.  
  
3.  Sobre o **selecione como definir a conexão** , clique em **New** para adicionar uma conexão para o [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] banco de dados.  
  
4.  No **provedor** lista **Gerenciador de Conexão**, selecione **Native OLE DB\SQL Server Native Client 11.0**.  
  
5.  No **nome do servidor** caixa, digite ou selecione o nome do servidor no qual você instalou [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)].  
  
     Por exemplo, digite **localhost** se o banco de dados estiver hospedado no servidor local.  
  
6.  No **faça logon no servidor** grupo, selecione **usar a autenticação do Windows**.  
  
    > [!IMPORTANT]  
    >  Sempre que possível, os implementadores deverão usar a Autenticação do Windows, já que ela oferece um método de autenticação mais seguro do que a Autenticação do SQL Server. No entanto, a Autenticação do SQL Server é fornecida somente para fins de compatibilidade com versões anteriores. Para obter mais informações sobre métodos de autenticação, consulte [configuração do mecanismo de banco de dados - provisionamento de conta](../../2014/sql-server/install/database-engine-configuration-account-provisioning.md).  
  
7.  No **selecione ou insira um nome de banco de dados** , selecione [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] e, em seguida, clique em **Okey**.  
  
8.  Clique em **Avançar**.  
  
9. Sobre o **informações sobre representação** , clique em **usar a conta de serviço**e, em seguida, clique em **próxima**.  
  
     Sobre o **Concluindo o assistente** página, observe que, por padrão, a fonte de dados é chamada Adventure Works DW 2012.  
  
10. Clique em **Concluir**.  
  
     A nova fonte de dados, Adventure Works DW 2012, aparece na **fontes de dados** pasta no Gerenciador de soluções.  
  
## <a name="next-task-in-lesson"></a>Próxima tarefa da lição  
 [Criar dados de um exibição da fonte &#40;Tutorial de mineração de dados básicos&#41;](../../2014/tutorials/creating-a-data-source-view-basic-data-mining-tutorial.md)  
  
## <a name="previous-task-in-lesson"></a>Tarefa anterior da lição  
 [Criando uma análise dos serviços de projeto &#40;Tutorial de mineração de dados básicos&#41;](../../2014/tutorials/creating-an-analysis-services-project-basic-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Consulte também  
 [Criar uma fonte de dados &#40;SSAS multidimensional&#41;](../analysis-services/multidimensional-models/create-a-data-source-ssas-multidimensional.md)   
 [Definindo uma fonte de dados](../analysis-services/lesson-1-2-defining-a-data-source.md)   
 [Definir opções de representação &#40;SSAS – Multidimensional&#41;](../analysis-services/multidimensional-models/set-impersonation-options-ssas-multidimensional.md)  
  
  
