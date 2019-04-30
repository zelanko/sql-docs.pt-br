---
title: Criar página de assinatura controlada por dados (Gerenciador de relatórios) | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 814b4653-572a-48c7-847f-b310ba0f3046
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 625afedabdb376f913d3353e2bda343bba66e3e1
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63265947"
---
# <a name="create-data-driven-subscription-page-report-manager"></a>Página Criar Assinatura Controlada por Dados (Gerenciador de Relatórios)
  Use a página Criar Assinatura Controlada por Dados para criar ou modificar uma assinatura que consulta um banco de dados de assinante para informações de assinatura cada vez que a assinatura é executada. Assinaturas controladas por dados usam resultados de consulta para determinar os destinatários da assinatura, as configurações de entrega e os valores de parâmetro do relatório. Em tempo de execução, o servidor de relatórioss executa uma consulta para obter valores usados nas configurações da assinatura. Você pode usar a página Criar Assinatura Controlada por Dados para definir a consulta e atribuir valores de consulta às configurações de assinatura. Os valores e as opções especificadas para uma assinatura controlada por dados são divididos entre várias páginas, semelhantes a um assistente. Há sete páginas ao todo.  
  
 Para criar uma assinatura controlada por dados, você deve saber como gravar uma consulta ou um comando que obtém os dados para a assinatura. Você também deve ter um repositório de dados que contenha os dados do assinante (por exemplo, nomes e endereços de e-mail do assinante) a serem usados na assinatura.  
  
 Essa página está disponível a usuários com permissões avançadas. Se você estiver usando a segurança padrão, as assinaturas controladas por dados não poderão ser usadas nos relatórios da pasta Meus Relatórios.  
  
> [!NOTE]  
>  Este recurso não está disponível em todas as edições do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Para obter uma lista de recursos com suporte nas edições do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], consulte [Features Supported by the Editions of SQL Server 2014](../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md).  
  
## <a name="navigation"></a>Navegação  
 Use o procedimento a seguir para navegar para este local na interface do usuário.  
  
###### <a name="to-open-the-data-driven-subscription-page"></a>Para abrir a página Assinatura Voltada para Dados  
  
1.  Abra o Gerenciador de Relatórios e localize o relatório para o qual você deseja criar uma assinatura controlada por dados.  
  
2.  Focalize o relatório e clique na seta do menu suspenso.  
  
3.  No menu suspenso, clique em **Gerenciar**. Esse procedimento abre a página de propriedades **Geral** do relatório.  
  
4.  Selecione a guia **Assinaturas** e clique em **Nova Assinatura Orientada por Dados**.  
  
    > [!NOTE]  
    >  A fonte de dados do relatório deve usar credenciais armazenadas para que esse botão seja habilitado.  
  
## <a name="start-a-subscription-page-1"></a>Iniciar uma assinatura (página 1)  
 **Descrição**  
 Forneça uma descrição para a assinatura. A descrição aparece em listas de assinatura em **Minhas Assinaturas** e na guia **Assinaturas** do relatório.  
  
 **Especificar como os destinatários serão notificados**  
 Selecione a extensão de entrega a ser usada para distribuir o relatório. Somente uma extensão de entrega pode ser usada para cada assinatura. As seguintes opções estão disponíveis:  
  
-   Selecione **Compartilhamento de Arquivo do Servidor de Relatório** para entregar os relatórios a um compartilhamento de arquivos. O relatório será entregue como um arquivo estático, desconectado do servidor de relatório. Para obter mais informações, consulte [File Share Delivery in Reporting Services](subscriptions/file-share-delivery-in-reporting-services.md).  
  
-   Selecione **Email do Servidor de Relatório** para entregar relatórios a uma caixa de entrada de emails. Para obter mais informações, consulte [E-Mail Delivery in Reporting Services](subscriptions/e-mail-delivery-in-reporting-services.md).  
  
-   Selecione **Provedor de Entrega Nulo** para entregar relatórios ao banco de dados do servidor de relatório. Essa opção cria instantâneos de relatório. Escolha essa opção quando quiser carregar antecipadamente o servidor de relatório com instantâneos de relatório com parâmetros ou específico de usuário em um agendamento específico. Para obter mais informações, consulte [Armazenando relatórios em cache &#40;SSRS&#41;](report-server/caching-reports-ssrs.md).  
  
 **Especifique uma fonte de dados que contém informações de destinatário**  
 Especifique como a conexão da fonte de dados é definida. Você poderá escolher uma fonte de dados compartilhada se tiver uma com as informações de conexão necessárias. Você também pode especificar informações de conexão diretamente nessa assinatura.  
  
 A fonte de dados fornece dados do assinante. Esses dados podem consistir em nomes de funcionário, IDs de funcionário, endereços de email e preferência para formatação de exportação (como HTML ou PDF). Se você estiver usando a extensão de entrega de email do servidor de relatórios, a fonte de dados deve conter endereços de email.  
  
## <a name="specify-a-connection-page-2"></a>Especificar uma Conexão (página 2)  
 Se você especificou uma fonte de dados compartilhada, use essa página para selecionar o item de fonte de dados compartilhada. Você pode usar o controle de árvore para navegar e selecionar o item. Se você estiver definindo uma conexão para essa assinatura, use essa página para especificar as opções a seguir.  
  
 **Tipo de Conexão**  
 Selecione qual extensão de processamento de dados usar com a fonte de dados.  
  
 **Cadeia de Conexão**  
 Digite uma cadeia de conexão a ser usada para conectar à fonte de dados.  
  
 **Conecte-se usando**  
 Digite as credenciais a serem usadas ao se conectar à fonte de dados. As credenciais são armazenadas como valores criptografados no banco de dados do servidor de relatórios.  
  
 Se a fonte de dados usar a Autenticação do Windows, selecione **Usar como Credenciais do Windows** ao especificar a conexão.  
  
 Se você estiver usando uma fonte de dados que não autentica conexões do usuário (por exemplo, se a fonte de dados for um arquivo XML), a seleção das Credenciais não será necessária. Essa opção requer que você tenha configurado antecipadamente a conta de execução autônoma. Para obter mais informações, consulte [Configurar a conta de execução autônoma &#40;Configuration Manager do SSRS&#41;](install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md).  
  
## <a name="specify-a-query-page-3"></a>Especificar uma Consulta (página 3)  
 Use essa página para inserir a consulta que recupera dados do assinante. Para um resultado melhor, execute a consulta no SQL Server Management Studio primeiro, antes de usá-la na assinatura controlada por dados. Você pode, então, examinar os resultados para verificar se eles contêm as informações necessárias. Pontos importantes a reconhecer sobre os resultados de consulta:  
  
-   As colunas no conjunto de resultados determinam os valores que você pode especificar para opções de entrega e parâmetros do relatório. Por exemplo, se você estiver criando uma assinatura controlada por dados para uma entrega de email, você deve ter uma coluna de endereços de email.  
  
-   Linhas no conjunto de resultados determinam o número de entregas de relatório geradas. Se você tiver 10.000 linhas, o servidor de relatório gerará 10.000 notificações e entregas.  
  
 **Consulta**  
 Especifique uma consulta SQL ou um comando que recupera um conjunto de resultados que contém uma linha para cada destinatário de assinatura. Nas páginas subsequentes, o conjunto de resultados é usado para popular configurações de extensão controladas por dados.  
  
 **Tempo Limite**  
 Especifique um valor de tempo limite para a consulta. Esse valor deve ser grande o bastante para concluir o processamento da consulta.  
  
 **Validar**  
 Clique em **Validar** para verificar a consulta. A consulta deve produzir resultados válidos antes que você possa continuar. Se você não clicar em **Validar**, a consulta será validada quando você clicar em **Avançar**.  
  
## <a name="set-delivery-options-page-4"></a>Definir Opções de Entrega (página 4)  
 Na quarta página, você especifica opções de extensão de entrega. As opções exibidas na página são derivadas da extensão da entrega. A especificação dessas opções pode variar consideravelmente, com base em como a extensão da entrega as apresenta. Se a extensão não tiver nenhuma configuração, nenhuma opção aparecerá nessa página.  
  
|Selecione isto|Para fazer isso|  
|-----------------|----------------|  
|**Especifique um valor estático**|Use um valor constante para a configuração da entrega. Algumas extensões de entrega fornecem valores estáticos entre os quais você pode escolher. Por exemplo, a entrega de email do servidor de relatório fornece valores para **IncludeReport**, **RenderFormat**, **Prioridade**e **Incluir Link**.|  
|**Obter o valor do banco de dados**|Use um valor do conjunto de resultados. As colunas do conjunto de resultados podem ser usadas para fornecer dados de assinante e valores de parâmetro de relatório.|  
|**Nenhum valor**|Omita a configuração da assinatura.|  
  
#### <a name="set-delivery-options-for-file-share-delivery"></a>Definir opções de entrega para entrega de compartilhamento de arquivo  
 A extensão de entrega de compartilhamento de arquivo é frequentemente usada porque não requer nenhuma configuração anterior. Se você estiver usando a extensão de entrega de compartilhamento de arquivo, a tabela a seguir descreverá as opções que você pode definir:  
  
 **Nome do arquivo**  
 Especifica um nome de arquivo para o relatório. A extensão de entrega do arquivo entrega um relatório como um arquivo de aplicativo estático a uma pasta compartilhada. Na maioria dos casos, você deve usar um valor do banco de dados para criar o nome do arquivo. Dependendo da definição do modo de gravação, o uso de um valor estático pode fazer com que cada nova entrega substitua a entrega anterior.  
  
 **Caminho**  
 Especifique uma pasta compartilhada que é acessível em uma conexão de rede. Para verificar se a pasta é acessível, clique em **executados** no menu Iniciar e insira o caminho da pasta neste formato: \\ \\< NomeDoComputador\>\\< nomedapastacompartilhada\>.  
  
 **Formato de renderização**  
 Especifique o formato de saída do arquivo. O servidor de relatório pode gravar o arquivo em formatos de aplicativo das extensões de renderização instaladas no servidor de relatório.  
  
 **Modo de gravação**  
 Especifique se o servidor de relatórios deve substituir um arquivo por uma versão mais nova, incrementá-lo ou descartar a entrega se um arquivo de mesmo nome for encontrado.  
  
 **Extensão de arquivo**  
 Especifique Verdadeiro para anexar uma extensão de arquivo que corresponda ao formato de renderização selecionado.  
  
 **Nome de usuário**  
 Insira a conta de usuário de domínio que tenha permissão para adicionar arquivos à pasta compartilhada neste formato: \<domínio >\\< nome de usuário\>.  
  
 **Senha**  
 Insira a senha para a conta.  
  
## <a name="set-parameters-page-5"></a>Definir Parâmetros (página 5)  
 Se um relatório incluir parâmetros, é necessário especificar quais valores de parâmetro usar com o relatório. Valores de parâmetros podem ser obtidos da fonte de dados do assinante (por exemplo, se você tiver um relatório de vendas regionais com parâmetros com base em um código regional, você pode obter informações da região de cada funcionário se as informações estiverem armazenadas no banco de dados de funcionário).  
  
|Selecione isto|Para fazer isso|  
|-----------------|----------------|  
|**Especifique um valor estático**|Use um valor constante para o parâmetro se você quiser usar o mesmo parâmetro para todos os assinantes. Se o parâmetro tiver valores múltiplos, você poderá escolher um valor da lista.|  
|**Usar padrão**|Alguns relatórios contêm um valor padrão para todos ou alguns dos parâmetros. Se o parâmetro de relatório tiver um valor padrão, clique nessa caixa de seleção para usá-lo.|  
|**Obter o valor do banco de dados**|Use um valor do conjunto de resultados. As colunas do conjunto de resultados podem ser selecionadas como um valor de fonte de dados a ser usado com cada instância da assinatura.|  
  
## <a name="specify-a-trigger-page-6"></a>Especificar um gatilho (página 6)  
 Selecione um evento que inicia o processamento da assinatura.  
  
|Selecione isto|Para fazer isso|  
|-----------------|----------------|  
|**Quando os dados do relatório são atualizados no servidor de relatório**|Se o relatório for configurado para executar como um instantâneo de execução de relatório, você pode especificar que a assinatura seja executada quando o instantâneo for atualizado.|  
|**Em um agendamento criado para esta assinatura**|Execute a assinatura e uma data e hora específicas.|  
|**Em uma agenda compartilhada**|Execute a assinatura usando informações de agenda fornecidas por uma agenda compartilhada.|  
  
## <a name="schedule-a-subscription-page-7"></a>Agendar uma assinatura (página 7)  
 Se você agendar a assinatura, deverá especificar a frequência de entrega do relatório. O primeiro conjunto de opções especifica uma categoria de frequência (a cada hora, diariamente, semanalmente e assim por diante). O segundo conjunto de opções que aparece é baseado em sua seleção inicial.  
  
 **Por hora**  
 Defina uma agenda que executa de hora em hora.  
  
 **Diário**  
 Define uma agenda que executa nos dias que você seleciona, em uma hora e minuto específico. Você pode especificar dias das seguintes maneiras: Cada  *\<dia >*, cada dia da semana e cada  *\<número >* dia. A escolha de uma abordagem invalida as outras, mesmo se os outros dias parecem selecionados.  
  
 **Semanal**  
 Define uma agenda que executa em intervalos semanais, em uma hora e minuto específicos. O intervalo pode ser em semanas completas (por exemplo, a cada duas semanas) ou dias dentro de uma semana.  
  
 **Mensal**  
 Defina uma agenda que executa mensalmente. Dentro de um mês você pode escolher um dia com base em um padrão (por exemplo, o último domingo de cada mês) ou datas de calendário específicas (como 1 e 15, para indicar o primeiro e o décimo quinto dia de cada mês). Usando vírgulas e hífens, você pode especificar vários dias e intervalos, por exemplo, 1, 5, 7-12, 21.  
  
 **Uma vez**  
 Defina uma agenda que só executa uma vez. Use a seção **Datas de início e término** para especificar o dia em que o agendamento deve ser executado. Esta agenda expira assim que é processada.  
  
 **Datas de início e término**  
 Especifique uma data de início que determina quando o agendamento entra em vigor e uma data de término que determina quando a agendamento expira. Os agendamentos expiram sem notificação. Após a data de término, a agenda não é mais executada.  
  
## <a name="saving-the-subscription"></a>Salvando a assinatura  
 O botão **Concluir** é habilitado quando há informações suficientes para a assinatura. Clique em **Concluir** para concluir a assinatura.  
  
## <a name="see-also"></a>Consulte também  
 [Gerenciador de Relatórios &#40;Modo Nativo do SSRS&#41;](../../2014/reporting-services/report-manager-ssrs-native-mode.md)   
 [Data-Driven Subscriptions](subscriptions/data-driven-subscriptions.md)   
 [Criar uma assinatura controlada por dados &#40;Tutorial do SSRS&#41;](create-a-data-driven-subscription-ssrs-tutorial.md)   
 [Especificar informações de credenciais e de conexão para fontes de dados de relatório](report-data/specify-credential-and-connection-information-for-report-data-sources.md)   
 [Assinaturas e entrega &#40;Reporting Services&#41;](subscriptions/subscriptions-and-delivery-reporting-services.md)   
 [Ajuda F1 do Gerenciador de Relatórios](../../2014/reporting-services/report-manager-f1-help.md)  
  
  
