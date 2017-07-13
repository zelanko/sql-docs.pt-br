---
title: "Trabalhar com instantâneos (portal da web) | Microsoft Docs"
ms.custom: 
ms.date: 07/02/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 9ae20556-e243-4a60-b076-9fd9e82c7355
caps.latest.revision: 6
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: dcf26be9dc2e502b2d01f5d05bcb005fd7938017
ms.openlocfilehash: 2bca4e3089bde763669c4fe518f509fbe94cb6eb
ms.contentlocale: pt-br
ms.lasthandoff: 07/03/2017

---

# Trabalhando com instantâneos (portal da Web)
<a id="working-with-snapshots-web-portal" class="xliff"></a>

[!INCLUDE[ssrs-appliesto](../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../includes/ssrs-appliesto-pbirs.md)]

Você pode controlar se os instantâneos são criados para um relatório selecionando o **reticências (...)**  de um relatório, selecionando **gerenciar** e selecionando **cache** ou **instantâneos de histórico**.  
  
> [!NOTE]
> O serviço SQL Server Agent precisa ser iniciado.  
   
Você pode criar um instantâneo de cache para permitir um carregamento mais rápido de propriedades específicas de execução. Você também pode trabalhar com instantâneos de histórico para capturas pontuais.  
  
## Criando um instantâneo de cache
<a id="creating-a-cache-snapshot" class="xliff"></a>  
  
Você pode criar um instantâneo fazendo o seguinte.  
  
![ssRSWebPortal-report-caching4](../reporting-services/media/ssrswebportal-report-caching4.png)  
  
1.  Na página **Cache** , selecione **Sempre executar esse relatório contra instantâneos gerados previamente** para habilitar as opções para a criação de um instantâneo.  
  
2.  Selecione **Criar instantâneos do cache segundo uma agenda** se quiser agendar um instantâneo recorrente. Você pode usar uma agenda compartilhada ou definir uma agenda personalizada para atualizar o instantâneo.  
  
3.  Selecione **Criar um instantâneo do cache quando eu clicar em Aplicar, nesta página** se quiser criar um instantâneo do cache agora. Se você selecionar somente essa opção, o instantâneo não será atualizado.  
  
## Criar, modificar e excluir instantâneos de histórico
<a id="create-modify-and-delete-history-snapshots" class="xliff"></a>  
  
Para trabalhar com instantâneos de histórico, gerencie um relatório e selecione **Instantâneos de Histórico**.  
  
Use a página **Instantâneos de Histórico** para exibir instantâneos de relatórios gerados e armazenados ao longo do tempo. Dependendo das opções definidas no servidor de relatório, o histórico poderá conter somente os instantâneos mais recentes.  
  
O histórico de relatório é sempre exibido no contexto do relatório de origem. Você não pode exibir o histórico de todos os relatórios em um servidor de relatórios em um único lugar.  
  
Para gerar um instantâneo de histórico, o relatório deve ser executado de modo autônomo (ou seja, ele deve usar credenciais armazenadas; relatórios com parâmetros devem conter valores de parâmetro padrão para todos os parâmetros). Histórico de Relatórios pode ser gerado manualmente ou como uma operação agendada. As propriedades de histórico no relatório determinam os modos pelos quais o histórico do relatório pode ser criado.  
  
![ssRSWebPortal-historysnapshots1](../reporting-services/media/ssrswebportal-historysnapshots1.png)  
   
1.  Para criar um instantâneo de histórico, selecione **+ Novo Instantâneo de Histórico**. Com isso, o relatório será processado e uma entrada será adicionada à lista.  
  
2.  Você poderá acessar as configurações para definir agendas e políticas de retenção.  
  
3.  Você poderá selecionar um instantâneo de histórico a ser exibido. Instantâneos exibidos em histórico de relatórios só são diferenciados pela data e hora em que foram criados. Não existe indicação visual para distinguir se um relatório foi gerado em resposta a uma operação programada ou manual.  
  
### Agenda e configurações
<a id="schedule-and-settings" class="xliff"></a>  
  
Selecionar **Agenda e Configurações** fornecerá opções adicionais para agendar e controlar a retenção dos instantâneos criados.  
  
![ssRSWebPortal-historysnapshots2](../reporting-services/media/ssrswebportal-historysnapshots2.png)  
   
Como opção, você pode criar uma agenda para a criação de instantâneos. Você também pode impedir que outras pessoas criem novos instantâneos. Desmarcar a opção **Permitir que as pessoas criem instantâneos manualmente** desabilitará o botão **+ Novo Instantâneo de Histórico**.  
  
Você também pode definir como quer reter os instantâneos.  
  
**Salvar instantâneos de cache no histórico de relatórios também**  
  
Marcar essa opção copiará um instantâneo de relatório gerado com base nas propriedades de execução de relatório no histórico de relatórios. Você pode definir propriedades de execução de relatório para executar um relatório de um instantâneo gerado. Definindo essa propriedade de histórico de relatórios você pode manter um registro de todos os instantâneos gerados com o tempo, colocando cópias deles no histórico de relatórios.

## Próximas etapas
<a id="next-steps" class="xliff"></a>

[Portal da Web](../reporting-services/web-portal-ssrs-native-mode.md)  
[Trabalhando com relatórios paginados](working-with-paginated-reports-web-portal.md)  
[Trabalhar com conjuntos de dados compartilhados](../reporting-services/work-with-shared-datasets-web-portal.md)

Mais perguntas? [Tente fazer o fórum do Reporting Services](http://go.microsoft.com/fwlink/?LinkId=620231)
