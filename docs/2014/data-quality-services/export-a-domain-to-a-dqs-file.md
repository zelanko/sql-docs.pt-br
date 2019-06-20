---
title: Exportar um domínio para um arquivo .dqs | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: eba10d3d-b5c4-447b-8a30-fa07996cb28e
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: b5b12aa1456f7f4009f48a8c8609f296dfa4b27d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65484338"
---
# <a name="export-a-domain-to-a-dqs-file"></a>Exportar um domínio para um arquivo .dqs
  Este tópico descreve como exportar um domínio para um arquivo .dqs no [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS). Você pode exportar um domínio ou uma base de dados de conhecimento inteira para um arquivo de dados. Para obter informações sobre como exportar uma base de dados de conhecimento, consulte [Exportar uma base de dados de conhecimento para um arquivo .dqs](../../2014/data-quality-services/export-a-knowledge-base-to-a-dqs-file.md).  
  
 A exportação de um domínio de uma base de dados de conhecimento para um arquivo de dados .dqs e sua subsequente importação para outra base de dados de conhecimento simplifica o processo de geração de conhecimento, economizando tempo e esforço. Isso permite que você compartilhe um domínio e sua base de dados de conhecimento com outras pessoas.  
  
 Você pode exportar um domínio único ou um domínio composto. Um arquivo .dqs com um único domínio inclui todos os dados do domínio, inclusive propriedades, valores e regras do domínio, exceto para as informações de dados de referência anexadas. Um arquivo .dqs com um domínio composto inclui todos os dados do domínio composto, incluindo todos os dados do domínio para os domínios contidos no domínio composto, além das propriedades, relações e regras de domínio, exceto para as informações de dados de referência. Você deve anexar novamente o domínio ou o domínio composto aos serviços de dados de referência apropriado, se necessário, depois de importar o arquivo .dqs. Os dados publicados e não publicados serão exportados.  
  
 O arquivo de dados .dqs criado pelo processo de exportação é criptografado; portanto, o conteúdo não pode ser exibido.  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Prerequisites"></a> Pré-requisitos  
 Para exportar um domínio para um arquivo .dqs, você deve ter criado e selecionado um domínio único ou um domínio composto contendo vários domínios únicos. Você não precisa ter um arquivo .dqs para exportação; um arquivo será criado para você.  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Você deve ter a função dqs_kb_editor ou dqs_administrator no banco de dados DQS_MAIN para poder exportar um domínio para um arquivo de dados .dqs.  
  
##  <a name="Export"></a> Export a domain to a .dqs file  
 Você pode exportar de qualquer página Gerenciamento de Domínio. O comando de exportação está disponível de um controle na interface do usuário e de um comando no menu de contexto do painel Lista de Domínios.  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)] [Executar o aplicativo Data Quality Client](../../2014/data-quality-services/run-the-data-quality-client-application.md).  
  
2.  Na tela inicial do [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] , abra uma base de dados de conhecimento na atividade Gerenciamento de Domínio.  
  
3.  Na página **Gerenciamento de Domínio** (com qualquer guia selecionada), selecione um domínio único ou um domínio composto na lista **Domínio** .  
  
4.  Clique no ícone **Exportar dados da Base de Dados de Conhecimento** acima da lista de domínios e clique em **Exportar Domínio**. Alternativamente, você pode clicar com o botão direito do mouse no domínio na lista **Domínio** , aponte para **Exportar**e clique em **Exportar Domínio**.  
  
5.  Na caixa de diálogo **Exportar para Arquivo de Dados**, vá para a pasta na qual você deseja salvar o arquivo, nomeie o arquivo ou mantenha o nome padrão, mantenha **Arquivos de Dados do DQS (\*.dqs)** como **Salvar como tipo** e, em seguida, clique em **Salvar**.  
  
6.  Na caixa de diálogo **Exportar Domínio** , verifique se a linha de status indica que a exportação foi concluída. Clique em **OK**.  
  
##  <a name="FollowUp"></a> Acompanhamento: Após exportar um domínio para um arquivo .dqs  
 Depois que você exportar um domínio para um arquivo .dqs, poderá importar o domínio para outra base de dados de conhecimento.  
  
  
