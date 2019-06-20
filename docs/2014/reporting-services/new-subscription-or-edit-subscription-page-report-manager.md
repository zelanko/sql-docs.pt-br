---
title: Página nova assinatura ou Editar assinatura (Gerenciador de relatórios) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: e02d6529-ce67-4305-b7f0-433997e99c21
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 968362b2835c0e76f2a44c44e6cd427af863e8e4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66108137"
---
# <a name="new-subscription-or-edit-subscription-page-report-manager"></a>Página Nova Assinatura ou Editar Assinatura (Gerenciador de Relatórios)
  Use a página Nova Assinatura ou Editar Assinatura para criar uma nova assinatura ou editar uma assinatura existente para um relatório. As opções nessa página variam, dependendo de sua atribuição de função. Os usuários com permissões avançadas podem trabalhar com opções adicionais.  
  
 As assinaturas têm suporte para relatórios que podem ser executados de modo autônomo. O relatório deve, no mínimo, usar credenciais armazenadas ou nenhuma credencial. Se o relatório usar parâmetros, um valor padrão deverá ser especificado. As assinaturas poderão ficar inativas se você alterar as configurações de execução do relatório ou remover os valores padrão usados por propriedades de parâmetro. Para saber mais, consulte [Crie e gerencie assinaturas de servidores de relatório no modo Nativo](../../2014/reporting-services/create-manage-subscriptions-native-mode-report-servers.md).  
  
> [!NOTE]  
>  Este recurso não está disponível em todas as edições do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Para obter uma lista de recursos com suporte nas edições do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], consulte [Features Supported by the Editions of SQL Server 2014](../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md).  
  
## <a name="navigation"></a>Navegação  
 Use o procedimento a seguir para navegar para este local na interface do usuário.  
  
### <a name="to-open-the-new-subscription-or-edit-subscription-page"></a>Para abrir a página Nova Assinatura ou Editar Assinatura.  
  
1.  Abra o Gerenciador de Relatórios e localize o relatório para o qual você deseja adicionar uma assinatura.  
  
2.  Focalize o relatório e clique na seta do menu suspenso.  
  
3.  No menu suspenso, siga um destes procedimentos:  
  
    -   Clique em **Gerenciar**. Esse procedimento abre a página de propriedades Geral do relatório. Em seguida, selecione a guia **Assinaturas** . Na barra de ferramentas, clique em **Nova Assinatura**ou selecione uma assinatura existente e clique em **Editar**.  
  
    -   Clique em **Assinar**. Esse procedimento abre a página **Nova Assinatura** para o relatório.  
  
## <a name="options"></a>Opções  
 **Entregue por**  
 Selecione a extensão de entrega a ser usada para distribuir o relatório. Dependendo da extensão de entrega selecionada, as configurações a seguir são exibidas:  
  
-   Assinaturas de email fornecem campos que são familiares a usuários de email (por exemplo, os campos **Para**, **Assunto**e **Prioridade** ). Especifique **Incluir Relatório** para inserir ou anexar o relatório ou **Incluir Link** para incluir uma URL ao relatório. Especifique **Formato de Renderização** para escolher um formato de apresentação para o relatório anexado ou inserido.  
  
-   Assinaturas de compartilhamento de arquivo fornecem campos que permitem especificar um local de destino. Você pode entregar qualquer relatório a um compartilhamento de arquivo. No entanto, relatórios que oferecem suporte a recursos interativos (incluindo relatórios matriz com suporte para busca detalhada em linhas e colunas) são renderizados como arquivos estáticos. Você não pode exibir busca detalhada em linhas e colunas em um arquivo estático. O nome do compartilhamento de arquivo deve ser especificado no formato UNC Uniform Naming Convention () (por exemplo, \\\mycomputer\public\myreportfiles). Não inclua barras invertidas à direita no nome do caminho. O arquivo de relatório será entregue em um formato de arquivo que tem base no formato de renderização (por exemplo, se você escolher **Excel**, o relatório será entregue como um arquivo .xls).  
  
 A disponibilidade de uma extensão de entrega depende se ela está instalada e configurada no servidor de relatório. O Email do Servidor de Relatório é a extensão de entrega padrão, mas deve ser configurado antes de ser usado. Entrega de Compartilhamento de Arquivo não requer configuração, mas você deve definir uma pasta compartilhada antes de usá-la.  
  
## <a name="subscription-processing-options"></a>Opções de processamento de assinatura  
 Use estas configurações para definir as condições que causam o processamento de uma assinatura. Algumas das opções só estão disponíveis para relatórios que usam parâmetros ou que são executados como instantâneos de execução de relatório.  
  
 **Quando o conteúdo do relatório for atualizado**  
 Selecione esta opção para assinar um instantâneo de relatório que é atualizado com base em agendamento. Essa opção só é visível quando você está assinando um relatório que é executado como um instantâneo de execução de relatório. O conteúdo de um instantâneo de execução de relatório é atualizado normalmente em uma agenda. Para relatórios que executados nesse modo, você pode definir que uma assinatura ocorra quando o instantâneo é atualizado.  
  
 **Quando a execução do relatório agendado estiver concluída**  
 Crie uma agenda que determina quando a assinatura é processada.  
  
 **Em uma agenda compartilhada**  
 Selecionar uma agenda predefinida para processar a assinatura.  
  
 **Insira valores de parâmetro**  
 Use essa opção quando você estiver assinando um relatório com parâmetros. Essa opção só está disponível para relatórios com parâmetros. Ao assinar um relatório com parâmetros, você pode especificar que os valores de parâmetro usados criem a versão do relatório entregue pela assinatura. Por exemplo, você pode especificar um código de região para selecionar dados de vendas para uma região específica. Se você não especificar um valor, o valor padrão será usado.  
  
## <a name="see-also"></a>Consulte também  
 [Configurar um servidor de relatório para entrega de email &#40;Configuration Manager do SSRS&#41;](../../2014/sql-server/install/configure-a-report-server-for-e-mail-delivery-ssrs-configuration-manager.md)   
 [Gerenciador de Relatórios &#40;Modo Nativo do SSRS&#41;](../../2014/reporting-services/report-manager-ssrs-native-mode.md)   
 [Criar, modificar e excluir agendas](subscriptions/create-modify-and-delete-schedules.md)   
 [Ajuda F1 do Gerenciador de Relatórios](../../2014/reporting-services/report-manager-f1-help.md)  
  
  
