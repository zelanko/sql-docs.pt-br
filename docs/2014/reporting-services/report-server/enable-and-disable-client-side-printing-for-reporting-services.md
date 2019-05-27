---
title: Habilitar e desabilitar a impressão do lado do cliente no Reporting Services | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 0e709c96-7517-4547-8ef6-5632f8118524
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: ea5016aa51a25bd296d2e77516b30b84a7a28cec
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66103927"
---
# <a name="enable-and-disable-client-side-printing-for-reporting-services"></a>Habilitar e desabilitar a impressão do lado do cliente para Reporting Services
  O [!INCLUDE[msCoName](../../includes/msconame-md.md)] controle de ActiveX **RSClientPrint**, fornece impressão do lado do cliente para relatórios exibidos em um navegador. O controle exibe uma caixa de diálogo de impressão personalizada que oferece suporte aos recursos comuns com outras caixas de diálogo de impressão. Os recursos incluem a visualização de impressão, as seleções de página para determinar páginas e intervalos específicos, as margens da página e a orientação. Embora a impressão do lado do cliente esteja habilitada por padrão, você pode desabilitar o recurso para impedi-lo de ser usado.  
  
> [!NOTE]  
>  Baixar controles ActiveX requer permissões de administrador.  
  
## <a name="downloading-the-activex-control"></a>Baixando o controle ActiveX  
 Cada usuário que deseja usar o recurso de impressão deve baixar e instalar o controle ActiveX que oferece a funcionalidade de impressão do cliente. Na primeira vez que um usuário clica o **impressora** ícone na barra de ferramentas de relatório, a Microsoft controle ActiveX é baixado no computador. Depois que o controle é baixado, a **Print** caixa de diálogo exibida sempre que o usuário clica o **impressora** ícone.  
  
 Dependendo das configurações do navegador, o usuário pode receber uma solicitação para instalar o controle, ser impedido de instalar o controle ou ter o controle instalado de maneira transparente em segundo plano.  
  
 Para [!INCLUDE[msCoName](../../includes/msconame-md.md)] Internet Explorer, as configurações que afetam a instalação e o download do controle ActiveX são especificadas por meio de **ActiveX plug-ins e controles** nó no **configurações de segurança** página para a zona de conteúdo da Web. As seguintes configurações determinam se os usuários podem baixar e executar o controle de impressão, com base nas preferências de segurança da zona da Web:  
  
-   Baixe os controles ActiveX assinados.  
  
-   Controles ActiveX de script marcados para segurança para script.  
  
-   Execute os controles ActiveX e plug-ins.  
  
 Os usuários que desejam usar **RSClientPrint** executar a impressão do lado do cliente deve habilitar o seguinte:  
  
-   **Baixar controles ActiveX assinados** e **controle de Script ActiveX marcados como seguro para script** para fins de instalação.  
  
-   **Executar controles ActiveX e plug-ins** para operações de impressão em andamento.  
  
 O **RSClientPrint** controle ActiveX é assinado, o que significa que ele contém um certificado digital válido da [!INCLUDE[msCoName](../../includes/msconame-md.md)].  
  
## <a name="enabling-and-disabling-client-side-printing"></a>Habilitando e desabilitando a impressão do lado do cliente  
 Os administradores de servidor de relatório tem a opção de desabilitar o recurso de impressão, definindo a propriedade de sistema do servidor de relatório **EnableClientPrinting** para `false`. Isso desabilitará a impressão do lado do cliente para todos os relatórios gerenciados por esse servidor. Por padrão, **EnableClientPrinting** é definido como `true`. Você pode desabilitar a impressão do lado do cliente das seguintes formas:  
  
-   Para um **Servidor de relatório no modo nativo**:  
  
    1.  Inicie o [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] com privilégios administrativos.  
  
    2.  Conecte-se a uma instância do servidor de relatório no [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)].  
  
    3.  Clique com o botão direito do mouse no nó do servidor de relatório e clique em **Propriedades**. Se a opção **Propriedades** estiver desabilitada, verifique se você iniciou o [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] com privilégios administrativos.  
  
    4.  Selecione **habilitar download para o controle de impressão do cliente ActiveX**.  
  
    5.  Clique em **OK**.  
  
-   Para um **servidor de relatório no modo do SharePoint**:  
  
    1.  Na Administração Central do SharePoint, clique em **Gerenciamento de Aplicativos**.  
  
    2.  Clique em **Gerenciar aplicativos de serviço**.  
  
    3.  Clique no nome do aplicativo de serviço do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e clique em **Gerenciar** na faixa de opções do SharePoint.  
  
    4.  Clique em **Configurações do Sistema**.  
  
    5.  Selecione **Habilitar Impressão de Cliente**. A opção **Habilitar Impressão de Cliente** está próxima à parte inferior da página.  
  
    6.  Clique em **OK**.  
  
-   Escreva um script ou código para definir a propriedade de sistema do servidor de relatório **EnableClientPrinting** para `false.`  
  
 O exemplo de script a seguir ilustra uma abordagem para desabilitar a impressão do lado do cliente. Compile e execute o seguinte código [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] para definir a propriedade **EnableClientPrinting** como **False**. Depois de executar o código, reinicialize o IIS.  
  
### <a name="sample-script"></a>Exemplo de Script  
  
```  
Imports System  
Imports System.Web.Services.Protocols  
Class Sample  
   Public Shared Sub Main()  
Dim rs As New ReportingService()  
      rs.Credentials = System.Net.CredentialCache.DefaultCredentials  
        Dim props(0) As [Property]  
        Dim setProp As New [Property]  
        setProp.Name = "EnableClientPrinting"  
        setProp.Value = "False"   
        props(0) = setProp  
        Try  
            rs.SetSystemProperties(props)  
        Catch ex As System.Web.Services.Protocols.SoapException  
            Console.Write(ex.Detail.InnerXml)  
        Catch e as Exception  
            Console.Write(e.Message)  
        End Try  
    End Sub 'Main  
End Class 'Sample  
```  
  
  
