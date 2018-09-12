---
title: Conectar ao Servidor (página Parâmetros Adicionais de Conexão) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.swb.connecttoserver.options.registeredservers.f1
ms.assetid: ba34b01a-6289-4eb8-8341-fa3d9ec87b3f
caps.latest.revision: 11
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 238a558f7b11c122012c2bfbe9538fa803fa8444
ms.sourcegitcommit: 8ae6e6618a7e9186aab3c6a37ea43776aa9a382b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/06/2018
ms.locfileid: "43816252"
---
# <a name="connect-to-server-additional-connection-parameters-page"></a>Conectar ao Servidor (página Parâmetros Adicionais de Conexão)
  A caixa de diálogo **Conectar a** do [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] apresenta os valores de cadeia de conexão mais comuns como opções. Use a página **Parâmetros Adicionais de Conexão** para acrescentar mais parâmetros de conexão à cadeia de conexões.  
  
-   Os parâmetros adicionais de conexão podem ser quaisquer parâmetro de conexão ODBC.  
  
-   Parâmetros adicionais de conexão devem ser adicionados no formato **;parameter1=value1;parameter2=value2**.  
  
-   Parâmetros adicionados através da página **Parâmetros de Conexão Adicionais** são adicionados aos parâmetros selecionados usando as opções da caixa de diálogo **Conectar a** .  
  
-   A última instância fornecida de cada parâmetro anula qualquer instância anterior do parâmetro. Parâmetros adicionados usando a página **Parâmetros de Conexão Adicionais** seguem e substituem os parâmetros fornecidos nas guias **Logon** ou **Propriedades da Conexão** . Por exemplo, se a guia **Logon** fornecer **SERVER1** como o **Nome do servidor**e a página **Parâmetros de Conexão Adicionais** contiver **;SERVER=SERVER2**, a conexão será feita com o **SERVER2**.  
  
-   Parâmetros adicionados usando a página **Parâmetros de Conexão Adicionais** sempre são transmitidos como texto sem formatação.  
  
    > [!IMPORTANT]  
    >  Não inclua credenciais de logon e senhas na guia **Parâmetros de Conexão Adicionais** . Eles não serão criptografados quando forem transmitidos pela rede. Use a guia **Logon** em vez disso.  
  
## <a name="task-list"></a>Lista de Tarefas  
  
### <a name="to-show-the-additional-connection-parameters-page"></a>Para exibir a página Parâmetros Adicionais de Conexão  
  
1.  No [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)], no menu **Consulta** , aponte a **Conexão**e clique em **Conectar**.  
  
2.  Na caixa de diálogo **Conectar a** , clique em **Opções**e depois clique na guia **Parâmetros de Conexão Adicionais** .  
  
## <a name="examples"></a>Exemplos  
  
### <a name="example-a-connecting-to-the-database-engine"></a>Exemplo A: Conectando ao Mecanismo de Banco de Dados  
 Para conectar ao banco de dados do [!INCLUDE[ssSampleDBnormal](../includes/sssampledbnormal-md.md)] em um servidor nomeado CONTABILIDADE, digite o seguinte na página **Parâmetros de conexão adicionais** :  
  
```  
;SERVER=ACCOUNTING;DATABASE=AdventureWorks2012  
```  
  
### <a name="example-b-connecting-to-analysis-services"></a>Exemplo B: Conectando a Analysis Services  
 Para conectar aos servidores de análises e fazer todas as partições escutarem as notificações a serem consultadas em tempo real (ignorando o cache) e para definir o valor do tempo limite de write-back como 5, digite o seguinte na página **Parâmetros de conexão adicionais** :  
  
```  
;Real Time Olap=TRUE;Writeback Timeout=5  
```  
  
  
