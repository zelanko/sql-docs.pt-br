---
title: Conectar ao Servidor (página Parâmetros Adicionais de Conexão) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- sql12.swb.connecttoserver.options.registeredservers.f1
ms.assetid: ba34b01a-6289-4eb8-8341-fa3d9ec87b3f
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e92fbb8bc29aed54e43925a0670d9a365388df62
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62808667"
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
  
### <a name="example-a-connecting-to-the-database-engine"></a>Exemplo a: conexão ao mecanismo de banco de dados  
 Para conectar ao banco de dados do [!INCLUDE[ssSampleDBnormal](../includes/sssampledbnormal-md.md)] em um servidor nomeado CONTABILIDADE, digite o seguinte na página **Parâmetros de conexão adicionais** :  
  
```  
;SERVER=ACCOUNTING;DATABASE=AdventureWorks2012  
```  
  
### <a name="example-b-connecting-to-analysis-services"></a>Exemplo b: Conectar-se ao Analysis Services  
 Para conectar aos servidores de análises e fazer todas as partições escutarem as notificações a serem consultadas em tempo real (ignorando o cache) e para definir o valor do tempo limite de write-back como 5, digite o seguinte na página **Parâmetros de conexão adicionais** :  
  
```  
;Real Time Olap=TRUE;Writeback Timeout=5  
```  
  
  
