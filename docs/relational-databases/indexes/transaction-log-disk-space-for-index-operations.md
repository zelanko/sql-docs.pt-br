---
title: "Espa&#231;o em disco de log de transa&#231;&#245;es para opera&#231;&#245;es de &#237;ndice | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-indexes"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "espaço em disco de índice [SQL Server]"
  - "espaço [SQL Server], índices"
  - "logs de transações [SQL Server], espaço em disco"
  - "espaço em disco [SQL Server], logs de transações"
  - "espaço [SQL Server], logs de transações"
ms.assetid: 4f8a4922-4507-4072-be67-c690528d5c3b
caps.latest.revision: 17
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 17
---
# Espa&#231;o em disco de log de transa&#231;&#245;es para opera&#231;&#245;es de &#237;ndice
  Operações de índice de larga escala podem gerar grandes carregamentos de dados que podem fazer com que o log da transação seja preenchido rapidamente. Para assegurar a reversão da operação de índice, o log da transação não pode ser truncado até que a operação de índice se complete. Durante a operação, no entanto, poderá ser feito backup do log. Portanto, o log de transações deve ter espaço suficiente para armazenar as transações da operação de índice e todas as transações simultâneas de usuário pelo período da operação de índice. Isso é verdade para operações de índice offline e online. Como as tabelas subjacentes não podem ser acessadas durante a operação de índice offline, pode haver poucas transações de usuário e o log pode não crescer na mesma proporção. As operações de índice online não impedem atividades simultâneas de usuário. Por isso, as operações de índice online de larga escala, combinadas com transações simultâneas significativas de usuário, podem causar o crescimento contínuo do log de transações sem opção para truncar o log.  
  
## Recomendações  
 Durante a execução de operações de índice de grande escala, considere estas recomendações:  
  
1.  Verifique se foi feito o backup do log de transações e se ele foi truncado antes de executar as operações de índice online de grande escala, e se o log tem espaço suficiente para armazenar o índice projetado e as transações do usuário.  
  
2.  Considere definir a opção SORT_IN_TEMPDB como ON para a operação de índice. Isso separará as transações de índice das transações de usuário simultâneas. As transações de índice serão armazenadas no log de transações **tempdb**, e as transações de usuário simultâneas serão armazenadas no log de transações do banco de dados de usuário. Isso permitirá que o log de transações do banco de dados de usuário seja truncado durante a operação de índice, se necessário. Além disso, se o log **tempdb** não estiver no mesmo disco do log de banco de dados de usuário, os dois logs não estarão competindo pelo mesmo espaço em disco.  
  
    > [!NOTE]  
    >  Confirme se o banco de dados **tempdb** e o log de transações têm espaço em disco suficiente para controlar a operação de índice. O log de transações **tempdb** não pode ser truncado até que a operação de índice seja concluída.  
  
3.  Use um modelo de recuperação de banco de dados que permita o registro mínimo da operação de índice. Isso poderá reduzir o tamanho do log e impedir que o log preencha o espaço de log.  
  
4.  Não execute a operação de índice online em uma transação explícita. O log não será truncado até que a transação explícita termine.  
  
## Conteúdo relacionado  
 [Requisitos de espaço em disco para operações de índice DDL](../../relational-databases/indexes/disk-space-requirements-for-index-ddl-operations.md)  
  
 [Exemplo de espaço em disco de índice](../../relational-databases/indexes/index-disk-space-example.md)  
  
  