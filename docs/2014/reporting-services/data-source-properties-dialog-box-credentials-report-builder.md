---
title: Caixa de diálogo Propriedades da fonte de dados, credenciais (Construtor de Relatórios) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10017"
ms.assetid: 4531f09f-d653-4c05-a120-d7788838bc99
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 5dd4d113c92e0a2d094aa02d49010a5dd477c6ba
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66109451"
---
# <a name="data-source-properties-dialog-box-credentials-report-builder"></a>Caixa de diálogo Propriedades da Fonte de Dados, Credenciais (Construtor de Relatórios)
  Selecione **Credenciais** na caixa de diálogo **Propriedades da Fonte de Dados** para exibir e modificar as credenciais a fim de estabelecer conexão com uma fonte de dados inserida do relatório. As credenciais fornecidas são usadas para acessar a fonte de dados para externas para a visualização de relatórios. Para obter mais informações sobre credenciais, consulte [Especificar as credenciais no Construtor de Relatórios](../../2014/reporting-services/specify-credentials-in-report-builder.md).  
  
## <a name="options"></a>Opções  
 **Usar a Autenticação do Windows (segurança integrada)**  
 Selecione esta opção para usar a Autenticação do Windows.  
  
 **Usar este nome de usuário e senha**  
 Selecione esta opção para fornecer um nome de usuário e senha específicos. Em fontes de dados inseridas: quando você publicar o projeto do servidor de relatório no servidor de destino, o nome de usuário e a senha serão salvos como as credenciais armazenadas no banco de dados. Para usar o nome de usuário e a senha como credenciais do Windows, é possível alterar as propriedades da fonte de dados compartilhada no servidor de destino. Para obter mais informações, consulte [Criar, excluir ou modificar uma fonte de dados compartilhada &#40;Gerenciador de Relatórios&#41;](../../2014/reporting-services/create-delete-or-modify-a-shared-data-source-report-manager.md) na documentação do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] nos [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [Manuais Online](https://go.microsoft.com/fwlink/?linkid=121312) do .  
  
 **Nome de usuário**  
 Digite um nome de usuário para fazer logon na fonte de dados.  
  
 **Senha**  
 Digite uma senha para fazer logon na fonte de dados.  
  
 **Pedir credenciais**  
 Selecione esta opção para solicitar as credenciais quando o relatório for executado.  
  
 **Informar a cadeia de caracteres da solicitação**  
 Digite uma instrução para que o usuário forneça as credenciais de logon para a fonte de dados.  
  
 **Sem credenciais**  
 Selecione esta opção para não fornecer nenhuma credencial para a fonte de dados. Esta opção só funcionará se a fonte de dados não aceitar credenciais ou se você estiver passando as credenciais de alguma outra forma.  
  
 Em algumas extensões de dados, a conta de execução autônoma deve estar configurada no servidor de relatório.  
  
 Para obter mais informações, consulte o tópico sobre o tipo de fonte de dados correspondente em [Adicionar dados de fontes de dados externas &#40;SSRS&#41;](report-data/add-data-from-external-data-sources-ssrs.md) e [Configurar a conta de execução autônoma &#40;SSRS Configuration Manager&#41;](install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md) na documentação do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] nos [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [Manuais Online](https://go.microsoft.com/fwlink/?linkid=121312) do .  
  
## <a name="see-also"></a>Consulte Também  
 [Construtor de Relatórios ajuda para caixas de diálogo, painéis e assistentes](../../2014/reporting-services/report-builder-help-for-dialog-boxes-panes-and-wizards.md)   
 [Caixa de diálogo Propriedades da fonte de dados, Construtor de Relatórios geral &#40;&#41;](../../2014/reporting-services/data-source-properties-dialog-box-general-report-builder.md)   
 [Adicionar e verificar uma conexão de dados ou uma fonte de dados &#40;Construtor de Relatórios e SSRS&#41;](report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md)   
 [Adicionar dados a um relatório &#40;Construtor de Relatórios e SSRS&#41;](report-data/report-datasets-ssrs.md)  
  
  
