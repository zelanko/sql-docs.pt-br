---
title: "Configurar propriedades de execu&#231;&#227;o de um relat&#243;rio (Gerenciador de Relat&#243;rios) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "propriedades de execução de relatório [Reporting Services]"
  - "relatórios [Reporting Services], propriedades"
  - "relatórios [Reporting Services], opções de execução"
ms.assetid: 73cc8dcc-ef80-40d7-9739-d33bba0eb28a
caps.latest.revision: 41
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 41
---
# Configurar propriedades de execu&#231;&#227;o de um relat&#243;rio (Gerenciador de Relat&#243;rios)
  Você pode definir opções de processamento de relatório para especificar quando os dados são recuperados para um relatório. É útil agendar o processamento de dados de um relatório se a fonte de dados externa for atualizada em horários específicos (por exemplo, um data warehouse que é atualizado diária ou semanalmente) e você desejar evitar a sobrecarga da recuperação dos mesmos dados sempre que um relatório for solicitado. O agendamento do processamento de dados também é útil se você desejar controlar a carga de processamento no servidor de banco de dados externo ou quando você quiser fornecer resultados consistentes para vários usuários que devem trabalhar com conjuntos de dados idênticos. Com dados voláteis, um relatório sob demanda pode produzir resultados diferentes de um minuto para o outro. Por outro lado, um instantâneo de relatório permite fazer comparações válidas com outros relatórios ou ferramentas analíticas que contêm dados do mesmo momento.  
  
 Um instantâneo de relatório é um relatório que contém instruções sobre layout e resultados de consulta que foram recuperados em um momento específico. Diferente dos relatórios sob demanda, que obtêm resultados de consulta atualizados quando o relatório é selecionado, os instantâneos de relatório são processados em uma agenda e salvos em um servidor de relatório. Quando você seleciona um instantâneo de relatório para exibição, o servidor de relatório recupera o relatório armazenado do banco de dados do servidor e mostra os dados e o layout correspondentes ao momento em que o instantâneo foi criado.  
  
 Os instantâneos de relatório não são salvos em um formato de renderização específico. Em vez disso, os instantâneos de relatório são renderizados em um formato de exibição final (como HTML) somente quando solicitado por um usuário ou aplicativo. A renderização adiada deixa o instantâneo portátil. O relatório pode ser renderizado no formato correto para a solicitação do dispositivo ou navegador da Web.  
  
### Para configurar opções de processamento de relatório  
  
1.  Inicie o [Gerenciador de Relatórios &#40;Modo Nativo do SSRS&#41;](../Topic/Report%20Manager%20%20\(SSRS%20Native%20Mode\).md).  
  
2.  Navegue até o relatório cujas opções de processamento você deseja definir e abra-o.  
  
 Focalize o relatório e clique na seta do menu suspenso.  
  
1.  No menu suspenso, clique em **Gerenciar** e selecione a guia **Opções de Processamento**.  
  
2.  Clique em **Renderizar este relatório em um instantâneo de execução de relatórios** e selecione uma das seguintes opções:  
  
    -   Se desejar criar um instantâneo, selecione **Use o agendamento a seguir para criar instantâneos de execução de relatórios** e defina uma agenda específica ao relatório ou selecione uma opção na lista **Agenda compartilhada**.  
  
    -   Se desejar criar um instantâneo imediatamente, selecione **Criar um instantâneo de relatórios ao clicar no botão Aplicar nesta página**.  
  
3.  Clique em **Aplicar**.  
  
## Consulte também  
 [Definir propriedades de processamento de relatórios](../../reporting-services/report-server/set-report-processing-properties.md)   
 [Abrir e fechar um relatório &#40;Gerenciador de Relatórios&#41;](../../reporting-services/reports/open-and-close-a-report-report-manager.md)   
 [Página Conteúdo &#40;Gerenciador de Relatórios&#41;](../Topic/Contents%20Page%20\(Report%20Manager\).md)   
 [Gerenciamento do conteúdo do Servidor de Relatório &#40;Modo Nativo do SSRS&#41;](../../reporting-services/report-server/report-server-content-management-ssrs-native-mode.md)   
 [Página de propriedades Opções de Processamento &#40;Gerenciador de Relatórios&#41;](../Topic/Processing%20Options%20Properties%20Page%20\(Report%20Manager\).md)  
  
  