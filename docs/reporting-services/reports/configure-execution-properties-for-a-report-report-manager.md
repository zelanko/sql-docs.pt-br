---
title: Configurar as propriedades de execução de um relatório (Reporting Services) | Microsoft Docs
description: Saiba como definir opções de processamento de relatório para especificar quando recuperar dados de relatório para evitar a sobrecarga de recuperar os mesmos dados cada vez que um relatório é solicitado.
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
ms.openlocfilehash: 9b1cecda6c4ec085efe7b18392eb06f06866352b
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97466557"
---
# <a name="configure-execution-properties-for-a-report"></a>Configurar propriedades de execução de um relatório
  Você pode definir opções de processamento de relatório para especificar quando os dados são recuperados para um relatório. É útil agendar o processamento de dados de um relatório se a fonte de dados externa for atualizada em horários específicos (por exemplo, um data warehouse que é atualizado diária ou semanalmente) e você desejar evitar a sobrecarga da recuperação dos mesmos dados sempre que um relatório for solicitado. O agendamento do processamento de dados também é útil se você desejar controlar a carga de processamento no servidor de banco de dados externo ou quando você quiser fornecer resultados consistentes para vários usuários que devem trabalhar com conjuntos de dados idênticos. Com dados voláteis, um relatório sob demanda pode produzir resultados diferentes de um minuto para o outro. Por outro lado, um instantâneo de relatório permite fazer comparações válidas com outros relatórios ou ferramentas analíticas que contêm dados do mesmo momento.  
  
 Um instantâneo de relatório é um relatório que contém instruções sobre layout e resultados de consulta que foram recuperados em um momento específico. Diferente dos relatórios sob demanda, que obtêm resultados de consulta atualizados quando o relatório é selecionado, os instantâneos de relatório são processados em uma agenda e salvos em um servidor de relatório. Quando você seleciona um instantâneo de relatório para exibição, o servidor de relatório recupera o relatório armazenado do banco de dados do servidor e mostra os dados e o layout correspondentes ao momento em que o instantâneo foi criado.  
  
 Os instantâneos de relatório não são salvos em um formato de renderização específico. Em vez disso, os instantâneos de relatório são renderizados em um formato de exibição final (como HTML) somente quando solicitado por um usuário ou aplicativo. A renderização adiada deixa o instantâneo portátil. O relatório pode ser renderizado no formato correto para a solicitação do dispositivo ou navegador da Web.  

::: moniker range="=sql-server-2016"
  
## <a name="to-configure-report-processing-options"></a>Para configurar opções de processamento de relatório  
  
1.  Inicie o [Gerenciador de Relatórios &#40;Modo Nativo do SSRS&#41;](../web-portal-ssrs-native-mode.md).  
  
2.  Navegue até o relatório cujas opções de processamento você deseja definir e abra-o.  
  
 Focalize o relatório e clique na seta do menu suspenso.  
  
1.  No menu suspenso, clique em **Gerenciar** e selecione a guia **Opções de Processamento** .  
  
2.  Clique em **Renderizar este relatório em um instantâneo de execução de relatórios** e selecione uma das seguintes opções:  
  
    -   Se desejar criar um instantâneo, selecione **Use o agendamento a seguir para criar instantâneos de execução de relatórios** e defina uma agenda específica ao relatório ou selecione uma opção na lista **Agenda compartilhada** .  
  
    -   Se desejar criar um instantâneo imediatamente, selecione **Criar um instantâneo de relatórios ao clicar no botão Aplicar nesta página**.  
  
3.  Clique em **Aplicar**.  
  
## <a name="see-also"></a>Consulte Também  
 [Definir as propriedades do processamento de relatórios](../../reporting-services/report-server/set-report-processing-properties.md)   
 [Página Conteúdo &#40;Gerenciador de Relatórios&#41;](/previous-versions/sql/sql-server-2016/ms186470(v=sql.130))   
 [Gerenciamento do conteúdo do Servidor de Relatório &#40;Modo Nativo do SSRS&#41;](../../reporting-services/report-server/report-server-content-management-ssrs-native-mode.md)   
 [Página de propriedades Opções de Processamento &#40;Gerenciador de Relatórios&#41;](/previous-versions/sql/sql-server-2016/ms178821(v=sql.130))  
  
::: moniker-end

::: moniker range=">=sql-server-2017"
  
## <a name="to-configure-report-execution-properties"></a>Para configurar propriedades de execução de relatório  
  
Do [portal da Web de um servidor de relatório (Modo Nativo do SSRS)](../../reporting-services/web-portal-ssrs-native-mode.md):  
  
1. Navegue até o relatório para o qual você deseja configurar as propriedades de execução.  
  
2. Clique com o botão direito do mouse no relatório e selecione **Gerenciar** no menu suspenso.

3. Selecione a guia **Instantâneos de histórico** para exibir a página **Instantâneos de histórico**.  
  
4. Selecione **Agendas e configurações** e marque **Criar instantâneos de histórico em uma agenda** se ainda não estiver marcado.
  
5. Selecione uma **Agenda compartilhada** ou uma **Agenda específica do relatório** conforme desejado.  
  
6. Na seção **Avançado**, selecione a política de **Retenção** desejada dos instantâneos de histórico.  
  
7. Escolha **Aplicar**.  
  
   >[!NOTE]
   >Se desejar criar um instantâneo imediatamente, selecione o botão **Novo instantâneo de histórico**, em vez do botão **Agendas e configurações**, e um instantâneo de relatório será criado imediatamente.  
  
## <a name="see-also"></a>Confira também  
 [Definir as propriedades do processamento de relatórios](../../reporting-services/report-server/set-report-processing-properties.md)   
 [Gerenciamento do conteúdo do servidor de relatório (Modo Nativo SSRS)](../../reporting-services/report-server/report-server-content-management-ssrs-native-mode.md)   
 [Definir propriedades de processamento de relatórios](../../reporting-services/report-server/set-report-processing-properties.md)   

::: moniker-end