---
title: "Definir a op&#231;&#227;o do banco de dados PAGE_VERIFY como CHECKSUM | Microsoft Docs"
ms.custom: ""
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Práticas recomendadas [Mecanismo de Banco de Dados]"
ms.assetid: 686b9a4a-ea61-4263-9ab8-f444a3077679
caps.latest.revision: 8
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 8
---
# Definir a op&#231;&#227;o do banco de dados PAGE_VERIFY como CHECKSUM
  Esta regra verifica se a opção do banco de dados PAGE_VERIFY está definida como CHECKSUM. Quando CHECKSUM é habilitado para a opção do banco de dados PAGE_VERIFY, o [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] calcula uma soma de verificação nos conteúdos da página inteira e armazena o valor no cabeçalho da página, quando uma página é gravada em disco. Quando a página é lida pelo disco, a soma de verificação é recalculada e comparada ao valor da soma de verificação armazenado no cabeçalho da página. Isso ajuda a fornecer um alto nível de integridade de arquivo de dados.  
  
## Práticas Recomendadas  
 Defina a opção do banco de dados PAGE_VERIFY como CHECKSUM.  
  
## Para obter mais informações  
 [Opções ALTER DATABASE SET &#40;Transact-SQL&#41;](../Topic/ALTER%20DATABASE%20SET%20Options%20\(Transact-SQL\).md)  
  
  