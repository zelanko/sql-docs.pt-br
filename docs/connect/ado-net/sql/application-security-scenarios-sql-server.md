---
title: Cenários de segurança de aplicativo no SQL Server
description: Contém os tópicos que abordam vários cenários de segurança de aplicativos para o ADO.NET e aplicativos do SQL Server.
ms.date: 09/26/2019
ms.assetid: 0164f3a4-406e-4693-bec3-03c8e18b46d7
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: rothja
ms.author: jroth
ms.reviewer: v-kaywon
ms.openlocfilehash: 2173a6aaf0f07ffaa50d87ed7563dca8022ceebc
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "75250971"
---
# <a name="application-security-scenarios-in-sql-server"></a>Cenários de segurança de aplicativo no SQL Server

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[Download ADO.NET](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

Não há nenhuma maneira correta de criar um aplicativo cliente seguro do SQL Server. Cada aplicativo é único em seus requisitos, ambiente de implantação e população de usuários. Um aplicativo razoavelmente seguro, após ser inicialmente implantado, pode se tornar menos seguro ao longo do tempo. É impossível prever com alguma precisão quais as ameaças que podem surgir no futuro.  
  
O SQL Server, como um produto, evoluiu durante várias versões para incorporar os recursos de segurança mais recentes que permitem aos desenvolvedores criar aplicativos de banco de dados seguros. No entanto, a segurança não vem pronta na caixa; ela requer monitoramento e atualização contínuos.  
  
## <a name="common-threats"></a>Ameaças comuns  
Os desenvolvedores precisam entender as ameaças de segurança, as ferramentas fornecidas para combatê-las e como evitar falhas de segurança autoprovocadas. A segurança pode ser considerada como uma cadeia, em que o rompimento de qualquer um dos elos compromete a força do todo. A lista a seguir inclui algumas ameaças comuns de segurança que são discutidas mais detalhadamente nos tópicos desta seção.  
  
### <a name="sql-injection"></a>injeção SQL  
A injeção de SQL é o processo pelo qual um usuário mal-intencionado insere instruções Transact-SQL em vez de uma entrada válida. Se a entrada for passada diretamente para o servidor sem ser validada e se o aplicativo executar inadvertidamente o código injetado, o ataque terá o potencial de danificar ou destruir dados. Você pode impedir ataques de injeção do SQL Server usando procedimentos armazenados e comandos parametrizados, evitando o SQL dinâmico e restringindo as permissões de todos os usuários.  
  
### <a name="elevation-of-privilege"></a>Elevação de privilégio  
Os ataques de elevação de privilégio ocorrem quando um usuário é capaz de assumir os privilégios de uma conta confiável, como um proprietário ou administrador. Sempre execute em contas de usuário com o mínimo de privilégios e atribua apenas as permissões necessárias. Evite usar contas administrativas ou de proprietário para executar o código. Isso limitará a quantidade de danos que podem ocorrer se um ataque for realizado com sucesso. Ao executar tarefas que exigem permissões adicionais, use a assinatura ou representação de procedimento somente pela duração da tarefa. Você pode assinar procedimentos armazenados com certificados ou usar a representação para atribuir permissões temporariamente.  
  
### <a name="probing-and-intelligent-observation"></a>Sondagem e observação inteligente  
Um ataque de sondagem pode usar mensagens de erro geradas por um aplicativo para pesquisar vulnerabilidades de segurança. Implemente o tratamento de erro em todo o código de procedimento para impedir que as informações de erro do SQL Server sejam retornadas ao usuário final.  
  
### <a name="authentication"></a>Autenticação  
Um ataque de injeção de cadeia de conexão pode ocorrer ao usar logons do SQL Server se uma cadeia de conexão baseada na entrada do usuário for construída em tempo de execução. Se a cadeia de conexão não for verificada em busca de pares de palavras-chave válidos, um invasor poderá inserir caracteres extras, potencialmente acessando dados confidenciais ou outros recursos no servidor. Use a autenticação do Windows sempre que possível. Se você precisar usar logons do SQL Server, use o <xref:Microsoft.Data.SqlClient.SqlConnectionStringBuilder> para criar e validar cadeias de conexão em tempo de execução.  
  
### <a name="passwords"></a>Senhas  
Muitos ataques são bem-sucedidos porque um invasor conseguiu obter ou adivinhar uma senha de um usuário privilegiado. As senhas são sua primeira linha de defesa contra intrusos; portanto, a configuração de senhas fortes é essencial para a segurança do seu sistema. Criar e impor políticas de senha para autenticação de modo misto.  
  
Sempre atribua uma senha forte à conta de `sa`, mesmo ao usar a Autenticação do Windows.  
  
## <a name="in-this-section"></a>Nesta seção  
[Gravação de SQL dinâmico seguro no SQL Server](writing-secure-dynamic-sql.md)  
Descreve técnicas para gravar SQL dinâmico seguro usando procedimentos armazenados.  

## <a name="next-steps"></a>Próximas etapas
- [Segurança do SQL Server](sql-server-security.md)
