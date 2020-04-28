---
title: Instalar a versão autônoma do Construtor de Relatórios (Construtor de Relatórios) | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 6b2291bb-1d20-4d08-81cb-a16dd8e01faf
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 60a96db6a7568c2af22242f10f96e7a2abf13937
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "73637833"
---
# <a name="install-the-stand-alone-version-of-report-builder-report-builder"></a>Instalar a versão autônoma do Construtor de Relatórios (Construtor de Relatórios)
  Você pode instalar o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Construtor de relatórios do Feature Pack no centro de download da [Microsoft](https://www.microsoft.com/download/details.aspx?id=53613) ou em um local, como a pasta pública na qual o ReportBuilder3_x86. msi, o pacote de Windows Installer para Construtor de relatórios, foi baixado.  
  
 Também é possível executar uma instalação de linha de comando do Construtor de Relatórios e fornecer argumentos para personalizar a instalação. Além dos parâmetros intrínsecos ao MSI padrão, você pode usar os parâmetros personalizados fornecidos pelo Construtor de Relatórios: RBINSTALLDIR e REPORTSERVERURL. RBINSTALLDIR especifica a pasta de instalação raiz para o Construtor de Relatórios. REPORTSERVERURL especifica o servidor de relatório padrão que o Construtor de Relatórios usa para salvar relatórios no servidor.  
  
 Se você quiser uma instalação completamente silenciosa, sem nenhuma interação com a interface do usuário, especifique a opção **/quiet** . Por padrão, o sinalizador de opção silenciosa suprime erros de instalação. Portanto, é recomendável incluir a opção **/l** que especifica o registro, quando você usar a opção silenciosa.  
  
> [!IMPORTANT]  
>  Os recursos de segurança do Windows Vista e do Windows 7 exigem permissões elevadas para executar operações de linha de comando e solicitarão permissão para executar a linha de comando. A instalação não é silenciosa. Para fazer a instalação silenciosa, é necessário executar a linha de comando como um administrador.  
  
### <a name="to-install-report-builder-from-the-download-site"></a>Para instalar o Construtor de Relatórios no site de download  
  
1.  Vá para [Microsoft SQL Server 2012 Construtor de relatórios](https://go.microsoft.com/fwlink/?LinkID=219138) e localize a seção Construtor de relatórios da página da Web.  
  
2.  Clique em **pacote x86**.  
  
3.  Na caixa de diálogo **download de arquivo** , clique em **executar**.  
  
    > [!IMPORTANT]  
    >  Baixe apenas arquivos de origens confiáveis.  
  
4.  Na caixa de diálogo Internet Explorer, clique em **executar**.  
  
    > [!IMPORTANT]  
    >  Execute apenas arquivos de origens confiáveis.  
  
5.  O Assistente do Construtor de Relatórios do Microsoft SQL Server é iniciado.  
  
6.  Na página **Bem-vindo ao assistente de instalação** , clique em **Avançar**.  
  
7.  Na página **contrato de licença** , leia o contrato e, em seguida, selecione a opção **eu aceito os termos do contrato de licença** . Clique em **Avançar**.  
  
8.  Forneça seu nome e o nome da sua empresa. Clique em **Avançar**.  
  
9. Na página **seleção de recursos** , opcionalmente, clique em **procurar** ou em **custo de disco**. Clique em **Avançar**.  
  
    -   Clique em **procurar** para ver o local padrão de construtor de relatórios e atualizá-lo.  
  
        > [!NOTE]  
        >  A pasta de instalação padrão para Construtor de Relatórios \<é Drive>arquivos de Programas\Microsoft SQL Server.  
  
    -   Clique em **custo do disco** para saber a quantidade de espaço em disco que o construtor de relatórios consome.  
  
        > [!NOTE]  
        >  Se um volume não tiver a quantidade suficiente de espaço livre em disco, esse volume será realçado.  
  
10. Na página **Servidor de Destino Padrão** , se desejar, forneça a URL ao servidor de relatório de destino se for diferente do padrão. Clique em **Avançar**.  
  
    > [!NOTE]  
    >  Se você planejar trabalhar com o Construtor de Relatórios quando estiver conectado a um servidor de relatório, será conveniente fornecer a URL ao servidor nesse momento. No entanto, você também pode fazer isso na caixa de diálogo **Opções** quando estiver trabalhando no construtor de relatórios.  
  
11. Clique em **instalar** para concluir a instalação do construtor de relatórios.  
  
### <a name="to-install-report-builder-from-a-share"></a>Para instalar o Construtor de Relatórios de um compartilhamento  
  
1.  Contate o administrador para saber a localização do arquivo ReportBuilder3_x86.msi que é executado para instalar o Construtor de Relatórios no computador local.  
  
2.  Localize o arquivo ReportBuilder3_x86.msi, o MSI (Windows Installer Package) do Construtor de Relatórios, e clique nele.  
  
     O Assistente do Construtor de Relatórios do Microsoft SQL Server é iniciado.  
  
3.  Na página **Bem-vindo ao assistente de instalação** , clique em **Avançar**.  
  
4.  Na página **contrato de licença** , leia o contrato e, em seguida, selecione a opção **eu aceito os termos do contrato de licença** . Clique em **Avançar**.  
  
5.  Forneça seu nome e o nome da sua empresa. Clique em **Avançar**.  
  
6.  Na página **seleção de recursos** , opcionalmente, clique em **procurar** ou em **custo de disco**. Clique em **Avançar**.  
  
    -   Clique em **procurar** para ver o local padrão de construtor de relatórios e atualizá-lo.  
  
        > [!NOTE]  
        >  A pasta de instalação padrão para Construtor de Relatórios \<é Drive>arquivos de Programas\Microsoft SQL Server.  
  
    -   Clique em **custo do disco** para saber a quantidade de espaço em disco que o construtor de relatórios consome.  
  
        > [!NOTE]  
        >  Se um volume não tiver a quantidade suficiente de espaço livre em disco, esse volume será realçado.  
  
7.  Na página **Servidor de Destino Padrão** , se desejar, forneça a URL ao servidor de relatório de destino se for diferente do padrão. Clique em **Avançar**.  
  
    > [!NOTE]  
    >  Se você planejar trabalhar com o Construtor de Relatórios quando estiver conectado a um servidor de relatório, será conveniente fornecer a URL ao servidor nesse momento. No entanto, você também pode fazer isso na caixa de diálogo **Opções** quando estiver trabalhando no construtor de relatórios.  
  
8.  Clique em **instalar** para concluir a instalação do construtor de relatórios.  
  
### <a name="to-install-report-builder-from-the-command-line"></a>Para instalar o Construtor de Relatórios na linha de comando  
  
1.  Vá para [Microsoft SQL Server 2012 Construtor de relatórios](https://go.microsoft.com/fwlink/?LinkID=219138) e localize a seção Construtor de relatórios.  
  
2.  Clique em **pacote x86**.  
  
3.  Clique em Salvar.  
  
4.  Opcionalmente, navegue até o local para salvar, verifique se a opção **salvar como** está **Windows Installer pacote**e, em seguida, clique em **salvar**.  
  
5.  No menu **Iniciar**, clique em **Executar**.  
  
6.  Na caixa de texto Abrir, digite `cmd.`  
  
7.  Na janela do prompt de comando, navegue até pasta em que você salvou o ReportBuilder3_x86.msi.  
  
8.  Digite um comando com o seguinte formato:  
  
     `msiexec/i ReportBuilder3_.msi /option [value] [/option [value]]`  
  
     As duas opções específicas para instalar o Construtor de Relatórios são: RBINSTALLDIR e REPORTSERVERURL. Não é necessário incluir esses argumentos na linha de comando. O comando de linha de base é o seguinte:  
  
     `msiexec /i ReportBuilder3_x86.msi /quiet`  
  
9. Para executar o comando, pressione Enter.  
  
## <a name="see-also"></a>Consulte Também  
 [Instalar, desinstalar e Construtor de Relatórios suporte](../install-uninstall-and-report-builder-support.md)   
 [Desinstale a versão autônoma do Construtor de Relatórios &#40;Construtor de Relatórios&#41;](install-report-builder.md)  
  
  
