---
title: Página de propriedades (Gerenciador de relatórios) opções de instantâneo | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: f6641f59-5267-4f57-8957-63b93d1a9679
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 7a73f3be75a7f0cadf633943aeafffb7217d8e29
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66101156"
---
# <a name="snapshot-options-properties-page-report-manager"></a>Página de propriedades Opções de Instantâneo (Gerenciador de Relatórios)
  Use a página de propriedades Opções de Instantâneo para agendar instantâneos de relatório a serem adicionados ao histórico de relatórios e para definir limites do número de instantâneos de relatórios armazenados nesse histórico.  
  
> [!NOTE]  
>  Este recurso não está disponível em todas as edições do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Para obter uma lista de recursos que têm suporte nas edições do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], consulte [serviços de banco de dados adicionais](../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md#Add_DBServices).  
  
## <a name="navigation"></a>Navegação  
 Use o procedimento a seguir para navegar para este local na interface do usuário.  
  
### <a name="to-open-the-snapshot-options-properties-page-for-a-report"></a>Para abrir a página de propriedades Opções de Instantâneo de um relatório  
  
1.  Abra o Gerenciador de Relatórios e localize o relatório cujas propriedades de instantâneo você deseja configurar.  
  
2.  Focalize o relatório e clique na seta do menu suspenso.  
  
3.  No menu suspenso, clique em **Gerenciar**. Esse procedimento abre a página de propriedades Geral do relatório.  
  
4.  Selecione a guia **Opções de Instantâneo** .  
  
## <a name="options"></a>Opções  
 **Permitir que o histórico de relatório a ser criado manualmente**  
 Marque esta caixa de seleção para adicionar instantâneos ao histórico de relatório conforme necessário. Marcando esta caixa de seleção, o botão **Novo Instantâneo** aparecerá na página Histórico.  
  
 **Store todos os instantâneos de execução de relatório no histórico de relatórios**  
 Marque essa caixa de seleção para copiar um instantâneo de relatório gerado com base nas propriedades de execução de relatório no histórico do relatório. Você pode definir propriedades de execução de relatório para executar um relatório de um instantâneo gerado. Definindo essa propriedade de histórico de relatórios você pode manter um registro de todos os instantâneos gerados com o tempo, colocando cópias deles no histórico de relatórios.  
  
 **Use o agendamento a seguir para adicionar instantâneos ao histórico de relatórios**  
 Marque esta caixa de seleção para adicionar instantâneos ao histórico do relatório em uma base de agendamento. Você pode criar uma agenda usada exclusivamente para esse propósito ou pode selecionar uma agenda compartilhada predefinida se ela contiver as informações de agendamento necessárias.  
  
 **Selecione o número de instantâneos a serem mantidos**  
 Selecione das opções seguintes para controlar o número de relatórios mantido no histórico de relatórios. Configurações de histórico de relatórios podem variar para cada relatório.  
  
-   Selecione **Usar configuração padrão** para reter a configuração padrão. O administrador de servidor de relatórios controla uma configuração mestre para armazenamento de histórico de relatórios. Se você escolher essa opção, o número de instantâneos retidos será obtido dessa configuração mestra.  
  
-   Selecione **Mantenha um número ilimitado de instantâneos no histórico de relatório** para reter todos os instantâneos de histórico de relatório. Você deve excluir instantâneos manualmente para reduzir o tamanho de histórico de relatórios.  
  
-   Selecione **Limitar as cópias do histórico de relatório** para reter um número fixo de instantâneos. Quando o limite é alcançado, cópias mais antigas são removidas do histórico do relatório para liberar espaço para cópias mais atuais.  
  
 O histórico de relatórios é armazenado no banco de dados do servidor de relatórios. Se você tiver grandes relatórios ou vários relatórios para os quais queira manter histórico, considere limitar a quantidade de histórico do relatório para ajudar a gerenciar os requisitos de espaço em disco do banco de dados do servidor de relatórios.  
  
 **Aplicar**  
 Clique para salvar as alterações.  
  
## <a name="see-also"></a>Consulte também  
 [Adicionar um instantâneo ao histórico de relatório &#40;Gerenciador de Relatórios&#41;](report-server/add-a-snapshot-to-report-history-report-manager.md)   
 [Gerenciador de Relatórios &#40;Modo Nativo do SSRS&#41;](../../2014/reporting-services/report-manager-ssrs-native-mode.md)   
 [Criar, modificar e excluir instantâneos no histórico de relatório](report-server/create-modify-and-delete-snapshots-in-report-history.md)   
 [Ajuda F1 do Gerenciador de Relatórios](../../2014/reporting-services/report-manager-f1-help.md)  
  
  
