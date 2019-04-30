---
title: Fonte de dados de caixa de diálogo de propriedades, as credenciais (construtor de relatórios) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10017"
ms.assetid: 4531f09f-d653-4c05-a120-d7788838bc99
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: b6798be8db7597de1d4c8d8542fcb6abc8621606
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63165121"
---
# <a name="data-source-properties-dialog-box-credentials-report-builder"></a>Caixa de diálogo Propriedades da Fonte de Dados, Credenciais (Construtor de Relatórios)
  Selecione **Credenciais** na caixa de diálogo **Propriedades da Fonte de Dados** para exibir e modificar as credenciais a fim de estabelecer conexão com uma fonte de dados inserida do relatório. As credenciais fornecidas são usadas para acessar a fonte de dados para externas para a visualização de relatórios. Para obter mais informações sobre credenciais, consulte [Especificar as credenciais no Construtor de Relatórios](../../2014/reporting-services/specify-credentials-in-report-builder.md).  
  
## <a name="options"></a>Opções  
 **Usar a autenticação do Windows (segurança integrada)**  
 Selecione esta opção para usar a Autenticação do Windows.  
  
 **Usar este nome de usuário e senha**  
 Selecione esta opção para fornecer um nome de usuário e senha específicos. Em fontes de dados inseridas: quando você publicar o projeto do servidor de relatório no servidor de destino, o nome de usuário e a senha serão salvos como as credenciais armazenadas no banco de dados. Para usar o nome de usuário e a senha como credenciais do Windows, é possível alterar as propriedades da fonte de dados compartilhada no servidor de destino. Para obter mais informações, consulte [Criar, excluir ou modificar uma fonte de dados compartilhada &#40;Gerenciador de Relatórios&#41;](../../2014/reporting-services/create-delete-or-modify-a-shared-data-source-report-manager.md) na documentação do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] nos [Manuais Online](https://go.microsoft.com/fwlink/?linkid=121312) do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
 **Nome de usuário**  
 Digite um nome de usuário para fazer logon na fonte de dados.  
  
 **Senha**  
 Digite uma senha para fazer logon na fonte de dados.  
  
 **Pedir credenciais**  
 Selecione esta opção para solicitar as credenciais quando o relatório for executado.  
  
 **Insira a cadeia de caracteres de prompt**  
 Digite uma instrução para que o usuário forneça as credenciais de logon para a fonte de dados.  
  
 **Nenhuma credencial**  
 Selecione esta opção para não fornecer nenhuma credencial para a fonte de dados. Esta opção só funcionará se a fonte de dados não aceitar credenciais ou se você estiver passando as credenciais de alguma outra forma.  
  
 Em algumas extensões de dados, a conta de execução autônoma deve estar configurada no servidor de relatório.  
  
 Para obter mais informações, consulte o tópico sobre o tipo de fonte de dados correspondente em [Adicionar dados de fontes de dados externas &#40;SSRS&#41;](report-data/add-data-from-external-data-sources-ssrs.md) e [Configurar a conta de execução autônoma &#40;SSRS Configuration Manager&#41;](install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md) na documentação do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] nos [Manuais Online](https://go.microsoft.com/fwlink/?linkid=121312) do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>Consulte também  
 [Ajuda do Construtor de Relatórios para caixas de diálogo, painéis e assistentes](../../2014/reporting-services/report-builder-help-for-dialog-boxes-panes-and-wizards.md)   
 [Caixa de diálogo Propriedades da Fonte de Dados, Geral &#40;Construtor de Relatórios&#41;](../../2014/reporting-services/data-source-properties-dialog-box-general-report-builder.md)   
 [Adicionar e verificar uma Conexão de dados ou uma fonte de dados &#40;relatórios e SSRS&#41;](report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md)   
 [Adicionar dados a um relatório &#40;relatórios e SSRS&#41;](report-data/report-datasets-ssrs.md)  
  
  
