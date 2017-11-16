---
title: "Definir dimensões vinculadas | Microsoft Docs"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- dimensions [Analysis Services], linked
- linked dimensions [Analysis Services]
ms.assetid: d5ad5eae-5dde-46a6-91c3-c8766d016dec
caps.latest.revision: 37
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: d7830d5075da8ab4b741ecb31bbdefb3acdf6cb9
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="define-linked-dimensions"></a>Definir dimensões vinculadas
  Uma dimensão vinculada baseia-se uma dimensão criada e armazenada em outro banco de dados do Analysis Services na mesma versão e no mesmo nível de compatibilidade. Usando uma dimensão vinculada, você pode criar, armazenar e manter uma dimensão em um banco de dados, ao mesmo tempo disponibilizando-o para usuários de vários bancos de dados. Para usuários, uma dimensão vinculada aparece como qualquer outra dimensão.  
  
 As dimensões vinculadas são somente leitura. Se desejar modificar a dimensão ou criar novas relações, altere a dimensão de origem e, em seguida, exclua e recrie a dimensão vinculada e suas relações. Você não pode atualizar uma dimensão vinculada para obter as alterações do objeto de origem.  
  
 Todos os grupos de medidas e dimensões relacionados devem vir do mesmo banco de dados de origem. Você não pode criar novas relações entre grupos de medidas locais e as dimensões vinculadas adicionadas ao cubo. Depois que as dimensões e os grupos de medidas vinculados foram adicionados ao cubo atual, as relações entre eles devem ser mantidas no seu banco de dados de origem.  
  
> [!NOTE]  
>  Como a atualização não está disponível, a maioria dos desenvolvedores do Analysis Services copiam as dimensões em vez de vinculá-las. Você pode copiar dimensões entre projetos dentro da mesma solução. Para obter mais informações, consulte [Atualização de uma dimensão vinculada no SSAS](http://sqlblog.com/blogs/marco_russo/archive/2006/09/12/refresh-of-a-linked-dimension-in-ssas.aspx).  
  
## <a name="prerequisites"></a>Pré-requisitos  
 O banco de dados de origem que fornece a dimensão e o banco de dados atual que o usam deve estar na mesma versão e nível de compatibilidade. Para obter mais informações, consulte [Nível de compatibilidade de um banco de dados multidimensional &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/compatibility-level-of-a-multidimensional-database-analysis-services.md).  
  
 O banco de dados de origem deve estar implantado e online. Os servidores que publicam ou consomem objetos vinculados devem ser configurados para permitir a operação (consulte abaixo).  
  
 A dimensão que você deseja usar não pode ser uma dimensão vinculada.  
  
## <a name="configure-server-to-allow-linked-objects"></a>Configurar o servidor para permitir objetos vinculados  
  
1.  No SQL Server Management Studio, conecte-se a um servidor do Analysis Services. No Pesquisador de Objetos, clique com o botão direito do mouse no nome do servidor e selecione **Facetas**.  
  
2.  Defina **LinkedObjectsLinksFromOtherInstancesEnabled** como **True** para permitir que o servidor emita solicitações de objetos vinculados que residem em bancos de dados em execução em outras instâncias.  
  
3.  Defina **LinkedObjectsLinksToOtherInstances** como **True** para permitir que o servidor solicite dados de bancos de dados vinculados em execução em outras instâncias.  
  
## <a name="create-a-linked-dimension-in-sql-server-data-tools"></a>Crie uma dimensão vinculada no SQL Server Data Tools  
  
1.  Inicie o assistente. No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], clique com o botão direito do mouse na pasta **Dimensões** em um banco de dados ou projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e clique em **Nova Dimensão Vinculada**.  
  
2.  Conecte-se ao banco de dados do Analysis Services que fornece a dimensão. Na página **Selecionar uma Fonte de Dados** do Assistente para Objetos Vinculados, escolha a fonte de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ou crie uma nova.  
  
3.  Na página **Selecionar Objetos** do assistente, escolha as dimensões que você deseja vincular a um banco de dados remoto.  
  
4.  Na página **Concluindo o Assistente** , você pode visualizar os objetos vinculados. Se você vincular uma dimensão e já existir outra com o mesmo nome, será adicionado um número ordinal (começando com "1" para o primeiro nome duplicado). Quando você concluir o assistente, a dimensão será adicionada à pasta **Dimensões** .  
  
##  <a name="bkmk_CreateNew"></a> Criar uma nova conexão de fonte de dados com um banco de dados do Analysis Services  
 Use o assistente Nova Fonte de Dados para adicionar as informações de conexão do seu projeto sobre o banco de dados do Analysis Services que fornece a dimensão. Você pode iniciar o assistente clicando em **Nova Fonte de Dados** , na página Selecionar Fonte de Dados do assistente Objetos Vinculados.  
  
1.  No Assistente para Fonte de Dados, na página Selecione como definir a conexão, clique em **Novo**.  
  
2.  No Gerenciador de Conexões, verifique se o provedor é definido como **OLE DB Nativo\Provedor Microsoft OLE DB para Analysis Services 11.0**.  
  
3.  Digite o nome do servidor (use *nomedoservidor*\\*nomedainstância* para uma instância nomeada) ou digite **localhost** para conectar-se a um servidor do Analysis Services que esteja em execução no mesmo computador.  
  
4.  Use a autenticação do Windows na conexão.  
  
5.  Em **Catálogo inicial**, clique na seta para baixo para selecionar um banco de dados nesse servidor.  
  
6.  No Assistente para Fonte de Dados, clique em **Avançar** para continuar.  
  
7.  Na página Informações sobre Representação, clique em **Usar a conta de serviço**. Clique em **Avançar**e conclua o Assistente. A conexão que você acaba de definir será selecionada no Assistente para Objetos Vinculados.  
  
## <a name="next-steps"></a>Próximas etapas  
 Não é possível alterar a estrutura de uma dimensão vinculada, portanto, você não pode exibi-la com a guia **Estrutura da Dimensão** do Designer de Dimensão. Depois de processar a dimensão vinculada, você pode exibi-la com a guia **Navegador** . Você também pode alterar seu nome e criar uma tradução para o nome.  
  
## <a name="see-also"></a>Consulte também  
 [Nível de compatibilidade de um banco de dados multidimensional &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/compatibility-level-of-a-multidimensional-database-analysis-services.md)   
 [Grupos de medidas vinculados](../../analysis-services/multidimensional-models/linked-measure-groups.md)   
 [Relações de dimensão](../../analysis-services/multidimensional-models-olap-logical-cube-objects/dimension-relationships.md)  
  
  

