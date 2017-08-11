---
title: "Adicionar e verificar uma Conexão de dados (construtor de relatórios e SSRS) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 1d3b2573-e29d-480d-9dde-d26379c86618
caps.latest.revision: 11
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: f50d9023da6fb4498f159c6622ed1d6648ad57a5
ms.contentlocale: pt-br
ms.lasthandoff: 08/09/2017

---
# <a name="add-and-verify-a-data-connection-report-builder-and-ssrs"></a>Adicionar e verificar uma conexão de dados (Construtor de Relatórios e SSRS)
  No Construtor de Relatórios, você pode adicionar uma fonte de dados compartilhada do servidor de relatório ou criar uma fonte de dados inserida no relatório. No Designer de Relatórios, você pode criar uma fonte de dados compartilhada ou uma fonte de dados inserida e implantá-la em um servidor de relatório.  
  
 Para adicionar uma fonte de dados compartilhada ao relatório, procure um servidor de relatório e selecione uma fonte de dados compartilhada. A fonte de dados compartilhada no seu relatório aponta para a definição de fonte de dados compartilhada no servidor de relatório.  
  
 Para criar uma fonte de dados inserida, você deve ter informações de conexão com a fonte de dados externa e deve saber quais permissões são necessárias para acessar os dados. Em geral, essas informações derivam do proprietário da fonte de dados. Você pode testar a conexão para verificar se as credenciais especificadas são suficientes.  
  
 Para obter mais informações, consulte [Conexões de dados, fontes de dados e cadeias de conexão no Construtor de Relatórios](http://msdn.microsoft.com/library/7e103637-4371-43d7-821c-d269c2cc1b34) e [Especificar as credenciais no Construtor de Relatórios](http://msdn.microsoft.com/library/7412ce68-aece-41c0-8c37-76a0e54b6b53).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-create-a-connection-to-a-shared-data-source-in-report-builder"></a>Para criar uma conexão com uma fonte de dados compartilhada no Construtor de Relatórios  
  
1.  Na barra de ferramentas do painel Dados do Relatório, clique em **Nova** e em **Fonte de Dados**. A caixa de diálogo **Propriedades da Fonte de Dados** é aberta.  
  
2.  Na caixa de texto **Nome** , digite um nome para a fonte de dados.  
  
    > [!NOTE]  
    >  Esse é o nome salvo na definição de relatório local. Esse nome não é o nome da fonte de dados compartilhada no servidor de relatório.  
  
3.  Selecione **Usar uma conexão compartilhada ou modelo de relatório**. A lista de fontes de dados compartilhadas e modelos de relatório usados recentemente é exibida. Para selecionar uma em um servidor de relatório, clique em **Procurar** e procure a pasta no servidor de relatório em que as fontes de dados compartilhadas estão disponíveis.  
  
4.  Selecione a fonte de dados compartilhada e clique em **Abrir**.  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
 A fonte de dados será exibida no painel de dados do relatório.  
  
### <a name="to-verify-a-data-connection"></a>Para verificar uma conexão de dados  
  
1.  Na barra de ferramentas no painel de dados do relatório, clique duas vezes na fonte de dados. A caixa de diálogo **Propriedades da Fonte de Dados** é aberta.  
  
2.  Clique em **Testar Conexão**.  
  
3.  Se a conexão for bem-sucedida, a seguinte mensagem aparecerá: Conexão criada com êxito". [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
4.  Se a conexão não for bem-sucedida, a seguinte mensagem aparecerá: "Não é possível conectar à fonte de dados".  
  
5.  Clique em **Detalhes**e use as informações para corrigir o problema.  
  
     Para obter mais informações, consulte [Especificar as credenciais no Construtor de Relatórios](http://msdn.microsoft.com/library/7412ce68-aece-41c0-8c37-76a0e54b6b53).  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Consulte também  
 [Conjuntos de dados de relatório &#40;SSRS&#41;](../../reporting-services/report-data/report-datasets-ssrs.md)   
 [Relatório de conjuntos de dados inseridos e compartilhados de conjuntos de dados &#40; Construtor de relatórios e SSRS &#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)   
 [Localizando, exibindo e Gerenciando relatórios &#40; Construtor de relatórios e SSRS &#41;](../../reporting-services/report-builder/finding-viewing-and-managing-reports-report-builder-and-ssrs.md)   
 [Conexões de dados, fontes de dados e cadeias de caracteres de Conexão no construtor de relatórios](http://msdn.microsoft.com/library/7e103637-4371-43d7-821c-d269c2cc1b34)  
  
  
