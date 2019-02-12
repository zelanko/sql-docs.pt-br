---
title: Iniciar o construtor de relatórios (construtor de relatórios) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
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
ms.openlocfilehash: 70ec1c794e86782551099b4fb5d8459c8bae6191
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/11/2019
ms.locfileid: "56041697"
---
# <a name="start-report-builder-report-builder"></a>Iniciar o Construtor de Relatórios (Construtor de Relatórios)
  [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] inclui autônomo e [!INCLUDE[ndptecclick](../../includes/ndptecclick-md.md)] versões do construtor de relatórios. A versão [!INCLUDE[ndptecclick](../../includes/ndptecclick-md.md)] pode ser usada com o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] instalado no modo nativo ou no modo integrado do SharePoint.  
  
> [!NOTE]  
>  Não é possível instalar o Construtor de Relatórios em computadores baseados no Itanium 64. Isso se aplica ao [!INCLUDE[ndptecclick](../../includes/ndptecclick-md.md)] e às versões autônomas do Construtor de Relatórios.  
  
 Se a versão [!INCLUDE[ndptecclick](../../includes/ndptecclick-md.md)] do Construtor de Relatórios que estiver aberta for uma versão anterior, contate o administrador que pode atualizar o Gerenciador de Relatórios e o site do SharePoint para que usem a versão do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] do Construtor de Relatórios.  
  
 Você também pode usar a versão [!INCLUDE[ndptecclick](../../includes/ndptecclick-md.md)] do Construtor de Relatórios para criar relatórios em uma pasta de trabalho do [!INCLUDE[ssGeminiClient](../../includes/ssgeminiclient-md.md)] que foi publicada no SharePoint. Para obter mais informações sobre como usar o construtor de relatórios com [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)], consulte [criar um relatório do Reporting Services com dados PowerPivot](https://go.microsoft.com/fwlink/?LinkId=185238) em technet.microsoft.com.  
  
 Para iniciar o construtor de relatórios autônomo na **iniciar** menu em seu computador local, você ou um administrador deve instalar o construtor de relatórios diretamente no seu computador antes da ferramenta está disponível para uso. A versão autônoma não é instalada quando você instala o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]; é necessário baixá-la e instalá-la separadamente. Para baixar o construtor de relatórios, consulte [construtor de relatórios do Microsoft® SQL Server® 2012](https://go.microsoft.com/fwlink/?LinkId=401502).  
  
### <a name="to-start-report-builder-clickonce-from-report-manager"></a>Para iniciar o Construtor de Relatórios ClickOnce a partir do Gerenciador de Relatórios  
  
1.  No navegador da Web, digite a URL do servidor de relatório na barra de endereços. Por padrão, a URL é http://\<*servername*>/reports. O Gerenciador de Relatórios é aberto.  
  
2.  Clique em **Construtor de Relatórios**.  
  
     O Construtor de Relatórios é aberto e você pode criar ou abrir um relatório no servidor de relatório.  
  
### <a name="to-start-report-builder-clickonce-using-a-url"></a>Para iniciar o Construtor de Relatórios ClickOnce usando a URL  
  
1.  No seu navegador da Web, digite a seguinte URL na barra de endereços:  
  
     http://\<servername>/reportserver/reportbuilder/ReportBuilder_3_0_0_0.application  
  
2.  Pressione ENTER.  
  
     O Construtor de Relatórios é aberto e você pode criar ou abrir um relatório no servidor de relatório.  
  
### <a name="to-start-report-builder-clickonce-in-sharepoint-integrated-mode"></a>Para iniciar o Construtor de Relatórios ClickOnce no modo integrado do SharePoint  
  
1.  Navegue até o site do SharePoint que contém a biblioteca desejada.  
  
2.  Abra a biblioteca.  
  
3.  Clique em **Documentos**.  
  
4.  No menu **Novo Documento** , clique em **Relatório do Construtor de Relatórios**.  
  
     O Construtor de Relatórios é aberto e você pode criar ou abrir um relatório no servidor de relatório.  
  
     **Observação** se o **novo documento** menu não lista as **construtor de relatórios**, **modelo do construtor de relatórios**, e **defontededadosdorelatório** opções, seus tipos de conteúdo precisarão ser adicionados à biblioteca do SharePoint. Para obter mais informações, consulte [Adicionar servidor de tipos de conteúdo relatório em uma biblioteca do &#40;Reporting Services no modo integrado do SharePoint&#41; ](../add-reporting-services-content-types-to-a-sharepoint-library.md) na [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [Manuais Online](https://go.microsoft.com/fwlink/?LinkId=154888) em MSDN.microsoft.com.  
  
### <a name="to-start-report-builder-stand-alone-from-the-start-menu"></a>Para iniciar o Construtor de Relatórios autônomo no menu Iniciar  
  
1.  No menu Iniciar, clique em **todos os programas**e, em seguida, clique em [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)] **construtor de relatórios**.  
  
2.  Clique em **Construtor de Relatórios** .  
  
     O Construtor de Relatórios é aberto e você pode criar ou abrir um relatório.  
  
3.  Para criar um novo relatório, clique no ícone do SQL Server no canto superior esquerdo do Construtor de Relatórios e clique em Novo.  
  
4.  Para abrir um relatório existente armazenado em seu computador local ou em um servidor de relatórios, clique no ícone do SQL Server no canto superior esquerdo e clique em Abrir.  
  
     Se você não vir o servidor de relatório na lista de servidores existentes, feche o **abrir relatório** caixa de diálogo e clique **Connect** na parte inferior do construtor de relatórios para se conectar ao servidor.  
  
## <a name="see-also"></a>Consulte também  
 [Construtor de Relatórios no SQL Server 2014](report-builder-in-sql-server-2016.md)  
  
  
