---
title: Configurar as propriedades de execução de um relatório (Reporting Services) | Microsoft Docs
ms.date: 06/26/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reports
ms.topic: conceptual
helpviewer_keywords:
- report execution properties [Reporting Services]
- reports [Reporting Services], properties
- reports [Reporting Services], execution options
ms.assetid: 73cc8dcc-ef80-40d7-9739-d33bba0eb28a
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 6dfb24b6314529b19fb7bb5edb81534f30dc018a
ms.sourcegitcommit: c0e48b643385ce19c65ca6e348ce83b2d22b6514
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2019
ms.locfileid: "67492743"
---
# <a name="configure-execution-properties-for-a-report"></a>Configurar propriedades de execução de um relatório
  Você pode definir opções de processamento de relatório para especificar quando os dados são recuperados para um relatório. É útil agendar o processamento de dados de um relatório se a fonte de dados externa for atualizada em horários específicos (por exemplo, um data warehouse que é atualizado diária ou semanalmente) e você desejar evitar a sobrecarga da recuperação dos mesmos dados sempre que um relatório for solicitado. O agendamento do processamento de dados também é útil se você desejar controlar a carga de processamento no servidor de banco de dados externo ou quando você quiser fornecer resultados consistentes para vários usuários que devem trabalhar com conjuntos de dados idênticos. Com dados voláteis, um relatório sob demanda pode produzir resultados diferentes de um minuto para o outro. Por outro lado, um instantâneo de relatório permite fazer comparações válidas com outros relatórios ou ferramentas analíticas que contêm dados do mesmo momento.  
  
 Um instantâneo de relatório é um relatório que contém instruções sobre layout e resultados de consulta que foram recuperados em um momento específico. Diferente dos relatórios sob demanda, que obtêm resultados de consulta atualizados quando o relatório é selecionado, os instantâneos de relatório são processados em uma agenda e salvos em um servidor de relatório. Quando você seleciona um instantâneo de relatório para exibição, o servidor de relatório recupera o relatório armazenado do banco de dados do servidor e mostra os dados e o layout correspondentes ao momento em que o instantâneo foi criado.  
  
 Os instantâneos de relatório não são salvos em um formato de renderização específico. Em vez disso, os instantâneos de relatório são renderizados em um formato de exibição final (como HTML) somente quando solicitado por um usuário ou aplicativo. A renderização adiada deixa o instantâneo portátil. O relatório pode ser renderizado no formato correto para a solicitação do dispositivo ou navegador da Web.  

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
  
## <a name="to-configure-report-processing-options"></a>Para configurar opções de processamento de relatório  
  
1.  Inicie o [Gerenciador de Relatórios &#40;Modo Nativo do SSRS&#41;](https://msdn.microsoft.com/library/80949f9d-58f5-48e3-9342-9e9bf4e57896).  
  
2.  Navegue até o relatório cujas opções de processamento você deseja definir e abra-o.  
  
 Focalize o relatório e clique na seta do menu suspenso.  
  
1.  No menu suspenso, clique em **Gerenciar** e selecione a guia **Opções de Processamento** .  
  
2.  Clique em **Renderizar este relatório em um instantâneo de execução de relatórios**e selecione uma das seguintes opções:  
  
    -   Se desejar criar um instantâneo, selecione **Use o agendamento a seguir para criar instantâneos de execução de relatórios**e defina uma agenda específica ao relatório ou selecione uma opção na lista **Agenda compartilhada** .  
  
    -   Se desejar criar um instantâneo imediatamente, selecione **Criar um instantâneo de relatórios ao clicar no botão Aplicar nesta página**.  
  
3.  Clique em **Aplicar**.  
  
## <a name="see-also"></a>Consulte Também  
 [Definir as propriedades do processamento de relatórios](../../reporting-services/report-server/set-report-processing-properties.md)   
 [Página Conteúdo &#40;Gerenciador de Relatórios&#41;](https://msdn.microsoft.com/library/6b16869b-158a-4934-9c85-bee934b35378)   
 [Gerenciamento do conteúdo do Servidor de Relatório &#40;Modo Nativo do SSRS&#41;](../../reporting-services/report-server/report-server-content-management-ssrs-native-mode.md)   
 [Página de propriedades Opções de Processamento &#40;Gerenciador de Relatórios&#41;](https://msdn.microsoft.com/library/28f07c70-7132-4d15-9505-4fdf31dc9cc0)  
  
::: moniker-end

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
  
## <a name="to-configure-report-execution-properties"></a>Para configurar propriedades de execução de relatório  
  
Do [portal da Web de um servidor de relatório (Modo Nativo do SSRS)](../../reporting-services/web-portal-ssrs-native-mode.md):  
  
1. Navegue até o relatório para o qual você deseja configurar as propriedades de execução.  
  
2. Clique com botão direito do mouse e selecione **gerenciar** no menu suspenso.

3. Selecione o **instantâneos de histórico** guia para exibir o **instantâneos de histórico** página.  
  
4. Selecione **agendamentos e configurações** botão e, em seguida, verifique **criar instantâneos de histórico segundo uma agenda** se já não estiver marcada.
  
5. Selecione uma **agenda compartilhada** ou um **agenda específica do relatório** conforme desejado.  
  
6. No **Advanced** , selecione o desejado **retenção** política para os instantâneos de histórico.  
  
7. Escolha **Aplicar**.  
  
   >[!NOTE]
   >Se você quiser criar um instantâneo imediatamente, selecione o **novo instantâneo de histórico** botão em vez da **agendamentos e configurações** botão e um instantâneo de relatório serão criado imediatamente.  
  
## <a name="see-also"></a>Confira também  
 [Definir as propriedades do processamento de relatórios](../../reporting-services/report-server/set-report-processing-properties.md)   
 [Gerenciamento do conteúdo do servidor de relatório (Modo Nativo SSRS)](../../reporting-services/report-server/report-server-content-management-ssrs-native-mode.md)   
 [Definir propriedades de processamento de relatórios](../../reporting-services/report-server/set-report-processing-properties.md)   

::: moniker-end