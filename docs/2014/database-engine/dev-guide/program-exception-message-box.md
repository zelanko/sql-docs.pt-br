---
title: Caixa de mensagem de exceção de programa | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.topic: reference
helpviewer_keywords:
- exception message box [SQL Server]
- displaying exception message box
ms.assetid: c771985b-149c-459a-b3cb-7b15fde01150
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 8cf02e2759c36ae6408beed0d72b677e130e105a
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48164106"
---
# <a name="program-exception-message-box"></a>Programar caixa de mensagem de exceção
  Você pode usar a caixa de mensagem de exceção em seus aplicativos para fornecer significativamente mais controle sobre a experiência de mensagens que é fornecido pelo <xref:System.Windows.Forms.MessageBox> classe. Para obter mais informações, consulte [caixa de mensagem de exceção programação](../../../2014/database-engine/dev-guide/exception-message-box-programming.md). Para obter informações sobre como obter e implantar a caixa de mensagem de exceção. dll, consulte [Implantando um aplicativo de caixa de mensagem de exceção](../../../2014/database-engine/dev-guide/deploying-an-exception-message-box-application.md).  
  
## <a name="procedure"></a>Procedimento  
  
#### <a name="to-handle-an-exception-by-using-the-exception-message-box"></a>Para tratar de uma exceção usando a caixa de mensagem de exceção  
  
1.  Adicione uma referência em seu projeto de código gerenciado ao assembly Microsoft.ExceptionMessageBox.dll.  
  
2.  (Opcional) Adicionar um `using` (c#) ou `Imports` ([!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic .NET) diretiva para usar o <xref:Microsoft.SqlServer.MessageBox> namespace.  
  
3.  Crie um bloco try-catch para tratar da exceção antecipada.  
  
4.  Dentro de `catch` bloquear, crie uma instância da <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox> classe. Passe o <xref:System.Exception> objeto tratado pelos `try` - `catch` bloco.  
  
5.  (Opcional) Defina uma ou mais das seguintes propriedades em <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox>:  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.Buttons%2A> - <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxButtons> enumeração que especifica os botões a serem exibidos na caixa de mensagem de exceção.  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.DefaultButton%2A> - <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxDefaultButton> enumeração que especifica o botão padrão para a caixa de mensagem de exceção.  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.Options%2A> - <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxOptions> enumeração que você pode usar para controlar outros comportamentos da caixa de mensagem de exceção.  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.Symbol%2A> - <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxSymbol> enumeração que especifica o símbolo a ser exibido na caixa de mensagem de exceção.  
  
6.  Chame o método <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.Show%2A> . Passe a janela pai à qual pertence a caixa de mensagem de exceção.  
  
7.  (Opcional) Observe o valor retornado <xref:System.Windows.Forms.DialogResult> enumeração se você precisar determinar em qual botão o usuário clicou.  
  
#### <a name="to-display-the-exception-message-box-without-an-exception"></a>Para exibir a caixa de mensagem de exceção sem uma exceção  
  
1.  Adicione uma referência em seu projeto de código gerenciado ao assembly Microsoft.ExceptionMessageBox.dll.  
  
2.  (Opcional) Adicionar um `using` (c#) ou `Imports` diretiva (Visual Basic .NET) para usar o <xref:Microsoft.SqlServer.MessageBox> namespace.  
  
3.  Crie uma instância da classe <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox> . Passar o texto da mensagem como um <xref:System.String> valor.  
  
4.  (Opcional) Defina uma ou mais das seguintes propriedades em <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox>:  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.Buttons%2A> - <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxButtons> enumeração que especifica os botões a serem exibidos na caixa de mensagem de exceção.  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.Caption%2A>- legenda da caixa de diálogo da caixa de mensagem de exceção.  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.DefaultButton%2A> - <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxDefaultButton> enumeração que especifica o botão padrão para a caixa de diálogo da caixa de mensagem de exceção.  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.Options%2A> - <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxOptions> enumeração que você pode usar para controlar outros comportamentos da caixa de mensagem de exceção.  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.Symbol%2A> - <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxSymbol> enumeração que especifica o símbolo a ser exibido na caixa de mensagem de exceção.  
  
5.  Chame o método <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.Show%2A> . Passe a janela pai à qual pertence a caixa de mensagem de exceção.  
  
6.  (Opcional) Observe o valor retornado <xref:System.Windows.Forms.DialogResult> enumeração se você precisar determinar em qual botão o usuário clicou.  
  
#### <a name="to-display-the-exception-message-box-with-customized-buttons"></a>Para exibir a caixa de mensagem de exceção com botões personalizados  
  
1.  Adicione uma referência em seu projeto de código gerenciado ao assembly Microsoft.ExceptionMessageBox.dll.  
  
2.  (Opcional) Adicionar um `using` (c#) ou `Imports` diretiva (Visual Basic .NET) para usar o <xref:Microsoft.SqlServer.MessageBox> namespace.  
  
3.  Crie uma instância da classe <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox> de uma destas duas maneiras:  
  
    -   Passe o <xref:System.Exception> objeto tratado por um `try` - `catch` bloco.  
  
    -   Passar o texto da mensagem como um <xref:System.String> valor.  
  
4.  Defina um dos seguintes valores para <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.Buttons%2A>:  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxButtons.AbortRetryIgnore> -Exibe a **anular**, **Repita**, e **ignorar** botões.  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxButtons.Custom> -Exibe botões personalizados.  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxButtons.OK> -Exibe a **Okey** botão.  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxButtons.OKCancel> -Exibe a **Okey** e **Cancelar** botões.  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxButtons.RetryCancel> -Exibe a **Repita** e **Cancelar** botões.  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxButtons.YesNo> -Exibe **Yes** e **não** botões.  
  
    -   <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxButtons.YesNoCancel> -Exibe **Yes**, **nenhuma**, e **Cancelar** botões.  
  
5.  (Opcional) Se você usar botões personalizados, chame uma das sobrecargas do <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.SetButtonText%2A> método para especificar o texto para até cinco botões personalizados.  
  
6.  Chame o método <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.Show%2A> . Passe a janela pai à qual pertence a caixa de mensagem de exceção.  
  
7.  (Opcional) Observe o valor retornado <xref:System.Windows.Forms.DialogResult> enumeração se você precisar determinar em qual botão o usuário clicou. Se você usar botões personalizados, observe o valor de <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBoxDialogResult> para o <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.CustomDialogResult%2A> propriedade para determinar qual dos personalizado botões que o usuário clicou.  
  
#### <a name="to-allow-users-to-decide-whether-to-show-the-exception-message-box"></a>Para permitir que os usuários decidam se mostrarão a caixa de mensagem de exceção  
  
1.  Adicione uma referência em seu projeto de código gerenciado ao assembly Microsoft.ExceptionMessageBox.dll.  
  
2.  (Opcional) Adicionar um `using` (c#) ou `Imports` diretiva (Visual Basic .NET) para usar o <xref:Microsoft.SqlServer.MessageBox> namespace.  
  
3.  Crie uma instância da classe <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox> de uma destas duas maneiras:  
  
    -   Passe o <xref:System.Exception> objeto tratado por um `try` - `catch` bloco.  
  
    -   Passar o texto da mensagem como um <xref:System.String> valor.  
  
4.  Defina as <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.ShowCheckbox%2A> propriedade para `true`.  
  
5.  (Opcional) Especifique o texto que pede ao usuário para decidir se mostrará a caixa de mensagem de exceção novamente para <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.CheckboxText%2A>. O texto padrão é "Não exibir esta mensagem novamente".  
  
6.  Se você precisar manter a decisão do usuário apenas para a duração da execução do aplicativo, defina o valor de <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.IsCheckboxChecked%2A> para um global <xref:System.Boolean> variável. Avalie esse valor antes de criar uma instância da caixa de mensagem de exceção.  
  
7.  Se você precisar armazenar a decisão de um usuário permanentemente, siga este procedimento:  
  
    1.  Chame o método CreateSubKey para abrir uma chave do registro personalizada usada pelo aplicativo e defina <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.CheckboxRegistryKey%2A> para o objeto RegistryKey retornado.  
  
    2.  Defina <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.CheckboxRegistryValue%2A> como o nome do valor do Registro que é usado.  
  
    3.  Definir <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.CheckboxRegistryMeansDoNotShowDialog%2A> para `true`.  
  
    4.  Chame o método <xref:Microsoft.SqlServer.MessageBox.ExceptionMessageBox.Show%2A> . A chave do Registro especificada é avaliada, e a caixa de mensagem de exceção só será exibida se os dados armazenados na chave do Registro forem 0. Se a caixa de diálogo for exibida e o usuário marcar a caixa de seleção antes de clicar em um botão, os dados da chave do Registro serão definidos como 1.  
  
## <a name="example"></a>Exemplo  
 Este exemplo usa a caixa de mensagem de exceção apenas com o botão **OK** para exibir as informações de uma exceção de aplicativo que inclui a exceção tratada juntamente com outras informações específicas de aplicativo.  
  
 [!code-csharp[HowTo#emb_showOKbutton](../../snippets/csharp/SQL15/replication/howto/cs/embform.cs#emb_showokbutton)]  
  
 [!code-vb[HowTo#emb_vb_showOKbutton](../../snippets/visualbasic/SQL15/replication/howto/vb/embform.vb#emb_vb_showokbutton)]  
  
## <a name="example"></a>Exemplo  
 Este exemplo usa a caixa de mensagem de exceção com os botões **Sim** e **Não** que o usuário pode escolher.  
  
 [!code-csharp[HowTo#emb_showYesNobutton](../../snippets/csharp/SQL15/replication/howto/cs/embform.cs#emb_showyesnobutton)]  
  
 [!code-vb[HowTo#emb_vb_showYesNobutton](../../snippets/visualbasic/SQL15/replication/howto/vb/embform.vb#emb_vb_showyesnobutton)]  
  
## <a name="example"></a>Exemplo  
 Este exemplo usa a caixa de mensagem de exceção com botões personalizados.  
  
 [!code-csharp[HowTo#emb_showcustombutton](../../snippets/csharp/SQL15/replication/howto/cs/embform.cs#emb_showcustombutton)]  
  
 [!code-vb[HowTo#emb_vb_showcustombutton](../../snippets/visualbasic/SQL15/replication/howto/vb/embform.vb#emb_vb_showcustombutton)]  
  
## <a name="example"></a>Exemplo  
 Este exemplo usa a caixa de seleção para determinar se a caixa de mensagem de exceção será exibida.  
  
 [!code-csharp[HowTo#emb_usecheckbox](../../snippets/csharp/SQL15/replication/howto/cs/embform.cs#emb_usecheckbox)]  
  
 [!code-vb[HowTo#emb_vb_usecheckbox](../../snippets/visualbasic/SQL15/replication/howto/vb/embform.vb#emb_vb_usecheckbox)]  
  
## <a name="example"></a>Exemplo  
 Este exemplo usa a caixa de seleção e uma chave do Registro para determinar se a caixa de mensagem de exceção será exibida.  
  
 [!code-csharp[HowTo#emb_useregkey](../../snippets/csharp/SQL15/replication/howto/cs/embform.cs#emb_useregkey)]  
  
 [!code-vb[HowTo#emb_vb_useregkey](../../snippets/visualbasic/SQL15/replication/howto/vb/embform.vb#emb_vb_useregkey)]  
  
## <a name="example"></a>Exemplo  
 Este exemplo usa a caixa de mensagem de exceção para mostrar informações adicionais úteis ao solucionar problemas ou depurar.  
  
 [!code-csharp[HowTo#emb_moreinfo](../../snippets/csharp/SQL15/replication/howto/cs/embform.cs#emb_moreinfo)]  
  
 [!code-vb[HowTo#emb_vb_moreinfo](../../snippets/visualbasic/SQL15/replication/howto/vb/embform.vb#emb_vb_moreinfo)]  
  
  
