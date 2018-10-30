---
title: Configurar as propriedades de execução de um relatório (Gerenciador de Relatórios) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: reports
ms.topic: conceptual
helpviewer_keywords:
- report execution properties [Reporting Services]
- reports [Reporting Services], properties
- reports [Reporting Services], execution options
ms.assetid: 73cc8dcc-ef80-40d7-9739-d33bba0eb28a
author: markingmyname
ms.author: maghan
ms.openlocfilehash: f3246d531a497706a2f73bb713dc382abf8bd29f
ms.sourcegitcommit: 3daacc4198918d33179f595ba7cd4ccb2a13b3c0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/25/2018
ms.locfileid: "50020510"
---
# <a name="configure-execution-properties-for-a-report--report-manager"></a>Configurar propriedades de execução de um relatório (Gerenciador de Relatórios)
  Você pode definir opções de processamento de relatório para especificar quando os dados são recuperados para um relatório. É útil agendar o processamento de dados de um relatório se a fonte de dados externa for atualizada em horários específicos (por exemplo, um data warehouse que é atualizado diária ou semanalmente) e você desejar evitar a sobrecarga da recuperação dos mesmos dados sempre que um relatório for solicitado. O agendamento do processamento de dados também é útil se você desejar controlar a carga de processamento no servidor de banco de dados externo ou quando você quiser fornecer resultados consistentes para vários usuários que devem trabalhar com conjuntos de dados idênticos. Com dados voláteis, um relatório sob demanda pode produzir resultados diferentes de um minuto para o outro. Por outro lado, um instantâneo de relatório permite fazer comparações válidas com outros relatórios ou ferramentas analíticas que contêm dados do mesmo momento.  
  
 Um instantâneo de relatório é um relatório que contém instruções sobre layout e resultados de consulta que foram recuperados em um momento específico. Diferente dos relatórios sob demanda, que obtêm resultados de consulta atualizados quando o relatório é selecionado, os instantâneos de relatório são processados em uma agenda e salvos em um servidor de relatório. Quando você seleciona um instantâneo de relatório para exibição, o servidor de relatório recupera o relatório armazenado do banco de dados do servidor e mostra os dados e o layout correspondentes ao momento em que o instantâneo foi criado.  
  
 Os instantâneos de relatório não são salvos em um formato de renderização específico. Em vez disso, os instantâneos de relatório são renderizados em um formato de exibição final (como HTML) somente quando solicitado por um usuário ou aplicativo. A renderização adiada deixa o instantâneo portátil. O relatório pode ser renderizado no formato correto para a solicitação do dispositivo ou navegador da Web.  
  
### <a name="to-configure-report-processing-options"></a>Para configurar opções de processamento de relatório  
  
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
 [Abrir e fechar um relatório &#40;Gerenciador de Relatórios&#41;](../../reporting-services/reports/open-and-close-a-report-report-manager.md)   
 [Página Conteúdo &#40;Gerenciador de Relatórios&#41;](https://msdn.microsoft.com/library/6b16869b-158a-4934-9c85-bee934b35378)   
 [Gerenciamento do conteúdo do Servidor de Relatório &#40;Modo Nativo do SSRS&#41;](../../reporting-services/report-server/report-server-content-management-ssrs-native-mode.md)   
 [Página de propriedades Opções de Processamento &#40;Gerenciador de Relatórios&#41;](https://msdn.microsoft.com/library/28f07c70-7132-4d15-9505-4fdf31dc9cc0)  
  
  
