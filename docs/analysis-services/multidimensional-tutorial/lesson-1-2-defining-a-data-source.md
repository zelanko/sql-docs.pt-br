---
title: Definindo uma fonte de dados | Microsoft Docs
ms.date: 05/06/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 6e52d6b6ef2a98089f17fe83a55d50b7693dbbc1
ms.sourcegitcommit: 54c8420b62269f6a9e648378b15127b5b5f979c1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/07/2019
ms.locfileid: "65404008"
---
# <a name="lesson-1-2---defining-a-data-source"></a>Lição 1-2 – definindo uma fonte de dados
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]

Depois de criar um projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , normalmente, você começa a trabalhar com esse projeto definindo uma ou mais fontes de dados que serão usadas pelo projeto. Ao definir uma fonte de dados, você está definindo as informações da cadeia de conexão que será usada para conectar-se à fonte de dados. Para obter mais informações, veja [Criar uma fonte de dados &#40;SSAS multidimensional&#41;](../multidimensional-models/create-a-data-source-ssas-multidimensional.md).  
  
Na tarefa a seguir, você definirá o banco de dados de exemplo do AdventureWorksDWSQLServer2012 como a fonte de dados do projeto do Tutorial do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Apesar de esse banco de dados estar hospedado no seu computador local por causa deste tutorial, os bancos de dados de origem são frequentemente hospedados em um ou mais computadores remotos.  
  
### <a name="to-define-a-new-data-source"></a>Para definir uma nova fonte de dados  
  
1.  No Gerenciador de Soluções (à direita da janela Microsoft Visual Studio), clique com o botão direito do mouse em **Fontes de Dados**e clique em **Nova Fonte de Dados**.  
  
2.  Na página **Bem-vindo ao Assistente para Fontes de Dados** do **Assistente para Fontes de Dados**, clique em **Avançar** para abrir a página **Selecionar como definir a conexão** .  
  
3.  Na página **Selecionar como definir a conexão** , você pode definir uma fonte de dados com base em uma nova conexão, em uma conexão existente ou em um objeto de fonte de dados definido anteriormente. Neste tutorial, você define uma fonte de dados com base em uma nova conexão. Verifique se a opção **Criar uma fonte de dados com base em uma conexão nova ou existente** está selecionada e clique em **Nova**.  
  
4.  Na caixa de diálogo **Gerenciador de Conexões** , você define as propriedades de conexão da fonte de dados. Na caixa de listagem **Provedor** , verifique se a opção **OLE DB Nativo\SQL Server Native Client 11.0** está selecionada.  
  
    [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] também dá suporte a outros provedores que são exibidos na lista **Provedor** .  
  
5.  Na caixa de texto **Nome do servidor** , digite **localhost**.  
  
    Para se conectar a uma instância nomeada no computador local, digite **localhost\\<instance name>**. Para conectar-se ao computador específico em vez do computador local, digite o nome do computador ou o endereço IP.  
  
6.  Verifique se a opção **Usar Autenticação do Windows** está selecionada. Na lista **Selecionar ou inserir um nome de banco de dados** , selecione **AdventureWorksDW2012**.  
  
7.  Clique em **Testar Conexão** para testar a conexão com o banco de dados.  
  
8.  Clique em **OK** e em **Avançar**.  
  
9. Na página **Informações sobre Representação** do assistente, você define as credenciais de segurança que o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] usará para se conectar à fonte de dados. A representação afeta a conta do Windows usada para conexão à fonte de dados quando a Autenticação do Windows é selecionada. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] não dá suporte à representação para o processamento de objetos OLAP. Selecione **Usar a conta de serviço**e clique em **Avançar**.  
  
10. Na página **Concluindo o Assistente** , aceite o nome padrão, **Adventure Works DW 2012**, e clique em **Concluir** para criar a nova fonte de dados.  
  
> [!NOTE]  
> Para modificar as propriedades da fonte de dados depois de criá-la, clique duas vezes na fonte de dados na pasta **Fontes de Dados** para exibir as propriedades dessa fonte de dados no **Designer de Fonte de Dados**.  
  
## <a name="next-task-in-lesson"></a>Próxima tarefa da lição  
[Definindo uma exibição da fonte de dados](lesson-1-3-defining-a-data-source-view.md)  
  
## <a name="see-also"></a>Consulte também  
[Criar uma fonte de dados &#40;SSAS multidimensional&#41;](../multidimensional-models/create-a-data-source-ssas-multidimensional.md)  
  
