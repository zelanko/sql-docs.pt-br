---
title: "Importar um domínio de um arquivo .dqs | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- data-quality-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: fabd88b0-22b3-4543-a993-6d5b202ded80
caps.latest.revision: 18
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: ae4adc315932a7632077913866b648cba4947a9d
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="import-a-domain-from-a-dqs-file"></a>Importar um domínio de um arquivo .dqs
  Este tópico descreve como importar um domínio de um arquivo .dqs para uma base de dados de conhecimento existente no [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS). Um arquivo de dados .dqs é criado por meio da exportação de um domínio ou de uma base de dados de conhecimento do aplicativo [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] . Um arquivo de dados .dqs é criptografado e, portanto, não pode ser exibido.  
  
 O uso de um arquivo de dados .dqs para exportar um domínio de uma base de dados de conhecimento e, em seguida, importá-lo para outra base de dados de conhecimento simplifica o processo de geração de conhecimento, economizando tempo e esforço. Isso permite que você compartilhe um domínio e seu conhecimento com outras pessoas, fazendo-as ganhar tempo. Você pode importar um único domínio ou um domínio composto (com vários domínios únicos). Um arquivo .dqs com um único domínio inclui todos os dados do domínio, inclusive os dados de propriedades, valores e regras do domínio, exceto para as informações de dados referenciados mapeados. Um arquivo .dqs com um domínio composto inclui todos os dados do domínio composto, incluindo todos os dados do domínio para os domínios únicos contidos no domínio composto, além das propriedades de domínio composto, das relações de valor e das regras de CD, exceto para os dados referenciados mapeados. Os dados publicados e não publicados serão importados.  
  
 Quando você importa um domínio, o nome do domínio permanece igual ao nome do domínio que foi exportado originalmente, a menos que o nome de domínio já exista; nesse caso, o DQS acrescentará "_1" ao nome. Isso também será verdade se você importar um domínio composto com um domínio individual com o mesmo nome de um domínio existente.  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Prerequisites"></a> Pré-requisitos  
 Para importar um domínio de um arquivo .dqs, você já deverá ter exportado um domínio único ou um domínio composto (com vários domínios únicos) para o arquivo .dqs. O arquivo .dqs só deve conter um domínio. Você também deverá ter criado e aberto uma base de dados de conhecimento para onde o domínio será importado.  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Você deve ter a função dqs_kb_editor ou dqs_administrator no banco de dados DQS_MAIN para poder importar um domínio de um arquivo de dados .dqs.  
  
##  <a name="Import"></a> Import a domain from a .dqs file  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)] [Executar o aplicativo Data Quality Client](../data-quality-services/run-the-data-quality-client-application.md).  
  
2.  Na tela inicial do [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] , abra uma base de dados de conhecimento na atividade Gerenciamento de Domínio.  
  
3.  Clique no **Importar Domínio do arquivo de dados** .  
  
4.  Na caixa de diálogo **Importar do Arquivo de Dados** , vá para a pasta de onde deseja importar o arquivo, selecione o arquivo (do tipo Arquivo DQS) e clique em **Abrir**.  
  
5.  Na caixa de diálogo **Importar Domínio** , clique no botão **OK**.  
  
    > [!NOTE]  
    >  A operação de importação só terá êxito se o arquivo .dqs que estiver sendo importado contiver somente um domínio único ou um domínio composto (com vários domínios únicos).  
  
6.  Verifique se o domínio que você importou é exibido na lista **Domínio** . Se você importou um domínio composto, verifique se o domínio composto e os domínios únicos contidos nele estão na lista **Domínio** .  
  
##  <a name="FollowUp"></a> Acompanhamento: depois de importar um domínio de um arquivo .dqs  
 Depois que você importar um domínio de um arquivo .dqs, poderá adicionar conhecimento ao domínio ou usar o domínio em um projeto de limpeza ou de correspondência, dependendo do conteúdo do domínio. Para obter mais informações, consulte [Executar a descoberta de conhecimento](../data-quality-services/perform-knowledge-discovery.md), [Gerenciando um domínio](../data-quality-services/managing-a-domain.md), [Gerenciando um domínio de composição](../data-quality-services/managing-a-composite-domain.md), [Criar uma política de conciliação](../data-quality-services/create-a-matching-policy.md), [Limpeza de dados](../data-quality-services/data-cleansing.md) ou [Correspondência de dados](../data-quality-services/data-matching.md).  
  
  
