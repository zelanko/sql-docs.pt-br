---
title: Barra de status (Editor de Consultas do Mecanismo de Banco de Dados) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
ms.assetid: e7f2d6f4-bb94-4cf5-a096-c34397e679af
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 11b55e2faeb251f8c3a7ab5220d9716476e66639
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52512076"
---
# <a name="status-bar-database-engine-query-editor"></a>Barra de status (Editor de Consultas do Mecanismo de Banco de Dados)
  A barra de status das janelas do Editor de Consultas do [!INCLUDE[ssDE](../../includes/ssde-md.md)] podem ser codificadas por cor para indicar a qual instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] cada janela está conectada.  
  
1.  **Antes de começar:**  [Cores da barra de status](#StatusBarColors)  
  
2.  **Para definir uma cor de status em:**  [Pesquisador de objetos](#SetOEServerColor), [servidor registrado](#SetRegServerColor)  
  
3.  **Para usar uma cor de status:**  [Abra o Editor de consulta usando uma cor de servidor](#OpenServerColor), [abrir um Editor de consultas especificando uma cor de Status](#OpenSpecColor)  
  
##  <a name="StatusBarColors"></a> Cores da barra de status  
 Você pode associar uma cor de barra de status a um nó de servidor específico em **Pesquisador de Objetos** ou **Servidores Registrados**. As cores podem ser especificadas somente para nós de servidor conectados a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)], e não para nós de servidor de outras tecnologias do SQL Server. Você também pode especificar uma cor de barra de status personalizada sempre que você conecta uma nova janela do Editor de Consultas do [!INCLUDE[ssDE](../../includes/ssde-md.md)] a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Em seguida, você pode abrir uma janela do Editor de Consultas usando a cor de status definida para o nó do servidor ou especificar uma cor exclusiva para essa janela do editor.  
  
 A definição de uma cor de barra de status personalizada para um nó de servidor no Pesquisador de Objetos deve ser feita durante o estabelecimento da conexão. Para alterar a cor associada a um nó de servidor existente, desconecte e reconecte especificando a nova cor.  
  
##  <a name="SetOEServerColor"></a> Definir a cor de status para um servidor no Pesquisador de Objetos  
 **Para definir uma cor de status no Pesquisador de Objetos**  
  
1.  No **Pesquisador de Objetos**, selecione o botão **Conectar** e depois a opção **Mecanismo de Banco de Dados...**.  
  
2.  Na caixa de diálogo **Conectar ao Servidor**, selecione **Opções >>**.  
  
3.  Marque a caixa de seleção **Usar cor personalizada** .  
  
4.  Para selecionar a cor, selecione o botão **Selecionar...**.  
  
5.  Selecione uma cor básica ou personalizada e clique em OK.  
  
6.  Preencha o restante das informações de conexão e selecione o botão **Conectar** .  
  
##  <a name="SetRegServerColor"></a> Definir a cor de status para um servidor registrado  
 **Par definir uma cor de status para um servidor registrado**  
  
1.  Em **Servidores Registrados**, clique com o botão direito do mouse no nó de servidor e selecione **Propriedades...**.  
  
2.  Na caixa de diálogo **Editar Propriedades de Registro do Servidor** , selecione a guia **Propriedades de Conexão** .  
  
3.  Marque a caixa de seleção **Usar cor personalizada** .  
  
4.  Para selecionar a cor, selecione o botão **Selecionar...**.  
  
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
  
-   Para selecionar a cor, selecione o botão **Selecionar...**.  
  
-   Selecione uma cor básica ou personalizada e clique em OK.  
  
-   Preencha o restante das informações de conexão e selecione o botão **Conectar** .  
  
## <a name="see-also"></a>Consulte também  
 [Editores de consultas e de texto &#40;SQL Server Management Studio&#41;](../scripting/query-and-text-editors-sql-server-management-studio.md)  
  
  
