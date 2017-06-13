---
title: "Desinstalar o construtor de relatórios | Microsoft Docs"
ms.custom: 
ms.date: 05/30/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
- reporting-services-sharepoint
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 009538c6-4941-4393-b14b-9144cffdbdaf
caps.latest.revision: 10
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: ebfb5781c80cac35936dfdb9ad2e434ee5ca7f9e
ms.contentlocale: pt-br
ms.lasthandoff: 06/13/2017

---

# <a name="uninstall-report-builder"></a>Desinstalar o Construtor de Relatórios

É possível desinstalar a versão autônoma do Construtor de Relatórios no painel de controle ou na linha de comando.

A desinstalação do Construtor de Relatórios a partir da linha de comando usa a sintaxe idêntica à sintaxe usada para instalar o Construtor de Relatórios, exceto pelo uso da opção /x em vez da opção /i. As linhas de comando de desinstalação também podem incluir a opção /quiet e outras opções padrão. Se o pacote do Windows Installer do Construtor de Relatórios (ReportBuilder3_x86.msi) tiver sido removido, não será possível usar a linha de comando para desinstalar facilmente o Construtor de Relatórios. Para saber mais sobre como você pode remover o Construtor de Relatórios usando sua GUID, consulte a documentação do programa msiexec em [Opções de Linha de Comando](https://msdn.microsoft.com/library/windows/desktop/aa367988.aspx).  

Se as pastas usadas pelo Construtor de Relatórios incluírem arquivos personalizados, as pastas e os arquivos serão preservados quando o Construtor de Relatórios for removido. Apenas os arquivos do Construtor de Relatórios serão removidos.  

### <a name="to-uninstall-report-builder-from-the-control-panel"></a>Para desinstalar o Construtor de Relatórios a partir do painel de controle.

1.  No menu **Iniciar** , clique em **Painel de Controle**.  
  
2.  No Painel de Controle, clique em **Programas e Recursos**.  
  
3.  Localize [!INCLUDE[msCoName](../../includes/msconame-md.md)] construtor de relatórios do SQL Server 2016 no **nome** lista e clique nele.  
  
4.  Clique em **Desinstalar**.  
  
5.  Se solicitado a confirmar a desinstalação do Construtor de Relatórios, clique em **Sim**.  
  
### <a name="to-uninstall-report-builder-from-the-command-line"></a>Para desinstalar o Construtor de Relatórios a partir da linha de comando  
  
1.  No menu **Iniciar** , clique em **Executar**.  
  
2.  Na caixa de texto **Abrir** , digite **cmd.**  
  
3.  Na janela do prompt de comando, navegue até pasta com ReportBuilder3_x86.msi.  
  
4.  Digite uma linha de comando básica, como a seguir:  
  
 `msiexec /x ReportBuilder3_x86.msi /quiet /l*v install.log`  
  
 Se você puder incluir o registro em log, use uma linha de comando como a seguinte:  
  
 `msiexec /x ReportBuilder3_x86.msi /quiet /l*v c:\junk\install.log`  
  
5.  Pressione **Enter**.  

## <a name="next-steps"></a>Próximas etapas

[Instalar o Construtor de Relatórios](../../reporting-services/install-windows/install-report-builder.md)  

Mais perguntas? [Tente fazer o fórum do Reporting Services](http://go.microsoft.com/fwlink/?LinkId=620231)
