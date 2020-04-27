---
title: Conectar um aplicativo de serviço PowerPivot a um aplicativo Web do SharePoint na administração central | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: a5da8e29-7ffd-44e7-bf61-344fa5bea8ce
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: da816635ab978e7baadfb810aed78fa0f3258dd8
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66071675"
---
# <a name="connect-a-powerpivot-service-application-to-a-sharepoint-web-application-in-central-administration"></a>Conectar um aplicativo de serviço PowerPivot a um aplicativo Web do SharePoint na Administração Central
  Um aplicativo de serviço PowerPivot pode ser usado por qualquer número de aplicativos Web do SharePoint no farm. Para disponibilizar um aplicativo de serviço PowerPivot, adicione-o a uma lista de associações de serviço.  
  
> [!IMPORTANT]  
>  Deve haver apenas um aplicativo do serviço PowerPivot no grupo padrão para garantir o funcionamento correto do Painel de Gerenciamento PowerPivot. Não adicione mais de um aplicativo de serviço PowerPivot ao grupo padrão. A adição de várias entradas do mesmo tipo de aplicativo do serviço não é uma configuração compatível e pode causar erros. Se você estiver criando aplicativos de serviço adicionais, adicione-os a listas personalizadas.  
  
 Este tópico contém as seguintes seções:  
  
 [Adicionar um aplicativo de serviço PowerPivot ao grupo padrão](#default)  
  
 [Adicionar um aplicativo de serviço PowerPivot a uma lista de associações de serviço personalizada](#custom)  
  
##  <a name="add-powerpivot-services-application-to-the-default-group"></a><a name="default"></a>Adicionar aplicativo de serviços PowerPivot ao grupo padrão  
 Uma lista de associações de serviço é uma lista de serviços compartilhados que fornece recursos a outros aplicativos Web do SharePoint no farm. Há um grupo padrão de associações de serviço para o farm.  
  
 Para constar na lista, um aplicativo de serviço PowerPivot pode ser adicionado quando você cria o aplicativo, ou posteriormente, usando as etapas a seguir.  
  
1.  Na Administração Central, em **Gerenciamento de Aplicativo**, clique em **Configurar associações de aplicativos de serviço**.  
  
2.  Em Grupo Proxy de Aplicativo, clique em **padrão**.  
  
3.  Marque a caixa de seleção ao lado do aplicativo de serviço PowerPivot (indicado pelo nome do tipo `PowerPivot Service Application Proxy`). Se houver mais de um aplicativo de serviço PowerPivot, escolha apenas um.  
  
4.  Clique em **OK**.  
  
##  <a name="add-powerpivot-services-application-a-custom-service-association-list"></a><a name="custom"></a>Adicionar um aplicativo de serviços PowerPivot a uma lista de associação de serviço personalizada  
 O grupo padrão pode ser substituído por uma lista personalizada. Uma lista personalizada é criada especificamente para um único aplicativo Web do SharePoint. Ela substitui o grupo padrão e o substitui por apenas uma dessas associações de serviço que um administrador de farm ou serviço especifica. Se você criou vários aplicativos de serviço PowerPivot, deverá usar uma lista personalizada para especificar o que será usado. Uma lista personalizada não pode ser reutilizada por outros aplicativos Web. Ela só se aplica ao aplicativo Web para o qual foi criada.  
  
1.  Na Administração Central, em **Gerenciamento de Aplicativo**, clique em **Gerenciar aplicativos Web**.  
  
2.  Selecione o aplicativo (por exemplo, SharePoint -80).  
  
3.  Em Aplicativos Web, em Gerenciar, clique em **Conexões de Serviço**.  
  
4.  Em **Editar o seguinte grupo de conexões**, selecione **[personalizado]**.  
  
5.  Marque a caixa de seleção ao lado de cada conexão de aplicativo de serviço a ser usada. Se você tiver vários aplicativos de serviço PowerPivot (indicado por Tipo definido como `PowerPivot Service Application Proxy`), escolha apenas um.  
  
6.  Clique em **OK**.  
  
## <a name="see-also"></a>Consulte Também  
 [Criar e configurar um aplicativo de serviço PowerPivot na administração central](create-and-configure-power-pivot-service-application-in-ca.md)   
 [PowerPivot para SharePoint de configuração inicial &#40;&#41;](../../sql-server/install/initial-configuration-powerpivot-for-sharepoint.md)  
  
  
