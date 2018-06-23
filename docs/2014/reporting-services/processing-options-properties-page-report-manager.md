---
title: Opções de processamento de página de propriedades (Gerenciador de relatórios) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 28f07c70-7132-4d15-9505-4fdf31dc9cc0
caps.latest.revision: 35
author: markingmyname
ms.author: maghan
manager: mblythe
ms.openlocfilehash: 17db40e24318fad194ec21ca30e6394f3fe607e3
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36020186"
---
# <a name="processing-options-properties-page-report-manager"></a>Página de propriedades Opções de Processamento (Gerenciador de Relatórios)
  Use a página de propriedades Opções de Processamento para definir as propriedades de execução do relatório selecionado. Essas opções determinam quando ocorre processamento de dados para o relatório. Você pode definir essas opções para recuperar dados de relatório nos horários de pouca atividade. Se você tiver um relatório que é acessado frequentemente, pode armazenar temporariamente cópias de cache nele para eliminar tempo de espera, se vários usuários estiverem acessando o mesmo relatório com diferença de minutos.  
  
> [!NOTE]  
>  Os instantâneos de histórico de Relatório, Execução e recursos de Cache não estão disponíveis em todas as edições do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Para obter uma lista de recursos com suporte nas edições do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], consulte [Features Supported by the Editions of SQL Server 2014](../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md).  
  
## <a name="navigation"></a>Navegação  
 Use o procedimento a seguir para navegar para este local na interface do usuário.  
  
###### <a name="to-open-the-processing-options-properties-page"></a>Para abrir a página de propriedades Opções de Processamento  
  
1.  Abra o Gerenciador de Relatórios e localize o relatório cujas propriedades de processamento você deseja definir.  
  
2.  Focalize o relatório e clique na seta do menu suspenso.  
  
3.  No menu suspenso, clique em **Gerenciar**. Esse procedimento abre a página de propriedades Geral do relatório.  
  
4.  Selecione a guia **Opções de Processamento** .  
  
## <a name="options"></a>Opções  
 **Sempre executar este relatório com os dados mais recentes**  
 Use essa opção quando você quiser recuperar dados de relatório quando o usuário selecionar o relatório. Se uma cópia em cache do relatório estiver disponível, ela será retornada ao usuário; senão, a recuperação dos dados e a renderização ocorrerão quando um usuário selecionar o relatório.  
  
 Selecione **Não armazenar cópias temporárias deste relatório em cache** para sempre executar o relatório com os dados mais recentes. Cada usuário que abre o relatório dispara uma consulta na fonte de dados que contém os dados usados no relatório.  
  
 Selecione **Armazenar uma cópia temporária do relatório em cache**para colocar uma cópia temporária do relatório em cache quando um usuário abrir o relatório pela primeira vez. Usuários subsequentes que executam o relatório dentro do período de cache recebem a cópia armazenada em cache do relatório. O cache normalmente aprimora o desempenho porque o relatório é retornado do cache em vez de ser processado novamente.  
  
 Relatórios de cache devem expirar eventualmente. Especifique o número de minutos para que a cópia armazenada em cache do relatório seja salva. Assim que uma cópia temporária expira, não é mais retornada do cache. Na próxima vez que um usuário abrir um relatório, o servidor de relatório processará o relatório novamente e colocará uma cópia do relatório atualizado no cache.  
  
 Você também pode usar uma agenda para expiração de um relatório em cache usando uma frequência diferente de minutos. Por exemplo, para que um relatório em cache expire no fim do dia, você pode escolher uma hora específica à noite na qual a cópia expira.  
  
 **Renderizar este relatório em um instantâneo de relatório**  
 Use essa opção para recuperar um relatório que foi armazenado como instantâneo no momento do agendamento. Quando você escolhe esta opção, pode agendar o processamento de dados para ocorrer em um período de pouca atividade. Diferentemente de cópias em cache criadas quando um usuário abre o relatório, um instantâneo é criado e subsequentemente atualizado em uma agenda. Instantâneos não expiram; eles permanecem em serviço até serem substituídos por versões mais novas.  
  
 Instantâneos gerados como resultado de configurações de execução de relatório têm as mesmas características dos instantâneos de histórico de relatórios. A diferença é que só há um instantâneo de execução de relatório e potencialmente muitos instantâneos de histórico de relatórios. Instantâneos de histórico de relatório são acessados da página de Histórico do relatório, que armazena muitas instâncias de um relatório existentes em diferentes momentos. Em contraste, os usuários acessam instantâneos de execução de relatório de pastas do mesmo modo que acessam relatórios em tempo real. No caso de instantâneos de execução de relatórios, não existe nenhuma dica visual para indicar aos usuários que o relatório é um instantâneo.  
  
 Selecione a opção relacionada **Criar um instantâneo de relatórios ao clicar no botão Aplicar nesta página** para criar um instantâneo de relatórios quando você clicar em Aplicar. Isso gera o instantâneo de relatório imediatamente para disponibilizá-lo antes da hora de início agendada.  
  
 **Tempo limite de execução de relatório**  
 Especifique se o tempo limite do relatório chega ao fim depois de um certo número de segundos. Se você escolher a configuração padrão, a configuração de tempo limite especificada na página Configurações de Site será usada para este relatório.  
  
 Esse valor se aplica ao processamento de relatório em um servidor de relatório. Ele não define tempo limite para o processamento de dados no servidor de banco de dados que fornece os dados para o seu relatório. No entanto, o valor especificado deve ser suficiente para concluir o processamento dos dados e do relatório. A contagem do processamento de relatórios começa quando o relatório é selecionado e termina quando o relatório é aberto.  
  
## <a name="see-also"></a>Consulte também  
 [Definir propriedades de processamento de relatório](report-server/set-report-processing-properties.md)   
 [Armazenando relatórios em cache &#40;SSRS&#41;](report-server/caching-reports-ssrs.md)   
 [Criar, modificar e excluir agendas](subscriptions/create-modify-and-delete-schedules.md)   
 [Ajuda F1 do Gerenciador de Relatórios](../../2014/reporting-services/report-manager-f1-help.md)  
  
  