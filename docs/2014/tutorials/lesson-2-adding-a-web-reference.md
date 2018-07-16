---
title: 'Lição 2: Adicionando uma referência da Web | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: a2c2b8b8-6b13-45ca-ab3b-1582447b6807
caps.latest.revision: 29
author: craigg-msft
ms.author: douglasl
manager: craigg
ms.openlocfilehash: ff0efdd840ee2f4efb0da802da64494640911b80
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37275622"
---
# <a name="lesson-2-adding-a-web-reference"></a>Lição 2: Adicionando uma referência da Web
  Descoberta de serviço Web é o processo pelo qual um cliente localiza um serviço Web e obtém a descrição desse serviço. O processo de descoberta de serviço Web no [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] envolve questionar um site que segue um algoritmo predeterminado. O objetivo do processo é localizar a descrição do serviço, que é um documento XML que usa linguagem WSDL.  
  
 A descrição do serviço descreve quais serviços estão disponíveis e como interagir com eles. Sem uma descrição de serviço, é impossível interagir programaticamente com um serviço Web.  
  
 Seu aplicativo deve ter meios para se comunicar com o serviço Web e localizá-lo em tempo de execução. A adição de uma referência da Web ao projeto para o serviço Web faz isso por meio da geração de uma classe proxy que executa a interface com o serviço Web e fornece uma representação local desse serviço. Para obter mais informações, consulte "Como gerar um proxy de serviço Web XML" na documentação do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)].  
  
### <a name="to-add-a-web-reference"></a>Para adicionar uma referência da Web  
  
1.  Sobre o **Project** menu, clique em **Add Service Reference**.  
  
2.  No **adicionar referência de serviço** caixa de diálogo, clique em **avançado**.  
  
3.  No **configurações de referência de serviço** caixa de diálogo, clique em **Add Web Reference**.  
  
4.  No **URL** caixa da **Add Web Reference** caixa de diálogo, digite a URL para obter a descrição do serviço Web servidor de relatório, como http://localhost/reportserver/reportservice2010.asmx. Em seguida, clique o **vá** botão para recuperar informações sobre o serviço Web.  
  
     \- ou –  
  
     Se o serviço Web servidor de relatórios existir no computador local, clique o **serviços Web no computador local** link no painel do navegador. Em seguida, clique no link do serviço Web ReportService2010 na lista fornecida.  
  
5.  No **nome da referência Web** caixa, renomeie a referência Web como ReportService2010, que é o namespace que você usará para esta referência Web.  
  
6.  Clique em **adicionar referência** para adicionar uma referência Web para o serviço Web de destino.  
  
     O [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] baixa a descrição do serviço e gera uma classe proxy para executar a interface entre o aplicativo e o serviço Web Servidor de Relatórios. Você também precisará adicionar uma referência ao namespace <xref:System.Web.Services> para que a referência da Web funcione.  
  
7.  No menu projeto, clique em **adicionar referência**.  
  
8.  No **adicionar referência** na caixa a **.NET** guia, selecione **System**, em seguida, clique em **Okey**.  
  
 Para obter mais informações, consulte [Acessando a API SOAP](../reporting-services/report-server-web-service/accessing-the-soap-api.md).  
  
## <a name="see-also"></a>Consulte também  
 [Serviço Web do Servidor de Relatório](../reporting-services/report-server-web-service/report-server-web-service.md)   
 [Lição 3: Acessando o serviço Web](../../2014/tutorials/lesson-3-accessing-the-web-service.md)   
 [Acessando o serviço de Web do servidor de relatório usando o Visual Basic ou Visual C&#35; &#40;Tutorial do SSRS&#41;](../../2014/tutorials/access-report-server-web-service-vb-vcsharp-ssrs-tutorial.md)  
  
  
