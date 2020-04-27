---
title: Iniciar Construtor de Relatórios (Construtor de Relatórios) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- Report Builder, launching
- launching Report Builder
- SharePoint integration [Reporting Services], starting Report Builder
- starting Report Builder
ms.assetid: 8c8c7d2e-b315-418d-bf65-90e7685e4259
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 6fc123be862320cd35ccf4aec76d8bc9cf7877af
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66107596"
---
# <a name="start-report-builder-report-builder"></a>Iniciar o Construtor de Relatórios (Construtor de Relatórios)
  [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)]inclui [!INCLUDE[ndptecclick](../../includes/ndptecclick-md.md)] versões autônomas de construtor de relatórios. A versão [!INCLUDE[ndptecclick](../../includes/ndptecclick-md.md)] pode ser usada com o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] instalado no modo nativo ou no modo integrado do SharePoint.  
  
> [!NOTE]  
>  Não é possível instalar o Construtor de Relatórios em computadores baseados no Itanium 64. Isso se aplica ao [!INCLUDE[ndptecclick](../../includes/ndptecclick-md.md)] e às versões autônomas do Construtor de Relatórios.  
  
 Se a versão [!INCLUDE[ndptecclick](../../includes/ndptecclick-md.md)] do Construtor de Relatórios que estiver aberta for uma versão anterior, contate o administrador que pode atualizar o Gerenciador de Relatórios e o site do SharePoint para que usem a versão do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] do Construtor de Relatórios.  
  
 Você também pode usar a versão [!INCLUDE[ndptecclick](../../includes/ndptecclick-md.md)] do Construtor de Relatórios para criar relatórios em uma pasta de trabalho do [!INCLUDE[ssGeminiClient](../../includes/ssgeminiclient-md.md)] que foi publicada no SharePoint. Para obter mais informações sobre como usar [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]Construtor de relatórios com [o, consulte criar um relatório de Reporting Services com dados PowerPivot](https://go.microsoft.com/fwlink/?LinkId=185238) no TechNet.Microsoft.com.  
  
 Para iniciar o Construtor de Relatórios autônomo no menu **Iniciar** no computador local, você ou um administrador deve instalar Construtor de relatórios diretamente no seu computador antes que a ferramenta esteja disponível para uso. A versão autônoma não é instalada quando você instala o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]; é necessário baixá-la e instalá-la separadamente. Para baixar Construtor de Relatórios, consulte [Microsoft® SQL Server® 2012 Construtor de relatórios](https://go.microsoft.com/fwlink/?LinkId=401502).  
  
### <a name="to-start-report-builder-clickonce-from-report-manager"></a>Para iniciar o Construtor de Relatórios ClickOnce a partir do Gerenciador de Relatórios  
  
1.  No navegador da Web, digite a URL do servidor de relatório na barra de endereços. Por padrão, a URL é http://\<*servername*>/reports. O Gerenciador de Relatórios é aberto.  
  
2.  Clique em **Construtor de Relatórios**.  
  
     O Construtor de Relatórios é aberto e você pode criar ou abrir um relatório no servidor de relatório.  
  
### <a name="to-start-report-builder-clickonce-using-a-url"></a>Para iniciar o Construtor de Relatórios ClickOnce usando a URL  
  
1.  No seu navegador da Web, digite a seguinte URL na barra de endereços:  
  
     http://\<servername>/ReportServer/ReportBuilder/ReportBuilder_3_0_0_0. Application  
  
2.  Pressione ENTER.  
  
     O Construtor de Relatórios é aberto e você pode criar ou abrir um relatório no servidor de relatório.  
  
### <a name="to-start-report-builder-clickonce-in-sharepoint-integrated-mode"></a>Para iniciar o Construtor de Relatórios ClickOnce no modo integrado do SharePoint  
  
1.  Navegue até o site do SharePoint que contém a biblioteca desejada.  
  
2.  Abra a biblioteca.  
  
3.  Clique em **Documentos**.  
  
4.  No menu **Novo Documento** , clique em **Relatório do Construtor de Relatórios**.  
  
     O Construtor de Relatórios é aberto e você pode criar ou abrir um relatório no servidor de relatório.  
  
     **Observação** Se o menu **novo documento** não listar as opções **Construtor de relatórios relatório**, **modelo de construtor de relatórios**e fonte de dados de **relatório** , seus tipos de conteúdo precisarão ser adicionados à biblioteca do SharePoint. Para obter mais informações, consulte [adicionar tipos de conteúdo do servidor de relatório a uma biblioteca &#40;Reporting Services no modo integrado do SharePoint&#41;](../add-reporting-services-content-types-to-a-sharepoint-library.md) nos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [manuais online](https://go.microsoft.com/fwlink/?LinkId=154888) do no msdn.Microsoft.com.  
  
### <a name="to-start-report-builder-stand-alone-from-the-start-menu"></a>Para iniciar o Construtor de Relatórios autônomo no menu Iniciar  
  
1.  No menu Iniciar, clique em **todos os programas**e, em [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)] seguida, clique em **Construtor de relatórios**.  
  
2.  Clique em **Construtor de Relatórios** .  
  
     O Construtor de Relatórios é aberto e você pode criar ou abrir um relatório.  
  
3.  Para criar um novo relatório, clique no ícone do SQL Server no canto superior esquerdo do Construtor de Relatórios e clique em Novo.  
  
4.  Para abrir um relatório existente armazenado em seu computador local ou em um servidor de relatórios, clique no ícone do SQL Server no canto superior esquerdo e clique em Abrir.  
  
     Se você não vir o servidor de relatório na lista de servidores existentes, feche a caixa de diálogo **abrir relatório** e clique em **conectar** na parte inferior da Construtor de relatórios para se conectar ao servidor.  
  
## <a name="see-also"></a>Consulte Também  
 [Construtor de Relatórios no SQL Server 2014](report-builder-in-sql-server-2016.md)  
  
  
