---
title: Barra de status (Editor de Consultas do Mecanismo de Banco de Dados) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssms-scripting
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: e7f2d6f4-bb94-4cf5-a096-c34397e679af
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 25820cea52bc5add459a5b86017086e3ecf50508
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="status-bar-database-engine-query-editor"></a>Barra de status (Editor de Consultas do Mecanismo de Banco de Dados)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  A barra de status das janelas do Editor de Consultas do [!INCLUDE[ssDE](../../includes/ssde-md.md)] podem ser codificadas por cor para indicar a qual instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] cada janela está conectada.  
  
1.  **Antes de começar:**  [Cores da barra de status](#StatusBarColors)  
  
2.  **Para definir uma cor de status do servidor no:**  [Pesquisador de Objetos](#SetOEServerColor), [Servidor Registrado](#SetRegServerColor)  
  
3.  **Para usar uma cor de status:**  [Abrir o Editor de Consultas que usando uma cor de servidor](#OpenServerColor), [Abrir o Editor de Consultas especificando uma cor de status](#OpenSpecColor)  
  
##  <a name="StatusBarColors"></a> Cores da barra de status  
 Você pode associar uma cor de barra de status a um nó de servidor específico em **Pesquisador de Objetos** ou **Servidores Registrados**. As cores podem ser especificadas somente para nós de servidor conectados a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)], e não para nós de servidor de outras tecnologias do SQL Server. Você também pode especificar uma cor de barra de status personalizada sempre que você conecta uma nova janela do Editor de Consultas do [!INCLUDE[ssDE](../../includes/ssde-md.md)] a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Em seguida, você pode abrir uma janela do Editor de Consultas usando a cor de status definida para o nó do servidor ou especificar uma cor exclusiva para essa janela do editor.  
  
 A definição de uma cor de barra de status personalizada para um nó de servidor no Pesquisador de Objetos deve ser feita durante o estabelecimento da conexão. Para alterar a cor associada a um nó de servidor existente, desconecte e reconecte especificando a nova cor.  
  
##  <a name="SetOEServerColor"></a> Definir a cor de status para um servidor no Pesquisador de Objetos  
 **Para definir uma cor de status no Pesquisador de Objetos**  
  
1.  No **Pesquisador de Objetos**, selecione o botão **Conectar** e depois a opção **Mecanismo de Banco de Dados…**.  
  
2.  Na caixa de diálogo **Conectar ao Servidor**, selecione **Opções >>**.  
  
3.  Marque a caixa de seleção **Usar cor personalizada** .  
  
4.  Para selecionar a cor, selecione o botão **Selecionar…** .  
  
5.  Selecione uma cor básica ou personalizada e clique em OK.  
  
6.  Preencha o restante das informações de conexão e selecione o botão **Conectar** .  
  
##  <a name="SetRegServerColor"></a> Definir a cor de status para um servidor registrado  
 **Par definir uma cor de status para um servidor registrado**  
  
1.  Em **Servidores Registrados**, clique com o botão direito no nó do servidor e selecione **Propriedades…**.  
  
2.  Na caixa de diálogo **Editar Propriedades de Registro do Servidor** , selecione a guia **Propriedades de Conexão** .  
  
3.  Marque a caixa de seleção **Usar cor personalizada** .  
  
4.  Para selecionar a cor, selecione o botão **Selecionar…** .  
  
5.  Selecione uma cor básica ou personalizada e clique em OK.  
  
6.  Selecione o botão **Salvar** na caixa de diálogo **Editar Propriedades de Registro do Servidor** .  
  
##  <a name="OpenServerColor"></a> Abrir um editor usando uma cor de servidor  
 **Para abrir uma janela do editor usando uma cor de servidor**  
  
-   Clique com o botão direito do mouse em um nó de servidor no **Pesquisador de Objetos** ou em **Servidores Registrados**e selecione **Nova Consulta**.  
  
-   Opcionalmente, realce um nó de servidor e selecione o botão **Nova Consulta** na barra de ferramentas.  
  
-   A barra de status da janela do editor usará a cor definida para o servidor associado.  
  
##  <a name="OpenSpecColor"></a> Abrir um editor especificando uma cor de status  
 **Para abrir uma janela do editor especificando uma cor de status**  
  
-   Abra o menu **Arquivo** , selecione **Novo**e, em seguida, selecione **Consulta do Mecanismo de Banco de Dados**.  
  
-   Na caixa de diálogo **Conectar ao Servidor**, selecione **Opções >>**.  
  
-   Marque a caixa de seleção **Usar cor personalizada** .  
  
-   Para selecionar a cor, selecione o botão **Selecionar…** .  
  
-   Selecione uma cor básica ou personalizada e clique em OK.  
  
-   Preencha o restante das informações de conexão e selecione o botão **Conectar** .  
  
## <a name="see-also"></a>Consulte Também  
 [Editores de consultas e de texto &#40;SQL Server Management Studio&#41;](../../relational-databases/scripting/query-and-text-editors-sql-server-management-studio.md)  
  
  
