---
title: Definir as propriedades de um Gerenciador de conexões | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- connection managers [Integration Services], modifying
- modifying connection managers
ms.assetid: 54793114-2198-4d80-8091-e241d5a5d13c
author: chugugrace
ms.author: chugu
ms.openlocfilehash: e435d5f3ea00707ba1b392058b118a06cfd7ce83
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85421603"
---
# <a name="set-the-properties-of-a-connection-manager"></a>Definir as propriedades de um Gerenciador de Conexões
  Todos os gerenciadores de conexões podem ser configurados usando a janela **Propriedades** .  
  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] também fornece caixas de diálogo personalizadas para modificar os tipos diferentes de gerenciadores de conexões em [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]. A caixa de diálogo tem um conjunto diferente de opções que dependem do tipo de gerenciador de conexões.  
  
### <a name="to-modify-a-connection-manager-using-the-properties-window"></a>Para modificar um gerenciador de conexões usando a janela Propriedades  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra o projeto do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] que contém o pacote desejado.  
  
2.  No Gerenciador de Soluções, clique duas vezes no pacote para abri-lo.  
  
3.  No SSIS Designer, clique na guia **Fluxo de Controle** , na guia **Fluxo de Dados** , ou na guia **Manipulador de Evento** para disponibilizar a área do **Gerenciador de Conexões** .  
  
4.  Clique com o botão direito do mouse no gerenciador de conexões e clique em **Propriedades**.  
  
5.  Na janela **Propriedades** , edite os valores de propriedades. A janela **Propriedades** fornece acesso a algumas propriedades que não são configuráveis no editor padrão de um gerenciador de conexões.  
  
6.  Clique em **OK**.  
  
7.  Para salvar o pacote atualizado, clique em **Salvar Itens Selecionados** no menu **Arquivo** .  
  
### <a name="to-modify-a-connection-manager-using-a-connection-manager-dialog-box"></a>Para modificar um gerenciador de conexões que usa uma caixa de diálogo de gerenciador de conexões  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra o projeto do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] que contém o pacote desejado.  
  
2.  No Gerenciador de Soluções, clique duas vezes no pacote para abri-lo.  
  
3.  No Designer [!INCLUDE[ssIS](../includes/ssis-md.md)] , clique na guia **Controle de Fluxo** , na guia **Fluxo de Dados** , ou na guia **Manipulador de Eventos** para disponibilizar o **Gerenciador de Conexões** .  
  
4.  Na área **Gerenciador de Conexões** , clique duas vezes no gerenciador de conexões para abrir a caixa de diálogo **Gerenciador de Conexões** . Para obter informações sobre tipos específicos de gerenciador de conexões e as opções disponíveis para cada tipo, veja a tabela a seguir.  
  
    |Gerenciador de conexões|Opções|  
    |------------------------|-------------|  
    |[Gerenciador de conexões ADO](connection-manager/ado-connection-manager.md)|[Configurar Gerenciador de Conexões OLE DB](configure-ole-db-connection-manager.md)|  
    |[Gerenciador de conexões ADO.NET](connection-manager/ado-net-connection-manager.md)|[Configurar Gerenciador de Conexões ADO.NET](configure-ado-net-connection-manager.md)|  
    |[Gerenciador de Conexões do Analysis Services](connection-manager/analysis-services-connection-manager.md)|[Referência da interface do usuário da caixa de diálogo Adicionar Gerenciador de Conexões do Analysis Services](connection-manager/add-analysis-services-connection-manager-dialog-box-ui-reference.md)|  
    |[Gerenciador de Conexões do Excel](connection-manager/excel-connection-manager.md)|[Editor de Gerenciador de Conexões Excel](../../2014/integration-services/excel-connection-manager-editor.md)|  
    |[Gerenciador de Conexões de Arquivos](connection-manager/file-connection-manager.md)|[Editor do Gerenciador de Conexões de Arquivos](../../2014/integration-services/file-connection-manager-editor.md)|  
    |[Gerenciador de Conexões de Vários Arquivos](connection-manager/multiple-files-connection-manager.md)|[Referência da interface do usuário da caixa de diálogo Adicionar Gerenciador de Conexões de Arquivos](connection-manager/add-file-connection-manager-dialog-box-ui-reference.md)|  
    |[Gerenciador de Conexões de Arquivos Simples](connection-manager/flat-file-connection-manager.md)|[Editor do Gerenciador de Conexões de Arquivos Simples &#40;Página Geral&#41;](general-page-of-integration-services-designers-options.md)<br /><br /> [Editor do Gerenciador de Conexões de Arquivos Simples &#40;Página Colunas&#41;](../../2014/integration-services/flat-file-connection-manager-editor-columns-page.md)<br /><br /> [Editor do Gerenciador de Conexões de Arquivos Simples &#40;Página Avançado&#41;](../../2014/integration-services/flat-file-connection-manager-editor-advanced-page.md)<br /><br /> [Editor do Gerenciador de Conexões de Arquivos Simples &#40;Página Visualização&#41;](../../2014/integration-services/flat-file-connection-manager-editor-preview-page.md)|  
    |[Gerenciador de Conexões de Vários Arquivos Simples](connection-manager/multiple-flat-files-connection-manager.md)|[Editor do Gerenciador de Conexões de Vários Arquivos Simples &#40;Página Geral&#41;](../../2014/integration-services/multiple-flat-files-connection-manager-editor-general-page.md)<br /><br /> [Editor do Gerenciador de Conexões de Vários Arquivos Simples &#40;Página Colunas&#41;](../../2014/integration-services/multiple-flat-files-connection-manager-editor-columns-page.md)<br /><br /> [Editor do Gerenciador de Conexões de Vários Arquivos Simples &#40;Página Avançado&#41;](../../2014/integration-services/multiple-flat-files-connection-manager-editor-advanced-page.md)<br /><br /> [Editor do Gerenciador de Conexões de Vários Arquivos Simples &#40;Página Visualização&#41;](../../2014/integration-services/multiple-flat-files-connection-manager-editor-preview-page.md)|  
    |[Gerenciador de Conexões de FTP](connection-manager/ftp-connection-manager.md)|[Editor do Gerenciador de Conexões FTP](../../2014/integration-services/ftp-connection-manager-editor.md)|  
    |[Gerenciador de Conexões de HTTP](connection-manager/http-connection-manager.md)|[Editor do Gerenciador de Conexões HTTP &#40;Página Servidor&#41;](../../2014/integration-services/http-connection-manager-editor-server-page.md)<br /><br /> [Editor do Gerenciador de Conexões HTTP &#40;Página Proxy&#41;](../../2014/integration-services/http-connection-manager-editor-proxy-page.md)|  
    |[Gerenciador de Conexões MSMQ](connection-manager/msmq-connection-manager.md)|[Editor do Gerenciador de Conexões MSMQ](../../2014/integration-services/msmq-connection-manager-editor.md)|  
    |[Gerenciador de Conexões ODBC](connection-manager/odbc-connection-manager.md)|[Referência da interface do usuário do Gerenciador de Conexões ODBC](../../2014/integration-services/odbc-connection-manager-ui-reference.md)|  
    |[gerenciador de conexões OLE DB](connection-manager/ole-db-connection-manager.md)|[Configurar Gerenciador de Conexões OLE DB](configure-ole-db-connection-manager.md)|  
    |[Gerenciador de Conexões SMO](connection-manager/smo-connection-manager.md)|[Editor do Gerenciador de Conexões SMO](../../2014/integration-services/smo-connection-manager-editor.md)|  
    |[Gerenciador de Conexões SMTP](connection-manager/smtp-connection-manager.md)|[Editor do Gerenciador de Conexões SMTP](../../2014/integration-services/smtp-connection-manager-editor.md)|  
    |[Gerenciador de Conexões do SQL Server Compact Edition](connection-manager/sql-server-compact-edition-connection-manager.md)|[Editor do Gerenciador de Conexões do SQL Server Compact Edition &#40;Página de Conexão&#41;](../../2014/integration-services/sql-server-compact-edition-connection-manager-editor-connection-page.md)<br /><br /> [Editor do Gerenciador de Conexões do SQL Server Compact Edition &#40;Página Tudo&#41;](../../2014/integration-services/sql-server-compact-edition-connection-manager-editor-all-page.md)|  
    |[Gerenciador de Conexões WMI](connection-manager/wmi-connection-manager.md)|[Editor do Gerenciador de Conexões WMI](../../2014/integration-services/wmi-connection-manager-editor.md)|  
  
5.  Para salvar o pacote atualizado, clique em **Salvar Itens Selecionados** no menu **Arquivo** .  
  
## <a name="see-also"></a>Consulte Também  
 [Integration Services &#40;conexões&#41; SSIS](connection-manager/integration-services-ssis-connections.md)   
 [Adicionar, excluir ou compartilhar um gerenciador de conexões em um pacote](../../2014/integration-services/add-delete-or-share-a-connection-manager-in-a-package.md)  
  
  
