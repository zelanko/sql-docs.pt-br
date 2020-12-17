---
description: Propriedades do SQL Server Agent (página Sistema de Alerta)
title: Propriedades do SQL Server Agent (página Sistema de Alerta)
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.ag.agent.alert.f1
ms.assetid: 3e6d3bfd-20ee-4593-86cc-f65b1c08c69d
author: markingmyname
ms.author: maghan
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016
ms.openlocfilehash: 19ee180bdc54ea36804f18b9ab064f459db0d23b
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97464357"
---
# <a name="sql-server-agent-properties-alert-system-page"></a>Propriedades do SQL Server Agent (página Sistema de Alerta)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> No momento, na [Instância Gerenciada de SQL do Azure](/azure/sql-database/sql-database-managed-instance), a maioria dos recursos do SQL Server Agent é compatível, mas não todos. Confira detalhes nas [Diferenças entre o T-SQL da Instância Gerenciada de SQL do Azure e o SQL Server](/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent).

Use esta página para ver e modificar as configurações de mensagens enviadas pelos alertas do [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
## <a name="options"></a>Opções  
**Sessão de email**  
As opções nessa seção configuram o Agent Mail do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
**Habilitar perfil de email**  
Habilita o Agent Mail do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Por padrão, o Agent Mail do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não está habilitado.  
  
**Sistema de email**  
Define o sistema de email para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent usar. Database Mail  
  
> [!NOTE]  
> Após alterar o sistema de email, você deve reiniciar o serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent para que a alteração entre em vigor.  
  
**Perfil de Email**  
Define o perfil para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent usar. Você também pode selecionar **\<new Database Mail profile...>** para criar um novo perfil.  
  
**Emails por pager**  
As opções desta seção permitem configurar mensagens de email enviadas para endereços de pager para funcionarem com o seu sistema de paginação.  
  
**Formatação de endereço para emails de pager**  
Essa seção permite que você especifique o formato dos endereços e a linha de assunto incluída nos emails de pager.  
  
**Linha Para**  
Especifica as opções para a linha **Para** da mensagem  
  
**Prefix**  
Digite qualquer texto fixo que o seu sistema solicita no início da linha **Para** de mensagens enviadas a um pager.  
  
**Pager**  
Inclui o endereço de email para a mensagem entre o prefixo e o sufixo.  
  
**Suffix**  
Digite qualquer texto fixo que o seu sistema de pagers solicita no fim da linha **Para** de mensagens enviadas a um pager.  
  
**Linha Cc**  
Especifica as opções para a linha **Cc** da mensagem.  
  
**Prefix**  
Digite qualquer texto fixo que o seu sistema solicita no início da linha **Cc** de mensagens enviadas a um pager.  
  
**Pager**  
Inclui o endereço de email para a mensagem entre o prefixo e o sufixo.  
  
**Suffix**  
Digite qualquer texto fixo que o seu sistema de pagers solicita no fim da linha **Cc** de mensagens enviadas a um pager.  
  
**Assunto**  
Especifica as opções para o assunto da mensagem.  
  
**Prefix**  
Digite qualquer texto fixo que o seu sistema de pagers solicita no início da linha **Assunto** de mensagens enviadas a um pager.  
  
**Suffix**  
Digite qualquer texto fixo que o seu sistema de pagers solicita no fim da linha **Assunto** de mensagens enviadas a um pager.  
  
**Inclua o corpo de email em mensagem de notificação**  
Inclui o corpo da mensagem de email na mensagem enviada ao pager.  
  
**Operador à prova de falhas**  
Essa seção permite que você especifique as opções para o operador à prova de falhas.  
  
**Habilitar o operador à prova de falhas**  
Especifica um operador à prova de falhas.  
  
**Operador**  
Define o nome do operador para receber notificações à prova de falhas.  
  
**Notificar usando**  
Define o método a usar ao notificar o operador à prova de falhas.  
  
**Substituição de Token**  
Essa seção permite que você habilite tokens de etapa de trabalho que podem ser usados em trabalhos executados pelos alertas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Para obter mais informações sobre tokens de etapa de trabalho, consulte [Usar tokens em etapas de trabalho](../../ssms/agent/use-tokens-in-job-steps.md).  
  
> [!IMPORTANT]  
> Qualquer usuário do Windows com permissões de gravação no Log de Eventos do Windows pode acessar etapas de trabalho ativadas pelos alertas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Para evitar riscos de segurança, os tokens do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent que podem ser usados em trabalhos ativados por alertas encontram-se desabilitados por padrão. Esses tokens são: **$(A-DBN)** , **$(A-SVR)** , **$(A-ERR)** , **$(A-SEV)** e **$(A-MSG)** .  
>   
> Se precisar usar esses tokens, certifique-se de que apenas membros dos grupos de segurança confiáveis do Windows, como o grupo Administradores, tenham permissões de gravação no Log de Eventos do computador em que reside o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] antes de habilitá-los.  
  
**Substitua os tokens para todas as respostas de trabalho a alertas**  
Marque essa caixa de seleção para habilitar a substituição de token para trabalhos que são ativados pelos alertas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="see-also"></a>Consulte Também  
[Operadores](../../ssms/agent/operators.md)  
[Configurar o SQL Server Agent Mail para usar o Database Mail](../../relational-databases/database-mail/configure-sql-server-agent-mail-to-use-database-mail.md)  
[Database Mail](../../relational-databases/database-mail/database-mail.md)  
