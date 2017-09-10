---
title: "Conecte-se o aplicativo de serviço do Power Pivot para o aplicativo Web do SharePoint na autoridade de certificação | Microsoft Docs"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: a5da8e29-7ffd-44e7-bf61-344fa5bea8ce
caps.latest.revision: 8
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: cbaf5f7fce645c4133c94a5ae1562b7aabcfc897
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="connect-power-pivot-service-app-to-sharepoint-web-app-in-ca"></a>Conecte-se o aplicativo de serviço do Power Pivot para o aplicativo Web do SharePoint na autoridade de certificação
  Um aplicativo de serviço do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] pode ser usado por qualquer número de aplicativos Web do SharePoint no farm. Para disponibilizar um aplicativo de serviço do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , adicione-o a uma lista de associações de serviço.  
  
> [!IMPORTANT]  
>  Deve haver apenas um aplicativo do serviço [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] no grupo padrão para garantir o funcionamento correto do Painel de Gerenciamento [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Não adicione mais de um aplicativo de serviço do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] ao grupo padrão. A adição de várias entradas do mesmo tipo de aplicativo do serviço não é uma configuração compatível e pode causar erros. Se você estiver criando aplicativos de serviço adicionais, adicione-os a listas personalizadas.  
  
 Este tópico contém as seguintes seções:  
  
 [Adicionar um aplicativo de serviço do Power Pivot ao grupo padrão](#default)  
  
 [Adicionar um aplicativo de serviço do Power Pivot a uma lista de associações de serviço personalizada](#custom)  
  
##  <a name="default"></a> Adicionar um aplicativo de serviço ao grupo padrão  
 Uma lista de associações de serviço é uma lista de serviços compartilhados que fornece recursos a outros aplicativos Web do SharePoint no farm. Há um grupo padrão de associações de serviço para o farm.  
  
 Para constar na lista, um aplicativo de serviço do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] pode ser adicionado quando você cria o aplicativo, ou posteriormente, usando as etapas a seguir.  
  
1.  Na Administração Central, em **Gerenciamento de Aplicativo**, clique em **Configurar associações de aplicativos de serviço**.  
  
2.  Em Grupo Proxy de Aplicativo, clique em **padrão**.  
  
3.  Marque a caixa de seleção ao lado do aplicativo de serviço [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] (indicado pelo nome do tipo **Power Pivot Service Application Proxy (Proxy de Aplicativo de Serviço Power Pivot)**). Se houver mais de um aplicativo de serviço do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , escolha apenas um.  
  
4.  Clique em **OK**.  
  
##  <a name="custom"></a> Adicionar um aplicativo de serviço do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] a uma lista de associações de serviço personalizada  
 O grupo padrão pode ser substituído por uma lista personalizada. Uma lista personalizada é criada especificamente para um único aplicativo Web do SharePoint. Ela substitui o grupo padrão e o substitui por apenas uma dessas associações de serviço que um administrador de farm ou serviço especifica. Se você criou vários aplicativos de serviço do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , deverá usar uma lista personalizada para especificar o que será usado. Uma lista personalizada não pode ser reutilizada por outros aplicativos Web. Ela só se aplica ao aplicativo Web para o qual foi criada.  
  
1.  Na Administração Central, em **Gerenciamento de Aplicativo**, clique em **Gerenciar aplicativos Web**.  
  
2.  Selecione o aplicativo (por exemplo, SharePoint -80).  
  
3.  Em Aplicativos Web, em Gerenciar, clique em **Conexões de Serviço**.  
  
4.  Em **Editar o seguinte grupo de conexões**, selecione **[personalizado]**.  
  
5.  Marque a caixa de seleção ao lado de cada conexão de aplicativo de serviço a ser usada. Se você tiver vários aplicativos de serviço [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] (indicado por Tipo definido como **Power Pivot Service Application Proxy**[Proxy de Aplicativo de Serviço Power Pivot]), escolha apenas um.  
  
6.  Clique em **OK**.  
  
## <a name="see-also"></a>Consulte também  
 [Criar e configurar um aplicativo de serviço do Power Pivot na Administração Central](../../analysis-services/power-pivot-sharepoint/create-and-configure-power-pivot-service-application-in-ca.md)   
 [Configuração inicial (Power Pivot para SharePoint)](http://msdn.microsoft.com/en-us/3a0ec2eb-017a-40db-b8d4-8aa8f4cdc146)  
  
  
