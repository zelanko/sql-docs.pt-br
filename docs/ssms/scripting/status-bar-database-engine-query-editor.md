---
title: Barra de status (Editor de Consultas do Mecanismo de Banco de Dados)
titleSuffix: T-SQL debugger
ms.prod: sql
ms.technology: scripting
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: e7f2d6f4-bb94-4cf5-a096-c34397e679af
author: markingmyname
ms.author: maghan
ms.custom: seo-lt-2019
ms.date: 12/04/2019
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: a579eeeb12795c76bbe585a982a159d6e069813d
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "75243452"
---
# <a name="status-bar-database-engine-query-editor"></a>Barra de status (Editor de Consultas do Mecanismo de Banco de Dados)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

A barra de status das janelas do Editor de Consultas do [!INCLUDE[ssDE](../../includes/ssde-md.md)] podem ser codificadas por cor para indicar a qual instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] cada janela está conectada.

1. **Antes de começar:**  [Cores da Barra de Status](#StatusBarColors)  

2. **Para definir uma cor de status do servidor em:**  [Pesquisador de Objetos](#SetOEServerColor), [Servidor Registrado](#SetRegServerColor)  

3. **Para usar uma cor de status:**  [Abrir o Editor de Consultas, usando uma cor de servidor](#OpenServerColor), [Abrir o Editor de Consultas, especificando uma cor de status](#OpenSpecColor)  

[!INCLUDE[ssms-old-versions](../../includes/ssms-old-versions.md)]

##  <a name="status-bar-colors"></a><a name="StatusBarColors"></a> Cores da barra de status

Você pode associar uma cor de barra de status a um nó de servidor específico em **Pesquisador de Objetos** ou **Servidores Registrados**. As cores podem ser especificadas somente para nós de servidor conectados a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)], e não para nós de servidor de outras tecnologias do SQL Server. Você também pode especificar uma cor de barra de status personalizada sempre que você conecta uma nova janela do Editor de Consultas do [!INCLUDE[ssDE](../../includes/ssde-md.md)] a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Em seguida, você pode abrir uma janela do Editor de Consultas usando a cor de status definida para o nó do servidor ou especificar uma cor exclusiva para essa janela do editor.  

A definição de uma cor de barra de status personalizada para um nó de servidor no Pesquisador de Objetos deve ser feita durante o estabelecimento da conexão. Para alterar a cor associada a um nó de servidor existente, desconecte e reconecte especificando a nova cor.  

##  <a name="set-the-status-color-for-a-server-in-object-explorer"></a><a name="SetOEServerColor"></a> Definir a cor de status para um servidor no Pesquisador de Objetos

**Para definir uma cor de status no Pesquisador de Objetos**  
  
1.  No **Pesquisador de Objetos**, selecione o botão **Conectar** e depois a opção **Mecanismo de Banco de Dados...** .  
  
2.  Na caixa de diálogo **Conectar ao Servidor**, selecione **Opções >>** .  
  
3.  Marque a caixa de seleção **Usar cor personalizada** .  
  
4.  Para selecionar a cor, selecione o botão **Selecionar...** .  
  
5.  Selecione uma cor básica ou personalizada e clique em OK.  
  
6.  Preencha o restante das informações de conexão e selecione o botão **Conectar** .  
  
##  <a name="set-the-status-color-for-a-registered-server"></a><a name="SetRegServerColor"></a> Definir a cor de status para um servidor registrado  
 **Par definir uma cor de status para um servidor registrado**  
  
1.  Em **Servidores Registrados**, clique com o botão direito do mouse no nó de servidor e selecione **Propriedades...** .  
  
2.  Na caixa de diálogo **Editar Propriedades de Registro do Servidor** , selecione a guia **Propriedades de Conexão** .  
  
3.  Marque a caixa de seleção **Usar cor personalizada** .  
  
4.  Para selecionar a cor, selecione o botão **Selecionar...** .  
  
5.  Selecione uma cor básica ou personalizada e clique em OK.  
  
6.  Selecione o botão **Salvar** na caixa de diálogo **Editar Propriedades de Registro do Servidor** .  
  
##  <a name="open-an-editor-using-a-server-color"></a><a name="OpenServerColor"></a> Abrir um editor usando uma cor de servidor  
 **Para abrir uma janela do editor usando uma cor de servidor**  
  
-   Clique com o botão direito do mouse em um nó de servidor no **Pesquisador de Objetos** ou em **Servidores Registrados**e selecione **Nova Consulta**.  
  
-   Opcionalmente, realce um nó de servidor e selecione o botão **Nova Consulta** na barra de ferramentas.  
  
-   A barra de status da janela do editor usará a cor definida para o servidor associado.  
  
##  <a name="open-an-editor-specifying-a-status-color"></a><a name="OpenSpecColor"></a> Abrir um editor especificando uma cor de status  
 **Para abrir uma janela do editor especificando uma cor de status**  
  
-   Abra o menu **Arquivo** , selecione **Novo**e, em seguida, selecione **Consulta do Mecanismo de Banco de Dados**.  
  
-   Na caixa de diálogo **Conectar ao Servidor**, selecione **Opções >>** .  
  
-   Marque a caixa de seleção **Usar cor personalizada** .  
  
-   Para selecionar a cor, selecione o botão **Selecionar...** .  
  
-   Selecione uma cor básica ou personalizada e clique em OK.  
  
-   Preencha o restante das informações de conexão e selecione o botão **Conectar** .  
  
## <a name="see-also"></a>Consulte Também  
 [Editores de consultas e de texto &#40;SQL Server Management Studio&#41;](../../relational-databases/scripting/query-and-text-editors-sql-server-management-studio.md)  
  
  
