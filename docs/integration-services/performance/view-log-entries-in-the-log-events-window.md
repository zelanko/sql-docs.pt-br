---
title: "Exibir entradas de log na janela Eventos de Log | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "logs [Integration Services], exibindo"
  - "pacotes do Integration Services, logs"
  - "pacotes [Integration Services], logs"
ms.assetid: c02123c3-67fc-4370-ad14-91ed259f1873
caps.latest.revision: 21
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 21
---
# Exibir entradas de log na janela Eventos de Log
  Este procedimento descreve como executar um pacote e exibir as entradas de log que ele grava. Você pode exibir as entradas de log em tempo real. As entradas de log, gravadas na janela **Eventos de Log**, também podem ser copiadas e salvas para uma análise posterior.  
  
 Não é necessário gravar as entradas de log em um log para gravar as entradas na janela **Eventos de Log**.  
  
### Para exibir entradas de log  
  
1.  No [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], abra o projeto do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que contém o pacote desejado.  
  
2.  No menu **SSIS**, clique em **Eventos de Log**. Opcionalmente, você pode exibir a janela **Eventos de Log** mapeando o comando View.LogEvents com uma combinação de teclas escolhidas por você na página **Teclado** da caixa de diálogo **Opções**.  
  
3.  No menu **Depurar** , clique em **Iniciar Depuração**.  
  
     Quando o tempo de execução encontra os eventos e as mensagens personalizadas habilitadas para registro, as entradas de log para cada evento ou mensagem são gravadas na janela **Eventos de Log**.  
  
4.  No menu **Depurar** , clique em **Parar Depuração**.  
  
     As entradas de log permanecem disponíveis na janela **Eventos de Log** até que você execute novamente o pacote, execute um pacote diferente ou feche o [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)].  
  
5.  Exibir as entradas de log na janela **Eventos de Log**.  
  
6.  Opcionalmente, clique nas entradas de log para copiar, clique com o botão direito do mouse e clique em **Copiar**.  
  
7.  Opcionalmente, clique duas vezes em uma entrada de log e, na caixa de diálogo **Entrada de Log**, exiba os detalhes de uma única entrada de log.  
  
8.  Na caixa de diálogo **Entrada de Log**, clique nas setas para baixo e para cima para exibir a entrada de log anterior ou posterior e clique no ícone de cópia para copiar a entrada de log.  
  
9. Abra um editor de textos, cole e salve a entrada de log em um arquivo de texto.  
  
## Consulte também  
 [Registro em Log do Integration Services &#40;SSIS&#41;](../../integration-services/performance/integration-services-ssis-logging.md)  
  
  