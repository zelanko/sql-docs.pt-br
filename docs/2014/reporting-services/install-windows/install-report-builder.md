---
title: Instalar a versão autônoma do construtor de relatórios (construtor de relatórios) | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 6b2291bb-1d20-4d08-81cb-a16dd8e01faf
caps.latest.revision: 10
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 0fb9e6b43faf8b3ff7e0b91ccb500b94547436aa
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37305076"
---
# <a name="install-the-stand-alone-version-of-report-builder-report-builder"></a>Instalar a versão autônoma do Construtor de Relatórios (Construtor de Relatórios)
  Você pode instalar o construtor de relatórios no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] pacote de recursos a [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkID=168472) ou em um local como pasta pública para o qual o ReportBuilder3_x86.msi, o pacote do instalador do Windows para o construtor de relatórios, tem foi baixado.  
  
 Também é possível executar uma instalação de linha de comando do Construtor de Relatórios e fornecer argumentos para personalizar a instalação. Além dos parâmetros intrínsecos ao MSI padrão, você pode usar os parâmetros personalizados fornecidos pelo Construtor de Relatórios: RBINSTALLDIR e REPORTSERVERURL. RBINSTALLDIR especifica a pasta de instalação raiz para o Construtor de Relatórios. REPORTSERVERURL especifica o servidor de relatório padrão que o Construtor de Relatórios usa para salvar relatórios no servidor.  
  
 Se você quiser uma instalação completamente silenciosa, sem nenhuma interação com a interface do usuário, especifique a opção **/quiet** . Por padrão, o sinalizador de opção silenciosa suprime erros de instalação. Portanto, é recomendável incluir a opção **/l** que especifica o registro, quando você usar a opção silenciosa.  
  
> [!IMPORTANT]  
>  Os recursos de segurança do Windows Vista e do Windows 7 exigem permissões elevadas para executar operações de linha de comando e solicitarão permissão para executar a linha de comando. A instalação não é silenciosa. Para fazer a instalação silenciosa, é necessário executar a linha de comando como um administrador.  
  
### <a name="to-install-report-builder-from-the-download-site"></a>Para instalar o Construtor de Relatórios no site de download  
  
1.  Vá para [construtor de relatórios do Microsoft SQL Server 2012](http://go.microsoft.com/fwlink/?LinkID=219138) e localize a seção construtor de relatórios da página da Web.  
  
2.  Clique em **X86 pacote**.  
  
3.  No **Download do arquivo** caixa de diálogo, clique em **executar**.  
  
    > [!IMPORTANT]  
    >  Baixe apenas arquivos de origens confiáveis.  
  
4.  Na caixa de diálogo do Internet Explorer, clique em **executar**.  
  
    > [!IMPORTANT]  
    >  Execute apenas arquivos de origens confiáveis.  
  
5.  O Assistente do Construtor de Relatórios do Microsoft SQL Server é iniciado.  
  
6.  Sobre o **bem-vindo ao Assistente de instalação** , clique em **próxima**.  
  
7.  Sobre o **contrato de licença** página, leia o contrato e, em seguida, selecione o **aceito os termos do contrato de licença** opção. Clique em **Avançar**.  
  
8.  Forneça seu nome e o nome da sua empresa. Clique em **Avançar**.  
  
9. Sobre o **seleção de recursos** , opcionalmente, clique em **procurar** ou **custo de disco**. Clique em **Avançar**.  
  
    -   Clique em **procurar** para ver o local padrão do construtor de relatórios e atualizá-lo.  
  
        > [!NOTE]  
        >  A pasta de instalação padrão do construtor de relatórios é \<unidade > arquivos de Programas\Microsoft SQL Server.  
  
    -   Clique em **custo de disco** saber quanto espaço em disco o construtor de relatórios consome.  
  
        > [!NOTE]  
        >  Se um volume não tiver a quantidade suficiente de espaço livre em disco, esse volume será realçado.  
  
10. Na página **Servidor de Destino Padrão** , se desejar, forneça a URL ao servidor de relatório de destino se for diferente do padrão. Clique em **Avançar**.  
  
    > [!NOTE]  
    >  Se você planejar trabalhar com o Construtor de Relatórios quando estiver conectado a um servidor de relatório, será conveniente fornecer a URL ao servidor nesse momento. No entanto, você também pode fazer isso a partir de **opções** caixa de diálogo quando você estiver trabalhando no construtor de relatórios.  
  
11. Clique em **instalar** para concluir a instalação do construtor de relatórios.  
  
### <a name="to-install-report-builder-from-a-share"></a>Para instalar o Construtor de Relatórios de um compartilhamento  
  
1.  Contate o administrador para saber a localização do arquivo ReportBuilder3_x86.msi que é executado para instalar o Construtor de Relatórios no computador local.  
  
2.  Localize o arquivo ReportBuilder3_x86.msi, o MSI (Windows Installer Package) do Construtor de Relatórios, e clique nele.  
  
     O Assistente do Construtor de Relatórios do Microsoft SQL Server é iniciado.  
  
3.  Sobre o **bem-vindo ao Assistente de instalação** , clique em **próxima**.  
  
4.  Sobre o **contrato de licença** página, leia o contrato e, em seguida, selecione o **aceito os termos do contrato de licença** opção. Clique em **Avançar**.  
  
5.  Forneça seu nome e o nome da sua empresa. Clique em **Avançar**.  
  
6.  Sobre o **seleção de recursos** , opcionalmente, clique em **procurar** ou **custo de disco**. Clique em **Avançar**.  
  
    -   Clique em **procurar** para ver o local padrão do construtor de relatórios e atualizá-lo.  
  
        > [!NOTE]  
        >  A pasta de instalação padrão do construtor de relatórios é \<unidade > arquivos de Programas\Microsoft SQL Server.  
  
    -   Clique em **custo de disco** saber quanto espaço em disco o construtor de relatórios consome.  
  
        > [!NOTE]  
        >  Se um volume não tiver a quantidade suficiente de espaço livre em disco, esse volume será realçado.  
  
7.  Na página **Servidor de Destino Padrão** , se desejar, forneça a URL ao servidor de relatório de destino se for diferente do padrão. Clique em **Avançar**.  
  
    > [!NOTE]  
    >  Se você planejar trabalhar com o Construtor de Relatórios quando estiver conectado a um servidor de relatório, será conveniente fornecer a URL ao servidor nesse momento. No entanto, você também pode fazer isso a partir de **opções** caixa de diálogo quando você estiver trabalhando no construtor de relatórios.  
  
8.  Clique em **instalar** para concluir a instalação do construtor de relatórios.  
  
### <a name="to-install-report-builder-from-the-command-line"></a>Para instalar o Construtor de Relatórios na linha de comando  
  
1.  Vá para [construtor de relatórios do Microsoft SQL Server 2012](http://go.microsoft.com/fwlink/?LinkID=219138) e localize a seção construtor de relatórios.  
  
2.  Clique em **X86 pacote**.  
  
3.  Clique em Salvar.  
  
4.  Opcionalmente, navegue até o local para salvar para verificar se o **Salvar como** opção é **pacote do Windows Installer**e, em seguida, clique em **salvar**.  
  
5.  No menu **Iniciar** , clique em **Executar**.  
  
6.  Na caixa de texto Abrir, digite `cmd.`  
  
7.  Na janela do prompt de comando, navegue até pasta em que você salvou o ReportBuilder3_x86.msi.  
  
8.  Digite um comando com o seguinte formato:  
  
     `msiexec/i ReportBuilder3_.msi /option [value] [/option [value]]`  
  
     As duas opções específicas para instalar o Construtor de Relatórios são: RBINSTALLDIR e REPORTSERVERURL. Não é necessário incluir esses argumentos na linha de comando. O comando de linha de base é o seguinte:  
  
     `msiexec /i ReportBuilder3_x86.msi /quiet`  
  
9. Para executar o comando, pressione Enter.  
  
## <a name="see-also"></a>Consulte também  
 [Instalar, desinstalar e oferecer suporte ao construtor de relatórios](../install-uninstall-and-report-builder-support.md)   
 [Desinstalar a versão autônoma do construtor de relatórios &#40;construtor de relatórios&#41;](install-report-builder.md)  
  
  
