---
title: Tarefa Notificar Operador (plano de manutenção) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
f1_keywords:
- sql12.swb.maint.notifyoperator.f1
helpviewer_keywords:
- Notify Operator Task dialog box
ms.assetid: 39c0797c-ad2b-4591-85c9-a23a7f902895
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 0ef94ed9e296c588b70789ace0bbbbe79bc8008f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68205958"
---
# <a name="notify-operator-task-maintenance-plan"></a>Tarefa de Notificação do Operador (Plano de Manutenção)
  Use a caixa de diálogo **tarefa notificar operadores** para adicionar uma notificação automática a este plano de manutenção. Para usar essa tarefa, você deve ter Database Mail habilitado e configurado corretamente com msdb como um banco de dados de host de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] email e ter um operador de agente com um endereço de email válido.  
  
 Esta tarefa usa o procedimento armazenado sp_notify_operator.  
  
## <a name="options"></a>Opções  
 **Conexão**  
 Selecione a conexão de servidor a ser usada na execução desta tarefa.  
  
 **Novo**  
 Crie uma nova conexão com o servidor para usar ao executar esta tarefa. A caixa de diálogo **Nova Conexão** é descrita abaixo.  
  
 **Operadores para notificar**  
 Especifique o destinatário do email.  
  
 **Assunto da mensagem de notificação**  
 Especifique o texto a ser incluído na linha do assunto da mensagem de notificação.  
  
 **Corpo da mensagem de notificação**  
 Especifique o texto a ser incluído no corpo da mensagem de notificação.  
  
 **Exibir T-SQL**  
 Exiba as instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] executadas no servidor para esta tarefa, com base nas opções selecionadas.  
  
> [!NOTE]  
>  Quando o número de objetos afetados é grande, essa exibição pode ser demorada.  
  
## <a name="new-connection-dialog-box"></a>Caixa de diálogo Nova Conexão  
 **Nome da conexão**  
 Digite um nome para a nova conexão.  
  
 **Selecione ou digite um nome de servidor**  
 Selecione um servidor com o qual se conectar ao executar esta tarefa.  
  
 **Atualizar**  
 Atualize a lista de servidores disponíveis.  
  
 **Digite as informações para fazer logon no servidor**  
 Especifica como autenticar no servidor.  
  
 **Use a segurança integrada do Windows**  
 Conecte-se a uma instância [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] do [!INCLUDE[msCoName](../../includes/msconame-md.md)] com a autenticação do Windows.  
  
 **Usar nome de usuário e senha específicos**  
 Conecte-se com uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] usando a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Essa opção não está disponível.  
  
 **Nome de usuário**  
 Forneça um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a ser usado na autenticação. Essa opção não está disponível.  
  
 **Senha**  
 Forneça uma senha a ser usada na autenticação. Essa opção não está disponível.  
  
## <a name="see-also"></a>Consulte Também  
 [Database Mail](../database-mail/database-mail.md)   
 [&#41;&#40;Transact-SQL de sp_notify_operator](/sql/relational-databases/system-stored-procedures/sp-notify-operator-transact-sql)  
  
  
