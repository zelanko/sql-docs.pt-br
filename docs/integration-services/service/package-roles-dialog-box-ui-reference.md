---
title: "Refer&#234;ncia da interface do usu&#225;rio da caixa de di&#225;logo Fun&#231;&#245;es do Pacote | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.dtsserver.packageroles.f1"
helpviewer_keywords: 
  - "Caixa de diálogo Funções do Pacote"
ms.assetid: 63f13416-c0aa-4480-a336-ef1e6e31a860
caps.latest.revision: 26
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 26
---
# Refer&#234;ncia da interface do usu&#225;rio da caixa de di&#225;logo Fun&#231;&#245;es do Pacote
  Use a caixa de diálogo **Funções do Pacote**, disponível no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], para especificar as funções de nível de banco de dados que têm acesso de leitura e as que têm acesso de gravação ao pacote. As funções de nível de banco de dados se aplicam apenas a pacotes armazenados no banco de dados **msdbmsdb** do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Para saber mais sobre as funções de nível de banco de dados do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] e suas permissões, consulte [Funções do Integration Services &#40;Serviço SSIS&#41;](../../integration-services/service/integration-services-roles-ssis-service.md).  
  
 As funções listadas na caixa de diálogo são as funções de banco de dados atuais do banco de dados de sistema **msdb** . Se nenhuma função for selecionada, serão aplicadas as funções do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Por padrão, a função de leitor inclui **db_ssisadmin**, **db_ssisoperator** e o usuário que criou o pacote. Um usuário membro de uma dessas funções ou criador dos pacotes pode enumerar, exibir, exportar e executar pacotes. Por padrão, a função de gravador inclui **db_ssisadmin** e o usuário que criou o pacote. Um usuário membro dessa função e o criador dos pacotes podem importar, excluir e alterar pacotes.  
  
 A coluna **ownersid** da tabela **sysssispackages** lista o identificador de segurança exclusivo do usuário que criou o pacote.  
  
## Opções  
 **Nome do Pacote**  
 Especifique o nome do pacote.  
  
 **Função de Leitor**  
 Selecione uma função na lista.  
  
 **Função de Gravador**  
 Selecione uma função na lista  
  
## Consulte também  
 [Funções de nível de banco de dados](../../relational-databases/security/authentication-access/database-level-roles.md)   
 [Visão geral de segurança &#40;Integration Services&#41;](../../integration-services/security/security-overview-integration-services.md)  
  
  