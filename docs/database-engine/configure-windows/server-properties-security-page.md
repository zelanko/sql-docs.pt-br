---
title: "Propriedades do Servidor (p&#225;gina Seguran&#231;a) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.swb.serverproperties.security.f1"
ms.assetid: b8a131c7-e7bd-4203-bf26-234f1ebfe622
caps.latest.revision: 31
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 31
---
# Propriedades do Servidor (p&#225;gina Seguran&#231;a)
  Use esta página para exibir ou modificar as opções de segurança do servidor.  
  
## Autenticação do servidor  
 **Modo de Autenticação do Windows**  
 Usa a autenticação do Windows para validar as conexões tentadas. Se a senha **sa** estiver em branco quando o modo de segurança estiver sendo alterado, será solicitado ao usuário que digite a senha **sa** .  
  
> [!IMPORTANT]  
>  A autenticação do Windows é muito mais segura do que a autenticação do SQL Server. Quando possível, você deve usar a autenticação do Windows.  
  
 **Modo de autenticação do SQL Server e do Windows**  
 Usa autenticação de modo misto para verificar conexões tentadas, para compatibilidade com versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se a senha **sa** estiver em branco quando o modo de segurança estiver sendo alterado, será solicitado ao usuário que digite a senha **sa** .  
  
> [!NOTE]  
>  A alteração da configuração de segurança requer que o serviço seja reiniciado. Ao alterar a autenticação do servidor para o modo de autenticação do SQL Server e do Windows a conta SA não é habilitada automaticamente. Para usar a conta SA, execute [ALTER LOGIN](../../t-sql/statements/alter-login-transact-sql.md) com a opção ENABLE.  
  
## Auditoria de logon  
 **Nenhuma**  
 Desativa a auditoria de logon.  
  
 **Somente logons com falha**  
 Auditoria somente de logons sem-êxito.  
  
 **Somente logons bem sucedidos**  
 Auditoria somente de logons bem sucedidos.  
  
 **Logons com falha e bem sucedidos**  
 Auditoria de todas as tentativas de logon.  
  
> [!NOTE]  
>  A alteração do nível de auditoria requer que o serviço seja reiniciado.  
  
## Conta proxy do servidor  
 **Habilitar conta proxy do servidor**  
 Habilita uma conta para uso do **xp_cmdshell**. As contas proxy permitem a representação de logons, funções de servidor e funções de bancos de dados quando um comando do sistema operacional está sendo executado.  
  
> [!CAUTION]  
>  O logon usado pela conta proxy do servidor dever ter os privilégios mínimos exigidos para executar o trabalho pretendido. Privilégios excessivos para a conta proxy podem ser usados por um usuário mal-intencionado para comprometer a segurança de seu sistema.  
  
 **Conta proxy**  
 Especifica a conta proxy usada.  
  
 **Senha**  
 Especifica a senha para a conta proxy.  
  
## Opções  
 **Habilitar rastreamento de auditoria C2**  
 Audita todas as tentativas de acessar instruções e objetos e as registra em um arquivo no diretório \MSSQL\Data para as instâncias padrão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou o diretório \MSSQL$*instancename*\Data para instâncias nomeadas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter mais informações, veja [Opção c2 audit mode de configuração de servidor](../../database-engine/configure-windows/c2-audit-mode-server-configuration-option.md).  
  
 **Encadeamento de propriedades de bancos de dados**  
 Selecione para permitir que o banco de dados seja a origem ou o destino de um encadeamento de propriedades de bancos de dados. Para obter mais informações, veja [Opção cross db ownership chaining de configuração de servidor](../../database-engine/configure-windows/cross-db-ownership-chaining-server-configuration-option.md).  
  
## Consulte também  
 [Opções de configuração do servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)  
  
  