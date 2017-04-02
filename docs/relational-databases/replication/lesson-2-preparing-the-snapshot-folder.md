---
title: "Li&#231;&#227;o 2: Preparando a pasta do instant&#226;neo | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to: 
  - "SQL Server 2016"
helpviewer_keywords: 
  - "replicação [SQL Server], tutoriais"
ms.assetid: f286cde9-c0d0-43ef-b7ba-53c3cbb8906c
caps.latest.revision: 20
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 20
---
# Li&#231;&#227;o 2: Preparando a pasta do instant&#226;neo
Nesta lição, você aprenderá a configurar a pasta do instantâneo, usada para criar e armazenar o instantâneo de publicação.  
  
### Para criar um compartilhamento para a pasta de instantâneo e atribuir permissões  
  
1.  No Windows Explorer, vá para a pasta de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O local padrão é C:\Arquivos de Programa\Microsoft SQL Server\MSSQL.X\MSSQL\Data.  
  
2.  Crie uma nova pasta chamada **repldata**.  
  
3.  Clique com o botão direito do mouse nessa pasta e clique em **Propriedades**.  
  
4.  Na guia **Compartilhamento** da caixa de diálogo **Propriedades de repldata**, clique em **Compartilhar**.  
  
5.  Na caixa de diálogo **Compartilhamento de Arquivos**, clique em **Compartilhar** e clique em **Concluído**.  
  
6.  Na guia **Segurança** , clique em **Editar**.  
  
7.  Na caixa de diálogo **Permissões**, clique em **Adicionar**. Na caixa de texto **Selecionar Usuário, Computadores, Conta de Serviço ou Grupos**, digite o nome da conta do Agente de Instantâneo criado na Lição 1, como \<*Machine_Name>***\repl_snapshot**, em que \<*Machine_Name>* é o nome do Publicador. Clique em **Verificar Nomes** e em **OK**.  
  
8.  Repita a etapa anterior para adicionar permissões para o Agente de Distribuição, como \<*Machine_Name>***\repl_distribution**, e para o Agente de Mesclagem, como \<*Machine_Name>***\repl_merge**.  
  
9. Verifique se as permissões a seguir são permitidas:  
  
    -   repl_snapshot - Controle total  
  
    -   repl_distribution - Leitura  
  
    -   repl_merge - Leitura  
  
10. Clique em **OK** para fechar a caixa de diálogo **Propriedades de repldata** e criar o compartilhamento de repldata.  
  
## Próximas etapas  
Você configurou com êxito o compartilhamento da pasta de instantâneo. A seguir, você configurará a distribuição. Consulte [Lição 3: Configurando a distribuição](../../relational-databases/replication/lesson-3-configuring-distribution.md).  
  
## Consulte também  
[Proteger uma pasta de instantâneo](../../relational-databases/replication/security/secure-the-snapshot-folder.md)  
  
  
  
